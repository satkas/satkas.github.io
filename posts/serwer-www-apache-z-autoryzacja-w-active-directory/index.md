<!--
.. title: Serwer www Apache z autoryzacją w Active Directory
.. slug: serwer-www-apache-z-autoryzacja-w-active-directory
.. date: 2019-04-14
.. tags: httpd, suse, linux, active directory
.. category: tech
.. link: 
.. description: 
.. type: text
-->


[![Apache](https://satkas.waw.pl/data/uploads/images/httpd_logo.webp "Apache")](https://satkas.waw.pl/?post=serwer-www-apache-z-autoryzacja-w-active-directory)

####Laboratorium

    
- Windows Server 2016 - Active Directory (SATKAS.LOCAL)
- Linux SUSE Standard Enterprise 15 - usługa www oparta o httpd

#####Operacje na Windows Server

Na Windows Server mamy utworzoną domenę SATKAS.LOCAL. Tworzymy grupę apache i użytkowników wedle uznania. Dodajemy użytkowników do grupy apache. Utworzyłem w grupie apache jeszcze jednego użytkownika, który odpowiedzialny będzie za powiązanie nazwy DN podczas fazy wyszukiwania. Nazwałem użytkownika Server Web (konto suse@satkas.local)

 

#####Operacje na SUSE Linux

Zainstalowany mamy serwer www httpd. Uaktywniamy moduły odpowiedzialne za autoryzację w bazie ldap. Są to: ldap i authnz_ldap

Można to zrobić w yast2 (Network Services->HTTP Server). Po czym wykonujemy alt+M (wchodzimy do sekcji Moduły) i z listy wybieramy wspomniane moduły wykonując na nich alt+t (zmień status). Wychodzimy wprowadzając alt+k i alt+z

Można powyższą operację wykonać bezpośrednio w pliku /etc/sysconfig/apache2 dopisując do sekcji

```bash

APACHE_MODULES="authz_host actions alias authz_user authz_groupfile authn_file auth_basic autoindex cgi dir env expires include log_config mime negotiation setenvif userdir ldap authnz_ldap ssl php7 authn_core reqtimeout socache_shmcb authz_core"

```

odpowiednie moduły ldap

Teraz trzeba skonfigurować miejsce w systemie plików do którego dostęp będzie na hasło z Active Directory.

Domyślnie w SUSE tzw DirectoryRoot serwera webowego znajduje się w:

```bash

/srv/www/htdocs (odpowiada za to plik konfiguracyjny w /etc/apache2/default-server.conf)

```

Tworzymy sobie katalog

```bash

mkdir /srv/www/htdoc/sec

```

Tworzymy zawartość katalogu

```bash

touch /srv/www/htdoc/sec/index.html
echo "Strona z uwzględnieniem autoryzacji w AD" > /srv/www/htdoc/sec/index.html

```

Edytujemy plik /etc/apache2/default-server.conf i tworzymy nową sekcję Directory (zaraz pod aktualną sekcją Directory)

```bash

<Directory /srv/www/htdocs/sec>
          AuthLDAPBindDN "CN=Server Web,CN=Users,DC=satkas,DC=local"
          AuthLDAPBindPassword xxxxxxx
          AuthLDAPURL "ldap://satkas.local/CN=Users,DC=satkas,DC=local?sAMAccountName?sub?(objectClass=*)"
          AuthType Basic
          AuthName "SATKAS.LOCAL Authentication"
          AuthBasicProvider ldap
          AuthLDAPGroupAttributeIsDN on
          Require ldap-group CN=apache,CN=Users,DC=satkas,DC=local
</Directory>

```

Po zapisaniu zmian wystarczy zrestartować usługę www

```bash

systemctl restart apache2

```

Autoryzujemy się użytkownikami z grupy (w AD) apache


