> \<br\>

# OOP

::: warning
::: title
Warning
:::

Questa parte della documentazione non è ancora pronta.

Usa la documentazione in PDF reperibile
[qui](https://www.adjam.org/next/index.php/s/egW7AnHxcif8n27?path=%2FPYTHON)
:::

Python è un linguaggio basato sulla OOP, ovvero sulla Object Oriented
Programming, la programmazione orientata agli oggetti.

La frase precedente non spiega nulla, mi rendo conto. Riprovo. Tutti i
tipi di dati che abbiamo incontrato e che incontreremo in Python sono
oggetti e quindi seguono le regole della OOP. Cerchiamo innanzitutto di
capire che cosa è un oggetto e che cosa è questa OOP\...

Partiamo da alcuni esempi semplici per definire il concetto di oggetto.
Un oggetto è un entità, concreta od astratta, che descrive un concetto.
Facciamo subito un esempio che alleggerisca la tensione! Secondo Python,
una casa, un tavolo, una persona, un colore\... sono tutte entità, tutti
concetti, tutti\... oggetti!!!

E possono essere contenuti in una variabile!

::: note
::: title
Note
:::

Un oggetto é un\'entità concreta o astratta, tipica anche della vita
comune, definibile elencando le sue caratteristiche e descrivendo il
modo con cui interagisce con l'ambiente esterno, cioè i suoi
comportamenti.
:::

Partiamo sempre da un esempio: l'oggetto \"Rettangolo\". Le sue
caratteristiche potrebbero essere la misura di base e altezza, il colore
del bordo e il colore di riempimento, mentre i suoi comportamenti
potrebbero essere quelli per il calcolo dell'area, del perimetro e della
diagonale. Vediamo un altro esempio: l'oggetto \"Automobile\". Le
caratteristiche potrebbero essere la marca, il modello, il colore, la
cilindrata, ecc\... i suoi comportamenti potrebbero essere avvia,
spegni, accelera, frena, curva, ecc\...

Spero sia abbastanza chiaro.

::: tip
::: title
Tip
:::

Le caratteristiche, o attributi di un oggetto, sono quegli elementi
utili a descriverne le proprietà e lo stato. Sono solitamente
individuate tramite dei sostantivi. I comportamenti, o metodi di un
oggetto sono quelle funzionalità che mette a disposizione per interagire
con esso. Sono solitamente individuati tramite dei verbi.
:::

Gli attributi e metodi definiti all'interno di un oggetto vengono
comunemente definiti i membri dell'oggetto.

Vediamo la sintassi utilizzata così da scrivere un po\' di codice:

``` python
# immagina che la variabile "c" sia un oggetto "Cerchio"
c = Cerchio()

# Per accedere ai membri (attributi e metodi) di un oggetto si utilizza
# il punto. Ad esempio:

# attributo "raggio"
# è come una variabile interna, a cui si accede con il punto
c.raggio = 3
# da ora in poi, l’oggetto Cerchio cerc ha raggio 3

# metodo "calcolaArea()"
# è come una funzione interna, a cui si accede con il punto
c.calcolaArea() 
# valutando PiGreco a 3.14, questa funzione ritorna 28.26

# metodo "calcolaCirconferenza()"
c.calcolaCirconferenza()  
# ritorna 18.84
```

Chiaro fino a qui? Facciamo un altro passetto, cercando di capire a cosa
ci serve sapere che secondo Python ogni \"cosa\" che si appoggia in una
variabile è un oggetto. Il concetto è abbastanza semplice, seguitemi
bene. Se ogni oggetto contiene tutti gli attributi che servono a
definirlo, potremo lavorare semplicemente con tutti gli oggetti
predefiniti di Python. Se inoltre ogni oggetto ha tutti i metodi che
ritiene utile sarà anche più conveniente lavorare con esso: avremo una
serie di funzionalità \"gratuite\" pronte per essere utilizzate.

Non riuscite a capire il concetto? Proviamo così. Nell'esempio
precedente abbiamo parlato di un fantomatico oggetto Cerchio. Più o meno
tutti sapevano già calcolare l'area dato il raggio. Ma se la figura
fosse stata un icosaedro? Con un oggetto pronto era ugualmente facile
tanto quanto chiamare il metodo area. Chiaro adesso???

Proviamo a dichiarare adesso questa fantomatica classe Cerchio:

``` python
# File "Cerchio.py"
import math

class Cerchio:
    # inizializza gli attributi della classe
    def __init__(self, raggio):
        # aggiunge l’attributo "raggio" alla classe e lo inizializza
        self.raggio = raggio

    def calcolaArea(self):
        a = math.pi * self.raggio * self.raggio
        return a

    def calcolaCirconferenza(self):
        c = 2* math.pi * self.raggio
        return c
```

Il fantomatico oggetto Cerchio si inizializza con il codice seguente:

``` python
cerc = Cerchio(4)   # crea un oggetto della classe Cerchio con raggio 4
print("Cerchio")
print("raggio:", cerc.raggio)
print("area:", cerc.calcolaArea())
print("circonferenza:", cerc.calcolaPerimetro())
```

``` 
Cerchio
raggio: 4
area: 50.26548245743669
circonferenza: 25.132741228718345
```

Spero adesso sia tutto ok\... Non è così, lo so. Per iniziare cerchiamo
di chiarirci alcuni termini e alcune funzioni \"strane\" che ho
utilizzato prima e poi vediamo qualche esercizio.

## Terminologia

Chiariamo bene i termini che andremo ad utilizzare per definire una
classe manualmente e che sono utilizzati da Python.

class Intanto faccio notare che, come abbiamo utilizzato la clausola def
per definire una funzione, bisogna utilizzare la clausola class per
dichiarare una classe.

class Cerchio:

:   . . .

Ricordate?

Classi e Oggetti Per evitare confusione fra i concetti mi piace
utilizzare i termini classe e oggetto. In OOP solitamente si usa il
termine \"classe\" per la definizione dell'oggetto, mentre \"oggetto\" è
l'istanza del tipo classe definito. Prima abbiamo scritto:

cerc = Cerchio(4)

Bene: cerc è un oggetto di tipo Cerchio, un'istanza della classe, mentre
Cerchio è la classe.

self Avrete notato questo parametro predefinito nelle funzioni della
classe e per inizializzare la variabile membro. Questo parametro viene
automaticamente istanziato da Python in questo modo:

cerc.area() diventa Cerchio.area(cerc)

In questo modo il parametro self permette accesso alla classe, ma
l'utente della classe non ha bisogno di occuparsene. Spero sia chiaro,
più facile di così non riesco. In pratica, la variabile self va messa
come primo membro di ogni metodo di una classe, in modo da poter
collegare il metodo alla classe stessa.

Metodi che iniziano (e finiscono) con doppio underscore \_\_ Ce ne sono
parecchi in ogni classe e hanno ognuno un compito specifico. Vengono
definite Funzioni Speciali. Ne introdurremo molte altre più avanti. La
cosa importante da capire su di esse è che questi metodi non vanno
eseguiti \"volontariamente\" (ad esempio come fareste con il metodo
\"area()\" della classe Cerchio se voleste calcolarne l'area) ma vengono
eseguiti automaticamente in determinate situazioni. Quindi ogni volta
che incontrate una funzione speciale dovete farvi sempre due domande:

> 1.  In quale momento particolare questa funzione speciale viene
>     eseguita automaticamente?
> 2.  Voglio modificare il comportamento della classe in quel caso
>     particolare? Bene, se la risposta a questa domanda è sì significa
>     che dovete re-implementare quella funzione. Man mano vedremo come.

Per adesso vediamo le 2 funzioni speciali più comuni in assoluto:

def \_\_init\_\_( self , . . . )

:   Questa particolare funzione speciale viene eseguita automaticamente
    quando si definisce un oggetto di una classe. La sua implementazione
    serve per dare un valore iniziale agli attributi della classe, siano
    essi inseriti come parametri della stessa o inizializzati ad un
    valore scelto dal programmatore.

    Vediamo un esempio per chiarirci al meglio le idee. Definiamo la
    classe Quadrato. L'utente potrà scegliere il lato del Quadrato, ma
    inizialmente esso sarà disegnato con sfondo bianco e lati neri.

``` python
class Quadrato:
    def __init__(self, lato):
        self.lato = lato
        self.coloreSfondo = "bianco"
        self.coloreBordo = "nero"
# ...
# nella riga sotto viene eseguita automaticamente la funzione __init__
c = Quadrato(4)
# si definisce così un oggetto della classe Quadrato, di lato 4
# con colore di sfondo bianco e colore del bordo nero.
```

def \_\_str\_\_ (self)

:   La funzione \_\_str\_\_ serve per visualizzare in maniera semplice
    informazioni sulla classe (praticamente per visualizzare il valore
    dei suoi attributi). Questa funzione viene eseguita automaticamente
    quando si esegue la funzione print() con parametro un oggetto della
    classe.

    La funzione \_\_str\_\_ non prende MAI parametri e ritorna sempre
    una stringa, ricordatelo! Ad esempio, definiamo la funzione
    \_\_str\_\_ per la classe Quadrato definita sopra:

``` python
def __str__(self):
    s = ""
    s += "Quadrato di lato " + str(self.lato)
    s += ", sfondo " + self.coloreSfondo
    s += ", bordo " + self.coloreBordo
    return s

...
# riferito all’oggetto c definito prima
print(c)
# visualizzerà "Quadrato di lato 4, sfondo bianco, bordo nero"
```

## Esercizio svolto: la classe Rettangolo

Definire un oggetto Rettangolo, tramite i parametri base e altezza e
implementare i metodi per il calcolo dell'area e del perimetro. Fornire
un test per un Rettangolo di base = 5 cm e altezza = 3 cm, visualizzando
i parametri e calcolando area e perimetro dello stesso.

``` python
class Rettangolo:
    def __init__(self,base,altezza):
        self.b = base
        self.h = altezza

    def __str__(self):
        s = "Rettangolo(" + str(self.b) + "," + str(self.h) + ")"
        return s

    def area(self):
        a = self.b * self.h
        return a

    def perimetro(self):
        p = 2*(self.b + self.h)
        return p

if __name__ == "__main__":
    r = Rettangolo(5,3)
    print(r)
    print("Base:", r.b)
    print("Altezza:", r.h)
    print("Area:", r.area())
    print("Perimetro:",r.perimetro())    
```

## Esercizi di comprensione

Prima di andare avanti, proviamo a definire alcune classi e proporre con
esse qualche test in cui inserire e modificare i valori degli attributi
definiti e visualizzare i risultati delle chiamate ai metodi definiti.

Per ognuna ricordate che è obbligatorio definire sempre la funzione
\_\_init\_\_ e la funzione \_\_str\_\_ e verificarne il funzionamento,
definendo un oggetto della classe e visualizzandone i valori con la
print().

**Esercizio 701**

Definire la classe Persona con attributi nome, cognome, data e luogo di
nascita, sesso (M/F). La funzione di \_\_init\_\_ della classe non deve
avere argomenti. Definite un maschio e una femmina della classe a libera
scelta.

--------------------------------------------------------------------

**Esercizio 702**

Definire la classe TriangoloRettangolo inserendo come attributi i due
cateti. Aggiungere i metodi per il calcolo dell'ipotenusa, dell'area e
del perimetro. Definire un oggetto della classe TriangoloRettangolo con
cateti uguali a 4 cm e 3 cm, visualizzare i suoi attributi e calcolare
l'ipotenusa, l'area e il perimetro.

--------------------------------------------------------------------

**Esercizio 703**

Definire la classe Animale con attributi nome e specie. Aggiungere il
metodo \"corri\" (ritorna la stringa \"sto correndo\...\") e \"mangia\"
(ritorna la stringa \"sto mangiando\"). Definire un cane di nome
\"Piero\" e farlo correre e mangiare. Visualizzare i suoi attributi.

--------------------------------------------------------------------

**Esercizio 704**

Definire la classe Persona con attributi nome, età e sesso (M/F). La
funzione di \_\_init\_\_ della classe deve prendere come argomento solo
il nome della persona, mentre l'età va impostata automaticamente a ZERO
e il sesso a \"M\" (o \"F\", scegliete voi). Aggiungere i metodi
\"invecchia\" (aggiunge un anno di età) e \"saluta\" (restituisce
\"signore\" o \"signora\" a seconda del sesso della persona). Definire 2
persone: \"Augusto\", maschio di 47 anni e \"Marianna\", femmina di 44
anni. Utilizzare i metodi \"invecchia\" e \"saluta\" per entrambi,
procedere poi a visualizzare gli attributi di entrambi.

--------------------------------------------------------------------

**Esercizio 705**

Definire la classe ContoCorrente con attributi proprietario e capitale;
il proprietario va definito tramite parametro della funzione
\_\_init\_\_ mentre il capitale va inizializzato a ZERO. Definire il
metodo \"deposita\", che prende un parametro reale, controlla che sia
positivo ed eventualmente lo aggiunge al capitale e il metodo
\"preleva\", che prende anch'esso un parametro reale, verifica che il
parametro sia positivo, verifica che sia minore del capitale ed
eventualmente lo sottrae da esso (il metodo ritorna True se possibile,
False altrimenti). Definire il Conto Corrente di \"Gigetto\". Depositare
in esso 1000 euro. Prelevare 600 euro per 2 volte. La seconda volta
l'operazione dovrebbe fallire. Visualizzare dopo ogni operazione i
valori dell'oggetto con la funzione print().

--------------------------------------------------------------------

**Esercizio 706**

Definire la classe Crittografia con attributo un numero intero che
indica lo spiazzamento dei caratteri. Ad esempio, se il numero è 3 ogni
carattere sarà traslato di 3 posti sull'alfabeto (le A diventano D, le B
diventano E\...). La classe contiene inoltre 2 funzioni: \"cripta\", che
prende una stringa qualsiasi e restituisce la stessa trasformata secondo
la regola descritta sopra; \"decripta\" che pende una stringa criptata e
la rimette \"a posto\". Definire due oggetti della classe Crittografia
con parametro a piacere e provare a \"criptare\" e \"decriptare\" una
stringa, verificando che la stringa decriptata è uguale a quella
inserita prima di essere criptata.

--------------------------------------------------------------------

**Esercizio 707**

Definire la classe Automobile con attributi marca, modello, velocità e
numero di persone trasportate. La funzione init prende come parametri la
marca e il modello e imposta a ZERO gli altri attributi. Implementare i
seguenti metodi:

-   *faiSalirePersona*: aggiunge una persona al numero di persone
    trasportate fino ad un massimo di 5. Ritorna True se è stato
    possibile aggiungere una persona, False altrimenti.
-   *faiScenderePersona*: toglie una persona al numero di persone
    trasportate (Se possibile ovviamente). Ritorna True se è stato
    possibile togliere una persona, False altrimenti.
-   *Accelera*: aggiunge 20 kmh alla velocità di marcia, fino ad un
    massimo di 120 kmh. Funziona solo se il numero di persone
    trasportate è positivo. Ritorna True se è stato possibile aumentare
    la velocità, False altrimenti.
-   *Rallenta*: toglie 20 kmh alla velocità di marcia, ovviamente fino a
    fermarsi. Ritorna True se è stato possibile diminuire la velocità,
    False altrimenti.
-   *Frena*: azzera la velocità di marcia. Ritorna True se è stato
    possibile frenare, False altrimenti.

Definire un oggetto della classe Automobile e progettare un test in modo
che ognuna delle funzioni venga eseguita almeno 2 volte, una ritornando
True, una ritornando False.

--------------------------------------------------------------------

**Esercizio 708**

Definire la classe TrapezioRettangolo, che prende come parametri la base
minore, la base maggiore e l'altezza del Trapezio. Definire i metodi
\"latoObliquo\", \"area\", \"perimetro\". Dichiarare un oggetto
TrapezioRettangolo e procedere a visualizzare i suoi parametri, la sua
area e il suo perimetro.

--------------------------------------------------------------------

**Esercizio 709**

Definire la classe \"Orario\", con parametri i tre interi per ore,
minuti e secondi. Implementare inoltre le seguenti funzioni: \*
*secondiDaMezzanotte()*: restituisce l\'intero che rappresenta il numero
di secondi trascorsi dalla mezzanotte. \* *aggiungiTempo(ore, minuti,
secondi)*: aggiunge tempo all'orario corrente. Ad esempio, se l'oggetto
della classe Orario segna le 03:14:22 e si esegue su di esso la funzione
aggiungoTempo(1,2,3) l\'orario diventa le 04:16:25. Attenzione a quando
\"il giro ricomincia\"\... \* *momento()*: ritorna la stringa
\"mattina\" se orario è fra le 8 e le 13, \"pomeriggio\" se fra 13 e 20,
\"sera\" fra 20 e 23, \"notte\" altrimenti

--------------------------------------------------------------------

**Esercizio 710**

Definire la classe CartaFedeltà, per la gestione degli utenti di un
grande magazzino. La carta fedeltà è nominativa (appartiene ad un solo
cliente) e consente l\'accumulo dei punti (attraverso il metodo
accumulaPunti(soldiSpesi)) calcolati sulla base della spesa effettuata:
ogni 12€ di spesa si aggiunga un punto. All\'inizio ovviamente il numero
di punti è ZERO. Il cliente può decidere, in ogni momento, di usufruire
di una parte dei punti accumulati per l\'ottenimento di un premio
(implementare un opportuno metodo utilizzaPunti(quantita): il metodo
ritorna True\... False altrimenti). Definire le carte fedeltà per 2
clienti. Il primo cliente fa una spesa pari a 150€. Il secondo cliente
fa una spesa di 300€. In seguito, il primo cliente fa una spesa pari a
1500€ e, dopo aver pagato, decide di utilizzare 100 dei punti accumulati
per ritirare un premio. Il secondo cliente chiede di utilizzare 50 dei
punti accumulati.

