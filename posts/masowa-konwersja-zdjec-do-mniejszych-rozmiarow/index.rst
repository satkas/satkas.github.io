.. title: Masowa konwersja zdjęć do mniejszych rozmiarów
.. slug: masowa-konwersja-zdjec-do-mniejszych-rozmiarow
.. date: 2017-05-16
.. tags: linux, bash, convert
.. category: tech
.. link: 
.. description: 
.. type: text


.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1
        :target: https://satkas.waw.pl/?post=masowa-konwersja-zdjec-do-mniejszych-rozmiarow
        :alt: 'Bash'

Czasami potrzebujemy szybko zmniejszyć zdjęcia do określonej wielkości. Problem w tym, że nie wiemy z jakim zdjęciem mamy do czynienia (portret, panorama). 

Skrypt który ogarnia dwie rzeczy. Sprawdza czy zdjęcie jest portretem lub panoramą i zmniejsza po wielkości. Oczywiście z zachowaniem proporcji

Otwieramy konsolę i wybieramy katalog w którym znajdują się zdjęcia. Po czym wykonujemy tzw jednolinijkowca
::

        for i in `ls *.jpg`;do
                z=$(convert $i -format "%[fx:w/h>1)?1:0]" info:)
                if [ $z -eq 1 ];then
                        convert $i -resize 2000x tmp1/$i
                else
                        convert $i -resize x2000 tmp1/$i
                fi
        done

Ja potrzebowałem przyciąć dłuższy bok do 2000px
