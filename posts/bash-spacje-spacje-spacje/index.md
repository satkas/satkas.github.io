<!--
.. title: BASH - spacje, spacje, spacje
.. slug: bash-spacje-spacje-spacje
.. date: 2020-04-30
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text
-->

[![Bash](https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1 "Bash")](https://satkas.waw.pl/?post=bash-spacje-spacje-spacje)  Świat nie jest idealny. Jednym z wielu aspektów, które obrazują nam taki obraz świata są przyzwyczajenia w tworzeniu plików i katalogów.

Według tzw "świata \*nixowgo" pliki/katalogi powinno się tworzyć bez spacji aby późniejsze przetwarzanie nie powodowało problemów. W swiecie windows-a nie ma to większego znaczenia i system ten "przyzwyczaił" ludzi do tworzenia nazw plików i katalogów tak jakby mieli napisać krótki esej.

Aby w Linuksie obejść problem spacji możemy posłużyć się pętlą while, która przetwarza pliki/wyjśćia innych poleceń linia po lini.

I tak jeśli chcemy coś zrobić z plikiem (np skopiować, przenieść w iine miejsce) możemy zastosować rozwiązanie:

```bash

while read p;do
  mv "${p}" "/tmp/${p}"
done <<< $(find . -mindepth 1 -maxdepth 1 -type f ! -name ".*")

```

Pętla filtruje tylko pliki i  przenosi pliki do katalogu /tmp

Komenda

```bash

find . -mindepth 1 -maxdepth 1 -type f ! -name ".*"

```

wyszukuje tylko pliki w katalogu, którym wykonywany jest skrypt i nie bierze pod uwagę tzw plików ukrytych

Nie ma znaczenia czy plik ma spację w nazwie.