--------------------------------------------------------------------

**Esercizio 711**

Definire la classe Giocatore con nome, numero di maglia e ruolo
ricoperto. Il nome del giocatore va impostato tramite parametro, mentre
il numero va impostato inizialmente a ZERO e il ruolo a \"X\".

Definire la funzione impostaRuolo(stringa) che prende una stringa come
parametro e imposta il ruolo del giocatore. Fare in modo che i ruoli
accettabili siano solo \"P\" (per portiere), \"D\" (per difensore),
\"C\" (per centrocampista), \"A\" (per attaccante). La funzione ritorna
True o False a seconda del fatto se il ruolo viene effettivamente
modificato oppure no.

Definire la funzione cambiaNumero(intero) che modifica il numero di
maglia solo se esso varia fra 1 e 99. Anche qui, la funzione ritorna
True o False\...

DIFFICILE E OPZIONALE: è possibile fare in modo anche che i numeri di
maglia dei vari giocatori siano tutti diversi fra loro? Proponi una
soluzione al problema. Definire un giocatore di nome \"Edoardo\".
Tramite la funzione impostaRuolo, impostare il suo ruolo ad attaccante
(con \"A\") e poi modificarlo a terzino (\"T\"). La seconda modifica
dovrebbe fallire. Utilizzare la funzione cambiaNumero per modificare il
suo numero a 103 e poi a 7. Definire un giocatore di nome
\"Alessandro\". Tramite la funzione impostaRuolo, impostare il suo ruolo
a centrocampista (con \"C\"). Utilizzare la funzione cambiaNumero per
modificare il suo numero a 7 (se avete implementato la parte opzionale,
dovrebbe fallire) e poi a 11.

--------------------------------------------------------------------

**Esercizio 712**

Definire la classe EstrazioneLotto. La classe contiene una lista,
inizialmente vuota, di stringhe che rappresentano le città ove ci sono
le ruote di estrazione. Prevedere un metodo aggiungiRuota(stringa) che
verifica se il nome della città da inserire sia già presente nelle ruote
e in caso negativo la aggiunge alla lista. Definire una funzioni
estrai(stringa) che verifica se il nome della città passata come
parametro è presente nelle ruote. In caso negativo, ritorna una tupla
vuota. In caso positivo, ritorna una tupla di 5 numeri casuali, diversi
fra loro, fra 1 e 90.

ULTERIORE DIFFICOLTA\' (opzionale): fare in modo che i numeri della
tupla siano ordinati in senso crescente.

Definire una funzione estrazioniDellaSettimana() che permette a tutte le
ruote presenti di estrarre i numeri del lotto. La funzione ritorna un
dizionario che ha come chiavi i nomi delle ruote in cui avvengono le
estrazioni e come valori le tuple dei 5 numeri estratti.

Definire un oggetto della classe EstrazioneLotto.

Inserire tramite il metodo aggiungiRuota le seguenti città: Jesi,
Senigallia, Ancona, Jesi (dovrebbe fallire, già presente), Monsano,
Moie, Ancona (err). Visualizzare il risultato della funzione
estrai(\"Jesi\"), estrai(\"Ancona\"), estrai(\"Milano\"). L\'ultima
dovrebbe ritornare una tupla vuota. Eseguire la funzione
estrazioniDellaSettimana e visualizzare ordinatamente il dizionario
ottenuto, con una visualizzazione simile a questa:

-   Jesi: (1,5,9,23,89)
-   Senigallia: (23,34,45,67,88)
-   Ancona: (39, 43, 44, 78, 81)

### Ereditarietà

L'ereditarietà è un concetto tipico della programmazione orientata agli
oggetti che ovviamente qui sarà declinato in salsa Python :)

L'ereditarietà è la capacità di definire una classe a partire da una già
esistente, facendo in modo che la nuova classe \"erediti\" tutte le
caratteristiche (attributi e metodi) della classe iniziale.

Poiché questo concetto viene definito \"ereditarietà\" solitamente si
usano nomi \"parentali\" per indicare le classi in gioco, ad esempio la
classe iniziale Padre e la classe finale Figlio, che eredita le
caratteristiche dalla classe Padre.

``` python
class Padre:
    def __init__(self):
        print("Init classe Padre")

    def saluta(self):
        return "buongiorno"

class Figlio(Padre):        # la classe Figlio "deriva" dalla classe Padre
    def __init__(self):
        print("Init classe Figlio")

# ------------------------------------ 
if __name__ == "__main__":
    ciccio = Figlio()
    print(ciccio.saluta())  # la classe Figlio "eredita" il metodo saluta()
```

## Overloading

Nella teoria della OOP il polimorfismo è la tecnica che definisce la
possibilità di ridefinire il comportamento di un metodo di una classe.
Fra le varie forme di polimorfismo (non azzardatevi a chiedere di
più\...) Python ne introduce una sola e la definisce \"overloading\",
quindi\... che cosa è l'overloading in Python? È la capacità di
reimplementare un metodo (una funzione) nella classe derivata, per
modificare il suo comportamento nella stessa. Anche qui parto con un
esempio semplicissimo per aiutare a capire il concetto. Ricordate le
classi Padre e Figlio precedentemente definite? Grazie all'ereditarietà
gli oggetti della classe Figlio salutano come gli oggetti della classe
Padre. Ma come è possibile che un ragazzo saluti dicendo \"buongiorno\"?
Ecco in aiuto il concetto di overloading. All'interno della classe
Figlio basta ridefinire il metodo in questione

``` python
. . .
class Figlio(Padre):        # la classe Figlio "deriva" dalla classe Padre
    def __init__(self):
        print("Init classe Figlio")

    def saluta(self):   # la funzione "saluta()" viene reimplementata
        return "ciao"
```

In questo modo ogni saluto di un oggetto della classe Figlio sarà
effettuato dicendo \"ciao\"!!!

## Python Object class

Il concetto che illustriamo in questo capitolo è molto semplice da
comprendere come concetto; purtroppo le motivazioni che hanno portato
gli sviluppatori Python a tale scelta non sono altrettanto semplici da
chiarire :)

Il concetto è: in Python 3 esiste una classe predefinita, chiamata
object, da cui automaticamente tutte le classi derivano, secondo una
sorta di eredità forzata.

Significa che tutte le classi che dichiariamo in Python 3
automaticamente derivano dalla classe object. Questo concetto di avere
una unica classe base da cui per ereditarietà derivano tutte le altre
non è una idea partorita in seno alla comunità Python ma una
\"genialata\" che le comunità Java e Qt/C++ sperimentano già da decenni.

L'idea alla base di questa \"moda\" è quella di sfruttare l'ereditarietà
per condividere con tutti gli oggetti una serie di proprietà comuni che
possano facilitare la gestione del codice e potenziare con semplicità e
in maniera automatica tutto il sistema OOP Python.

Volendo essere precisi e pignoli, le caratteristiche nuove che vengono
introdotte sono:

-   il supporto per i descrittori
-   il \"Method Resolution Order\" (MRO)
-   il metodo super() di accesso alla classe superiore

Io credo che addentrarci su queste caratteristiche sia al di là del
nostro corso: vedremo semplicemente come funziona la OOP in Python. Se e
quando studierete un altro linguaggio di programmazione Object Oriented
potrete valutare le differenze e googlare su queste cose.

## Funzioni predefinite

Per verificare che la struttura di ereditarietà che vi ho prospettato (e
tutte le altre che vi capiteranno) potete utilizzare le funzioni
predefinite

-   isinstance();
-   issubclass().

La funzione isinstance() prende due parametri, un oggetto e una classe
(ricordate questi termini? Controllate nella terminologia) e ritorna
True se l'oggetto è una istanza della classe, False altrimenti. Come al
solito, con un esempio è più facile capire:

``` python
class Prova:
    pass

a = Prova()
b = 2
isinstance(a, Prova)        # ritorna True
isinstance(b, Prova)        # ritorna False
isinstance(a, object)       # ritorna True
```

La funzione issubclass() prende due parametri, due classi e ritorna True
se la prima classe è una sottoclasse della seconda.

``` python
issubclass(Prova, object)   # ritorna True
issubclass(int, Prova)      # ritorna False
```

Come avete visto, porta tutto :)

