.. title: Synchronizacja czasu w domenie Samba4 na Windows 10 Prof
.. slug: 3-synchronizacja-czasu-w-domenie-samba4-na-windows-10-prof
.. date: 2016-11-28 
.. tags: samba, linux
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.samba.png&c=1
        :target: https://satkas.waw.pl/?post=samba4-problem-z-polaczeniem-do-karberosa
        :alt: 'Samba AD'

Domena na podstawie Samba 4 (4.5.1) na CentOS Linux release 7.2.1511 (Core)

Klient: Windows 10 Prof

Objawy: Brak zakładki Time Internet w Ctrl+I (Ustawienia) -> Data i Czas -> Dodaj zegary do różnych stref czasowych

Rozwiązanie:

Menu Start -> cmd (jako administrator) -> i wpisujemy::

        net time /domain /set /y

Komunikat powinien być taki:

.. figure:: https://satkas.waw.pl/data/uploads/images/ntp.png
        :target: https://satkas.waw.pl/?post=synchronizacja-czasu-w-domenie-samba4-na-windows-10-prof
        :alt: 'Czas w konsoli cmd'


