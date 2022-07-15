# Funzioni


<!-- ############################################################################################ -->

## Funzioni in Python

Il termine "*funzione*" viene utilizzato in programmazione con un significato analogo a quello della matematica: 
una funzione è una procedura che può ricevere valori come argomenti e restituire un **unico** valore come risultato. 
Nel linguaggio comune si dice anche che una funzione **ritorna** un valore.

La sintassi generale per le funzioni in Python è così strutturata:

    def nome_funzione ( parametri: tipo ) -> tipo_di_ritorno :
        # blocco di codice che implementa la funzione
        # codice... 
        # la funzione ritorna un valore con l'istruzione return
        # return valore (del tipo_di_ritorno)

Come al solito, cominciamo con un semplice esempio per capire il funzionamento:

    def isPositive ( number:float ) -> bool:
        if number > 0 :
            return True
        return False
    
    numero = float(input("Inserisci un numero: "))
    if isPositive(numero):
        print("Hai inserito un numero positivo")
    else:
        print("NON Hai inserito un numero positivo")
    
    
Alcune considerazioni banali:

- la funzione si chiama "isPositive"
- la dichiarazione della funzione inizia con la clausola def
- eventuali parametri della funzione vanno fra parentesi tonde
- questa funzione prende un parametro di tipo float e ritorna un valore booleano
- **PRIMA** la funzione si dichiara (una volta), **POI** si può usare (quante volte ti pare)

Altro esempio banale:

    def somma (addendo1: float , addendo2: float) -> float:
        return addendo1 + addendo2
    
    print("27 + 35 = " , somma(27,35) )
    print("12 + 5 = " , somma(12,5) )

Questo solo per mettere in evidenza che, se ci sono più parametri, essi
vanno elencati fra virgole dentro le parentesi tonde.

Le funzioni in sé non aggiungono nessun nuovo potere al linguaggio che
le utilizza, se non una nuova sconvolgente comodità: quella di poter
riorganizzare e riutilizzare con semplicità il codice!

Le funzioni infatti hanno una definizione (quella che... comincia con
def!!!), utile appunto a definire il suo nome, i parametri di cui ha
bisogno e il suo comportamento e poi possono essere utilizzate
un'infinità di volte, semplicemente richiamando il loro nome e fornendo
i parametri necessari! Quante volte fino ad oggi avete usato la funzione
print()? Qualcuno si è chiesto per caso ***come*** faccia a scrivere
l'argomento sul monitor? Forse, ma non più di tanto. Tutti si sono
semplicemente preoccupati di capire ***cosa*** la funzione print()
faccia... e poi l'hanno utilizzata. E riutilizzata. E...

