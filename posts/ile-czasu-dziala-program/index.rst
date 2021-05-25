.. title: Ile czasu działa program?
.. slug: ile-czasu-dziala-program
.. date: 2018-04-06
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text

Jeśli chcemy sprawdzić jaki czas temu został uruchomiony program to można to zrobić na kilka sposobów.

Pierwszy dotyczy kombinacji narzędzi pidof i ps,  a drugi kombinacji narzędzi pidof i ls.

**Rozwiązanie 1 - kombinacja narzędzi pidof i ps**

W shellu wpisujemy pidof firefox.
::

        pidof firefox

Wyświetla się lista wszystkich pid-ów procesów firefoxa. Wybieramy o najniższej wartości po czym używamy narzędzia ps
::

        ps -p TWÓJ_PID -o args,etime,lstart

        
<h3>Wyjaśnienie opcji narzędzia ps:</h3>



-p TWÓJ_PID (należy podać pid programu)

-o args (wyświetli się scieżka do programu)

-o etime (jak długo uruchomiony jest program)

-o lstart (początek uruchomienia programu)

**Rozwiązanie 2 - kombinacja narzędzia pidof i ls**

W shellu wpisujemy pidof firefox.
::

        pidof firefox

Wyświetla się lista wszystkich pid-ów procesów firefoxa. Wybieramy o najniższej wartości po czym używamy narzędzia ls
::

        ls -ld /proc/twój_PID

W wyniku sprawdzamy kolumnę z datą i czasem
