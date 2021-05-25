.. title: Usunięcie pustych folderów w bash-u
.. slug: usuniecie-pustych-folderow-w-bash-u
.. date: 2017-01-02
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text


.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1
        :target: https://satkas.waw.pl/?post=usuniecie-pustych-folderow-w-bash-u
        :alt: 'Bash'

Czasami potrzeba usunąć puste foldery w określonej ścieżce. W bashu robi się to banalnie prosto.
::

        find . -type d -empty -delete

wcześniej można sprawdzić jakie katalogi ów polecenie może nam usunąć. Zatem komenda::

        find . -type d -empty -print

pokaże nam wszystkie puste katalogi w określonej ścieżce

Kropka (.) w komendzie określa aktualny katalog. Powyższa komenda działa rekursywnie