Dopo aver visto le funzioni, all'interno di questo capitolo, studieremo
una modalità che ci permetterà di utilizzarle ancora meglio! I moduli
(l'argomento successivo) non sono altro che collezioni di funzioni
divise per argomento (matematiche, statistiche, grafiche, data e ora,
ecc...) già pronte all'uso! Una pacchia :)

Per adesso però, cerchiamo di prendere mano con la definizione e
l'utilizzo delle funzioni. Vediamo ancora qualche piccola cosa e poi
*divertiamoci* con una valanga di esercizi da svolgere!!!



<!-- ############################################################################################ -->

### Parametri delle funzioni

I parametri di una funzione sono quelle variabili indicate tra parentesi
nella sua dichiarazione e che prendono i valori che vengono inseriti in
essa al momento della sua chiamata.

Capisco lo sconcerto... riprovo con un esempio:

    # la variabile "nome" è il parametro (di tipo str) della funzione saluta()
    def saluta (nome: str) -> str:
        return "ciao " + nome

Quando poi la funzione viene chiamata i parametri prendono dei valori:

    # il valore "ciccio" sarà inserito nel parametro "nome"
    # della funzione "saluta()"
    print( saluta("ciccio") )
    
    # scrive "ciao ciccio"

Se la funzione prende più di un parametro, Python fornisce 2 possibilità:

1. **l'inserimento ordinato** dei valori
2. **l'inserimento nominale** dei valori

Partiamo come al solito definendo una funzione di prova e verificando cosa succede:

    # la funzione ritorna parola ripetuta per un certo numero di volte
    # (con uno spazio di separazione in mezzo, ma non alla fine):
    # ripeti("ciao", 3) ritorna "ciao ciao ciao"
    def ripeti(parola:str , numero:int)->str :
        res = (parola + " " ) * (numero - 1) + parola
        return res

Nella chiamata con inserimento ordinato dei valori basta inserire i dati
nell'ordine della definizione: prima la parola e poi il numero:

    print( ripeti ("ciao", 4) ) # scrive "ciao ciao ciao ciao"

mentre se si inseriscono i dati nell'ordine errato si va incontro ad un errore:

    print( ripeti (3, "ciao") ) # ***ERRORE***

Se lo si desidera è anche possibile procedere ad un **inserimento nominale**, 
indicando cioè il nome della variabile in cui inserire il valore: in questo caso, l'ordine di inserimento non conta.

    print( ripeti (parola = "ciao" , numero = 3) ) # ciao ciao ciao
    print( ripeti (numero = 3 , parola = "ciao") ) # ciao ciao ciao

È inoltre possibile passare alle funzioni alcuni **valori di default**: questi vengono utilizzati se la funzione 
viene chiamata senza i valori da passare ai parametri o ignorati in presenza di essi.

    # definizione della funzione `saluta` con valore di default "ciccio"
    # per il parametro nome
    def saluta(nome = "ciccio"):
        return "ciao " + nome

Allora è possibile scrivere in fase di chiamata:

    saluta()        # ritorna la stringa "ciao ciccio"
    saluta("pippo") # ritorna la stringa "ciao pippo"

Spero sia chiaro, a me perlomeno sembra così.

<!-- ############################################################################################ -->

### Documentare le funzioni


Se ricordate la struttura di base di una funzione, proveremo adesso ad aggiungere una piccola parte: la documentazione!

    def nome_funzione ( parametri: tipo ) -> tipo_di_ritorno :
        """ documentazione di nome_funzione in formato doc_string """
        # blocco di codice che implementa la funzione
        # return valore del tipo_di_ritorno

La documentazione di una funzione va strutturata nel modo seguente:

    def nome_funzione ( par1: tipo1, par2: tipo2 ) -> tipo_di_ritorno :
    """una riga che descrive quello che la funzione fa
    
       alcune righe (opzionali) per descrivere più precisamente cosa la funzione 
       vuole ottenere
       
       Parameters
       ---------
       par1
            Una descrizione del parametro1
       par2
            Una descrizione del parametro2
            
       Returns
       -------
       tipo_di_ritorno
            La descrizione del valore ottenuto
    """
    
Facciamo una prova, implementando la funzione `trova(carattere, stringa)` che ritorna True se il carattere è presente nella stringa,
False altrimenti.

```python
def trova(carattere:str, stringa:str) -> bool:
    """
    Dice se carattere è presente o meno nella stringa.
    
    Parameters
    ----------
    carattere
        il carattere da cercare
    stringa
        la stringa in cui cercare il carattere
        
    Returns
    -------
    bool
        il valore booleano che dice se il carattere è presente o meno nella stringa
    """
    
    if carattere in stringa:
        return True
    
    return False
```

Tutto qui! Di sicuro non è una cosa molto complicata... ma chiaramente ci vorrà un pò di esercizio per essere sicuri di avere capito tutto bene.
Per fortuna stanno arrivando...

<!-- ############################################################################################ -->

### Importare moduli

Per lavorare con moduli e funzioni, finora abbiamo scritto cose del tipo:


<!-- ############################################################################################ -->

### Nomi dei moduli 


Tutte le persone hanno un nome che le identifica (ad esempio il mio nome è Andrea), ma quando le persone parlano di se stesse usano la parola `io` (*io* mi chiamo Andrea).
E fin qui mi sembra tutto semplice.

Abbiamo detto finora (e nel dubbio, lo ripeto con chiarezza) che anche i moduli, ovvero i file Python con estensione `.py`, hanno un nome, che dipende dal nome del file stesso:
ad esempio, il file `pippo.py` definisce il modulo di nome `pippo`. Ogni volta che definite un modulo, Python inizializza alcune variabili speciali, fra cui la variabile `__name__`
che contiene il nome del modulo (fra un attimo faccio un esempio).

Così come le persone, parlando di se stesse, dicono *io*, i moduli, al loro interno non utilizzano il loro nome, ma utilizzano la parola `__main__`.

Cerchiamo di chiarire subito questo primo concetto, il resto verrà naturalmente di conseguenza:

**Esempio 1: un unico file**

```python
# file pippo.py

# la variabile __name__ si riferisce al nome del modulo pippo
# essendo al suo interno, conterrà la parola "__main__"
print(__name__)
```

**Esempio 2: un altro file**
```python
# file ciccio.py

# importo il modulo pippo, dell'esempio 1
# importando il modulo, andrò ad eseguirlo. la print sopra (eseguita all'esterno del modulo pippo)
# scriverà il suo nome: "pippo".
import pippo

# la variabile __name__ qui sotto si riferisce al nome del modulo ciccio
# essendo al suo interno, conterrà la parola "__main__"
print(__name__)

# la variabile __name__ qui sotto si riferisce al nome del modulo pippo
# NON essendo dentro al modulo pippo, conterrà il suo nome proprio, ovvero "pippo"
print(pippo.__name__)
```

Tutto qui :)


<!-- ############################################################################################ -->

### Test delle funzioni