## Funzione super()

Dato che ci sono introdurrò un'altra funzione importante, la funzione
super(). Essa restituisce un riferimento alla classe genitore da cui una
classe deriva. Grazie ad essa è possibile accedere ai metodi della
classe Padre che sono stati sovrascritti sulla classe Figlio.

Esempio di utilizzo della funzione super()

``` python
# Nella classe Punto2D
class Punto2D:
    def __init__ (self, x, y):
        self.x = x
        self.y = y

# Nella classe Punto3D
class Punto3D(Punto2D):
    def __init__ (self, x, y, z):
        super().__init__(x,y)   # richiama __init__ della classe Punto2D
        self.z = z
```

Spero sia chiaro già così. In ogni caso\... ci sarà modo di chiarire i
propri dubbi facendo gli esercizi qui sotto!!!

## Esercizi su ereditarietà

**Esercizio 721**

Definire la classe Quadrato con attributo il lato e metodi \"area\" e
\"perimetro\". Da quella derivare la classe Cubo, in cui va aggiunto il
metodo \"volume\" e ridefinito il metodo \"area\" in modo che esso
restituisca l'area delle 6 facce del cubo.

Dichiarare un oggetto Quadrato di lato 4, visualizzando i suoi attributi
e il risultato dei metodi area e perimetro.

