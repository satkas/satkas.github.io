<!--
.. title: Bash - wyodrębnianie danych IPTC XMP ze zdjęcia
.. slug: bash-wyodrebnianie-danych-iptc-xmp-ze-zdjecia
.. date: 2018-05-22
.. tags: linux, bash, skrypt
.. category: tech
.. link: 
.. description: 
.. type: text
-->

![Bash]( https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1 "Bash")

Jeśli chcemy wydobyć jakąś pojedyńczą sekcję (fotografa, agencję lub opis) ze zdjęcia można użyć narzędzia exiv2.

Wyodrębnienie całości metadanych ze zdjęcia do pliku:

```bash

exiv2 -ea image.jpg

```

Ta komenda utworzy plik o tej samej nazwie co zdjęcie z rozszerzeniem .exv

Wstrzyknięcie tych samych danych z pliku .exv do zdjęcia:

```bash

exiv2 -kia image.jpg

```

Aby wyodrębnić konkretną sekcję np IPTC wydajemy komendę:

```bash

exiv2 -PI image.jpg

```

lub

```bash

exiv2 -pi image.jpg

```

Jeśli chcemy tylko wyodrębnić np. tytuł wydarzenia uwieńczonego na zdjęciu wydajemy komendę:

```bash

exiv2 -PIv -g Iptc.Application2.Headline

```

Oczywiście musimy być pewni, że fotograf, agencja foto podpisuje swoje zdjęcia w programie do edycji meta danych. Inaczej nic nie zobaczymy. Osoby prywatne raczej nie opisują zdjęć więc zobaczysz tylko metadane EXIF(metadane generowane przez aparat fotograficzny).

Jeśli chcemy dodać pojedyńcze rekordy w sekcji np IPTC wydajemy komendę:

```bash

exiv2 -kM"add Iptc.Application2.Headline Jakiś tytuł wydarzenia na zdjęciu" image.jpg

```

Usunięcie sekcji IPTC, XMP, EXIF wykonamy narzędziem jhead

```bash

jhead -dc -de -di -dx image.jpg

```

Oba narzędzia exiv2 i jhead zainstalujemy w ubuntu

```bash

sudo apt install exiv2 jhead

```
