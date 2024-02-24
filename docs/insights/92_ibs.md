# Interi, bytes, stringhe

In questa sezione vorrei regalare alcune piccole delucidazioni su come funzionano gli interi in Python e come si confrontano con i bytes
e la loro rappresentazione sotto forma di stringhe.

Questo approfondimento è necessario soprattutto quando si lavora con dati in rete, in cui il formato privilegiato per la trasmissione è chiaramente
quello in `bytes`.

Ma andiamo con ordine.


## Interi, base 2, 8, 10, 16

Le basi numeriche più comuni sono chiaramente (in rigoroso ordine crescente) le basi 2, 8, 10, 16. A dire la verità, la base più comune è la base 10 (e questo perché abbiamo 10 dita...).
Le altre sono diventate comuni soprattutto grazie all'informatica.

Vediamo come rappresentare cifre nelle diverse basi:

``` python
interoBase10 = 27       # come ovvio... è 27 in base 10. 27...
interoBase2  = 0b1101   # 1101 in base 2. Ovvero 13 in base 10.
interoBase8  = 0o13     # 13 in base 8. Ovvero 11 in base 10.
interoBase16 = 0xAF     # AF in base 16. Ovvero 175 in base 10.
```

Come si vede Python fornisce dei prefissi semplici per indicare un numero nelle basi comuni. Facile!

!!! warning "Attenzione!"

    Quando andate a visualizzare questi numeri, ad esempio con una print, vedrete sempre e comunque la loro rappresentazione decimale:
    
    ``` python
    print(interoBase10) # scrive 27
    print(interoBase2)  # scrive 13
    print(interoBase8)  # scrive 11
    print(interoBase16) # scrive 175
    ```

Se invece **avete un numero decimale e lo volete rappresentare in binario, ottale, esadecimale**, Python fornisce delle comodissime funzioni predefinite. 
Occhio che per *cristallizzare* la rappresentazione dei numeri in quella base, Python in realtà crea delle stringhe!

Vediamo il codice:

``` python
a = 67
b = bin(a)   # b è la stringa '0b1000011'
c = oct(a)   # c è la stirnga '0o103'
d = hex(a)   # d è la stringa '0x43'
```

Se invece abbiamo delle stringhe che rappresentano dei numeri in base 2,8,10,16, lo strumento da utilizzare è la funzione `int()` con accortezza!

Infatti!

``` python
s1 = '89'
n1 = int(s1)            # Vale l'intero 89. Questo lo sapevamo già...

s2 = '0b101'
n2 = int(s2)            # ERRORE!!! Non sa come convertire la b...
n2 = int(s2, base = 2)  # Vale l'intero 5, la conversione di 101(2) in decimale

s3 = '0o23'
n3 = int(s3)            # ERRORE!!! Non sa come convertire la o...
n3 = int(s3, base = 8)  # Vale l'intero 19, la conversione di 23(8) in decimale

s4 = '0x2E'
n4 = int(s4)            # ERRORE!!! Non sa come convertire la x...
n4 = int(s4, base = 16) # Vale l'intero 47, la conversione di 2E(16) in decimale
```


## Stringhe e codifiche

In Python il tipo stringa (`str`) codifica i dati in [UNICODE](https://it.wikipedia.org/wiki/Unicode), utilizzando il sistema di codifica [UTF-8](https://it.wikipedia.org/wiki/UTF-8).


!!! tip "Codifca dei caratteri (più in breve possibile)"

    All'inizio c'era solo `ASCII`, in cui c'era una corrispondenza 1 a 1 fra un byte e un carattere della lingua americana. Poiché con un byte puoi distinguere massimo 256 caratteri
    diversi, `ASCII` non è sufficiente per tutte le lingue (con tutti i loro simboli) del mondo. Quindi ognuno ha pensato al proprio standard di rappresentazione dei caratteri.
    
    Un bordello!
    
    Entra in scena `UNICODE`. Un unico codice per tutti i caratteri del mondo. Per farceli stare tutti, codifica ogni carattere in due byte, per un totale di 65.536 caratteri 
    diversi! Abbastanza...<br>
    Il problema con questa codifica è che tutto diventa grosso il doppio!!! Una parola di 4 lettere (ad esempio: "ciao") diventa pesante 8 byte...
    
    Bestemmiano tutti!
    
    L'idea di usare un unico codice per TUTTI i caratteri è una figata... la teniamo! Pensiamo una codifica per risparmiare spazio: nascono le codifiche a lunghezza variabile.
    La migliore sembra essere `UTF-8` (lo standard de facto attuale). In UTF-8 un carattere può occupare 1,2,3,4 bytes, ma nel 98% dei casi la rappresentazione delle stringhe
    è più corta di quella a lunghezza fissa a 2 bytes!!
    
    Il bello è che contiene anche tutte le faccine :wink:


Con le stringhe in Python dunque, mentre osservandola (o usando la funzione `len`) puoi sapere con certezza da quanti caratteri questa è formata, a meno di non conoscere a fondo UTF-8,
non possiamo sapere *ad occhio* quanti bytes occupa in memoria! 

Almeno fino al prossimo capitolo...



## bytes e bytearray

Per gestire i bytes originati da una conversione (ad esempio di una stringa) o da una trasmissione di rete, Python 3 mette a disposizione 2 tipi di dati:

* la classe `bytes`, immutabile, paragonabile ad una tupla di byte.
* la classe `bytearray`, mutabile, paragonabile ad una lista di byte.

Sostanzialmente, i dati in una di queste classi possono arrivare in pochi modi:

* tramite la conversione di una stringa (encoding)
* come prodotto di una trasmissione di rete
* generando una nuova sequenza tramite le funzione predefinite `bytes()` e `bytearray()`

Partiamo da (scrivimi)





<br>
<br>
<br>

