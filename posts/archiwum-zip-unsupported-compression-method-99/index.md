<!--
.. title: Archiwum zip - unsupported compression method 99
.. slug: archiwum-zip-unsupported-compression-method-99
.. date: 2021-06-02 09:40:20 UTC+02:00
.. tags: linux, zip
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Próbując w Środowisku gnome (u mnie Ubuntu 21.04) otworzyć archiwum zip, które dodatkowo posiada hasło dostaje komunikat, że otwarcie się nie powidło.
Używając prawego przycisku myszy na pliku archiwum zip i wybraniu "Rozpakuj tutaj" tworzy się puste archiwum.
W konsoli sprawdzamy archiwum poleceniem: **file archiwum.zip** otrzymujemy komunikat

```archiwum.zip: Zip archive data, at least v2.0 to extract```

Zwykłe polecenie **unzip archiwum.zip** również nic nie rozpakowywuje jednocześnie informuje komunikatem *unsupported compression method 99*

Rozwiązaniem jest zainstalowanie pakietu *p7zip-full*
