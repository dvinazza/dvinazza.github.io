.. title: Respaldar/Restaurar los permisos de una carpeta con BackupPC
.. slug: respaldarrestaurar-los-permisos-de-una-carpeta-con-backuppc
.. date: 2014-09-12 21:44:40 UTC-03:00
.. tags: 
.. link: 
.. description: 
.. type: text

Hace unos días un servidor de archivos con windows amaneció con un RAID degradado. Si bien teníamos respaldo de los archivos, dada la complejidad del árbol de directorios, queríamos respaldar también los permisos de cada carpeta/compartido.

Descubrimos que windows guarda las carpetas compartidas y los permisos de acceso en el registro, y esto vuelve la configuración básica fácil de exportar/importar. Pero no va más allá de quien puede acceder a la carpeta.

.. code-block:: 

    regedit.exe /E compartidos.reg "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Shares"

Por otro lado, microsoft tiene su propias herramienta para administrar los permisos. Pero no llegamos muy lejos por ahí. Nos daba algunos errores incomprensibles.. Así que buscamos directamente una third party que pueda resolver nuestro dilema sin chillar. Ahí encontramos a SetACL_. Si bien tiene una versión paga con interfaz gráfica, la versión gratuita por línea de comandos resultó ideal para programar lo que necesitabamos.

.. _SetACL: https://helgeklein.com/setacl/ 


