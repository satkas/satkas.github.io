.. title: Samba4 - problem z połączeniem do kerberosa
.. slug: samba4-problem-z-polaczeniem-do-kerberosa
.. date: 2016-11-12 
.. tags: samba, linux, kerberos
.. category: tech
.. link: 
.. description: Problem z połączeniem do kerberosa
.. type: text

.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.samba.png&c=1
        :target: https://satkas.waw.pl/?post=samba4-problem-z-polaczeniem-do-karberosa
        :alt: 'Samba AD'

Po zainstalowaniu samba4 (ze źródeł) i próbując połączyć się w Ubuntu 16.04 z usługa kerberosa przez wydanie polecenia kinit administrator dostałem komunikat::

        root@rpi:/usr/local/samba/sbin# kinit administrator
        kinit: Cannot contact any KDC for realm 'SATKAS.LOCAL' while getting initial credentials

Wszystkie inne usługi tj: dns, samba działają dobrze.

**Rozwiązanie:**

Edytujemy plik /etc/nsswitch.conf i zmieniamy linię::

        hosts:          files mdns4_minimal [NOTFOUND=return] dns

na::

        hosts:          dns files mdns4_minimal [NOTFOUND=return]
