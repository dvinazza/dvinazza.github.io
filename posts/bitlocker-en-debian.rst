.. title: Bitlocker en Debian
.. slug: bitlocker-en-debian
.. date: 2015-07-13 22:51:03 UTC-03:00
.. tags: debian linux bitlocker
.. category: 
.. link: 
.. description: 
.. type: text


Instalación de requisitos

.. code-block:: bash

    apt-get install libfuse-dev libpolarssl-dev
    cd /tmp
    wget https://github.com/Aorimn/dislocker/archive/master.zip
    unzip master.zip 
    cd dislocker-master
    make
    sudo make install 


Montaje de la unidad encriptada, primero como archivo intermedio.

.. code-block:: bash

    mkdir /tmp/dislocker #creo una carpeta para el montaje intermedio
    sudo dislocker -r -V [particion] -p[clave] /tmp/dislocker 


Luego como montaje tradicional.

.. code-block:: bash

    sudo mount -r -o loop /tmp/dislocker/dislocker-file [carpeta donde montar]
