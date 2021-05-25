<!--
.. title: Filtrowanie logów poczty
.. slug: filtrowanie-logow-poczty
.. date: 2018-09-15
.. tags: poczta, postfix, linux, bash, spam
.. category: tech
.. link: 
.. description: 
.. type: text
-->

![Postfix](https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.postfix.png&c=1 "Postfix")  Potrzebowałem na szybko wyciągnąć wszystkie adresy IP z pliku /var/log/mail.log, które wylądowały w specjalnym folderze z niechcianą pocztą. IP-ki będą wprowadzone na czarną listę adresów.

Wchodzimy do określonego folderu z niechcianą pocztą i wykonujemy polecenie:

```bash

grep -h -o -E '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' *  |sort|uniq |grep -v ".0$" |grep -v "127.0.0.1"

```

####Wyjaśnienie:

Narzędzie grep jest świetnym narzędziem w powłoce BASH na takie zabawy.

Fraza ```'[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}'``` określa adres IP do wyszukania.

Część ```grep -v ".0$"``` realizuje pomijanie całych podsieci (np. x.x.x.0/24)

Część ```grep -v "127.0.0.1"``` pomija adres loopback, który nie ma nic wspólnego z adresem serwera clienta.

Teraz dodajemy adresy do pliku (plik czarnej listy zdefiniowaliśmy w main.cf):

```bash

x.x.x.x REJECT

....

....


```

i klient dostaję zwrotkę na swoją pocztę (wiem, wiem spamerzy mają to głęboko :) )

```bash

Sep 15 09:12:42 rod postfix/smtpd[14454]: NOQUEUE: reject: RCPT from laconic.pauladowson.com[192.155.99.74]: 554 5.7.1 <laconic.pauladowson.com[192.155.99.74]>: Client host rejected: Access denied; from=<milenaxjjpgegbednarek@accvxz.com> to=<jakisnaszemail@jakasnaszadomena> proto=ESMTP helo=<laconic.accvxz.com>

```
