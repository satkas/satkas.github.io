.. title: Wyświetlenie nasłuchujących portów w Windows
.. slug: wyswietlenie-nasluchujacych-portow-w-windows
.. date: 2017-01-08
.. tags: cmd, windows
.. category: tech
.. link: 
.. description: 
.. type: text


Aby zobaczyć jakie porty nasłuchują w Windows otwieramy terminal (cmd) i wpisujemy::

        netstat -aon -p tcp | find /i "listening"

Polecenie dotyczy tylko protokołu tcp (analogicznie można zastąpić tcp frazą udp lub innym protokołem)
