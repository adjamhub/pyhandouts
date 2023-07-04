# Ereditarietà



L'ereditarietà è un concetto tipico della programmazione orientata agli oggetti che ovviamente qui sarà declinato in salsa Python :)
Essa è la capacità di definire una classe (la ***classe derivata***) a partire da una già esistente (la ***classe base***), facendo in modo che 
la nuova classe *erediti* tutte le caratteristiche della classe iniziale.

``` python
class Persona:
    def __init__(self, name):
        self.nome = name

    def saluta(self):
        return f"buongiorno, mi chiamo {self.nome}"

class Studente(Persona):        # la classe Studente "deriva" dalla classe Persona
    pass
    
# ------------------------------------ 
if __name__ == "__main__":
    p = Studente("Gino")
    print(p.saluta())        # la classe Studente "eredita" il metodo saluta()

# scrive: buongiorno, mi chiamo gino
```

Fin qui, mi sembra molto semplice... La classe Studente deriva dalla classe Persona e quindi eredita tutte le sue caratteristiche, in particolare, le sue funzioni!
Quindi può usare la funzione saluta() ereditata.

Adesso pensate che uno studente voglia comportarsi in modo *diverso* da una generica Persona... salutando in maniera più sciolta, più informale, 

E' possibile modificare il comportamente di una funzione ereditata semplicemente riscrivendola da capo nella classe derivata: 
questo comportamento si definisce ***OVERRIDING***, cioè la nuova funzione implementata va a sovrapporsi alla funzione ereditata nascondendola dall'esecuzione.

``` python
class Persona:
    def __init__(self, name):
        self.nome = name

    def saluta(self):
        return f"buongiorno, mi chiamo {self.nome}"

class Studente(Persona):        # la classe Studente "deriva" dalla classe Persona
    def saluta(self):
        return f"bella raga, io sono {self.nome}!!!"
    
# ------------------------------------ 
if __name__ == "__main__":
    p = Studente("Gino")
    print(p.saluta())        # la classe Studente utilizza il metodo saluta() reimplementato
    
# scrive: bella raga, io sono gino!!!
```

Visti questi due esempi, possiamo azzardare a dare una definizione del comportamento dell'ereditarietà in Python.


> In Python il meccanismo dell'ereditarietà si abilita semplicemente scrivendo:
>
> ```
> class Derivata(Base):
>     ...
> ```
> il che significa che la nuova classe Derivata eredita tutte le caratteristiche della classe Base, da cui deriva.


Ok, ma... quali sono queste caratteristiche che vengono ereditate??? E qui, la risposta mi sembra abbastanza evidente: **le funzioni!!!**


> In Python, dal punto di vista pratico, l'ereditarietà permette *il passaggio* di tutte le funzioni 
> presenti nella classe Base alla classe Derivata


Quando attivi l'ereditarietà, tutte le funzioni definite nella classe Base passano automaticamente nella classe Derivata.


!!!warning "Attenzione!"

    Se pensate alle semplici classi che scriviamo adesso, l'ereditarietà è solo una inutile complicazione.
    
    Se pensate però al prossimo step, in cui importeremo librerie di classi fighissime (fatte da altri!!!) e con
    funzionalità incredibili, capite bene che programmare in OOP diventerà una *sciccheria*!
    
    Con una riga di codice avrete già implementato il mondo :smile:<br>
    E funziona tutto!!!
    

Se vuoi modificare il comportamento di una funzione devi agire tramite **overriding** reimplementando la funzione nella classe Derivata.

I metodi ereditati dalla classe Base, ma reimplementati tramite *overriding* non vengono cancellati, ma sono semplicemente nascosti dal metodo reimplementato
(*overriding* si potrebbe tradurre con *prevalente*, nel senso che il metodo reimplementato è prevalente rispetto a quello ereditato: non lo cancella, lo prevarica).

Per accedere ai metodi ereditati dalla classe Base, ma nascosti tramite *overriding*, Python mette a disposizione la funzione `super()`. 
Vediamo un esempio di utilizzo:


``` python
class Persona:
    def __init__(self, name):
        self.nome = name

    def saluta(self):
        return f"buongiorno, mi chiamo {self.nome}"

class Studente(Persona):        # la classe Studente "deriva" dalla classe Persona
    def saluta(self):
        s = super().saluta()
        return s + " e sono uno studente"
        
# ------------------------------------ 
if __name__ == "__main__":
    p = Studente("Gino")
    print(p.saluta())        # la classe Studente utilizza il metodo saluta() reimplementato
    
# scrive: buongiorno, mi chiamo Gino e sono uno studente
```


