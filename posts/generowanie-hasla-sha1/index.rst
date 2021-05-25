.. title: Generowanie hasła sha1
.. slug: generowanie-hasla-sha1
.. date: 2017-05-13
.. tags: bash, linux
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1
        :target: https://satkas.waw.pl/?post=generowanie-hasla-sha1
        :alt: 'Bash'

W konsoli linuksa wpisujemy
::

        echo -n "satkas" | sha1sum | awk '{print $1}'

Wynik
::

        5e6030bc66eab28e4b5eb6c9278cf41462c88cee


