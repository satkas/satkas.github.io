.. title: Przydatne polecenia w Zimbra
.. slug: przydatne-polecenia-w-zimbra
.. date: 2017-06-10
.. tags: linux, zimbra, poczta
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/data/uploads/images/zimbra.png
        :target: https://satkas.waw.pl/?post=przydatne-polecenia-w-zimbra
        :alt: 'Zimbra'

Jak chcemy cokolwiek zrobić w shellu w systemie Zimbra trzeba się przelogować na użytkownika zimbra
::

        su - zimbra

Wyświetl wszystkich użytkowników domeny
::

        zmprov -l gaa domain.com

Sprawdzenie jaki status ma użytkownik
::

        zmprov ga user@domain.com zimbraAccountStatus | grep zimbraAccountStatus | awk '{print $2}'

Zablokowanie użytkownika
::

        zmprov ma user@domain.com zimbraAccountStatus lock

Odblokowanie użytkownika
::

        zmprov ma user@domain.com zimbraAccountStatus active

Pokaż aktywność w ciągu doby  dla danego konta (wysyłka)
::

        ./libexec/zmmsgtrace -s user@domain.com

Skrypt, który pokaze listę statusu kont dla wszystkich domen
::

        #!/bin/bash
        domeny=$(/opt/zimbra/bin/zmprov gad)
        for domena in $domeny
        do
                konta=$(/opt/zimbra/bin/zmprov -l gaa $domena)
                for konto in $konta
                do
                        wynik=$(/opt/zimbra/bin/zmprov ga $konto zimbraAccountStatus | grep zimbraAccountStatus | awk '{print $2}')
                        echo "$konto $wynik"
                done
        done
