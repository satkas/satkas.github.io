<!--
.. title: Nowy plik w Ubuntu files (nautilus)
.. slug: nowy-plik-w-ubuntu-files-nautilus
.. date: 2018-04-28
.. tags: linux, ubuntu
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Jak otworzymy manager plików w Ubuntu (środowisko Gnome) i chcemy założyć nowy plik np. plik tekstowy to próbójąc w danym katalogu kliknąć prawym przyciskiem myszy (PPM) nie zobaczymy możliwości utworzenia pliku. Jest możliwość założenia katalogu ale nie wiem dlaczego developerzy Gnome nie dali możliwości użytkownikowi zakładać na starcie nowych plików

![Nautilius](https://satkas.waw.pl/data/uploads/images/ubuntu-files-without-newfile.png "Nautilius")

Aby móc zakadać swobodnie nowe pliki przechodzimy do katalogu domowego użytkownika i wchodzimy do katalogu Szablony (Templates). W katalogu PPM wybieramy "Otwórz w terminalu". W wyświetlonym terminalu wpisujemy

```sh

touch Nowy-plik-tekstowy.txt

```

W menadżerze plików ponownie klikamy PPM i widzimy nową pozycję "Nowy dokument", który prowadzi do możliwości założenia nowego pliku.

U mnie wygląda to tak:

![Nautilius](https://satkas.waw.pl/data/uploads/images/ubuntu-files-with-newfile.png "Nautilius")
