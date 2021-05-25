<!--
.. title: Windows CMD - brak dostępu
.. slug: windows-cmd-brak-dostepu
.. date: 2020-10-29
.. tags: windows, cmd
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Bardzo często administratorzy Windowsa/AD blokują standardowemu użytkownikowi dostęp do powloki cmd.

Obejściem może tutaj być wykonanie poniższych czynności:

Otwieramy menu start i zaczynamy wpisywać:

```bash

cmd /k jakiś_tool

```

i klikamy enter

Jeśli narzędzie ma jakieś opcje to musimy zamknąć ten wpis w podwójne apostrofy

```bash

cmd /k "ipconfig /all"

```

Jest jeszcze jedna trudność. Jeśli w poleceniu np scieżka ma spację trzeba zrobić to w ten sposób:

```bash

cmd /k "certutil -hashfile "C:\Program Files (x86)\plik.txt" MD5"

```
