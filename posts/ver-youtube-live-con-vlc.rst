.. title: Ver Youtube Live con VLC
.. slug: ver-youtube-live-con-vlc
.. date: 2014-08-31 19:25:53 UTC-03:00
.. tags: 
.. link: 
.. description: 
.. type: text

Estoy mirando 'Fútbol para Todos' con el VLC, funciona espectacular. El único problema que le encontré: no puedo elegir la resolución, y el VLC no siempre reanuda automáticamente la recepción.

Por suerte encontré una aplicación en python que se encarga de extraer el stream adecuado y abrir el VLC para verlo.


.. code-block:: bash 

    $ sudo pip install livestreamer

    #livestreamer [url del video]
    $ livestreamer http://www.youtube.com/watch?v=HBfpr5Ye35c
    [cli][info] Found matching plugin youtube for URL http://www.youtube.com/watch?v=HBfpr5Ye35c
    Available streams: 240p, 360p, 480p, 720p (best), 72p (worst)

    #livestreamer [url del video] [stream]
    $ livestreamer http://www.youtube.com/watch?v=HBfpr5Ye35c 480p
    [cli][info] Found matching plugin youtube for URL http://www.youtube.com/watch?v=HBfpr5Ye35c
    [cli][info] Available streams: 240p, 360p, 480p, 720p (best), 72p (worst)
    [cli][info] Opening stream: 480p (hls)
    [cli][info] Starting player: /usr/bin/vlc



