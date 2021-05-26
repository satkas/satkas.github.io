.. title: Zestawienie VPN klient-serwer na stałe (pptp)
.. slug: zestawienie-vpn-klient-serwer-na-stale-pptp
.. date: 2017-03-26
.. tags: mikrotik, vpn, pptp, sieć
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.mikrotik.png&c=1
        :target: https://satkas.waw.pl/?post=zestawienie-vpn-pptp
        :alt: 'Mikrotik'


Mamy taki sobie schemat

.. figure:: https://satkas.waw.pl/data/uploads/images/schematpptp-client-server.jpg
        :alt: 'Schemat sieci vpn'
        :width: 500 px

W biurze mamy skonfigurowany vpn (pptp) jako server. Utworzyliśmy użytkownika.

Po stronie klienta (home) na Mikrotiku klikamy w terminalu
::

        interface pptp-client add connect-to=IP-Server user=login password=password disabled=no name=pptp-out1 profile=default-encryption

user i password wstaw takie dane jak wpisałeś przy zakładaniu użytkowników na serwerze PPTP.

Aby sprawdzić, że urządzenia nawiązały połączenie wykonujemy po stronie klienta
::

        interface pptp-client monitor pptp-out1 without-paging

Powinno nam się wyświetlić coś w tym stylu
::

        status: connected
          uptime: 48m6s
        encoding: MPPE128 stateless
             mtu: 1450
             mru: 1450
        local-address: TWÓJ-IP-PRZYZNANY-PRZEZ-SERVER
        remote-address: ADRES-IP-SERVERA PPTP(PUNKT-PUNKT PPTP)
        
Ważna informacja to pierwsza linia status. Powinno być connected

Teraz aby można było się komunikować potrzebujemy ustawić trasę statyczną do wewnętrznej zdalnej sieci i przez jaki interfejs ma wychodzić. Na Mikrotiku kliencie wpisujemy w terminalu
::

        ip route add dst-address=FIRMOWA-SIEC-LAN/MASKA gateway=pptp-out1

Ponadto potrzeba jeszcze zrobić maskaradę na interfejsie pptp-out1 dla naszej lokalnej sieci w domu

Czyli robimy na Mikrotiku kliencie
::

        ip firewall nat add chain=srcnat action=masquerade src-address=LAN-HOME out-interface=pptp-out1

To powinno dać nam połączenie pomiędzy siecią w domu i firmą.

Dla mnie najlepsze jest w tym to, że nie muszę konfigurować po stronie stacji roboczej żadnego vpn-a. Jak chcę się połączyć do firmy to używam narzędzi takich samych jak wewnątrz firmy.
