# Classi e Oggetti


La prima cosa da fare è cercare di capire cosa si intende quando si utilizzano i termini `Classe` e `Oggetto`: vediamo se si riesce al primo colpo!!!

Partiamo da un concetto qualsiasi, ad esempio... **la sedia**!

**Le classi** servono per descrivere i concetti: parlando delle sedie, potremmo citare ad esempio: 

- il materiale
- il colore
- l'altezza
- l'ampienzza della seduta
- etc...

Una classe descrive il concetto attraverso una serie di informazioni (ad esempio, quelle che abbiamo citato prima) che saranno dello stesso tipo per tutte le sedie 
(cioè, tutte le sedie sono fatte di un materiale, hanno un colore, etc...) ma che chiaramente possono avere valori diversi (sedie di legno o di ferro, bianche oppure blu, etc...).

**Gli oggetti** rappresentano le istanze dei concetti descritti dalle classi. Ad esempio, se state leggendo seduti, la vostra sedia è un oggetto, 
mentre un'altra sedia è un altro oggetto.

Se in cucina avete sei sedie significa che avete sei oggetti (diversi) della (stessa) classe Sedia. 


!!! note "Classi e Oggetti"

    Le Classi sono un concetto analogo ai tipi di variabile, ad esempio il tipo intero, che descrive tutti i numeri che sono interi.
    
    Gli Oggetti sono un concetto analogo alle variabili, che possono contenere un unico valore! Quello è l'oggetto!
    

Spero di essere stato chiaro... più di così non riesco!!!


## Le Classi


Partiamo sempre da un concetto, ad esempio l'Automobile.
Partiamo sempre da un esempio: l'oggetto "Rettangolo". Le sue
caratteristiche potrebbero essere la misura di base e altezza, il colore
del bordo e il colore di riempimento, mentre i suoi comportamenti
potrebbero essere quelli per il calcolo dell'area, del perimetro e della
diagonale. Vediamo un altro esempio: l'oggetto "Automobile". Le
caratteristiche potrebbero essere la marca, il modello, il colore, la
cilindrata, ecc... i suoi comportamenti potrebbero essere avvia,
spegni, accelera, frena, curva, ecc...

Spero sia abbastanza chiaro.


!!! tip "Attributi e Metodi di un oggetto"

    Le caratteristiche, o **attributi di un oggetto**, sono quegli elementi
    utili a descriverne le proprietà e lo stato. Sono solitamente
    individuate tramite dei sostantivi. 
    
    I comportamenti, o **metodi di un oggetto** sono quelle funzionalità che mette a disposizione per interagire
    con esso. Sono solitamente individuati tramite dei verbi.


Gli attributi e metodi definiti all'interno di un oggetto vengono
comunemente definiti i membri dell'oggetto.

Vediamo la sintassi utilizzata così da scrivere un po' di codice:

``` python
# immagina che la variabile "cx" sia un oggetto "Cerchio"
cx = Cerchio()

# Per accedere ai membri (attributi e metodi) di un oggetto si utilizza
# il punto. Ad esempio:

# attributo "raggio"
# è come una variabile interna, a cui si accede con il punto
cx.raggio = 3
# da ora in poi, l’oggetto Cerchio cx ha raggio 3

# metodo "calcolaArea()"
# è come una funzione interna, a cui si accede con l'operatore punto
cx.calcolaArea() 
# valutando PiGreco a 3.14, questa funzione ritorna 28.26

# metodo "calcolaCirconferenza()"
cx.calcolaCirconferenza()  
# ritorna 18.84
```

Chiaro fino a qui? Facciamo un altro passetto, cercando di capire a cosa
ci serve sapere che secondo Python ogni "cosa" che si appoggia in una
variabile è un oggetto. Il concetto è abbastanza semplice, seguitemi
bene. Se ogni oggetto contiene tutti gli attributi che servono a
definirlo, potremo lavorare semplicemente con tutti gli oggetti
predefiniti di Python. Se inoltre ogni oggetto ha tutti i metodi che
ritiene utile sarà anche più conveniente lavorare con esso: avremo una
serie di funzionalità "gratuite" pronte per essere utilizzate.

Non riuscite a capire il concetto? Proviamo così. Nell'esempio
precedente abbiamo parlato di un fantomatico oggetto Cerchio. Più o meno
tutti sapevano già calcolare l'area dato il raggio. Ma se la figura
fosse stata un icosaedro? Con un oggetto pronto era ugualmente facile
tanto quanto chiamare il metodo area. Chiaro adesso???

