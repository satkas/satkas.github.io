<!--
.. title: Bash - pojemność katalogu z filtrem na pliki
.. slug: bash-pojemnosc-katalogu-z-filtrem-na-pliki
.. date: 2018-05-15
.. tags: linux, bash, skrypt
.. category: tech
.. link: 
.. description: 
.. type: text
-->

![Bash](https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1 "Bash")

Zawartość skryptu. Skrypt posiada 2 zmienne. Zmienna $folder to obliczany folder. Zmienna $ext to rozszerzenie plików, które będą zliczane. Skrypt oblicza pojemność katalogu rekursywnie i ogranicza się tylko do plików jpg  

```bash

#!/bin/bash
folder='/home/user/Obrazy'
ext='.jpg'

foldersize() {
    if [ -d $folder ]; then
        size=$(ls -alRF $folder/ | grep -i $ext | awk 'BEGIN {tot=0} { tot=tot+$5 } END { print tot }')
        countsize=${#size}
        echo "Znaków: $countsize"
        echo "Podliczanie plików $ext"
        if [ $countsize -lt 4 ];then
         echo -n "Zajętość katalogu `realpath $folder`"
         echo "${size}B"
        elif [ $countsize -ge 4 ] && [ $countsize -lt 7 ];then
         echo -n "Zajętość katalogu `realpath $folder` w KB: "
         echo "scale=2;$size/1024" |bc -l
        elif [ $countsize -ge 7 ] && [ $countsize -le 9 ];then
         echo -n "Zajętość katalogu `realpath $folder` w MB: "
         echo "scale=2;$size/1024/1024" |bc -l
        else
         echo -n "Zajętość katalogu `realpath $folder` w GB: "
         echo "scale=2;$size/1024/1024/1024" |bc -l
        fi
    else
        echo "$folder: folder does not exist"
    fi
}

foldersize

```
