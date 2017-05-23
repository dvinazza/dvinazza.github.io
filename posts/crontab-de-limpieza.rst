.. title: Crontab de limpieza
.. slug: crontab-de-limpieza
.. date: 2014-06-30 11:51:14 UTC-03:00
.. tags: linux, crontab, find, cleanup
.. link: 
.. description: 
.. type: text

Frecuentemente necesitamos limpiar carpetas que usamos de forma temporal, por ejemplo, una carpeta compartida que utilizamos para intercambiar archivos.
Para realizar la limpieza, podemos utilizar el crontab y el comando find. 

Por ejemplo, podemos limpiar la carpeta los lunes por la madrugada.

.. code-block:: bash

    0 5 * * 1 find [carpeta] -mindepth 1 -mtime +[dias de antigüedad] -delete

