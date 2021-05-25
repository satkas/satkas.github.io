<!--
.. title: CentOS - NRPE: Unable to read output
.. slug: centos-nrpe-unable-to-read-output
.. date: 2020-09-15
.. tags: linux, centos, nrpe, nagios
.. category: 
.. link: 
.. description: 
.. type: text
-->

Jeśli mamy skonfigurowaną na kliencie usługę nrpe do monitorowania przez nagios/centreon na Centosie/RedHacie/Fedorze (generalnie tam gdzie włączony jest Selinux) możemy otrzymać zwrot w postaci takiego komunikatu:

```bash

NRPE: Unable to read output

```

Okazuje się, że odpowiedzialny za ten stan jest Selinux. Po prostu nie pozwala zdalnie wykonać skryptu, który wrzuciliśmy do lokalizacji:

```bash

/usr/lib64/nagios/plugins/

```

U mnie chodziło o skrypt perlowy check_ifutil.pl

#####Rozwiązanie 1:

Wykonujemy komendę:

```bash

sudo chcon -t nagios_unconfined_plugin_exec_t /usr/lib64/nagios/plugins/check_ifutil.pl

```

#####Rozwiązanie 2:

Jeśli nie masz włączonego SElinuxa to przyczyną może być brak uprawnień do wykonywania skryptu. Wykonaj więc:

```bash

chmod +x nazwa_pliku

```