La funzione `super()` permette di accedere a tutti i metodi ereditati dalla classe Base (la classe Persona, nel caso della classe Studente).
Capisco che l'esempio sopra è un pò sempliciotto, però rende l'idea: prima ottengo l'output della funzione `saluta()` ereditata e poi ci aggiungo
qualcosa (leggi: ci faccio quello che mi pare).

In programmazione OOP la funzione `super()` è clamorosamente utile nel caso di overriding della funzione `__init__`: vediamo perché.

Nel seguente esempio proveremo ad aggiungere una variabile membro alla classe Studente relativa alla scuola frequentata dallo studente.
Per farlo dobbiamo forzatamente reimplementare la funzione `__init__` della classe, modificando così anche il numero dei parametri.
Questa cosa mi forza (poiché facendo overriding, la funzione `__init__` ereditata viene nascosta) a reimplementare tutto quanto viene definito 
nella funzione `__init__` della classe Base.

``` python
class Persona:
    def __init__(self, name):
        self.nome = name

class Studente(Persona):
    def __init__(self,name,school):
        self.nome = name
        self.scuola = school

# ------------------------------------ 
if __name__ == "__main__":
    p = Studente("Gino", "Liceo")    
```

Questo modo di fare può funzionare per classi banali come la classe Persona e la classe Studente... NON può funzionare quando si eredita da classi
complesse: bisogna usufruire della funzione `__init__` ereditata grazie alla funzione `super()`:


``` python
class Persona:
    def __init__(self, name):
        self.nome = name

class Studente(Persona):
    def __init__(self,name,school):
        super().__init__(name)
        self.scuola = school

# ------------------------------------ 
if __name__ == "__main__":
    p = Studente("Gino", "Liceo")    
```


La funzione `super()` che richiama la funzione `__init__` ereditata deve essere eseguita per prima cosa, fornendole tutti i parametri necessari (nel nostro caso, solo il nome),
mentre l'attributo aggiunto (self.scuola) si definisce subito dopo.



<!-- ################################################################################################# -->
## Python Object class

L'ereditarietà è un meccanismo talmente comodo che tutto il linguaggio Python è basato su di esso.

In Python 3 esiste una classe predefinita, chiamata `object`, da cui automaticamente tutte le classi derivano, secondo una
sorta di eredità forzata. Significa che tutte le classi che dichiariamo in Python 3 automaticamente derivano dalla classe `object`. 

Questo concetto di avere una unica classe base da cui per ereditarietà derivano tutte le altre non è una idea partorita 
in seno alla comunità Python ma una "genialata" che le comunità Java e Qt/C++ sperimentano già da decenni.

L'idea alla base di questa "moda" è quella di sfruttare l'ereditarietà per condividere con tutti gli oggetti una serie di proprietà comuni che
possano facilitare la gestione del codice e potenziare con semplicità e in maniera automatica tutto il sistema OOP Python.

Per verificare la struttura di ereditarietà che vi ho prospettato potete utilizzare le funzioni predefinite:

- `isinstance()`
- `issubclass()`

La funzione `isinstance()` prende due parametri, un oggetto e una classe (ricordate questi termini? Controllate nella terminologia) e ritorna
True se l'oggetto è una istanza della classe, False altrimenti. Come al solito, con un esempio è più facile capire:

``` python
class Prova:
    pass

a = Prova()
b = 2
isinstance(a, Prova)        # ritorna True
isinstance(b, Prova)        # ritorna False
isinstance(a, object)       # ritorna True
```

La funzione `issubclass()` prende due parametri, due classi e ritorna True se la prima classe è una sottoclasse della seconda.

``` python
issubclass(Prova, object)   # ritorna True
issubclass(int, Prova)      # ritorna False
issubclass(int, object)     # ritorna True, tutto deriva da object. Ricordate?
```

Come avete visto, porta tutto :)




<!-- ################################################################################################# -->
## Esercizi su ereditarietà

**Esercizio 741**

Definire la classe Quadrato con attributo il lato e metodi "area" e
"perimetro". Da quella derivare la classe Cubo, in cui va aggiunto il
metodo "volume" e ridefinito il metodo "area" in modo che esso
restituisca l'area delle 6 facce del cubo.

Dichiarare un oggetto Quadrato di lato 4, visualizzando i suoi attributi
e il risultato dei metodi area e perimetro.

Dichiarare un oggetto Cubo di lato 4, visualizzando i suoi attributi e
il risultato dei metodi area e volume.

--------------------------------------------------------------------

**Esercizio 742**

