.. title: Ile waży baza MySQL?
.. slug: ile-wazy-baza-mysql
.. date: 2017-02-09 
.. tags: mysql
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.mysql.svg.png&c=1
        :target: https://satkas.waw.pl/?post=ile-wazy-baza-mysql
        :alt: 'MySQL'

Wchodzimy do shella (konsola, terminal itp) i dostajemy się do naszego silnika mysql
::

        mysql -u root -p

Zgłasza nam się znak zachęty
::

        mysql>

Wpisujemy komendę
::

        SELECT table_schema "DB", Round(Sum(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB" FROM   information_schema.tables GROUP  BY table_schema;