Dalle considerazioni fatte nei precedenti capitoli, vorrei farvi capire una tecnica molto utilizzata in ambito Python per l'esecuzione dei moduli e i test delle funzioni
in essi contenute.

La strategia è questa:

* scrivo il modulo con la definizione delle funzioni che mi interessano
* faccio delle prove per assicurarmi che tutto... funzioni! (faccio i **test**!!!) in fondo al file, dentro un `if __name__ == "__main__"`
* Se eseguo direttamente il modulo con le funzioni, l'if mi permette di svolgere i test (e verificare che tutto funzioni correttamente)
* Se importo il modulo in un altro contesto, il suo nome NON sarà "__main__" e i test non saranno svolti, permettendo di importare solo le funzioni!

Da questa spiegazione, deriva questa modalità di scrittura dei moduli con funzioni:

```python
# file prova.py

def molt(a:float,b:molt) -> float:
    """
    esempio di moltiplicazione
    
    Parameters
    ----------
    a,b
        i termini della moltiplicazione
    
    Returns
    -------
    float
        il prodotto
    """
    return a*b
    
# questa parte NON sarà eseguita all'esterno del modulo "prova"
if __name__ == "__main__":
    x = 5
    y = 4
    print("x:",x)
    print("y:",y)
    print( f"molt({x},{y}):{molt(x,y)}" )
    # ... e così via...
```

Da ora in poi scriveremo così i nostri moduli e in questo modo faremo tutti gli esercizi che seguono. Questo ci permetterà di definire un *modus operandi* logico e professionale, che ci
tornerà enormemente utile quando le cose diventeranno inevitabilmente più complicate.

Adesso, sotto con gli esercizi!

<!-- ############################################################################################ -->

### Esercizi sulle funzioni


!!! warning "Attenzione"

    Da ora in poi dovrete organizzare i vostri file come descritto sopra, aggiungendo **sempre** la documentazione
    delle funzioni implementate e inserendo alcuni test in fondo alle definizioni, dentro il controllo `if __name__ == "__main__"`
    
    Buon lavoro!
    

**Esercizio 501**

Scrivere una funzione che calcola l'area di un rettangolo e una che ne
calcola il perimetro, date la base e l'altezza.

------------------------------------------------------------------------------------------------

**Esercizio 502**

Scrivere una funzione che calcola l'area di un cerchio e una che
calcola la sua circonferenza. Entrambe richiedono (ovviamente) come
parametro il raggio del cerchio.

------------------------------------------------------------------------------------------------

**Esercizio 503: triangoli rettangoli**

Scrivere 3 funzioni relative ai triangoli rettangoli. Tutte e tre
prendono come parametri la lunghezza reale dei cateti e calcolano
rispettivamente:

- l'ipotenusa
- l'area
- il perimetro.

Utilizzare la funzione `ipotenusa` all'interno della funzione `perimetro`.

------------------------------------------------------------------------------------------------

**Esercizio 504: potenze**

Dati un parametro per la base e uno (intero) per l'esponente,
implementare la funzione potenza. Attenzione ai valori negativi degli
esponenti.

(Per implementare questa funzione **non** potete usare la sintassi Python `base**esp`, ma dovete *scrivere* i calcoli da fare)

------------------------------------------------------------------------------------------------

**Esercizio 505: MCD**

Scrivere una funzione che, dati due numeri interi positivi come parametri, ritorna il Massimo Comun Divisore fra questi.

------------------------------------------------------------------------------------------------

**Esercizio 506: mcm**

Scrivere una funzione che, dati due numeri interi positivi come parametri, ritorna il minimo comune multiplo fra questi.

------------------------------------------------------------------------------------------------

**Esercizio 507: carattere**

Scrivere una funzione che, dato un carattere, ritorna la stringa
"vocale", "consonante", "cifra" o "alfanumerico" a seconda del
carattere passato.

------------------------------------------------------------------------------------------------

**Esercizio 508: inverti stringa**

Scrivere una funzione che, data una stringa, ritorna la stringa
rovesciata. Ad esempio fornito "ciao" come parametro, la funzione
ritorna la stringa "oaic".

------------------------------------------------------------------------------------------------

**Esercizio 509: palindroma**

Scrivere una funzione che, data una stringa, dice se è palindroma oppure
no. Una stringa palindroma (ad esempio: "anna") si legge uguale in
entrambi i versi. Ritornare True o False a seconda che la stringa sia
palindroma oppure no.

------------------------------------------------------------------------------------------------

**Esercizio 510: farfallese**

Scrivere una funzione che, data una stringa, ritorna la stringa
convertita in farfallese. In farfallese ogni vocale viene seguita da una
f + la vocale ripetuta. Ad esempio la stringa "ciao" in farfallese
diventa "cifiafaofo".

------------------------------------------------------------------------------------------------

**PIU ESERCIZI SULLE FUNZIONI!!! Anche con liste, tuple, dizionari!!! interi...**

