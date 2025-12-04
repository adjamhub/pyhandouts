# OOP: Caratteristiche avanzate


Vengono descritte qua di seguito alcune caratteristiche avanzate tipiche della OOP che ritroviamo
anche in Python.


<!-- ################################################################################################# -->
## Funzioni operatori

La classe object introduce tutta una serie di funzioni (che ovviamente,
tutte le classi ereditano) per standardizzare una serie di comportamenti
Partiamo da un esempio per chiarire l'utilità del concetto: definiamo la
classe Punto2D che descrive un punto nel piano cartesiano

``` python
class Punto2D:
    def __init__ (self, x, y):
        self.x = x
        self.y = y
```

Definiamo due oggetti della classe Punto2D e proviamo a sommarli

``` python
a = Punto2D (2, 3)
b = Punto2D (1, 1)
c = a + b           # ERRORE!!!
```

Per poter definire l'operazione di addizione all'interno della nuova
classe basta reimplementare la funzione abbinata `__add__` : faremo in
modo che la somma di due punti crei un nuovo punto con le coordinate
uguali alla somma delle coordinate dei punti sommati.

``` python
# nella classe Punto2D
def __add__ (self, other):
    xS = self.x + other.x
    yS = self.y + other.y
    return Punto2D( xS, yS )
```

Quindi da ora in poi...

``` python
# c diventa un Punto2D di coordinate x = 2 + 1 = 3 e y = 3 + 1 = 4
c = a + b
```

Data una generica classe `Pippo` e due oggetti qualunque, diciamo `a` e `b`
della classe `Pippo`:


| Se vuoi usare:       | e scrivere      | Implementa nella classe la funzione:| che ritorna                     |
|----------------------|-----------------|-------------------------------------|---------------------------------|
| print                | print ( a )     | `def __str__(self)`                 | una stringa                     |
| Addizione            | a + b           | `def __add__(self,other)`           | un oggetto della classe         |
| Sottrazione          | a - b           | `def __sub__(self,other)`           | un oggetto della classe         |
| Moltiplicazione      | a * b           | `def __mul__(self,other)`           | un oggetto della classe         |
| Divisione            | a / b           | `def __truediv__(self,other)`       | un oggetto della classe         |
| Divisione Intera     | a // b          | `def __floordiv__(self,other)`      | un oggetto della classe         |
| Potenza              | a ** b          | `def __pow__(self,other)`           | un oggetto della classe         |
| Modulo               | a % b           | `def __mod__(self,other)`           | un oggetto della classe         |
| Minore               | a < b           | `def __lt__(self,other)`            | un bool (True o False)          |
| Minore o uguale      | a <= b          | `def __le__(self,other)`            | un bool (True o False)          |
| Uguale               | a == b          | `def __eq__(self,other)`            | un bool (True o False)          |
| Diverso              | a != b          | `def __ne__(self,other)`            | un bool (True o False)          |
| Maggiore             | a > b           | `def __gt__(self,other)`            | un bool (True o False)          |
| Maggiore o uguale    | a >= b          | `def __ge__(self,other)`            | un bool (True o False)          |


La funzione `__str__` permette ad un oggetto della classe di essere
utilizzato nella funzione `print()`. Questa cosa dovremmo già averla capita...

Le funzioni aritmetiche (addizione, sottrazione, etc...) prendono come
parametro 2 oggetti di una classe (tipicamente coi 2 parametri `self` , `other`) 
e ritornano sempre un oggetto della classe stessa!

Ripropongo la funzione `__add__` della classe `Punto2D` implementata poche righe fa:

``` python
# come vedete la funzione prende 2 parametri, che rappresentano
# altrettanti oggetti
def __add__ (self, other):
    xS = self.x + other.x
    yS = self.y + other.y
    # poiché questa funzione implementa la somma fra 2 Punto2D, ritorna
    # un oggetto Punto2D che rappresenta la somma dei 2 punti identificati
    # da self e other
    return Punto2D( xS, yS )
```

Le funzioni di confronto (minore, maggiore, diverso, etc...) prendono
come parametro i 2 oggetti da confrontare e ritornano un booleano.

Ad esempio per implementare l'operatore minore bisogna definire la funzione `__lt__`.
Essa prende i 2 parametri `self`, `other` che rappresentano i 2 oggetti. 
Se la funzione ritorna `True` significa che il primo oggetto è minore del secondo,
altrimenti, se ritorna `False` significa che il primo oggetto NON è minore del secondo.

