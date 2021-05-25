<!--
.. title: Przekierowanie adresu url przy pomocy pliku .htaccess
.. slug: przekierowanie-adresu-url-przy-pomocy-pliku-htaccess
.. date: 2018-04-09
.. tags: linux, httpd
.. category: tech
.. link: 
.. description: 
.. type: text
-->


Czasami potrzeba przekierować url naszej domeny na inny adres (np. gdy chcemy przekierowywać zaindeksowane przez google, nieaktywne pliki na poprawne)

W głównym korzeniu aplikacji www (tam gdzie wskazuje zmienna DocumentRoot w VirtualHost konfiguracji domeny na serwerze Apache2) tworzymy plik .htaccess i wpisujemy do niego:

```bash

Redirect 301 /katalog/plik.html https://domena.tld/katalog2/plik.html

```

####Wyjaśnienie:

```/katalog/plik.html``` 
(to część adresu url po nazwie domeny, który trzeba przekierować)

```https://domena.tld/katalog2/plik.html```
 (nowy adres na który wskazuje przekierowanie)

Czasami trzeba przekierować adres który wskazuje na katalog/kategorię na nowy adres

Wtedy wpisujemy:


```sh

Redirect 301 /katalog/?$ https://domena.tld/katalog2/plik.html

```