Proviamo a dichiarare adesso questa fantomatica classe Cerchio:

``` py title="Definizione della classe Cerchio"

# File "cerchio.py"
import math

class Cerchio:
    # inizializza gli attributi della classe
    def __init__(self, raggioInserito):
        # aggiunge l’attributo "raggio" alla classe e lo inizializza
        self.raggio = raggioInserito

    def calcolaArea(self):
        a = math.pi * self.raggio * self.raggio
        return a

    def calcolaCirconferenza(self):
        c = 2* math.pi * self.raggio
        return c
```

Il fantomatico oggetto Cerchio si inizializza con il codice seguente:

``` python
cx = Cerchio(4)   # crea un oggetto della classe Cerchio con raggio 4
print("Cerchio")
print("raggio:", cx.raggio)
print("area:", cx.calcolaArea())
print("circonferenza:", cx.calcolaCirconferenza())
```

che dovrebbe visualizzare:

``` 
Cerchio
raggio: 4
area: 50.26548245743669
circonferenza: 25.132741228718345
```

Spero adesso sia tutto ok... Non è così, lo so. Per iniziare cerchiamo
di chiarirci alcuni termini e alcune funzioni *strane* che ho
utilizzato prima e poi vediamo qualche esercizio.


<!-- ################################################################################################# -->
## Terminologia

Chiariamo bene i termini che andremo ad utilizzare per definire una
classe manualmente e che sono utilizzati da Python.

class Intanto faccio notare che, come abbiamo utilizzato la clausola def
per definire una funzione, bisogna utilizzare la clausola class per
dichiarare una classe.

`class Cerchio:`

Ricordate?

Per evitare confusione fra i concetti mi piace utilizzare i termini classe e oggetto. In OOP solitamente si usa il
termine "classe" per la definizione dell'oggetto, mentre "oggetto" è l'istanza del tipo classe definito. Prima abbiamo scritto:

`cx = Cerchio(4)`

Bene: `cx` è un oggetto di tipo Cerchio, un'istanza della classe, mentre `Cerchio` è la classe.

`self` 

Avrete notato questo parametro predefinito nelle funzioni della classe e per inizializzare la variabile membro. 
Questo parametro viene automaticamente istanziato da Python in questo modo:

`cx.area()` diventa `Cerchio.area(cx)`

In questo modo il parametro self permette accesso alla classe, ma
l'utente della classe non ha bisogno di occuparsene. Spero sia chiaro,
più facile di così non riesco. In pratica, la variabile self va messa
come primo membro di ogni metodo di una classe, in modo da poter
collegare il metodo alla classe stessa.