Dichiarare un oggetto Cubo di lato 4, visualizzando i suoi attributi e
il risultato dei metodi area e volume.

--------------------------------------------------------------------

**Esercizio 722**

Definire la classe Persona, con attributi nome ed età e metodi saluta()
(restituisce la stringa \"ciao, sono + nome\") e invecchia() (aggiunge
un anno all'età).

Derivare da questa la classe Docente, che aggiunge l'attributo materia,
inizialmente vuoto.

Un docente invecchia più velocemente di una persona normale\...
ridefinire la funzione invecchia() che aggiunge ad ogni chiamata 2 anni
al docente.

Aggiungere alla classe Docente il metodo insegna(materia), che prende
una stringa per il nome della materia da insegnare. Se la materia è una
fra \"matematica\", \"italiano\", \"inglese\" la funzione imposta
l'attributo materia e ritorna True. Altrimenti ritorna False.

Definire la persona \"Giacomo\", di anni 28. Testare i metodi saluta,
invecchia e poi visualizzare gli attributi della classe.

Definire il docente \"Francesca\", di anni 31. Testare i metodi saluta,
invecchia (ridefinito) e il metodo insegna con le materie \"diritto\" e
\"inglese\". Visualizzare infine gli attributi della classe.

--------------------------------------------------------------------

**Esercizio 723**

Definire la classe Punto2D, con attributi le coordinate del punto nel
piano cartesiano e le funzioni \"distanzaDalCentro\" e
\"distanzaDalPunto\". Questa seconda funzione prende come parametro un
ulteriore Punto2D da cui calcolare la distanza nel piano.

Derivare dalla classe Punto2D la classe Punto3D.

Definire il Punto2D di coordinate (3,4), visualizzare i suoi attributi
ed eseguire le funzioni distanzaDalCentro e distanzaDalPunto. Per
quest'ultima funzione definire il Punto2D di coordinate (6,8).

Definire il Punto3D di coordinate (4,5,6), visualizzare i suoi attributi
ed eseguire le funzioni distanzaDalCentro e distanzaDalPunto. Per
quest'ultima funzione definire il Punto3D di coordinate (1,1,2).

--------------------------------------------------------------------

**Esercizio 724**

Definire la classe Cerchio con gli attributi e i metodi che ritenete
opportuni.

Derivare da essa la classe Sfera.

Definire un cerchio di raggio 5, di cui calcolare area e circonferenza.
Definire una sfera di raggio 3, di cui calcolare area e volume.

--------------------------------------------------------------------

**Esercizio 725**

Definire la classe Contatto con nome, nick, numero, mail. In fase di
definizione la classe prende solo nome e numero e imposta gli altri alla
stringa vuota.

Definire i seguenti contatti:

-   Giacomo (detto \"Jack\"), numero +39-340-1234567, mail
    <jack@mail.com>.
-   Giovanni (detto \"John\"), numero +39-333-4567890, mail
    <john@mail.com>.

La classe ContattoLavoro deriva dalla classe Contatto, ma aggiunge le
informazioni fax e partitaIVA. Il costruttore prende ancora una volta
solo nome e numero, impostando le restanti variabili alla stringa vuota.

Definire il seguente contatto di lavoro:

-   Alessandro (detto \"Alex\"), numero +39-345-6789012, mail
    <alex@mail.com>, fax +39-0721-098765, partitaIVA 1234567890A

--------------------------------------------------------------------

**Esercizio 726**

Definire una classe Persona con attributi nome e anno di nascita,
forniti tramite parametri e indirizzo, inizialmente impostato alla
stringa vuota. Derivare da essa una classe Abbonato, che comprenda il
numero di noleggi effettuati e la percentuale di sconto a cui l'utente
ha diritto. Ovviamente il numero di noleggi all'inizio è zero, mentre lo
sconto iniziale è del 5% per tutti gli adulti fino a 50 anni e del 10%
per i più grandi (da 50 in su). Ogni 2 noleggi lo sconto aumenta del 5%
fino ad un massimo del 50% di sconto sul prezzo di noleggio. Definire
una funzione \"noleggiaFilm\" che aggiunge un noleggio all'abbonato,
eventualmente aggiornando le informazioni dell'abbonato.

--------------------------------------------------------------------

**Esercizio 727**

Definire una classe Veicolo, che contempli fra le sue caratteristiche la
possibilità di indicare la velocità massima (in km/h) e che in fase di
definizione imposta il numero dei chilometri percorsi a ZERO.

Implementare in essa, oltre alle funzioni che ritenete opportune, una
funzione chiamata \"faiStrada\" che richiede la velocità da tenere (che
dovrà essere minore della velocità massima) e il tempo per cui tenerla:
la funzione dovrà aggiornare il numero di chilometri percorsi.

Derivare da questa una classe Autobus, che comprende, oltre alle
caratteristiche ereditate, il numero massimo di posti all\'interno e il
numero di persone attualmente all\'interno, da inizializzare a ZERO.

Modificare la funzione di \_\_init\_\_ in modo tale che il bus non possa
avere una velocità massima superiore ai 100 km/h.

Implementare una funzione chiamata \"eseguiFermata\" che prende come
parametro il numero di persone che salgono e il numero di persone che
scendono e aggiorna il numero di persone attualmente presenti
nell\'autobus.

### Funzioni operatori

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
classe basta reimplementare la funzione abbinata \_\_add\_\_ : faremo in
modo che la somma di due punti crei un nuovo punto con le coordinate
uguali alla somma delle coordinate dei punti sommati.

``` python
# nella classe Punto2D
def __add__ (self, other):
    xS = self.x + other.x
    yS = self.y + other.y
    return Punto2D( xS, yS )
```

Quindi da ora in poi\...

``` python
# c diventa un Punto2D di coordinate x = 2 + 1 = 3 e y = 3 + 1 = 4
c = a + b
```

Per definire altri tipi di operazioni basta consultare la tabella qua
sotto.

  Operatore                                 Espressione                 Funzione interna per l'overloading
  ----------------------------------------- --------------------------- ---------------------------------------------------------------------
  print                                     print ( a )                 a.\_\_str\_\_()
  Addizione                                 a + b                       a.\_\_add\_\_(b)
  Sottrazione                               a - b                       a.\_\_sub\_\_(b)
  Moltiplicazione                           a \* b                      a.\_\_mul\_\_(b)
  Divisione                                 a / b                       a.\_\_truediv\_\_(b)
  Divisione Intera                          a // b                      a.\_\_floordiv\_\_(b)
  Potenza                                   a \*\* b                    a.\_\_pow\_\_(b)
  Modulo                                    a % b                       a.\_\_mod\_\_(b)
  \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--   \-\-\-\-\-\-\-\-\-\-\-\--   \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
  Minore                                    a \< b                      a.\_\_lt\_\_(b)
  Minore o uguale                           a \<= b                     a.\_\_le\_\_(b)
  Uguale                                    a == b                      a.\_\_eq\_\_(b)
  Diverso                                   a != b                      a.\_\_ne\_\_(b)
  Maggiore                                  a \> b                      a.\_\_gt\_\_(b)
  Maggiore o uguale                         a \>= b                     a.\_\_ge\_\_(b)

La funzione \_\_str\_\_ permette ad un oggetto della classe di essere
utilizzato nella funzione print(). Questa per noi non dovrebbe più
risultare un problema.

Le funzioni aritmetiche (addizione, sottrazione, etc\...) prendono come
parametro 2 oggetti di una classe (tipicamente coi 2 parametri self ,
other ) e ritornano sempre un oggetto della classe stessa!

Ripropongo la funzione \_\_add\_\_ della classe Punto2D implementata
poche righe fa:

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

Le funzioni di confronto (minore, maggiore, diverso, etc\...) prendono
come parametro i 2 oggetti da confrontare e ritornano un booleano

ad esempio per implementare l'operatore minore bisogna definire la
funzione \_\_lt\_\_ che prende i 2 parametri self , other che
rappresentano i 2 oggetti. Se secondo la tua implementazione la funzione
ritorna True significa che il primo oggetto è minore del secondo,
altrimenti se si ritorna False significa che il primo oggetto NON è
minore del secondo.

``` python
# dati 2 punti, uno è minore dell’altro 
# se la sua distanza dal centro è minore.
def __lt__ ( self , other ):
    if self.distanzaDalCentro() < other.distanzaDalCentro():
        return True
    return False
```

Spero sia chiaro! Come al solito\... per capire meglio ci sono gli
esercizi :)

## Esercizi sulle funzioni operatori

**Esercizio 741**

Definire la classe Frazione, con parametri numeratore e denominatore.

Definire in essa le funzioni:

-   valuta(): ritorna il valore reale che la frazione rappresenta. Ad
    esempio se il numeratore è 39 e il denominatore è 10, allora la
    funzione valuta() ritorna 3.9.

\* semplifica(): riduce ai minimi termini i generatori (numeratore e
denominatore) della frazione. Ad esempio se il numeratore è 25 e il
denominatore è 30, allora si possono entrambe dividere per 5 ( il MCD
fra 25 e 30) ottenendo 5 e 6.

Definire inoltre le funzioni operatori per somma, moltiplicazione,
diverso e minore o uguale.

Dichiarare almeno 3 frazioni con cui testare le funzioni implementate.

--------------------------------------------------------------------

**Esercizio 742**

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

**Esercizio 743**

Definire la classe Reale (che rappresenta un numero reale) con l'unico
attributo float che rappresenta il suo valore. Definire in essa le
funzioni operatore per somma, sottrazione, divisione, maggiore, uguale.

Derivare da essa la classe Complesso, che rappresenta un numero
complesso. Reimplementare le funzioni ereditate secondo necessità.
Definire inoltre la funzione modulo(), che calcola il modulo del numero
e la funzione coniugato() che ritorna un oggetto Complesso che
rappresenta il complesso coniugato del numero iniziale.

Definire i numeri reali: 4.5 , -7.2 , 9.1 Testare le funzioni
implementate. Definire i numeri complessi: 4 + 5i , -7 + 3i Testare le
funzioni implementate.

--------------------------------------------------------------------

**Esercizio 744**

Definire la classe DataSemplice, con i due attributi interi che
rappresentano i giorni e i mesi. Nella classe DataSemplice i mesi hanno
la lunghezza normale (Gennaio ne ha 31, Febbraio 28, etc\...) ma non ci
sono gli anni e quindi non esistono gli anni bisestili.

Presenta una funzione \"isValid()\" che ritorna True se la data
rappresentata è valida, ovvero la coppia di numeri rappresenta una
combinazione giorno/mese esistente, False altrimenti.

Presenta una funzione \"contaGiorni()\" che restituisce il numero di
giorni trascorsi dal 1 Gennaio alla data rappresentata, se valida. -1
altrimenti. Implementare le funzioni operatori per l'addizione, la
sottrazione, il minore e il diverso. Due date si sommano sommando il
numero di giorni trascorsi dall'inizio dell'anno (e analogamente si
sottraggono). Ad esempio \"01 gen\" + \"02 gen\" fa \"03 gen\".

Una data è minore di un'altra se è precedente all'interno di un anno.
Diverso è facile\...

Definire una data per il 3 marzo e una per il 45 settembre. Verificare
che la prima è valida e la seconda no. Utilizzare la funzione
contaGiorni. La seconda dovrebbe restituire -1.

Testare le seguenti operazioni:

-   03 mar + 05 lug
-   03 mar -- 2 feb
-   03 mar \< 2 feb
-   05 lug != 2 feb
