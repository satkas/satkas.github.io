<!--
.. title: Bash - sprawdzenie czy proces jest aktywny z najmniejszymi uprawnieniami
.. slug: bash-sprawdzenie-czy-proces-jest-aktywny-z-najmniejszymi-uprawnieniami
.. date: 2020-09-18
.. tags: bash, linux
.. category: tech
.. link: 
.. description: 
.. type: text
-->

[![Bash](https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1)](https://satkas.waw.pl/?post=bash-sprawdzenie-czy-proces-jest-aktywny-z-namniejszymi-uprawnieniami) Musiałem zrobić skrypt gdzie odpytuję usługi i sprawdzam czy "żyją" i podaję kod wyjśćia dla nagiosa.

Wymaganie było aby zrobić to przy jak najmniejszym nadawaniu uprawnień.

Niby prosta komenda systemctl is-active \*.service jest dobra ale zdalne wykonanie skryptu przez nrpe nie chciało zaskoczyć. Czały cas w logach były komunikaty o u słabych uprawnieniach

Skrypt wykonałem w Bash-u zaprzęgając do tego poczciwą komendę ps. Reszta to już tylko tablice. Dodatkowo problemem było jeszcze nazewnictwo  usług. Np Tomcat posiada proces java, a baza danych PostgreSQL uruchamia proces posmaster. W skrypcie uwzględniłem taki przypadek. Choć wiem, że nie jest elastyczny (można zrobić porównanie po stringach, a nie po indeksach).

```bash

#!/bin/bash

nameS=(httpd java postmaster)
licznik1=0
for i in ${nameS[@]}
do
	ps -C $i >/dev/null
	if [ $? -eq 0 ];then 
		if [ $licznik1 -eq 1 ];then
			wynikP[$licznik1]="Service Tomcat is active"
			((licznik1++))
		elif [ $licznik1 -eq 2 ];then
                        wynikP[$licznik1]="Service PostgreSQL is active"
		else	
			wynikP[$licznik1]="Service $i is active"
			((licznik1++))
		fi
	else
		if [ $licznik1 -eq 1 ];then
                        wynikF[$licznik1]="Service Tomcat is inactive"
                        ((licznik1++))
                elif [ $licznik1 -eq 2 ];then
                        wynikF[$licznik1]="Service PostgreSQL is inactive"
                else
                        wynikF[$licznik1]="Service $i is inactive"
                        ((licznik1++))
                fi
	fi
done

if [ ${#wynikP[@]} -eq 3 ];then
	echo "All services is active: ${wynikP[@]}"
	exit 0
else
	echo "${wynikF[@]}"
	exit 2
fi

```

Aktualizacja: 20 wrzesień 2020r.

Skorygowałem skrypt na taki, który nie używa tablic indeksowych tylko polecenia case. Wydaje się prostszy.

```bash

#!/bin/bash

nameS=(upowerd gnome-shell nautilus)
SUCCESS=""
FAILED=""

for i in ${nameS[@]}
do
	ps -C $i >/dev/null
	if [ $? -eq 0 ];then 
		case $i in
		  "upowerd")
		    SUCCESS+="Service $i is active " ;;
		  "gnome-shell")
		    SUCCESS+="Service Gnome is active " ;;
		  "nautilus")
		    SUCCESS+="Service Menadzer plikow is active" ;;
		esac
		else
		  case $i in
		  "upowerd")
		    FAILED+="Service $i is deactive ";;
		  "gnome-shell")
		    FAILED+="Service Gnome is deactive ";;
		  "nautilus")
		    FAILED+="Service Manadzer plikow is deactive";;
		esac
	fi
done

if [ -z "$FAILED" ];then
	echo "$SUCCESS"
	exit 0
else
	echo "$FAILED"
	exit 2
fi

```

