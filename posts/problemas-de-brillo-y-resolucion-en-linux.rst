.. title: Problemas de Brillo y Resolución en Linux
.. slug: problemas-de-brillo-y-resolucion-en-linux
.. date: 2014-07-16 15:28:50 UTC-03:00
.. tags: linux nomodeset backlight grub video
.. link: 
.. description: 
.. type: text

Varias veces me sucedió que, al instalar linux en PCs con alguna placa de video poco común, sea necesario activar el flag 'nomodeset' en el kernel.

Hace unos días un compañero de trabajo me comentó que al instalar Ubuntu en su notebook, la PC booteaba 'a oscuras', es decir, no funcionaba el backlight. Cuando agrego la opción 'nomodeset', se resolvió el probema del brillo... pero dió lugar a un nuevo fenómeno: la computadora iniciaba con una resolución vetusta e inapropiada.

Para resolverlo, sustituimos el parámetro 'nomodeset' por otros dos, 'acpi_osi=Linux' y 'acpi_backlight=vendor'.

El modelo de la notebook es: hp pavilion dm3-1048la.

El output del comando 'lscpi' en lo relativo a la placa de video.

.. code-block:: bash 

    00:02.0 VGA compatible controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07) (prog-if 00 [VGA controller])
        Subsystem: Hewlett-Packard Company Device 3649
        Control: I/O+ Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
        Status: Cap+ 66MHz- UDF- FastB2B+ ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
        Latency: 0
        Interrupt: pin A routed to IRQ 44
        Region 0: Memory at d0000000 (64-bit, non-prefetchable) [size=4M]
        Region 2: Memory at c0000000 (64-bit, prefetchable) [size=256M]
        Region 4: I/O ports at 40f0 [size=8]
        Expansion ROM at <unassigned> [disabled]
        Capabilities: [90] MSI: Enable+ Count=1/1 Maskable- 64bit-
            Address: fee0300c  Data: 41e1
        Capabilities: [d0] Power Management version 3
            Flags: PMEClk- DSI+ D1- D2- AuxCurrent=0mA PME(D0-,D1-,D2-,D3hot-,D3cold-)
            Status: D0 NoSoftRst- PME-Enable- DSel=0 DScale=0 PME-
        Kernel driver in use: i915
    00: 86 80 42 2a 07 04 90 00 07 00 00 03 00 00 80 00
    10: 04 00 00 d0 00 00 00 00 0c 00 00 c0 00 00 00 00
    20: f1 40 00 00 00 00 00 00 00 00 00 00 3c 10 49 36
    30: 00 00 00 00 90 00 00 00 00 00 00 00 0b 01 00 00

.. code-block:: bash 

    00:02.1 Display controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
        Subsystem: Hewlett-Packard Company Device 3649
        Control: I/O+ Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx-
        Status: Cap+ 66MHz- UDF- FastB2B+ ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
        Latency: 0
        Region 0: Memory at d2400000 (64-bit, non-prefetchable) [size=1M]
        Capabilities: [d0] Power Management version 3
            Flags: PMEClk- DSI+ D1- D2- AuxCurrent=0mA PME(D0-,D1-,D2-,D3hot-,D3cold-)
            Status: D0 NoSoftRst- PME-Enable- DSel=0 DScale=0 PME-
    00: 86 80 43 2a 07 00 90 00 07 00 80 03 00 00 80 00
    10: 04 00 40 d2 00 00 00 00 00 00 00 00 00 00 00 00
    20: 00 00 00 00 00 00 00 00 00 00 00 00 3c 10 49 36
    30: 00 00 00 00 d0 00 00 00 00 00 00 00 00 00 00 00
