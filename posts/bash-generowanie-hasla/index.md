<!--
.. title: Bash - generowanie hasła
.. slug: bash-generowanie-hasla
.. date: 2020-09-08
.. updated: 2021-05-26 14:34
.. tags: bash, linux, password 
.. category: tech
.. link: 
.. description: 
.. type: text
-->

[![Bash](https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1)](https://satkas.waw.pl/?post=bash-generowanie-hasla) Jest wiele sposobów na wygenerowanie hasła. Służą do tego wyspecjalizowane programy(pwgen, keepass itp). Link do tej [strony](https://www.howtogeek.com/howto/30184/10-ways-to-generate-a-random-password-from-the-command-line/) pokazuje "ocean możliwości". Można również samemu sobie stworzyć automat w postacji skryptu bash. Bash się do tego nadaje idealnie.

```bash

#!/usr/bin/env sh

sumaZnakow='16'
probkiHasel='6'

#opcja z argumentami
#sumaZnakow=$1
#probkiHasel=$2

echo "Generowanie $probkiHasel haseł. Hasło ma długość $sumaZnakow znaków"

for ((n=0; n<$probkiHasel; n++))
 do dd if=/dev/urandom count=1 2> /dev/null | uuencode -m - | sed -ne 2p | cut -c-$sumaZnakow 
done

```

Wartości dwóch pierwszych zmiennych można zastąpić argumentami ```$1, $2```

Wtedy wywołanie będzie:

```bash

bash generowanieHasla.sh 16 6

```

#####Aktualizacja

W Ubuntu (u mnie 20.04) trzeba doinstalować pakiet sharutils aby można było używać narzędzia uuencode.
Zmodyfikowałem zatem skrypt aby automatycznie doinstalowywał pakiet.

```bash

#!/usr/bin/env sh

sumaZnakow='16'
probkiHasel='20'

[ -f /usr/bin/uuencode ] &&  echo "Generowanie Haseł" ||  echo "Brak zainstalowanego pakietu uuencode $(sudo apt install -q sharutils -y)"
#opcja z argumentami
#sumaZnakow=$1
#probkiHasel=$2

echo "Generowanie $probkiHasel haseł. Hasło ma długość $sumaZnakow znaków"

for ((n=0; n<$probkiHasel; n++))
 do dd if=/dev/urandom count=1 2> /dev/null | uuencode -m - | sed -ne 2p | cut -c-$sumaZnakow 
done

```
