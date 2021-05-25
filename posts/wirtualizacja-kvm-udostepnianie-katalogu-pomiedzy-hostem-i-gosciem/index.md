<!--
.. title: Wirtualizacja KVM - udostępnianie katalogu pomiedzy hostem i gościem
.. slug: wirtualizacja-kvm-udostepnianie-katalogu-pomiedzy-hostem-i-gosciem
.. date: 2019-09-28
.. tags: linux, kvm, wirtualizacja
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Aby udostepnić katalog pomiędzy hostem (maszyna, która zarządza maszynami wirtualizacyjnymi), a gościem (maszyna wirtualna) wykonujemy:

- na hoscie zakładamy katalog

```bash

mkdir /share

```

nadajemy uprawnienia

```bash

chmod 777 /share

```

- na hoście uruchamiamy virt-manager i otwieramy szczegóły maszyny wirtualnej (ikona żarówki)
- na samym dole klikamy przycisk "dodaj sprzet" i wybieramy "system plików"
- po prawej stronie w sterowniku wybieramy Default
- Tryb wybieram Squash
- ścieżka żródłowa to ścieżka do założonego wcześniej  katalogu (/share)
- w ścieżce docelowej wpisujemy /shares (nazwa może być jakakolwiek)
- startujemy maszynę wirtualną i zakładamy katalog np: /share
- w systemie gościa wykonujemy montowanie:

```bash

mount -t 9p -o trans=virtio,version=9p2000.L /nazwa_nadana_w_virt-manager_w_pozycji_sciezka_docelowa /katalog_zalozony_w_systemie_goscia

```

czyli:

```bash

mount -t 9p -o trans=virtio,version=9p2000.L /shares /share

```
