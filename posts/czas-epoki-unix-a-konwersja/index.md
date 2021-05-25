<!--
.. title: Czas epoki unix-a - konwersja
.. slug: czas-epoki-unix-a-konwersja
.. date: 2019-11-23
.. tags: bash, ntp, time
.. category: tech
.. link: 
.. description: 
.. type: text
-->

[![Bash](https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1 "Bash")](https://satkas.waw.pl/?post=czas-epoki-unix-a-konwersja) Czas w Linuksie liczymy wg tzw epoki unix-a. Co to znaczy?

Jeśli wydamy komendę w Linuksie (terminal)

```bash

 date "+%s"

```
to otrzymamy wynik

```bash

1574511413

```

który nie jest czytelny dla człowieka. Przyzwyczajeni jesteśmy do innego schematu przedstawiania daty i czasu. Czas który widzimy pokazuje ile sekund upłyneło od daty  1970-01-01 00:00:00 UTC.

Aby odczytać czas zapisany w notacji unix-owej możemy użyć komendy

```bash

date -d @1574511413

```

Możemy również użyć perla

```perl

perl -e 'print scalar(localtime(1574511413)), "\n"'

``` 

Z zapisem bardzo często można się spotkać w bazach danych lub logach.

Jak można wykorzystać konwersję w locie?

Przeglądając logi mojego pihole możemy użyć jednolinijkowca awk

Najpierw wgląd jak wygląda standardowe wyjście:

```bash

1574514699|192.168.80.11|POST /admin/list.php?l=black HTTP/1.1|200|20907
1574514700|192.168.80.11|GET /admin/img/donate.gif HTTP/1.1|200|3592
1574514700|192.168.80.11|GET /admin/scripts/pi-hole/php/get.php?list=black&_=1574514700224 HTTP/1.1|200|88
1574514717|192.168.80.11|POST /admin/scripts/pi-hole/php/sub.php HTTP/1.1|200|0

```

Teraz wykonujemy polecenie:

```awk

awk -F"|"  '{ $1=strftime("%F %T",$1); print }' /var/log/lighttpd/access.log

```

Funkcja strftime nie jest dostepna w standardowym awk. Jak wykonamy polecenie pokaże nam się błąd:

```bash

error: "function strftime never defined"

```

Musimy doinstalować gawk. Na raspberrypi zainstalowanego mam Resbiana (Debian) wykonamy więc:

```bash

apt get install gawk

```

Następnie można wykonać ponownie polecenie

```awk

awk -F"|"  '{ $1=strftime("%F %T",$1); print }' /var/log/lighttpd/access.log

```

Wynik, który nam się ukaże to:

```bash

2019-11-23 14:11:37 192.168.80.11 GET /admin/style/vendor/bootstrap/fonts/glyphicons-halflings-regular.woff2 HTTP/1.1 200 18028
2019-11-23 14:11:37 192.168.80.11 GET /admin/img/logo.svg HTTP/1.1 200 1649
2019-11-23 14:11:39 192.168.80.11 POST /admin/list.php?l=black HTTP/1.1 200 20907
2019-11-23 14:11:40 192.168.80.11 GET /admin/img/donate.gif HTTP/1.1 200 3592
2019-11-23 14:11:40 192.168.80.11 GET /admin/scripts/pi-hole/php/get.php?list=black&_=1574514700224 HTTP/1.1 200 88
2019-11-23 14:11:57 192.168.80.11 POST /admin/scripts/pi-hole/php/sub.php HTTP/1.1 200 0

```
