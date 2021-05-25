.. title: Usprawnienia dla logowania po ssh
.. slug: usprawnienia-dla-logowania-po-ssh
.. date: 2018-02-26
.. tags: ssh
.. category: tech
.. link: 
.. description: 
.. type: text


Jeśli mamy wiele serwerów i musimy często się na nie logować to można sobie taką czynność uprościć. Pierwsza sprawa to wyłączenie logowania po haśle i logowanie przy pomocy kluczy.

Druga to utworzenie pliku ~/.ssh/config i wpisanie wszystkich hostów na które będziemy się logować. Struktura takiego pliku to np::

        Host mail
        Hostname x.x.x.x
        user jakislogin
        Port 22
        TCPKeepAlive yes
