<!--
.. title: KVM - zmiana na żywo rozmiaru "file" dysku - bez LVM-a
.. slug: kvm-zmiana-na-zywo-rozmiaru-file-dysku-bez-lvm-a
.. date: 2020-05-14
.. tags: linux, kvm, wirtualizacja, lvm, storage
.. category: tech
.. link: 
.. description: 
.. type: text
-->


[![iKVM](https://satkas.waw.pl/data/uploads/images/kvm-logo.webp "KVM"){ width=300 }](https://satkas.waw.pl/?post=kvm-zmiana-na-zywo-rozmiaru-file-dysku) Czasami staniemy przed sytuacją zapełnienia dysku w maszynie wirtualnej.

Jeśli używamu KVM i za dysk służy nam plik (qcow2) możemy dokonać zmiany rozmiaru poprzez standardowe narzędzia.

Najpierw identyfikujemy nasze maszyny wirtualne

```bash

virsh list --all
Id Name      State
----------------------------
1  centos8-2 running
-  centos8   shut off
-  debian10  shut off
-  win10     shut off

```

Póżniej sprawdzamy jaki rodzaj pamięci masowej podpięty jest pod maszynę wirtualną

```bash

virsh domblklist centos8-2

Target  Source
------------------------------------
vda     /home/tk/vm/Resize.qcow2
sda     -

```

Widzimy, że za dysk służy plik. Aby sprawdzić informacje o takim file dysku użyjemy polecenia:

sudo qemu-img info /home/tk/vm/Resize.qcow2

Niestety aby otrzymać informację musimy wyłączyć maszynę.

Nie o to nam przecież chodzi. Musimy wszystko przeprowadzić na działającej maszynie.

Użyjemy do tego polecenia:

```bash

virsh qemu-monitor-command centos8-2 info block --hmp

libvirt-2-format: /home/tk/vm/Resize.qcow2 (qcow2)
	Attached to: /machine/peripheral/virtio-disk0/virtio-backend
	Cache mode: writeback

sata0-0-0: [not inserted] Attached to: sata0-0-0 Removable device: not locked, tray closed

```

Tutaj mamy więcej danych. Lub możemy wykorzystać poprzednie polecenie ale w rozszerzonym formacie:

```bash

virsh domblklist centos8-2 --details

Type Device Target Source
----------------------------------------------------
file disk   vda /home/tk/vm/Resize.qcow2
file cdrom  sda -

```

Następnie dokonujemy rozszeżenia dysku

```bash

virsh blockresize centos8-2 vda 20G
Block device 'vda' is resized

```

Sprawdzamy fdisk-iem czy powiększył nam się dysk

```bash

fdisk -l

```

Ostatnim krokiem jest rozszeżenie filesystemu (u mnie główna partycja)

Najpierw na maszynie wirtualnej instalujemy paczkę:

Dla Ubuntu

```bash

sudo apt install cloud-guest-utils

```

dla CentOS-a

```bash

sudo yum install cloud-utils-growpart

```

Poniższym poleceniem wskazujemy dysk i numer partycji do wypełnienia (u mnie 3). Jak mamy ponumerowane partycje na dysku możemy sobie sprawdzić narzędziem parted. Po wykonaniu polecenia parted, wpisujemy print. Kolumna Number pokazuje nam partycje ponumerowane.

```bash

growpart /dev/vda 3

```

Na sam koniec wykonujemy rozszerzenie na filesytemie

```bash

xfs_grows /

```

