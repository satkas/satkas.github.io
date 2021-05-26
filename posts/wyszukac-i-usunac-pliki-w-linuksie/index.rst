.. title: Wyszukać i usunąć pliki w Linuksie
.. slug: wyszukac-i-usunac-pliki-w-linuksie
.. date: 2016-12-06
.. tags: linux, bash, skrypt
.. category: tech
.. link: 
.. description: 
.. type: text


.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1
        :target: https://satkas.waw.pl/?post=wyszukac-i-usunac-pliki-w-linuksie
        :alt: 'Bash'

Jak równocześnie wyszukać i przeprowadzić na tych plikach pewne działania, np. usunięcie plików?
::

        find sciezka_do_katalogu -type f -name "*.jpg" -newermt 2015-01-01 ! -newermt 2016-12-05 -exec rm -f {} \;

Co robi to polecenie?

Szuka pliki jpg w przedziale czasowym od 2015-01-01 do 2016-12-05 i usuwa je z systemu
