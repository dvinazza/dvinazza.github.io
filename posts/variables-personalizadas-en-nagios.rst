.. title: Variables Personalizadas en Nagios
.. slug: variables-personalizadas-en-nagios
.. date: 2014-07-01 12:02:44 UTC-03:00
.. tags: nagios 
.. link: 
.. description: .. type: text

En caso de que sea necesario agregar una propiedad particular a un objeto de nagios, se pueden definir variables personalizadas anteponiendo un guión bajo al nombre de la propiedad.

Algunos ejemplos:

.. code-block:: 

    define contact {
        contact_name        Pepito Sysadmin
        _twitter_username   nagioslover
    }
    
    define host {
        host_name       SwitchImportante
        _mac_address    00:06:5B:A6:AD:AA
    }

Es importante destacar que cuando se utilicen los macros para completar los valores personalizados en los comandos, es necesario anteponer el origen de la propiedad deseada.


.. code-block:: 

    define command {
        command_name    check_ficticio
        command_line    /usr/local/nagios/libexec/check_ficticio.py $_HOSTMAC_ADDRESS$
    }


http://nagios.sourceforge.net/docs/3_0/customobjectvars.html
