<!--
.. title: Rozszerzenie partycji w wirtualnym systemie (cfdisk)
.. slug: rozszerzenie-partycji-w-wirtualnym-systemie-cfdisk
.. date: 2021-04-04
.. tags: wirtualizacja, linux, kvm, storage 
.. category: tech
.. link: 
.. description: 
.. type: text
-->

Używam KVM-a jako wirtualizatora. Przychodzi czas kiedy trzeba rozszerzyć partycję na jednym z systemów gościa.

#####Laboratorium:

Host:

```bash

#lsb_release -a
No LSB modules are available.
Distributor ID:    Ubuntu
Description:    Ubuntu Hirsute Hippo (development branch)
Release:    21.04
Codename:    hirsute

```

```

Hypervizor: KVM (libvirtd)

```

```
libvirtd -V
libvirtd (libvirt) 7.0.0

```
 

System Gość: Fedora 34 (beta)

System posiada jeden dysk /dev/vda (24 GB) i partycje mają LVM-a. Powiększę jedną partycję o 2 GB. System gość cały czas jest online


- Wchodzimy do konsoli i wpisujemy virsh.
- Sprawdzamy jakie mamy systemy poprzez wydanie komendy list --all

```bash

Id   Name          State
------------------------------
 3    fedora        running

```

- Sprawdzamy jak nazywa się dysk dla fedora. Wprowadzamy polecenie domblklist fedora

```bash

Target   Source
------------------------------------------------
 vda      /var/lib/libvirt/images/fedora.qcow2
 sda      -

```

- Zwiększamy dysk dla systemu Fedora. Dysk jest plikiem qcow2. Wprowadzamy polecenie blockresize fedora vda 26GB
- Wychodzimy z virsh
- Wchodzimy do systemu gościa fedora
- Wydajemy polecenie jako użytkownik root fdisk -l i patrzymy jak nazywa się dysk widziany przez fedorę

```bash

#fdisk -l

Dysk /dev/vda: 24 GiB, bajtów: 25769803776, sektorów: 50331648
Jednostki: sektorów, czyli 1 * 512 = 512 bajtów
Rozmiar sektora (logiczny/fizyczny) w bajtach: 512 / 512
Rozmiar we/wy (minimalny/optymalny) w bajtach: 512 / 512
Typ etykiety dysku: dos
Identyfikator dysku: 0x2ed117a3

Urządzenie Rozruch Początek   Koniec  Sektory Rozmiar Id Typ
/dev/vda1  *           2048  2099199  2097152      1G 83 Linux
/dev/vda2           2099200 50331647 48232448     23G 8e Linux LVM


Dysk /dev/mapper/fedora_fedora-root: 23 GiB, bajtów: 24691867648, sektorów: 48226304
Jednostki: sektorów, czyli 1 * 512 = 512 bajtów
Rozmiar sektora (logiczny/fizyczny) w bajtach: 512 / 512
Rozmiar we/wy (minimalny/optymalny) w bajtach: 512 / 512


Dysk /dev/zram0: 1,93 GiB, bajtów: 2071986176, sektorów: 505856
Jednostki: sektorów, czyli 1 * 4096 = 4096 bajtów
Rozmiar sektora (logiczny/fizyczny) w bajtach: 4096 / 4096
Rozmiar we/wy (minimalny/optymalny) w bajtach: 4096 / 4096

```

- Interesuje nas dysk /dev/vda2 na którym jest LVM i jest tam główny system plików
- Wprowadzamy w konsoli cfdisk /dev/vda
- Zaznaczamy kursorem pozycję partycji /dev/vda2 i klikamy [Zmiana rozmiaru]
- Narzędzie podpowiada nam rozmiar partycji powiększony o wolną przestrzeń. Klikamy enter i Zapisz. Potwierdzamy wpisując "tak" i klikamy Zakończ
- Partycja jest powiększona ale file system tego jeszcze nie widzi.
- Wykonujemy polecenie pvs

```bash

PV         VG            Fmt  Attr PSize   PFree
/dev/vda2  fedora_fedora lvm2 a--  <23,00g    0

```

- Wykonujemy partprobe /dev/vda i później pvresize /dev/vda2. Sprawdzamy co się zmieniło poprzez komendę pvs

```bash

PV         VG            Fmt  Attr PSize   PFree
/dev/vda2  fedora_fedora lvm2 a--  <25,00g 2,00g

```

- Widać, że mamy dodatkowe 2 GB wolnego miejsca.
- Wydajemy komendę vgs aby potwierdzić, że pojawiło się 2 GB wolnego miejsca

```bash

VG            #PV #LV #SN Attr   VSize   VFree
fedora_fedora   1   1   0 wz--n- <25,00g 2,00g

```

- Teraz rozszerzamy nasz lvm. Polecenie lvs pokazuje listę woluminów logicznych

```bash

LV   VG            Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert

root fedora_fedora -wi-ao---- <23,00g

#lvresize -r -l +100%FREE /dev/fedora_fedora/root
  Size of logical volume fedora_fedora/root changed from <23,00 GiB (5887 extents) to <25,00 GiB (6399 extents).
  Logical volume fedora_fedora/root successfully resized.
meta-data=/dev/mapper/fedora_fedora-root isize=512    agcount=7, agsize=983040 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=0
data     =                       bsize=4096   blocks=6028288, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =log wewnętrzny        bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =brak                   extsz=4096   blocks=0, rtextents=0
bloki danych zmienione z 6028288 na 6552576

```
