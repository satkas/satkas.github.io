<!--
.. title: Szyfrowane połączenie klientem ftp w konsoli
.. slug: szyfrowane-polaczenie-klientem-ftp-w-konsoli
.. date: 2018-08-31
.. tags: ftp, linux, ssl
.. category: tech
.. link: 
.. description: 
.. type: text
-->

![FTP](https://satkas.waw.pl/data/uploads/images/ftp-ssl.jpg "FTP")

Musimy połączyć się do serwera ftp, który oferuje szyfrowanie. Wiadomo, domyślnie protokół ftp przesyła czystym tekstem wszystkie dane.

W aplikacjach graficznych typu FileZilla przy konfiguracji konta możemy sobie ustawić jakie ma być połączenie (szyfrowane lub zwykłe).

W konsoli narzędzie ftp nie ma zaimplementowanej opcji wyboru trybu szyfrowanego. W repozytoriach jest natomiast aplikacja ftp-ssl, która robi to samo co zwykły klient ftp dodatkowo szyfrując komunikację

Instalujemy aplikację:

```bash

sudo apt install ftp-ssl

```

i logujemy się do serwera:

```bash

ftp-ssl nasz.serwer.ftp

Connected to nasz.serwer.ftp.
220 (vsFTPd 3.0.3)
Name (nasz.serwer.ftp:user):jakis-zalozony-na-serwerze-ftp-user

234 Proceed with negotiation.
[SSL Cipher ECDHE-RSA-AES256-GCM-SHA384]
200 PBSZ set to 0.
200 PROT now Private.
[Encrypted data transfer.]
331 Please specify the password.
Password:

```

Teraz wpisujemy hasło i możemy cieszyć się szyfrowanym połączeniem ftp
