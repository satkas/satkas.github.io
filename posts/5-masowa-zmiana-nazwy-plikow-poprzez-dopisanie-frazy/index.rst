.. title: Masowa zmiana nazwy plików poprzez dopisanie frazy
.. slug: 5-masowa-zmiana-nazwy-plikow-poprzez-dopisanie-frazy
.. date: 2016-12-02
.. tags: linux, bash, skrypt
.. category: tech
.. link: 
.. description: 
.. type: text

Potrzebowałem zmienić nazwę plików jpg poprzez dodanie określonej frazy. Czyli mam plik1.jpg, plik2.jpg itd i musze dodać na początku frazę satkas (satkas-plik1.jpg, satkas-plik2.jpg)

W windows można to zrobić w powłoce. Menu start wpisuje cmd i otwieramy "Wiersz polecenia" (taki czarny ekran ;))

W otwartym oknie wpisujemy:

cd ścieżka_do_katalogu_z_plikami

dla upewnienia się sprawdzamy czy są pliki jpg::

        dir *.jpg

Jeśli wszystko się zgadza wpisujemy w terminalu::

        for %%a in (*.jpg) do ren %%a satkas-%%a

Można z tego zrobić plik .bat, który po przeciągnięciu do katalogu i kliknięciu zamieni nam pliki.
::

        @echo off
        setlocal enabledelayedexpension
        set katalog=%cd%
        cd %katalog%
        for %%a in (*.jpg) do (
                ren %%a satkas-%%a
        )
