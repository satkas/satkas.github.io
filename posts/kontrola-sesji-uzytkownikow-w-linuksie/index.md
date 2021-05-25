<!--
.. title: Kontrola sesji użytkowników w Linuksie
.. slug: kontrola-sesji-uzytkownikow-w-linuksie
.. date: 2019-11-09
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Często słyszy się, że w terminalu/konsoli ciężko zarządza się zalogowanymi użytkownikami.

To prawda - jeśli myślimy w perspektywie zarządzania Windowsami. W Linuksie też znajdziemy narzędzia, które pozwalają nam sprawnie zarządzać użytkownikami.

Jest kilka możliwości. Pierwsza to znajome narzędzie who

Za man-em ```who - show who is logged on```

Jeśli chcemy zobaczyć kto jest zalogowany w systemie to wydajemy komendę:

```bash

who

root@raspberrypi:~# who
     pi      pts/0       2019-11-09 13:54 (192.168.80.42)
     user1   pts/1       2019-11-09 15:13 (192.168.80.42)

```

Jest to tylko poglądowa informacja. Aby zobaczyć trochę więcej informacji na temat sesji użytkownika wydajemy polecenie:

```bash

root@raspberrypi:~# who -a
           start systemu 1970-01-01 01:00
           LOGIN     tty1        2019-11-09 12:33              473 id=tty1
           run-level 3 2019-11-09 12:33
           pi      - pts/0       2019-11-09 13:54  .          794 (192.168.80.42)
           user1   + pts/1       2019-11-09 15:13 00:07       1066 (192.168.80.42)

```

Pierwsza kolumna informuje kto jest zalogowany

Druga kolumna informuje do jakiego pseudoterminala lub terminala dany użytkownik został przypisany.

Trzecia kolumna informuje czas kiedy zostało to uczynione.

Czwarta jaki jest PID procesu (będzie ważny jeśli będziemy niedelikatnie podziękować użytkownikowi)

Piąta kolumna informuje skąd nastąpiło logowanie (może to być adres IP lub lokalny terminal czyli tty)

Jeśli chcemy osunąć sesję użytkownika to wydajemy polecenie:

```bash

kill PID czyli w moim przypadku kill 1066

```

polecenie who z opcją -H pokazuje ładnie nam nagłówki kolumn.

Jak wiemy w systemie są nie tylko użytkownicy tzw standardowi (założeni przez administratora) ale również systemowi. Tworzeni są zazwyczaj na potrzeby konkretnych aplikacji.

Aby ich wyświetlić wydajemy polecenie:

```bash

who -Hl ##l jak lolek

```

Drugim narzedziem jest komenda w. Jest bardziej bogatszą wersją w informacje ale brakuje jej jednej ważnej informacji PID procesu. Trzeba szukać jaki proces ma użytkownik pseudoerminala/terminala.

```bash

ps -ef |awk '$9 ~ /pts/ { print $0 }'

```

bądź

```bash

ps -ef |awk '$9 ~ /pts/ || $6 ~ /tty/ { print $0 }'

```

Zdecydowanie polecam ostatnie polecenie. Ma najwięcej możliwość i związany jest z wraz z wprowadzeniem systemd.

Komenda ```loginctl -l``` pokazuje sesje użytkowników

Aby wyświetlić więcej informacji dotyczących sesji wykonujemy polecenie:

```bash

loginctl session-status id_sesji

```

Aby ubić sesję uzytkownika wydajemy polecenie:

```bash

loginctl terminate-session id_sesji

```

lub

```bash

loginctl kill-session id_sesji

```