``` python
# dati 2 punti, uno è minore dell’altro 
# se la sua distanza dal centro è minore.
def __lt__ ( self , other ):
    if self.distanzaDalCentro() < other.distanzaDalCentro():
        return True
    return False
```


!!! tip "Liste e ordinamenti di oggetti"

    Se create una lista di Punto2D o di oggetti in genere, per far funzionare
    correttamente la funzione `sort` vi basta implementare la funzione `__lt__`!!!


Spero sia chiaro! Come al solito... per capire meglio ci sono gli esercizi :)

<!-- ################################################################################################# -->
### Esercizi sulle funzioni operatori

**Esercizio 1361**

Definire la classe Frazione, con parametri numeratore e denominatore.

Definire in essa le funzioni:

- `valuta()`: ritorna il valore reale che la frazione rappresenta. Ad
  esempio se il numeratore è 39 e il denominatore è 10, allora la
  funzione valuta() ritorna 3.9.

- `semplifica()`: riduce ai minimi termini i generatori (numeratore e
  denominatore) della frazione. Ad esempio se il numeratore è 25 e il
  denominatore è 30, allora si possono entrambe dividere per 5 (il MCD
  fra 25 e 30) ottenendo 5 e 6.

Definire inoltre le funzioni operatori per somma, moltiplicazione,
diverso e minore o uguale.

Dichiarare almeno 3 frazioni con cui testare le funzioni implementate.

--------------------------------------------------------------------

**Esercizio 1362**

Definire la classe Rettangolo, con attributi base e altezza e metodi
area e perimetro. Implementare in essa le funzioni aritmetiche, che
operano sugli attributi della classe e le funzioni di confronto, che
confrontano i rettangoli in base alle aree. In pratica la somma di 2
rettangoli crea un rettangolo che ha base la somma delle basi e altezza
la somma delle altezze. Per quanto riguarda il confronto un rettangolo è
minore di un altro se la sua area è minore. Dichiarare 2 rettangoli e
procedete a testare le operazioni aritmetiche e di confronto
implementate.

--------------------------------------------------------------------

**Esercizio 1363**

Definire la classe Reale (che rappresenta un numero reale) con l'unico
attributo float che rappresenta il suo valore. Definire in essa le
funzioni operatore per somma, sottrazione, divisione, maggiore, uguale.

Derivare da essa la classe Complesso, che rappresenta un numero
complesso. Reimplementare le funzioni ereditate secondo necessità.
Definire inoltre la funzione `modulo()`, che calcola il modulo del numero
e la funzione `coniugato()` che ritorna un oggetto Complesso che
rappresenta il complesso coniugato del numero iniziale.

Definire i numeri reali: 4.5 , -7.2 , 9.1 Testare le funzioni
implementate. Definire i numeri complessi: 4 + 5i , -7 + 3i Testare le
funzioni implementate.

--------------------------------------------------------------------

**Esercizio 1364**

Definire la classe DataSemplice, con i due attributi interi che
rappresentano i giorni e i mesi. Nella classe DataSemplice i mesi hanno
la lunghezza normale (Gennaio ne ha 31, Febbraio 28, etc...) ma non ci
sono gli anni e quindi non esistono gli anni bisestili.

Presenta una funzione `isValid()` che ritorna True se la data
rappresentata è valida, ovvero la coppia di numeri rappresenta una
combinazione giorno/mese esistente, False altrimenti.

Presenta una funzione `contaGiorni()` che restituisce il numero di
giorni trascorsi dal 1 Gennaio alla data rappresentata, se valida. -1
altrimenti. Implementare le funzioni operatori per l'addizione, la
sottrazione, il minore e il diverso. Due date si sommano sommando il
numero di giorni trascorsi dall'inizio dell'anno (e analogamente si
sottraggono). Ad esempio "01 gen" + "02 gen" fa "03 gen".

Una data è minore di un'altra se è precedente all'interno di un anno.
Diverso è facile...

Definire una data per il 3 marzo e una per il 45 settembre. Verificare
che la prima è valida e la seconda no. Utilizzare la funzione
contaGiorni. La seconda dovrebbe restituire -1.

Testare le seguenti operazioni:

-   03 mar + 05 lug
-   03 mar -- 2 feb
-   03 mar < 2 feb
-   05 lug != 2 feb

Procedere dichiarando una lista e inserendo al suo interno fino a 10 DataSemplice 
con valori casuali (validi) per giorno e mese. Visualizzare la lista così generata.
Testare l'ordinamento tramite funzione `sort` e visualizzare la lista ordinata.

<br>
<br>
<br>

