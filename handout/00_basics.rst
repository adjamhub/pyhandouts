==========
Prime cose
==========


.. warning::
    Questa parte della documentazione non è ancora pronta.

    Usa la documentazione in PDF reperibile `qui <https://www.adjam.org/next/index.php/s/egW7AnHxcif8n27?path=%2FPYTHON>`_


.. ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


PRIMA PARLA DELLA DIFFERENZA FRA UNA SCRIPT E UNA COSA INSERITA NELL'INTERPRETE

POI PARLA DI PRINT(), INPUT(), COMMENTI

CAMBIA IL DISCORSO SU HELLO WORLD

Quando si comincia a studiare un nuovo linguaggio, il primo programma che si scrive di solito è il cosiddetto "Hello, World!". 
E’ un semplice programma che scrive semplicemente "Hello, World!", ma in realtà serve per fare un numero incredibile di cose:

* familiarizzare con il nuovo ambiente di programmazione
* provare a scrivere un primo programma
* riuscire nella fase di compilazione/interpretazione/esecuzione del codice
* conoscere l’istruzione principale di output
* e molto altro...

L’istruzione da utilizzare per visualizzare del testo è l’istruzione print(), dove all’interno delle parentesi va inserito, fra doppi apici, 
il testo da visualizzare. Ad esempio:

.. code:: python

    >>> print("Ciao")
    Ciao


Non mi sembra molto complicato... Capite bene che il programma "Hello, World!" consta di un’unica riga contenente la stringa stessa.

.. code:: python

    >>> print("Hello, World!")
    Hello, World!


Ecco fatto!

Proviamo adesso a scrivere il codice che dovrebbe andare nel file "HelloWorld.py" e provate ad eseguire quello per verificare che sappiamo far 
funzionare anche questa cosa.

.. code:: python

    File: HelloWorld.py
    # Questo è un commento
    # serve a spiegare in italiano alcune cose...
    # ad esempio:
    # l’istruzione print() visualizza sullo schermo il suo contenuto
    print("Hello, World!")

Con la scusa di scrivere insieme il file HelloWorld.py abbiamo inserito un concetto nuovo: i commenti al codice!
Come vedete, ogni commento inizia con un # e fino a fine riga potete scrivere ciò che volete. Se vi serve o preferite una riga di commento in più... 
rimettete un # all’inizio.

I commenti semplificano il lavoro di rilettura del codice, soprattutto quando le righe di codice si avvicinano pericolosamente alle centinaia. 
Inoltre, cosa ancora più importante, piacciono al vostro prof! Quindi scriveteceli! Sempre! Spiegate in ogni porzione di codice l’idea che vi frulla 
in mente e quello che volete fare per realizzarla!


Il secondo programma da provare prevede l’introduzione della funzione complementare alla print(), ovvero quella che permette all’utente di inserire un valore: 
**la funzione input()**. Vediamo un esempio:

.. code:: python

    >>> # i commenti funzionano anche nell’interprete :)
    >>> nome = input("Come ti chiami? ")
    Come ti chiami? Andrea
    >>> nome
    ‘Andrea’

Ecco fatto! Provate questo codice e scrivete lo script WhatsYourName.py per chiedere all’utente il proprio nome. E il primo step è fatto…



Esercizi
========


Per ognuno dei seguenti quesiti, creare uno script per eseguire la richiesta dell’esercizio:


**Esercizio 1**

Visualizzare sullo schermo la scritta seguente:

.. code::

    Ciao, mi chiamo Pinco Pallino


.. line::


**Esercizio 2**

Visualizzare sullo schermo la scritta seguente (andando a capo quando necessario):


.. code::
    
    Ciao, 
    mi chiamo 
    Pinco Pallino

.. line::


**Esercizio 3**

Visualizzare sullo schermo il seguente disegno:

.. code::

    + + + +
    +     +
    +     +
    + + + +

