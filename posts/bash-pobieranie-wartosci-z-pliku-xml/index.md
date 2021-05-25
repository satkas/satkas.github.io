<!--
.. title: Bash - pobieranie wartości z pliku xml
.. slug: bash-pobieranie-wartosci-z-pliku-xml
.. date: 2019-06-20
.. tags: linux, bash, xml
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Czasami potrzebujemy przetworzyć plik xml. Najprawdopodobniej wszystkie liczące się języki programowania mają w swoich zasobach funkcje, które takie operacje realizują. Jeśli chodzi o bash-a to jest trochę inaczej ale jak na środowisko Linuksa przystało zrealizować to zadanie możemy różnymi innymi narzędziami.

W systemie (u mnie OpenSuse 15.1) instalujemy potrzebne narzędzie:

```bash

sudo zypper in xmlstarlet

```

Za plik xml posłuży nam ogólnodostępny plik w serwisie GDDKiA (Generalna Dyrekcja Dróg Krajowych i Autostrad) umieszczony tutaj: https://www.gddkia.gov.pl/dane/zima_html/utrdane.xml

W podanym pliku mamy umieszczone dane z remontów, prac w całej Polsce na drogach administrowanych przez GDDKiA.

Mnie interesuje ile prowadzonych jest inwestycji w poszczególnych województwach. Taką informację możemy wydobyć w bashu tzw jednolinijkowcem.

```bash

curl -s -q https://www.gddkia.gov.pl/dane/zima_html/utrdane.xml |xmlstarlet sel -t -m "utrudnienia" -m "utr" -v "woj" -n |sort |uniq -c |sort -k1 -r

```

Wynik jaki dostanemy to:

```bash

65 mazowieckie
56 małopolskie
36 kujawsko-pomorskie
35 zachodniopomorskie
30 śląskie
28 wielkopolskie
24 lubuskie
22 warmińsko-mazurskie
19 lubelskie
17 podkarpackie
15 świętokrzyskie
13 opolskie
13 łódzkie
11 pomorskie
11 podlaskie
11 dolnośląskie

```
