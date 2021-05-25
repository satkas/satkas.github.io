.. title: Czytanie pliku w skrypcie linia po linii
.. slug: czytanie-pliku-w-skrypcie-linia-po-linii
.. date: 2017-11-07
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text


.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1
        :target: https://satkas.waw.pl/?post=czytanie-pliku-w-skrypcie-linia-po-linii
        :alt: 'Bash'

Bardzo często trzeba w skryptach bash czytać pliki linia po linii i coś z tymi liniami robić.
Bash posiada dwie pętle, które się do tego zadania nadają.

.. code-block:: bash

        for .. in .. ;do .. done

i

.. code-block:: bash

        while .. ;do .. done

Rozwiązanie dla pętli for

.. code-block:: bash
        :linenos:
        
         nIFS=$IFS
         IFS=$(echo -ne "\n\b")
                for i in $(cat plik.txt);do
                        echo $i
                done
         IFS=$nIFS

Rozwiązanie dla pętli while

.. code-block:: bash
        :linenos: 

        while read i;do
                echo $i
        done < plik.txt




