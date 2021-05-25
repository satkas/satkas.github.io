<!--
.. title: Bash - wyświetlenie plików w strukturze podobnych katalogów
.. slug: bash-wyswietlenie-plikow-w-strukturze-podobnych-katalogow
.. date: 2019-09-21
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Wyświetlenie plików (lub wpisanie ich do pliku) w pewnej usystematyzowanej strukturze katalogów.

Katalogów jest bardzo dużo ja na potrzeby przykładu utworzyłem katalog-120 do katalog-130. Praca ręczna nigdy nie zostanie wzięta pod uwagę więc trzeba zrobić automat.

Musimy wyświetlić pliki z pewnego przedziału np katalog-120 do katalog-129. Rozwiązań zapewne jest nieskończenie wiele.

- Pierwsze rozwiązanie wykorzystuje printf

```bash

printf "$PWD/%s\n" katalog-12[0-9]/*


/home/tk/skrypty/bash/lab/katalog-120/file2-1
/home/tk/skrypty/bash/lab/katalog-122/file2-1
/home/tk/skrypty/bash/lab/katalog-123/plik1
/home/tk/skrypty/bash/lab/katalog-125/plik5_1
/home/tk/skrypty/bash/lab/katalog-126/file6-1

```

Jeśli chcielibyśmy wypisać same nazwy plików to wynik wkładamy do pętli i poddajemy pod narzędzie basename.

```bash

for i in $(printf "$PWD/%s\n" katalog-12[0-9]/*);do basename $i;done

```

- Drugie rozwiązanie wykorzystuje narzędzie find (moim zdaniem bardziej uniwersalna ponieważ działa również jeśli w katalogach są podkatalogi)

```bash

find ./katalog-12[0-6] -type f -exec basename {} \;

file2-1
file2-1
plik1
plik5_1
file6-1

```

- Trzecie rozwiązanie wykorzystuje narzędzie ls

```bash

ls -1 katalog-12[0-7]/* |tr "\n" "\0" |xargs -0 -n 1 basename

```

bądź krócej:

```bash

ls katalog-12[0-7]/* |xargs -n 1 basename

```

- I kolejna wariacja

```bash

for i in $(find . -print |grep "katalog-12[0-9]");do [[ -f $i ]] && basename $i;done

```

- Bonus w postaci kodu w perl-u

```perl

#!/usr/bin/perl
use strict;
use warnings;
use File::Basename;

my @files = glob('/home/tk/skrypty/bash/lab/katalog-12[0-5]/*');
foreach (@files) {
        print basename($_), "\n";
}

```


