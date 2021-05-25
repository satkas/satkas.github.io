<!--
.. title: Certyfikat dla usługi IIS
.. slug: certyfikat-dla-uslugi-iis
.. date: 2019-07-09
.. tags: windows, iis, certyfikat, ssl
.. category: tech
.. link: 
.. description: 
.. type: text
-->


Certyfikat dla usługi IIS

Opublikowano 9 lip 2019

Przeprowadzamy proces generowania wniosku (możliwości są dwie)

- Generowanie wniosku na stronie podmiotu u którego kupujemy certyfikat
- Na własnym komputerze. Ja realizuję to narzędziem openssl

Wysyłamy wniosek do podmiotu u którego kupujemy certyfikat

Po pewnym czasie otrzymujemy prośbę o potwierdzenie, że chcemy kupić certyfikat (wiadomość pochodzi od podmiotu, który generuje certyfikat - u mnie był to RapidSSL)

W końcu dostajemy certyfikat, klucz i certyfikat RootCA

Teraz przystępujemy do konwersji certyfikatu z formatu .pem do .pfx

```bash

openssl pkcs12 -export -out certyfikat-naszadomena.pfx -inkey klucz.key -in certyfikat-naszadomena.pem -certfile RootCA.pem

```

Podczas konwertowania zostaniemy poproszeni o ustanowienie hasła. Powinniśmy go teraz ustanowić.

Przekonwertowany certyfikat kopiujemy na serwer Windows. Klikamy prawym przyciskiem myszy i instalujemy certyfikat. (Wybieramy Local machine, wpisujemy hasło i zaznaczamy opcję Automatically select the certificate store based on the type of certificate). Po zainstalowaniu certyfikatu wchodzimy do Internet Information Services. W panelu po lewej rozwijamy IIS->Sites->Default Web Site i klikamy aby zaznaczyć. Po prawej w panelu wybieramy Bindings..

Pokaże nam się lista na jakich portach nasłuchuje usługa www. Powinno być 80 i 443 (jeśli nie ma to ją tworzymy). Zaznaczamy pozycję 443 i edytujemy. W pozycji SSL Certificate klikamy Select i wybieramy certyfikat, który zainstalowaliśmy wcześniej. Akceptujemy i certyfikat jest podmieniony.
