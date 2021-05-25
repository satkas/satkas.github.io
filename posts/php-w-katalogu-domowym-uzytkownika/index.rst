.. title: PHP w katalogu domowym użytkownika
.. slug: php-w-katalogu-domowym-uzytkownika
.. date: 2017-01-26
.. tags: linux, httpd, php
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.1459870313php-logo.svg.png&c=1
        :target: https://satkas.waw.pl/?post=php-w-katalogu-domowym-uzytkownika
        :alt: 'PHP'

Domyślnym katalogiem składowania plików html i php jest (we współczesnych dystrybucjach) /var/www/html.

W ramach testowania wolę korzystać z katalogu public_html w lokalizacji
::

        /home/*/public_html

Serwer www Apache posiada moduł, który nam to umożliwi.

Pomijam instalację serwera www Apache jak i modułu php dla tego serwera.

Włączamy moduł userdir
::

        a2enmod userdir

restartujemy serwer Apache
::

        service apache2 restart

W ubuntu 16.04 edytujemy plik
::

        /etc/apache2/mods-enabled/php7.0.conf

i komentujemy linię
::

        #php_admin_flag engine Off

Restartujemy usługę
::

        service apache2 restart

i możemy cieszyć się php-em we własnym katalogu

Dostęp przez przeglądarkę możliwy jest poprzez wpis w url
::

        http://localhost/~TwojLogin/


