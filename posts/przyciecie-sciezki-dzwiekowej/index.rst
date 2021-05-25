.. title: Przycięcie ścieżki dźwiękowej
.. slug: przyciecie-sciezki-dzwiekowej
.. date: 2018-01-08
.. tags: ffmpeg, video
.. category: tech
.. link: 
.. description: 
.. type: text

.. figure:: https://satkas.waw.pl/data/uploads/images/ffmpeg.png
        :target: https://satkas.waw.pl/?post=przyciecie-sciezki-dzwiekowej
        :alt: 'FFMPEG"

Czasami trzeba wyciąć pewien odcinek dźwięku z określonej ścieżki dźwiękowej. Zrobimy to narzędziem ffmpeg.

.. code-block:: bash

        fmpeg -ss 00:00:01 -t 00:01:00 -i wejsciowy-plik.mp3 wyjsciowy-plik.mp3

Wyjaśnienie opcji:

-ss (początek wycięcia względem ścieżki dźwiękowej)

-t (koniec wycięcia względem ścieżki dźwiękowej)

Powstanie nowy plik z 1 - minutową ścieżką dźwiękową

Strona projektu: https://ffmpeg.org