Definire la classe Persona, con attributi nome ed età e metodi saluta()
(restituisce la stringa "ciao, sono + nome") e invecchia() (aggiunge
un anno all'età).

Derivare da questa la classe Docente, che aggiunge l'attributo materia,
inizialmente vuoto.

Un docente invecchia più velocemente di una persona normale...
ridefinire la funzione invecchia() che aggiunge ad ogni chiamata 2 anni
al docente.

Aggiungere alla classe Docente il metodo insegna(materia), che prende
una stringa per il nome della materia da insegnare. Se la materia è una
fra "matematica", "italiano", "inglese" la funzione imposta
l'attributo materia e ritorna True. Altrimenti ritorna False.

Definire la persona "Giacomo", di anni 28. Testare i metodi saluta,
invecchia e poi visualizzare gli attributi della classe.

Definire il docente "Francesca", di anni 31. Testare i metodi saluta,
invecchia (ridefinito) e il metodo insegna con le materie "diritto" e
"inglese". Visualizzare infine gli attributi della classe.

--------------------------------------------------------------------

**Esercizio 743**

Definire la classe Punto2D, con attributi le coordinate del punto nel
piano cartesiano e le funzioni "distanzaDalCentro" e
"distanzaDalPunto". Questa seconda funzione prende come parametro un
ulteriore Punto2D da cui calcolare la distanza nel piano.

Derivare dalla classe Punto2D la classe Punto3D.

Definire il Punto2D di coordinate (3,4), visualizzare i suoi attributi
ed eseguire le funzioni distanzaDalCentro e distanzaDalPunto. Per
quest'ultima funzione definire il Punto2D di coordinate (6,8).

Definire il Punto3D di coordinate (4,5,6), visualizzare i suoi attributi
ed eseguire le funzioni distanzaDalCentro e distanzaDalPunto. Per
quest'ultima funzione definire il Punto3D di coordinate (1,1,2).

--------------------------------------------------------------------

**Esercizio 744**

Definire la classe Cerchio con gli attributi e i metodi che ritenete
opportuni.

Derivare da essa la classe Sfera.

Definire un cerchio di raggio 5, di cui calcolare area e circonferenza.
Definire una sfera di raggio 3, di cui calcolare area e volume.

--------------------------------------------------------------------

**Esercizio 745**

Definire la classe Contatto con nome, nick, numero, mail. In fase di
definizione la classe prende solo nome e numero e imposta gli altri alla
stringa vuota.

Definire i seguenti contatti:

- Giacomo (detto "Jack"), numero +39-340-1234567, mail <jack@mail.com>.
- Giovanni (detto "John"), numero +39-333-4567890, mail <john@mail.com>.

La classe ContattoLavoro deriva dalla classe Contatto, ma aggiunge le
informazioni fax e partitaIVA. Il costruttore prende ancora una volta
solo nome e numero, impostando le restanti variabili alla stringa vuota.

Definire il seguente contatto di lavoro:

- Alessandro (detto "Alex"), numero +39-345-6789012, mail <alex@mail.com>, 
  fax +39-0721-098765, partitaIVA 1234567890A

--------------------------------------------------------------------

**Esercizio 746**

Definire una classe Persona con attributi nome e anno di nascita,
forniti tramite parametri e indirizzo, inizialmente impostato alla
stringa vuota. Derivare da essa una classe Abbonato, che comprenda il
numero di noleggi effettuati e la percentuale di sconto a cui l'utente
ha diritto. Ovviamente il numero di noleggi all'inizio è zero, mentre lo
sconto iniziale è del 5% per tutti gli adulti fino a 50 anni e del 10%
per i più grandi (da 50 in su). Ogni 2 noleggi lo sconto aumenta del 5%
fino ad un massimo del 50% di sconto sul prezzo di noleggio. Definire
una funzione "noleggiaFilm" che aggiunge un noleggio all'abbonato,
eventualmente aggiornando le informazioni dell'abbonato.

--------------------------------------------------------------------

**Esercizio 747**

Definire una classe Veicolo, che contempli fra le sue caratteristiche la
possibilità di indicare la velocità massima (in km/h) e che in fase di
definizione imposta il numero dei chilometri percorsi a ZERO.

Implementare in essa, oltre alle funzioni che ritenete opportune, una
funzione chiamata "faiStrada" che richiede la velocità da tenere (che
dovrà essere minore della velocità massima) e il tempo per cui tenerla:
la funzione dovrà aggiornare il numero di chilometri percorsi.

Derivare da questa una classe Autobus, che comprende, oltre alle
caratteristiche ereditate, il numero massimo di posti all'interno e il
numero di persone attualmente all'interno, da inizializzare a ZERO.

Modificare la funzione di `__init__` in modo tale che il bus non possa
avere una velocità massima superiore ai 100 km/h.

Implementare una funzione chiamata "eseguiFermata" che prende come
parametro il numero di persone che salgono e il numero di persone che
scendono e aggiorna il numero di persone attualmente presenti
nell'autobus.



<br>
<br>
<br>

