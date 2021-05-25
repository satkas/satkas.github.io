.. title: Aktualizacja samby jako domain controller
.. slug: aktualizacja-samby-jako-domain-controller
.. date: 2017-01-18
.. tags: linux, samba
.. category: tech
.. link: 
.. description: 
.. type: text

Używana wersja to 4.5.3 i była instalowana ze źródel.

Pobieramy wersję 4.5.4
::

        wget https://download.samba.org/pub/samba/stable/samba-4.5.4.tar.gz

zabijamy wszystkie procesy samby działające w systemie
::

        pkill samba

Robimy backup obecnej samby
::

        tar czvf samba-4.5.3.tar.gz /usr/local/samba

Rozpakowujemy archiwum nowej samby
::

        tar xzvf samba-4.5.4.tar.gz

wchodzimy do katalogu
::

        cd samba-4.5.4

i wykonujemy polecenie
::

        ./configure

po skończeniu budujemy
::

        make

i ostatecznie instalujemy (z uprawnieniami root)
::

        make install

Po skończeniu sprawdzamy czy nasza baza jest spójna
::

        /usr/local/samba/bin/samba-tool dbcheck

Startujemy z nową sambą wydając polecenie
::

        /usr/local/samba/sbin/samba

Sprawdzamy status wersji
::

        /usr/local/samba/bin/samba-tool -V

Cały proces u mnie na Raspberry PI3 trwa 2h
