.. title: Octoprint en OpenWRT (tp-link 1043nd)
.. slug: octoprint-en-openwrt-tp-link-1043nd
.. date: 2017-05-22 23:05:27 UTC-03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Hace un par de años Leí la `nota de Matt Defenthaler`_ donde cuenta que se encontró un router tirado en la calle y lo resucitó en forma de servidor de impresiones 3d. Como la impresora 3d que armamos no tiene display (ni tarjeta usb), la venía usando conectada a un raspberry pi, corriendo repetier server.

Si, lo sé, es un overkill, pero hasta hace poco no dispuse del tiempo y las ganas[1]_ para resolverlo.

OpenWRT en TP-Link 1043nd (v2.0)
================================

La maravilla del router tp-link es que trae un puerto usb. El mismo se puede utilizar para albergar una carpeta compartida, o compartir una impresora (tradicional, de esas que escriben en papel) en la red local. Para conectarle una impresora 3d en cambio hace falta cambiar su sistema operativo.

Si bien hay varios SO para reemplazar el que traen de fabrica los routers, el tutorial original que encontré utiliza OpenWRT así que fui por ahí. En teoría se podría usar tanto Tomato como DD-WRT mediante Optware.

Flasheo
-------

Bastante sencillo pero está fuera de alcance de este post. Hay cientos de tutoriales y por lo general son bastante claros aunque a veces pequen de simplistas y poco descriptivos. Personalmente no tuve problemas al seguir (la pobre) documentación que encontré en `la página dedicada al wr1043nd de openwrt`_.
https://wiki.openwrt.org/toh/tp-link/tl-wr1043nd

Configuración pendrive como almacenamiento
------------------------------------------

Una vez que está instalado OpenWRT, lo siguiente es disponer de lugar para instalar nuestras porquerías (cerca de 250mb, que para la memoria de un router es muchísimo).

Vamos a usar un pendrive cualunque, lo recomendable es formatearlo de antemano (no en el router) para hacer más rápido. De yapa podemos armar una partición de swap y rezar un poco para no precisarla jamás.

overlayfs y swap

https://wiki.openwrt.org/doc/howto/extroot

Configuración puerto Serie
--------------------------

Lo siguiente es instalar el driver del puerto serie y el del arduino.

.. code-block:: bash

    opkg install kmod-usb-acm kmod-usb-serial-ch341  # Driver para el Arduino    

SSL
---

Al instalar los paquetes de python vamos a conectarnos a sitios HTTPS así vamos a precisar instalar los certificados. Quizá exista alguna manera de evitar que pip compruebe las identidades, pero de nuevo, la intersección tiempo y ganas me resulta casi inexistente.

https://wiki.openwrt.org/doc/howto/wget-ssl-certs

.. code-block:: bash

    opkg install ca-certificates

Esto lo hice pero no estoy seguro de que sea necesario.

.. code-block:: bash
   
    opkg update
    opkg install wget
    mkdir -p /etc/ssl/certs
    echo "export SSL_CERT_DIR=/etc/ssl/certs" >> /etc/profile
    source /etc/profile

Octoprint
=========

Lamentablemente no pude instalar la versión más reciente. Aparentemente en algún momento requiere compilar código y en el OpenWRT no hay con que, ni me interesa configurar un ambiente para hacer cross-compiling. Quizá más adelante pueda ser un desafío, ahora mismo quiero terminar esto y dormir como cualquier ser humano.

Así que agarré la versión que puso el tipo acá: https://docs.google.com/file/d/0B6-A_C5DmUPxZFhtMnlVaWdsOWc

También la subi yo por si se cae: https://www.dropbox.com/s/vcwxxzgpwq3t9es/octoprint.zip?dl=0

Environment
-----------

Esto hay que comprobar que funcione realmente. En teoría entrás al environment e instalás todo, pero cuando lo desactivas sigue todo ahí. Super desprolijo... voy a tener pesadillas.

.. code-block:: bash

    opkg install python python-setuptools

Mi router tiene aproximadamente 30mb para archivos temporales en /tmp, que es donde el pip descarga y extrae los paquetes de python. Como lo hace uno por uno, para la mayoría de los paquetes va a funcionar pero hubo uno o dos que daban problema así que directamente armé otro directorio temporal.

.. code-block:: bash
    
    mkdir ~/tmp
    TMPDIR=~/tmp pip install -r octoprint_requirements.txt  # Cambio el dir de los temporales


Conclusiones
============

Velocidad en general. Estabilidad. Ruido en la alimentación?

.. _nota de Matt Defenthaler: http://csmatt.com/notes/?p=154
.. _la página dedicada al wr1043nd de openwrt: https://wiki.openwrt.org/toh/tp-link/tl-wr1043nd

.. [1] Aunque la vida adulta parece ser justamente la extinción de la intersección entre ambas.
