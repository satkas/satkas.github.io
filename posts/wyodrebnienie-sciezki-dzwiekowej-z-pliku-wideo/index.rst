.. title: Wyodrębnienie ścieżki dźwiękowej z pliku wideo
.. slug: wyodrebnienie-sciezki-dzwiekowej-z-pliku-wideo
.. date: 2018-01-08
.. tags: video, ffmpeg
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/data/uploads/images/ffmpeg.png
        :target: https://satkas.waw.pl/?post=wyodrebnienie-sciezki-dzwiekowej-z-pliku-wideo
        :alt: 'ffmpeg'

Instalujemy aplikację ffmpeg (w linux Ubuntu 16.04)

.. code-block:: bash

        sudo apt install ffmpeg
        ffmpeg -i wejsciowy_plik_wideo.mkv wyjsciowy_plik_dzwiekowy.mp3

Format pliku wideo może być inny niż \*.mkv

Strona projektu: https://ffmpeg.org