Metodi che iniziano (e finiscono) con doppio underscore `__` Ce ne sono
parecchi in ogni classe e hanno ognuno un compito specifico. Vengono
definite Funzioni Speciali. Ne introdurremo molte altre più avanti. La
cosa importante da capire su di esse è che questi metodi non vanno
eseguiti "volontariamente" (ad esempio come fareste con il metodo
"area()" della classe Cerchio se voleste calcolarne l'area) ma vengono
eseguiti automaticamente in determinate situazioni. Quindi ogni volta
che incontrate una funzione speciale dovete farvi sempre due domande:

> 1.  In quale momento particolare questa funzione speciale viene
>     eseguita automaticamente?
> 2.  Voglio modificare il comportamento della classe in quel caso
>     particolare? Bene, se la risposta a questa domanda è sì significa
>     che dovete re-implementare quella funzione. Man mano vedremo come.

Per adesso vediamo le 2 funzioni speciali più comuni in assoluto:

`def __init__( self , . . . )`

:   Questa particolare funzione speciale viene eseguita automaticamente
    quando si definisce un oggetto di una classe. La sua implementazione
    serve per dare un valore iniziale agli attributi della classe, siano
    essi inseriti come parametri della stessa o inizializzati ad un
    valore scelto dal programmatore.

    Vediamo un esempio per chiarirci al meglio le idee. Definiamo la
    classe Quadrato. L'utente potrà scegliere il lato del Quadrato, ma
    inizialmente esso sarà disegnato con sfondo bianco e lati neri.

``` py title="Classe Quadrato"

class Quadrato:
    def __init__(self, lato):
        self.lato = lato
        self.coloreSfondo = "bianco"
        self.coloreBordo = "nero"

# ...

# nella riga sotto viene eseguita automaticamente la funzione __init__
obj = Quadrato(4)

# si definisce così un oggetto della classe Quadrato, di lato 4
# con colore di sfondo bianco e colore del bordo nero.
```

`def __str__ (self)`

:   La funzione `__str__` serve per visualizzare in maniera semplice
    informazioni sulla classe (praticamente per visualizzare il valore
    dei suoi attributi). Questa funzione viene eseguita automaticamente
    quando si esegue la funzione print() con parametro un oggetto della
    classe.

    La funzione `__str__` non prende MAI parametri e ritorna sempre
    una stringa, ricordatelo! Ad esempio, definiamo la funzione
    `__str__` per la classe Quadrato definita sopra:


``` python
def __str__(self):
    s = ""
    s += "Quadrato di lato " + str(self.lato)
    s += ", sfondo " + self.coloreSfondo
    s += ", bordo " + self.coloreBordo
    return s

...
# riferito all’oggetto obj definito prima
print(obj)
# visualizzerà "Quadrato di lato 4, sfondo bianco, bordo nero"
```

<!-- ################################################################################################# -->
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

    def calcolaArea(self):
        a = self.b * self.h
        return a

    def calcolaPerimetro(self):
        p = 2*(self.b + self.h)
        return p

if __name__ == "__main__":
    ret = Rettangolo(5,3)
    print(ret)
    print("Base:", ret.b)
    print("Altezza:", ret.h)
    print("Area:", ret.calcolaArea())
    print("Perimetro:", ret.calcolaPerimetro())    
```

<!-- ################################################################################################# -->
## Esercizi di comprensione

Prima di andare avanti, proviamo a definire alcune classi e proporre con
esse qualche test in cui inserire e modificare i valori degli attributi
definiti e visualizzare i risultati delle chiamate ai metodi definiti.

Per ognuna ricordate che è obbligatorio definire sempre la funzione
`__init__` e la funzione `__str__` e verificarne il funzionamento,
definendo un oggetto della classe e visualizzandone i valori con la
print().

--------------------------------------------------------------------

**Esercizio 701**

Definire la classe Persona con attributi nome, cognome, data e luogo di
nascita, sesso (M/F). La funzione di `__init__` della classe non deve
avere argomenti. 

Definite un maschio e una femmina della classe a libera scelta.

--------------------------------------------------------------------

**Esercizio 702**

Definire la classe TriangoloRettangolo inserendo come attributi i due
cateti. Aggiungere i metodi per il calcolo dell'ipotenusa, dell'area e
del perimetro. 

Definire un oggetto della classe TriangoloRettangolo con cateti uguali a 4 cm e 3 cm, 
visualizzare i suoi attributi e calcolare l'ipotenusa, l'area e il perimetro.

--------------------------------------------------------------------

**Esercizio 703**

Definire la classe Animale con attributi nome e specie. Aggiungere il
metodo "corri" (ritorna la stringa "sto correndo...") e "mangia"
(ritorna la stringa "sto mangiando"). 

Definire un cane di nome "Piero" e farlo correre e mangiare. Visualizzare i suoi attributi.

--------------------------------------------------------------------

**Esercizio 704**

Definire la classe Persona con attributi nome, età e sesso (M/F). La
funzione di `__init__` della classe deve prendere come argomento solo
il nome della persona, mentre l'età va impostata automaticamente a ZERO
e il sesso a "M" (o "F", scegliete voi). 

Aggiungere i metodi `invecchia` (aggiunge un anno di età) e `saluta` (restituisce
"signore" o "signora" a seconda del sesso della persona). 

Definire 2 persone: "Augusto", maschio di 47 anni e "Marianna", femmina di 44
anni. Utilizzare i metodi `invecchia` e `saluta` per entrambi,
procedere poi a visualizzare gli attributi di entrambi.

--------------------------------------------------------------------

**Esercizio 705**

Definire la classe ContoCorrente con attributi proprietario e capitale;
il proprietario va definito tramite parametro della funzione
`__init__` mentre il capitale va inizializzato a ZERO. 

Definire il metodo `deposita`, che prende un parametro reale, controlla che sia
positivo ed eventualmente lo aggiunge al capitale e il metodo
`preleva`, che prende anch'esso un parametro reale, verifica che il
parametro sia positivo, verifica che sia minore del capitale ed
eventualmente lo sottrae da esso (il metodo ritorna True se possibile,
False altrimenti). 

Definire il Conto Corrente di "Gigetto". Depositare
in esso 1000 euro. Prelevare 600 euro per 2 volte. La seconda volta
l'operazione dovrebbe fallire. Visualizzare dopo ogni operazione i
valori dell'oggetto con la funzione print().

--------------------------------------------------------------------

**Esercizio 706**

Definire la classe Crittografia con attributo un numero intero che
indica lo spiazzamento dei caratteri. Questo numero sarà utilizzato per criptare le stringhe traslando i caratteri
di `numero` posti sull'alfabeto: ad esempio se il numero è 3 e vuoi criptare la stringa "ale", prendi la "a" e vai avanti
di 3 sull'alfabeto ("d"), prendi la "l" e vai avanti di 3 sull'alfabeto ("o") e lo stesso con la "e": la stringa criptata ottenuta è "doh".

La classe contiene due funzioni: 

- `cripta`, che prende una stringa come parametro e restituisce la stessa trasformata (*criptata*) secondo la regola descritta sopra; 

- `decripta`, che prende una stringa come parametro e la rimette "a posto" (la *decripta*). 

Definire due oggetti della classe Crittografia con parametro a piacere e provare a "criptare" e "decriptare" una
stringa, verificando che la stringa decriptata sia uguale a quella inserita prima di essere criptata.

--------------------------------------------------------------------

**Esercizio 707**

Definire la classe Automobile con attributi marca, modello, velocità e
numero di persone trasportate. La funzione init prende come parametri la
marca e il modello e imposta a ZERO gli altri attributi. Implementare i
seguenti metodi:

-   `faiSalirePersona`: aggiunge una persona al numero di persone 
    trasportate fino ad un massimo di 5. Ritorna True se è stato
    possibile aggiungere una persona, False altrimenti.
-   `faiScenderePersona`: toglie una persona al numero di persone
    trasportate (Se possibile ovviamente). Ritorna True se è stato
    possibile togliere una persona, False altrimenti.
-   `accelera`: aggiunge 20 kmh alla velocità di marcia, fino ad un
    massimo di 120 kmh. Funziona solo se il numero di persone
    trasportate è positivo. Ritorna True se è stato possibile aumentare
    la velocità, False altrimenti.
-   `rallenta`: toglie 20 kmh alla velocità di marcia, ovviamente fino a
    fermarsi. Ritorna True se è stato possibile diminuire la velocità,
    False altrimenti.
-   `frena`: azzera la velocità di marcia. Ritorna True se è stato
    possibile frenare, False altrimenti.

Definire un oggetto della classe Automobile e progettare un test in modo
che ognuna delle funzioni venga eseguita almeno 2 volte, una ritornando
True, una ritornando False.

--------------------------------------------------------------------

**Esercizio 708**

Definire la classe TrapezioRettangolo, che prende come parametri la base
minore, la base maggiore e l'altezza del Trapezio. 

Definire i metodi `latoObliquo`, `area`, `perimetro`. Dichiarare un oggetto
TrapezioRettangolo e procedere a visualizzare i suoi parametri, la sua
area e il suo perimetro.

--------------------------------------------------------------------

**Esercizio 709**

Definire la classe "Orario", con parametri i tre interi per ore,
minuti e secondi. Implementare inoltre le seguenti funzioni:

- `secondiDaMezzanotte()`: restituisce l'intero che rappresenta il numero di secondi trascorsi dalla mezzanotte. 
- `aggiungiTempo(ore, minuti, secondi)`: aggiunge tempo all'orario corrente. Ad esempio, se l'oggetto della classe Orario segna 
   le 03:14:22 e si esegue su di esso la funzione aggiungoTempo(1,2,3) l'orario diventa le 04:16:25. Attenzione a quando "il giro ricomincia"...
- `momento()`: ritorna la stringa "mattina" se orario è fra le 8 e le 13, "pomeriggio" se fra 13 e 20, "sera" fra 20 e 23, "notte" altrimenti

--------------------------------------------------------------------

**Esercizio 710**

Definire la classe CartaFedeltà, per la gestione degli utenti di un
grande magazzino. La carta fedeltà è nominativa (appartiene ad un solo
cliente) e consente l'accumulo dei punti (attraverso il metodo
accumulaPunti(soldiSpesi)) calcolati sulla base della spesa effettuata:
ogni 12€ di spesa si aggiunga un punto. All'inizio ovviamente il numero
di punti è ZERO. Il cliente può decidere, in ogni momento, di usufruire
di una parte dei punti accumulati per l'ottenimento di un premio
(implementare un opportuno metodo utilizzaPunti(quantita): il metodo
ritorna True... False altrimenti). 

Definire le carte fedeltà per 2 clienti. Il primo cliente fa una spesa pari a 150€. 
Il secondo cliente fa una spesa di 300€. In seguito, il primo cliente fa una spesa pari a
1500€ e, dopo aver pagato, decide di utilizzare 100 dei punti accumulati
per ritirare un premio. Il secondo cliente chiede di utilizzare 50 dei
punti accumulati.

--------------------------------------------------------------------

**Esercizio 711**

Definire la classe Giocatore con nome, numero di maglia e ruolo
ricoperto. Il nome del giocatore va impostato tramite parametro, mentre
il numero va impostato inizialmente a ZERO e il ruolo a "X".

Definire la funzione impostaRuolo(stringa) che prende una stringa come
parametro e imposta il ruolo del giocatore. Fare in modo che i ruoli
accettabili siano solo "P" (per portiere), "D" (per difensore),
"C" (per centrocampista), "A" (per attaccante). La funzione ritorna
True o False a seconda del fatto se il ruolo viene effettivamente
modificato oppure no.

Definire la funzione cambiaNumero(intero) che modifica il numero di
maglia solo se esso varia fra 1 e 99. Anche qui, la funzione ritorna
True o False...

DIFFICILE E OPZIONALE: è possibile fare in modo anche che i numeri di
maglia dei vari giocatori siano tutti diversi fra loro? Proponi una
soluzione al problema. Definire un giocatore di nome "Edoardo".
Tramite la funzione impostaRuolo, impostare il suo ruolo ad attaccante
(con "A") e poi modificarlo a terzino ("T"). La seconda modifica
dovrebbe fallire. Utilizzare la funzione cambiaNumero per modificare il
suo numero a 103 e poi a 7. Definire un giocatore di nome
"Alessandro". Tramite la funzione impostaRuolo, impostare il suo ruolo
a centrocampista (con "C"). Utilizzare la funzione cambiaNumero per
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

ULTERIORE DIFFICOLTA' (opzionale): fare in modo che i numeri della
tupla siano ordinati in senso crescente.

Definire una funzione estrazioniDellaSettimana() che permette a tutte le
ruote presenti di estrarre i numeri del lotto. La funzione ritorna un
dizionario che ha come chiavi i nomi delle ruote in cui avvengono le
estrazioni e come valori le tuple dei 5 numeri estratti.

Definire un oggetto della classe EstrazioneLotto.

Inserire tramite il metodo aggiungiRuota le seguenti città: Jesi,
Senigallia, Ancona, Jesi (dovrebbe fallire, già presente), Monsano,
Moie, Ancona (err). Visualizzare il risultato della funzione
estrai("Jesi"), estrai("Ancona"), estrai("Milano"). L'ultima
dovrebbe ritornare una tupla vuota. Eseguire la funzione
estrazioniDellaSettimana e visualizzare ordinatamente il dizionario
ottenuto, con una visualizzazione simile a questa:

-   Jesi: (1,5,9,23,89)
-   Senigallia: (23,34,45,67,88)
-   Ancona: (39, 43, 44, 78, 81)


--------------------------------------------------------------------

**Esercizio 713: Agenda**


Una agenda contiene una serie di impegni identificati con una descrizione generica e con il giorno in cui questo impegno è preso. 
Esempi di impegni potrebbero essere:

- Calcetto, Lunedì
- Parrucchiere, Mercoledì
- Pizza con gli amici, Venerdì

Quando si crea un oggetto della classe Agenda si parte (ovviamente) con una lista di impegni vuota! 
La classe presenta inoltre le seguenti funzioni:

- `inserisciImpegno ( descrizione, giorno )` : prende i dati dai parametri della funzione e inserisce il nuovo impegno in agenda. Non ritorna nulla.
- `listaImpegniDi ( giorno )` : prende come parametro un giorno della settimana e ritorna la lista delle descrizioni degli impegni per quel giorno.
- `rimuoviImpegno ( descrizione )` : prende come parametro la descrizione di un impegno e, se lo trova in agenda, rimuove l’impegno corrispondente. 
  Ritorna True se viene rimosso un impegno, False altrimenti.
- `trovaImpegno ( descrizione )` : prende come parametro la descrizione di un impegno e, se lo trova in agenda, ritorna il giorno in cui quell’impegno è stato preso. 
  Se non trova nulla, ritorna la stringa "NON TROVATO".

Definire la classe Agenda, un oggetto della classe stessa, inserire in essa almeno 4 impegni (tramite la funzione inserisciImpegno) 
e fare un test di utilizzo di tutte le altre funzioni


--------------------------------------------------------------------

**Esercizio 714: Rubrica**

Una rubrica contiene una lista di contatti. Ogni contatto comprende un nome ed un numero di telefono (memorizzabile comunque come una stringa). 
Esempi di contatti potrebbero essere:

- prof , 555-12345
- tizio di Dallas, 214-748-3647
- casa, 0731-24680

Quando si crea un oggetto della classe Rubrica, si parte con un elenco di contatti vuoto.
La classe presenta inoltre le seguenti funzioni:

- `inserisciContatto ( nome , numero )` : prende i dati dai parametri della funzione e inserisce il nuovo contatto in rubrica. Non ritorna nulla.
- `modificaContatto ( nome , nuovoNumero )` : modifica il contatto identificato dal parametro nome, aggiornando il suo numero con il parametro nuovoNumero. 
  Ritorna True se il numero viene aggiornato, False altrimenti.
- `rimuoviContatto ( nome )` : rimuove dalla rubrica il contatto identificato dal parametro nome. 
  Ritorna True se è stato possibile rimuovere il contatto, false altrimenti.
- `trovaNumero ( nome )` : ritorna il numero del contatto con nome la stringa riportata nel parametro. 
  Se non si trova nessun contatto, ritorna la stringa "NESSUN CONTATTO".

Definire la classe Rubrica, un oggetto della stessa, inserirvi almeno 4 contatti (tramite la funzione inserisciContatto) e fare un test di utilizzo di tutte le altre funzioni.



<!-- ################################################################################################# -->
## Accesso agli attributi

Nei linguaggi di programmazione più *antichi* e *strutturati* (come C++ e Java) esiste il concetto di *visibilità* di un membro (un attributo o un metodo)
della classe. Ogni membro può essere specificato come:

- `public`, ovvero visibile a chiunque utilizzi la classe e le sue istanze;
- `protected`, ovvero visibile solo all'interno della propria classe di appartenenza e dall'interno di ogni sua classe derivata;
- `private`, ovvero visibile solo all'interno della propria classe di appartenenza. Questa è la visibilità di default.


Questi concetti in Python (che è un linguaggio molto più... moderno. Non so quanto in questo caso sia un bene...) è stato tradotto in maniera molto particolare.

La visibilità di default è diventata quella `public` per eliminare alla radice qualunque problema di accesso. Di sicuro una mossa a favore di chi è poco esperto.

Per ottenere la visibilità `protected` basta iniziare il nome della variabile con un underscore `_`. Una roba tipo:

```python
class Persona:
    def __init__(self, name):
        self._nome = name
```

Attenzione però! Il livello di visibilità che si introduce con un underscore è puramente sociale!!! Questo significa che se qualcuno volesse accedere alla vostra
variabile dall'esterno, potrà sempre farlo e l'interprete Python non si lamenterà! Qualunque programmatore Python però... lo considererebbe alquanto scortese!

```python
p = Persona("Ciccio")
print(p._nome) # ecco... adesso sono un programmatore maleducato. Corretto, ma maleducato!!!
```

Avrete già capito... la visibilità `private` si ottiene iniziando il nome di una variabile (o di una funzione membro) con 2 underscore. Stavolta però le cose cambiano...
l'interprete custodisce eccome i membri privati e riporta un **AttributeError**. Insisto col mio esempio:

```python
class Persona:
    def __init__(self, name):
        self.__nome = name

p = Persona("Ciccio")
print(p.__nome)      # ERRORE!!! Adesso sono solo un somaro...
```

Capito come Python rende la visibilità dei membri delle classi, passiamo alla domanda di concetto: che cosa può interessarci tutto ciò? Risposta: a proteggere le variabili!
Dall'esterno. Da un uso libero. Da chi vuole visualizzarle senza permesso. Da chi vuole modificarne il valore come crede.

---------------------------------------------------------------------------------------------------------

Inserisco un pezzo di codice di linguaggio C++ nella speranza di rendere evidente il concetto:

```c
class Persona
{
// attributi privati (in C gli attributi si segnano con un solo underscore)
    string _nome;

// metodi pubblici
public:
    // setter method: permette di impostare il valore dell'attributo _nome
    bool setNome(string n) {
        if (n == "")
            return False;
        _nome = n;
        return True;
    };
    
    // getter method: ritorna il valore dell'attributo _nome
    string nome() const {
        return _nome;
    }; 
};
```

Anche se non conosciamo il linguaggio C++, quello che vediamo è molto semplice da comprendere: l'attributo `_nome` è privato e quindi 
**NON** modificabile direttamente dall'esterno della classe `Persona`.<br>
Questo significa che un codice del genere da errore:

```c
Persona pers;
pers._nome = "Andrea"; // ERRORE! L'attributo è PRIVATO!!!
```

> Questa sovrastruttura, tipica dei linguaggi compilati come C e Java, 
> fornisce un livello di protezione aggiuntivo ai valori delle variabili membro!

Se il programmatore vuole che all'esterno venga visualizzato il nome della Persona, inserisce nella classe un metodo *getter* (tipicamente `nome()`)
cioè un metodo che *ritorna* il valore di `_nome`.

Se il programmatore vuole che dall'esterno sia possibile modificare il nome della Persona, inserisce nella classe un metodo *setter* (tipicamente `setNome(string n)`),
cioè un metodo che permette di impostare un nuovo valore per `_nome` (se il valore  accettabile!)

---------------------------------------------------------------------------------------------------------


Nel linguaggio Python esiste uno strumento che permette una implementazione analoga (ovvero... *simile*, **NON** *uguale*) a questo livello di protezione
delle variabili che si definisce il **Python @property decorator**.

Un codice funzionalmente analogo a quello sopra in `C++`, che scriviamo in `Python`, potrebbe essere fatto così:

```python
class Persona:
    def __init__(self, name):
        # funziona anche se usi il livello private con il doppio underscore 
        self._nome = name
    
    @property
    def nome(self):
        """ DOCUMENTA QUI LA TUA PROPRIETA': il nome della persona """
        return self._nome
        
    @nome.setter
    def nome(self, name):
        if name == "":
            raise ValueError("Tutte le persone hanno un nome...")
        self._nome = name
        return
```

Mamma mia, quante cose da spiegare... Cominciamo!

```python
def __init__(self, name):
    self._nome = name
```

Secondo la convenzione già esposta, si intende mantenere `nascosta` la variabile membro `_nome`.

```python
@property
def nome(self):
    """ DOCUMENTA QUI LA TUA PROPRIETA': il nome della persona """
    return self._nome
```

Questo decoratore (`@property` con la chiocciolina davanti si dice *decoratore* in Python) fa in modo che `nome` (in questo caso, il nome della funzione) 
diventi una `Python property`. La `docstring` interna specifica la descrizione della proprietà.


> Una proprietà è una caratteristica tipica di un oggetto, 
> a cui possono essere aggiunti funzioni `getter` e `setter`.


La definizione della proprietà implica automaticamente l'esistenza della funzione `getter`, quella che ritorna il valore. Se vogliamo inserire anche la funzione
`setter`, che permette i modificare il valore della proprietà, allora scriviamo:

```python
@nome.setter
def nome(self, name):
    if name == "":
        # questa la ignoriamo??? La scriviamo così e basta :D
        raise ValueError("Tutte le persone hanno un nome...")
    self._nome = name
    return
```

A questo punto, la proprietà `nome` diventa una sorta di nuova *variabile membro* della classe, che invoca automaticamente le funzioni *getter* e *setter* ad essa collegate:

```python
pers = Persona()
pers.nome = "Andrea"        # esegue la funzione "setter" automaticamente
print("Nome:", pers.nome)   # esegue la funzione "getter" automaticamente
```

Questo modo di implementare le variabili membro di una classe è la via scelta dai programmatori Python per gestire i valori delle stesse.



<!-- ################################################################################################# -->
### Read-Only Properties


Capire il concetto di proprietà di sola lettura è molto semplice: basta *dimenticarsi* di aggiungere ad una prorietà 
la funzione *setter*... ed ecco che diventa impossibile modificarla al di fuori della classe!!!

```python
class Oggetto:
    def __init__(self):
        self._valore = 0
    
    @property
    def valore(self):
        return self._valore

obj = Oggetto()
obj.valore = 5 # ERRORE!!!! NO setter!!!
```

Questa caratteristica delle proprietà ritorna utile quando abbiamo delle caratteristiche *derivate* da altre: ad esempio,
l'area di un rettangolo può essere definita come proprietà read-only, in modo che essa venga calcolata automaticamente a partire
dai valori attuali di base e altezza, ma non possa essere impostata da codice. Proviamo:

```python
class Rettangolo:
    def __init__(self, b, h):
        self.base = b
        self.altezza = h
    
    @property
    def area(self):
        return self.base * self.altezza

ret = Rettangolo(5,4)
print("Area:", ret.area)    # scrive "Area: 20"
ret.area = 30               # ERRORE!!! Quali sono base e altezza di un rettangolo di area 30? Boh...
```

Mi sembra facile.
Provate a verificare la vostra comprensione coi seguenti esercizi.


<!-- ################################################################################################# -->
### Esercizi sulle proprietà

--------------------------------------------------------------------

**Esercizio 720: SVOLTO**

(Ri)definire la classe Rettangolo, facendo in modo che base e altezza siano numeri comunque positivi e che area e perimetro
siano calcolate automaticamente come proprietà in sola lettura.

Il codice che segue mi sembra alquanto chiaro. Provate a leggerlo con calma, a copiarlo sul vostro computer e a provare alcune modifiche 
per essere sicuri di aver capito tutto!

```python
class Rettangolo:
    def __init__(self, b, h):
        # i valori passati nella init NON sono sottoposti al controllo
        # imposto dai decoratori sotto, quindi...
        self._base = abs(b)
        self._altezza = abs(h)
    
    def __str__(self):
        return f"Rettangolo {self._base} x {self._altezza}"

    @property
    def base(self):
        return self._base
    
    @base.setter
    def base(self, value):
        if value < 0:
            raise ValueError("La base di un rettangolo non può essere negativa")
        self._base = value
        return
    
    @property
    def altezza(self):
        return self._altezza
    
    @altezza.setter
    def altezza(self, value):
        if value < 0:
            raise ValueError("L'altezza di un rettangolo non può essere negativa")
        self._altezza = value
        return
    
    @property
    def area(self):
        return self._base * self._altezza
    
    @property
    def perimetro(self):
        return (self._base + self._altezza) * 2
    
if __name__ == "__main__":
    r1 = Rettangolo(5,3)
    print(r1)
    # se decommenti sotto vedi il ValueError con la nostra spiegazione
    #r1.base = -12
    r1.base = 12
    print("base:", r1.base)
    print("altezza:", r1.altezza)
    # area e perimetro sono proprietà NON funzioni, quindi vanno SENZA parentesi
    print("area:", r1.area)
    print("perimetro:", r1.perimetro) 
    # se decommenti sotto, vedi l'interprete lamentarsi per l'assegnazione
    #r1.area = 23
```

E adesso sotto con un esercizio analogo!

--------------------------------------------------------------------

**Esercizio 721**

(Ri)definire la classe Cerchio, facendo in modo che il raggio sia un numero sempre positivo e che il diametro, l'area e la circonferenza 
siano calcolate automaticamente come proprietà in sola lettura.

--------------------------------------------------------------------

**Esercizio 722**

Definire una classe Temperatura, che NON prende parametri in fase di inizializzazione. Ha una sola variabile membro, la temperatura in gradi Kelvin, che
(come sapete) deve essere non negativa. Presenta inoltre due proprietà in sola lettura per visualizzare la temperatura in gradi Celsius e in gradi Farheneit.


--------------------------------------------------------------------

**Esercizio 723**

Definire la classe Data con giorno, mese, anno che NON possono essere modificati (capito come fanno le classi Datetime???)


--------------------------------------------------------------------

**Esercizio 724**

Definire la classe Contatore. Essa ha un solo valore membro (la conta, appunto).
La conta parte da zero, non può essere modificata e viene incrementata ogni volta che viene visualizzata.

--------------------------------------------------------------------

<!-- 
INSERISCI ALTRI DUE ESERCIZI (almeno!!!) per proprietà e metodi.
-->



<br>
<br>
<br>

