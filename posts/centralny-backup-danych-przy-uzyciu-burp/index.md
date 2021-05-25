<!--
.. title: Centralny backup danych przy użyciu Burp
.. slug: centralny-backup-danych-przy-uzyciu-burp
.. date: 2018-09-23
.. tags: linux, backup
.. category: tech
.. link: 
.. description: 
.. type: text
-->

[Strona projektu Burp backup](https://burp.grke.org/)

OS serwera: Linux Mint 19.1 (na podstawie Ubuntu 18.04).
Klient (dla przykładu ten sam host co serwer).
Każdy nowy klient tworzony jest analogicznie jak pierwszy na tym samym hoście. Trzeba tylko określić poprawny adres IP serwera.

Instalujemy aplikację na serwerze:

```bash

sudo apt install burp

```

Lokalizacja plików konfiguracyjnych to:

/etc/burp/burp-server.conf (plik konfiguracyjny serwera)

/etc/burp/burp.conf (plik konfiguracyjny klienta)

/etc/default/burp (dodatkowy plik umożliwoający start serwera - wystapuje on tylko w debianopochodnych)

Najpierw w pliku /etc/default/burp zmieniamy opcję:

```bash

RUN=no
na
RUN=yes

```

Idea pracy z aplikacją burp oparta jest na certyfikatach SSL. Przy starcie serwera aplikacja sama automatycznie wystawia certyfikat dla serwera. Domyślnie aplikacja ustawia nazwę CA na burpCA (będzie nam to potrzebne do wystawiania certyfikatów dla klientów)

W pliku konfiguracyjnym serwera zmieniamy:

```bash

address = 192.168.x.x (wpisz adres IP hosta serwera)

status_address = ten sam adres IP co pozycja address

```

Przeładowujemy aplikację:

```bash

systemctl restart burp.service

```

Przechodzimy do konfiguracji klienta. Najpierw wystawiamy certyfikat dla klienta (na serwerze):

```bash

 burp_ca --name Acer --ca burpCA --key --request --sign --batch

```

Opis istotnych przełączników:

--name Acer (dedykowana nazwa cname dla konkretnego klienta)

--ca burpCA (nazwa naszego CA - niezmienna)

Teraz kopiujemy 3 pliki do klienta

- /etc/burp/CA/Acer.crt  (certyfikat klienta)

- /etc/burp/CA/Acer.key (klucz klienta)

- /etc/burp/CA/CA_burpCA.crt (certyfikat naszego CA)

Na serwerze zakładamy plik o nazwie cn jaki nadaliśmy w generowaniu certyfikatu dla klienta (u mnie było to Acer):

- /etc/burp/clientconfdir/Acer

W nim wypełniamy minimum jedną opcję (password = jakieś hasło). Takie samo hasło musi być w konfigu klienta.

Ważna jest też zmiana ścieżki do klucza, certyfikatu i CA w konfigu klienta. Po prostu wpisz ścieżkę (najlepiej w lokalizacji /etc/burp) do tych plików

```bash

ssl_cert_ca = /etc/burp/ssl_cert_ca.pem
ssl_cert = /etc/burp/CA/Acer.crt
ssl_key = /etc/burp/CA/Acer.key

```

Zmieniamy również scieżkę co chcemy "backupować" czyli zmieniamy opcję:

```bash

include = /etc

```

Można takich includów wpisać więcej. Teraz uruchamiamy pierwszy backup. Z pozycji klienta wykonujemy:

```bash

burp -ab

```

Sprawdzamy ile jest backupów:

```bash

burp -al

```

sprawdzamy co jest np w backupie nr 3:

```bash

burp -a l -b 3

```

Teraz chcemy odzyskać backup nr 3

```bash

burp -a r -b 3

```

Chcemy odzyskać pewien katalog z backupu nr 3

```bash

burp -a r -b 3 -r moj_katalog

```

Chcemy odzyskać mój_katalog do innej lokalizacji (domyślnie system próbuje nadpisać oryginalną lokalizację)

```bash
burp -a r -b 3 -r mój_katalog -d /tmp

```

