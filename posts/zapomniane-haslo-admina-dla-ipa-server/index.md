<!--
.. title: Zapomniane hasło admina dla ipa server
.. slug: zapomniane-haslo-admina-dla-ipa-server
.. date: 2018-12-02
.. tags: linux, freeipa
.. category: tech
.. link: 
.. description: 
.. type: text
-->

[![FreeIPA](https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.freeipa.png&c=1)](https://satkas.waw.pl/?post=zapomniane-haslo-admina-dla-ipa-server) Jeśli zapomnimy hasło dla super użytkownika admin w usłudze ipa server to zmiana hasła odbywa się wg poniższej procedury.

W konsoli wpisujemy:

```bash

# kadmin.local

kadmin.local:  cpw admin
Enter password for principal "admin@SATKAS.LOCAL":<nowe hasło>
Re-enter password for principal "admin@SATKAS.LOCAL":<nowe hasło>
Password for "admin@SATKAS.LOCAL" changed.

```
