.. title: Autoresponder dla kont pocztowych
.. slug: autoresponder-dla-kont-pocztowych
.. date: 2018-02-18
.. tags: bash, poczta
.. category: tech
.. link: 
.. description: 
.. type: text

W "najsurowszej" kombinacji usług pocztowych (postfix+dovecot+amavisd) dzięki którym możemy stworzyć własny system pocztowy nie ma funkcji autorespondera.

Możemy szybko taką funkcję dodać do wspomnianej konfiguracji.

W systemie Ubuntu instalujemy paczkę vacation.

Pliki, które są istotne

.. code-block:: bash

        ~/.vacation.db   plik bazy tworzony podczas inicjalizacji.
        ~/.vacation.msg  plik wiadomości autorepondera
        ~/.forward plik dzięki któremu przekazujemy otrzymaną pocztę do aplikacji vacation

::

        ~ 
       
Tylda oznacza katalog domowy użytkownika. Czyli jak konto jest user1@domena.net to wspomniane pliki muszą znajdować się w lokalizacji (przy założeniu, że system pocztowy opiera się na zwykłych kontach systemu operacyjnego ):

::

        /home/user1

Tworzymy wspomniane pliki i wypełniamy treścią:

plik ~/.forward zawiera

.. code-block:: bash

        \user1, "|/usr/bin/vacation -a user1@domena.net"

plik ~/.vacation.msg zawiera

::

        MIME-Version: 1.0
        Content-Type: text/html; charset="utf-8"
        Content-Transfer-Encoding: 8bit
        Subject: [Autoresponder] Urlop

        Dziękuje za wiadomość. W dniach 19/02/2018 - 28/02/2018 jestem nieobecny w biurze. Na wszystkie wiadomości odpowiem po powrocie.

Wyjaśnienie:

Pierwsze 3 linie są potrzebne po to aby w kliencie pocztowym odbiorców treść autorespondera wyświetlała polskie znaki (2 linia). Jeśli używasz tylko języka angielskiego to te 3 linie nie są wymagane. Czasami serwery pocztowe są tak skonfigurowane, że jak nie ma odpowiednich nagłówków we wiadomości to podnoszą ryzyko wystąpienia jako spam. Więc warto tworzyć właściwą kopertę wiadomości.

Wystarczy teraz tylko wydać polecenie
::

        vacation -i

i wszystko co przychodzi na konto pocztowe user1@domena.net jest domyślnie raz na dobę odbijane do nadawcy treścią z pliku .vacation.msg

