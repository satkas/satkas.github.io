.. title: Podtrzymywanie "demona" przy życiu
.. slug: podtrzymywanie-demona-przy-zyciu
.. date: 2016-12-17
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text


.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1
        :target: https://satkas.waw.pl/?post=podtrzmywanie-demona-przy-zyciu
        :alt: 'Bash'

Aktualizuję firmowego Ubuntu Server z usługą ftp-a od wersji 8.04 poprzez systemową komendę do-release-upgrade. Aktualnie mam wersję 14.04. Podczas ostatniej aktualizacji do 14.04 usługa ftp zarządzana przez proftpd wywala mi się w nocy. Nie chciało mi się szukać po forach dlaczego co i po co.

Mały skrypt zapuszczony w sesji screen daje pożądany efekt::

        while true; do sleep 45;pidof proftpd;if [ $? -eq 0 ];then echo "Demon nasluchuje"; else echo "Demon wyłączony włączam go"; /etc/init.d/proftpd restart;fi;done


potem tylko Ctrl+A+D i sobie działa
