.. title: Aktualizacja Roundcube
.. slug: 4-aktualizacja-roundcube
.. date: 2016-11-29 
.. tags: linux, roundcube
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.roundcube.png&c=1
        :target: https://satkas.waw.pl/?post=aktualizacja-roundcube
        :alt: 'Roundcube'

Co jakiś czas należy zaktualizować roundcube.

Programiści tej aplikacji zadbali aby proces ten był lekki, fajny i powabny :)

Pobieramy najnowszą paczkę ze strony https://roundcube.net/download/

Rozpakowujemy archiwum: tar xvf roundcubemail-1.2.3-complete.tar.gz

Wchodzimy do archiwum, następnie wchodzimy do katalogu bin

W katalogu tym wydajemy polecenie::

        ./instalto.sh /var/www

Skrypt potrzebuje ścieżki gdzie położona jest struktura katalogów z oryginalną instalacją roundcube. U mnie jest to /var/www

Odpalamy skrypt i to wszystko
