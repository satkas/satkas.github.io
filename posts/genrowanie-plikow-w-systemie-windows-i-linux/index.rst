.. title: Genrowanie plików w systemie Windows i Linux
.. slug: genrowanie-plikow-w-systemie-windows-i-linux
.. date: 2016-12-02
.. tags: linux, bash, windows, cmd, skrypt
.. category: tech
.. link: 
.. description: 
.. type: text

Czasami zachodzi potrzeba wygenerowania sobie plików na potrzeby różnych testów.

W Windows robię w ten sposób.

Otwieram "Wiersz poleceń" i wpisuję::

        for /L %%a in (1,1,100) do fsutil file createnew plik-%%a.txt 0

W Linuksie otwieram konsolę i wpisuję::

        for i in `seq 1 100`;do touch plik-$i.txt;done

I pod Windowsem i pod Linuksem skrypcik wygeneruje nam 100 plików o zerowym rozmiarze
