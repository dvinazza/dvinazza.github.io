.. title: Encoger discos VirtualBox
.. slug: encoger-discos-virtualbox
.. date: 2014-07-24 15:16:47 UTC-03:00
.. tags: 
.. link: 
.. description: 
.. type: text

La operacion de encoger los discos de VirtualBox no siempre es directa. A veces es necesario 'limpiar' dichos discos de forma tal que todos sus sectores queden realmente vacíos (y no simplemente 'huérfanos').

Cuando el disco en cuestión tiene particiones linux, podemos utilizar la aplicación 'zerofree' para limpiarlo. E incluso podemos montar el disco directamente en un anfitrion para saltarnos la virtualización en lo que a la limpieza concierne.

1. Montaje en el anfitrion

.. code-block:: bash

    modprobe nbd
    qemu-nbd -c /dev/nbd0 [archivo vdi]
    mount -o ro /dev/nbd0p[nro de particion] [punto de montaje]
    #montarlo como read only, para el zerofree


2. Limpieza

.. code-block:: bash

    zerofree /dev/nbd0[nro de particion]

3. Recuperar el espacio asignado

.. code-block:: bash

   umount /dev/nbd0p[nro de particion]
   VBoxManage modifyhd [archivo vdi] --compact



Sitios consultados:
http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/
http://www.thelinuxdaily.com/2010/02/shrinking-a-dynamic-virtualbox-disk-image/

