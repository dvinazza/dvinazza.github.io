.. title: Instalando Nagios Core
.. slug: instalando-nagios-core
.. date: 2014-06-30 11:06:50 UTC-03:00
.. tags: nagios, linux, monitoring, network
.. description: Configuración Básica de Nagios Core a partir de los sources
.. type: text
.. author: David Vinazza

Hace tiempo vengo postergando pasar del Nagios disponible en los repositorios de debian/ubuntu a la versión más reciente de Nagios. Por suerte, cuando por fin me decidí encontré mucha documentación al respecto. No inventé nada, lo único que hice fue recopilar información de varios sitios y darle un diseño más simpático, para que sirva de documentación.

requerimientos: apache y php activado

.. code-block:: bash

    apt-get install build-essential

    cd /tmp
    wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.0.7.tar.gz
    tar xvfz nagios-4.0.7.tar.gz
    cd nagios-4.0.7


Creamos los usuarios y grupones necesarios

.. code-block:: bash

    useradd nagios 
    groupadd nagcmd
    /usr/sbin/usermod -a -G nagios nagios
    /usr/sbin/usermod -a -G nagcmd www-data
    /usr/sbin/usermod -a -G nagcmd nagios 

Procedemos con la instalación 

.. code-block:: bash
    
    ./configure --with-nagios-group=nagios --with-command-group=nagcmd --with-mail=/usr/bin/sendmail --with-httpd_conf=/etc/apache2/conf-available
    make all
    make install
    make install-init
    make install-config
    make install-commandmode
    make install-webconf

Activamos la configuración de apache y reiniciamos los servicios 

.. code-block:: bash

    a2enconf nagios.conf 
    service apache2 restart 
    service nagios restart

Y los plugins? Lo mismo. Descarga e instalación. 

.. code-block:: bash

    cd /tmp
    wget http://nagios-plugins.org/download/nagios-plugins-2.0.3.tar.gz
    tar xvfz nagios-plugins-2.0.3.tar.gz

    cd nagios-plugins-2.0.3
    ./configure --with-nagios-user=nagios --with-nagios-group=nagios
    make
    make install 

    service nagios restart #reiniciamos el servicio

