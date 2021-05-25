.. title: Darmowy certyfikat od Let's Encrypt
.. slug: darmowy-certyfikat-od-lets-encrypt
.. date: 2017-01-12
.. tags: certyfikat, httpd, linux
.. category: tech
.. link: 
.. description: 
.. type: text

Aby nie płacić za certyfikat ssl można skorzystać z darmowej alternatywy od Let's Encrypt.

Instrukcja dotyczy systemu operacujnego Debian Wheezy i usługi serwera www (Server version: Apache/2.2.22 (Debian))
::

        wget https://dl.eff.org/certbot-auto
        chmod a+x certbot-auto
        ./certbot-auto --apache
        ./certbot-auto renew

Pierwsza komenda pobiera skrypt
Następnie ustawiamy na skrypcie mozliwość uruchamiania (bit wykonalności)
Odpalamy skrypt z argumentem --apache (to jest mój server www). Po tej operacji mamy zapewniony certyfikat na 3 miesiące.
Ostatnia komenda odnawia nam na kolejne 3 miesiące certyfikat. Wykonujemy ją cyklicznie przed wygaśnięciem certyfikatu.
