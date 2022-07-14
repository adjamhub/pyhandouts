# Funzioni

!!! warning

    Questa parte della documentazione non è ancora pronta.

    Usa la documentazione in PDF reperibile
    [qui](https://www.adjam.org/next/index.php/s/egW7AnHxcif8n27?path=%2FPYTHON)



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

### Documentare le funzioni (TODO)

Qui spiega come si scrive la documentazione delle funzioni e come si vede quanto scritto

<!-- ############################################################################################ -->

### Testare le funzioni (TODO)

Qui spiega il problema di if `__name__ == "__main__"` e chiedi un atto di fede. Poi fai un esercizio svolto per spiegare il concetto

<!-- ############################################################################################ -->

### Esercizi sulle funzioni

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

