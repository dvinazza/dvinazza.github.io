.. title: Alertas de BackupPC sin sendmail
.. slug: alertas-de-backuppc-sin-sendmail
.. date: 2014-07-01 21:37:49 UTC-03:00
.. tags: sendmail, backuppc, msmtp, respaldos, monitoreo, linux
.. link: 
.. description: 
.. type: text

Reemplazar en la configuración del BackupPC el valro de la opción de 'SendmailPath' por '/usr/bin/msmtp'

.. code-block:: bash

    apt-get install msmtp 

Crear un archivo de configuracion en el home de backuppc

.. code-block:: bash 

    su - backuppc
    touch .msmtprc
    chmod .msmtprc

Cargar los siguientes datos dentro.

.. code-block:: 

    account default
    logfile ~/.msmtp.log
    tls off
    auth login
    host [servidor de correo]
    from [usuario]
    user [usuario]
    password [clave]
