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

Se però sei veramente determinato a saperlo... puoi usare la funzione predefinita `ord()`. Questa, dato un carattere, ritorna il valore esadecimale che corrisponde alla sua rappresentazione in UTF-8. Prima di fare qualche esempio, fatemi dire solo che esiste anche la funzione che fa l'inverso, ovvero dato un intero ritorna il carattere corrispondente
in UTF-8 (o in ASCII. Ve l'ho detto che UTF-8 è stato progettato per essere identico ad ASCII nei primi 127 caratteri???).

``` python
print( ord('a') )       # scrive 97. In UTF-8, come in ASCII
print( chr(97) )        # scrive 'a'
i = 8364
print( chr(i) )         # simbolo dell'Euro €
```


## bytes e bytearray

Per gestire i bytes originati da una conversione (ad esempio di una stringa) o da una trasmissione di rete, Python 3 mette a disposizione 2 tipi di dati:

* la classe `bytes`, immutabile, paragonabile ad una **tupla di byte**.
* la classe `bytearray`, mutabile, paragonabile ad una **lista di byte**.

Sostanzialmente, i dati in una di queste classi possono arrivare in pochi modi:

1. tramite la conversione di una stringa (encoding)
2. come prodotto di una trasmissione di rete
3. generando una nuova sequenza tramite le funzione predefinite `bytes()` e `bytearray()`

Partiamo dall'ultima opzione! Possiamo usare entrambe le funzioni in due modi analoghi: l'unica differenza fra loro è che una crea un oggetto di tipo `bytes` e l'altra
un oggetto di tipo `bytearray`.

Vediamo il codice:

``` python
# bytes(size:int) oppure bytearray(size:int). Se passi un intero, crea una sequenza di "size" bytes tutti a zero!

b = bytes(3)            # b  vale b'\x00\x00\x00' ,            una sequenza IMMUTABILE di 3 bytes (8x3 = 24 bit) tutti a zero.
ba = bytearray(3)       # ba vale bytearray(b'\x00\x00\x00') , una sequenza MUTABILE   di 3 bytes tutti a zero.

# bytes(iterable) oppure bytearray(iterable). Prende la sequenza di dati e crea una sequenza di byte con i dati della sequenza.

tupla = (1, 2, 3)
b1 = bytes(tupla)       # b1 vale b'\x01\x02\x03',             una sequenza immutabile, riempita con i byte ricavati dalla conversione dei dati della tupla
ba1 = bytearray(tupla)  # ba1 vale bytearray(b'\x01\x02\x03'), una sequenza mutabile,   riempita con i byte ricavati dalla conversione dei dati della tupla
```


## String encoding


Il passaggio da stringa a bytes è davvero semplice, considerando che le stringhe utilizzano la codifica UTF-8.

Per passare da stringa a bytes, usiamo la funzione `str.encode(self, encoding='utf-8')`:

``` python
s = "Andrea"
b = s.encode()    # b è un bytes che vale b'Andrea'
```

Se invece hai una sequenza di bytes e vuoi ottenere una stringa, devi utilizzare la funzione `bytes.decode(self, encoding='utf-8')`.

``` python
b = b'Andrea'
s = b.decode()    # s è una stringa che vale 'Andrea'
```

## Int conversion


Il passaggio da interi a bytes è analogo a quello delle stringhe, ma con una piccola difficoltà in più: intuire quanti bytes saranno necessari per stanziare la 
conversione dell'intero in questione non è banale! Nel dubbio... esagerate un pò!!

Le funzioni da utilizzare sono queste:

* **da int a bytes**: funzione `int.to_bytes(len:int)` occorre specificare quanti bytes occuperà il numero convertito. Se ne metti troppo pochi da errore!!! Se ne metti troppi... sprechi memoria.
* **da bytes a int**: funzione `int.from_bytes(b)`: una semplice conversione 1:1 del bytes in intero.

Vediamo due esempi

``` python
n = 13
b = n.to.bytes(3)       # b è un bytes che vale b'\x00\x00\r'

# adesso, per riconvertirlo in int:
a = int.from_bytes(b)   # a è un intero che vale 13
```


<br>
<br>
<br>

