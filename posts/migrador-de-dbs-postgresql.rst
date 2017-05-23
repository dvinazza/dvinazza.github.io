.. title: Migrador de DBs (PostgreSQL)
.. slug: migrador-de-dbs-postgresql
.. date: 2015-07-31 14:40:26 UTC-03:00
.. tags: 
.. category: postgresql 
.. link: 
.. description: 
.. type: text

Hace poco necesité migrar varias bases de postgresql pesadas de un servidor a otro, de una version a otra además, así que tuve que repetir el procedimiento varias veces y asegurarme de que la migración no traía problemas y que la base migrada quedaba actualizada. Naturalmente que fui armando un script para automatizar todo lo posible.

Básicamente lo que hice fue intercambiar las llaves de SSH para que el postgresql del origen pudiese conectarse en el destino. A partir de ahi, probé varias configuraciones para encontrar la más efectiva considerando el uso de recursos como cpu y red.

En caso de que a alguien le sirva, lo dejo en pastebin_. Saludos!

.. _pastebin: http://pastebin.com/g75HRppc
