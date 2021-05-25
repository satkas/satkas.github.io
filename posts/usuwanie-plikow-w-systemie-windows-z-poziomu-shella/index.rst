.. title: Usuwanie plików w systemie Windows z poziomu shella
.. slug: usuwanie-plikow-w-systemie-windows-z-poziomu-shella
.. date: 2017-10-30
.. tags: windows, cmd
.. category: tech
.. link: 
.. description: 
.. type: text

Jak administrujemy systemami Windows z pewnością zachodzi potrzeba zwalniania miejsca poprzez usuwanie danych.

Oczywiście mowa tutaj o shellu aby nie robić takich prac z "ręki".

Windows wyposażony jest w narzędzie forfiles.

Mój przykład użycia
::

        forfiles /P F:\ /M *.bak /D -15 /C "cmd /c del @file"

Wyjaśnienie przełączników:

\/P wskazanie scieżki gdzie mamy szukać plików. U mnie w przykładzie jest F:\\

\/M maska jakie pliki mamy szukać. U mnie w przykładzie są pliki \*.bak

\/D opcja wskazuje do jakiej daty program ma zostawiać pliki. Ja ustawiłem 15 dni. Pliki starsze niż 15 dni program ma usunąć.

\/C wywołuje polecenie. Ja wybrałem aby powloka usuwała pasujące pliki. 

Mały skrypt: sprawdz.bat
::

        @echo off
        :main
        CLS

        IF EXIST F:\ (GOTO yes) ELSE (GOTO no)

        :yes
        CLS
        forfiles /P F:\ /M *.bak /D -15 /C "cmd /c del @file"
        exit

        :no
        CLS
        exit
