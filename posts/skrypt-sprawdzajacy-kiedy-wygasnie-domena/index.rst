.. title: Skrypt sprawdzający kiedy wygaśnie domena
.. slug: skrypt-sprawdzajacy-kiedy-wygasnie-domena
.. date: 2017-10-31 22:00:00
.. tags: linux, bash, skrypt
.. category: tech
.. link: 
.. description: 
.. type: text


.. figure:: https://satkas.waw.pl/plugins/news_manager/browser/pic.php?p=https://satkas.waw.pl/data/thumbs/images/thumbnail.bash-logo-web.png&c=1
        :target: https://satkas.waw.pl/?post=skrypt-sprawdzajacy-kiedy-wygasnie-domena
        :alt: 'Bash'

Dla Debiana/Ubuntu/Minta sprawdzamy czy mamy zainstalowany whois wydając w shellu polecenie
:: 

        [ -f '/usr/bin/whois' ] && echo Zainstalowany || apt-get -y install whois

.. code-block:: bash
        :linenos: 

        #!/bin/bash
        
        dzis=$(date +%Y%m%d)
        whois='/usr/bin/whois'
        declare -a domeny='satkas.waw.pl
                jakasinnadomena1.tld
                jakasinnadomena2.tld'

        function sprawdz {
                local red=`tput setaf 1`
                local reset=`tput sgr0`
                local koncowka=${i##*.}
                if [ $koncowka == "com" ]
                then
                        wynik=$( whois $i |grep "Registry Expiry Date" |tr  -d '[:blank:]'|cut -d':' -f2)
                        wynik2=${wynik:0:10}
                        wynik3=$(echo $wynik2 |tr -d '-')
                        roznica=$(( ($(date --date=$wynik3 +%s) - $(date --date=$dzis +%s) )/(60*60*24) ))
                        [$roznica -lt 30 ] && echo "$red ALARM dla domeny $i pozostało $roznica dni   $reset" || echo "$i: Pozostało $roznica dni"

                elif [ $koncowka == "pl" ]
                then
                        wynik=$( whois $i |grep "renewal" |tr  -d '[:blank:]'|cut -d':' -f2)
                        wynik2=${wynik:0:10}
                        wynik3=$(echo $wynik2 |tr -d '.')
                        roznica=$(( ($(date --date=$wynik3 +%s) - $(date --date=$dzis +%s) )/(60*60*24) ))
                        [ $roznica -lt 30 ] && echo "$red ALARM dla domeny $i pozostało $roznica dni      $reset" || echo "$i: Pozostało $roznica dni"

                else
                        echo "Posiadasz domenę która nie odpowiada masce .pl i .com"
                fi
        }

        for i in $domeny
        do
                sprawdz
        done

Pod zmienną tablicową $domeny podstawiamy własne domeny. Pamiętać należy, że główny KRD (Krajowy Rejestr Domen) nakłada limit zapytań do bazy z jednego IP (limit ten to chyba 100 zapytań na dobę)

