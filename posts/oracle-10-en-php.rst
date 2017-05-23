.. title: Oracle 10 en PHP
.. slug: oracle-10-en-php
.. date: 2014-06-30 18:54:03 UTC-03:00
.. tags: oracle, instantclient, php, oci8, linux
.. link: 
.. description: 
.. type: text

Tiempo atras necesité instalar una versión antigua del cliente de Oracle para un sitio en PHP.

En debian, va a ser necesario tener instalado el programa 'alien', porque Oracle solo provee los RPM para instalar.

Para no depender de Oracle, guardé una copia de los archivos en dropbox_. 

.. _dropbox: https://www.dropbox.com/sh/jyz3zhg0gny63u5/17TascJy9u/instantclient?lst

.. code-block:: bash

    alien -i oracle-instantclient-basic-10.2.0.3-1.i386.rpm
    alien -i oracle-instantclient-devel-10.2.0.3-1.i386.rpm


También va a ser necesario activar la extensión OCI8, mediante el programa 'pecl', creo que es parte del packete 'php-pear'.

.. code-block:: bash

    pecl install oci8

Hay que verificar que en la configuración de php.ini exista lo siguiente 

.. code-block:: 
    
    extension=oci8.so
