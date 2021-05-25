<!--
.. title: Windows CMD - Sprawdzenie sumy kontrolnej md5 pliku
.. slug: windows-cmd-sprawdzenie-sumy-kontrolnej-md5-pliku
.. date: 2020-10-29
.. tags: windows, cmd
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Czasami trzeba sprawdzić sumę kontrolną pliku. W linuksie jest to bardzo proste poprzez użycie narzędzi typu md5sum sha256sum. Ale w Windowsie? Moim zdaniem narzędzie do sprawdzania sum kontrolnych powinno być na wysposarzeniu systemu operacyjnego bez instalowania jakiś zewnętrznych paczek. Szukałem, szukałem i się doszukałem

```bash

certutil

```

Tak wiem to jest narzędzie do zarządzania certyfikatami. Można jednak nim sprzwdzić sumę kontrolną pliku i jest domyślnie w systemie.

Sprawdzenie sumy kontrolnej md5 pliku

```bash

certutil -hashfile plik MD5

```
