# Strutture di ripetizione


In Python esistono due tipi di strutture di ripetizione, ovvero per
ripetere un certo numero di volte una istruzione (fare *un ciclo*):

1.  ***Istruzione for***, che si utilizza per scorrere gli elementi di una sequenza
2.  ***Istruzione while***, che si utilizza per ripetere un blocco di istruzioni finché non si verifica una determinata condizione.

Queste istruzioni possono essere usate alla bisogna in un programma
Python e rappresentano due possibilità di implementazione per la
struttura iterativa. Vediamole nel dettaglio.


<!-- ###################################################################################################### -->

## Istruzione for


L'istruzione for permette di scorrere in maniera semplice gli elementi
di una sequenza ed effettuare una qualsivoglia operazione che si ripete
con oggetto l'ennesimo elemento di essa. La struttura di base è:

``` title="Definizione ciclo for"
for variabile in sequenza:
    # blocco da ripetere, indentato di 4 caratteri
    # . . .

# finita l'indentazione, termina il blocco
```

In questi primi esempi proveremo a lavorare solo con sequenze numeriche,
autogenerate con il comando `range`. Vediamo un semplice esempio:


``` py
for w in range(4):
    print(w)
```

``` title="Esecuzione"
0
1
2
3
```

Penso si capisca in maniera abbastanza intuitiva come funziona `range`:
parte da ZERO e va avanti di UNO fino al numero immediatamente prima a
quello indicato.

Tutto quello che viene indentato (spostato a destra) di 4 caratteri fa
parte del for. Quando si ritorna incolonnati alla parola `for` si
passa alla prossima istruzione. Ad esempio:


``` python
for n in range(6):
    if n % 2 == 0:
        print (n, "è pari")
    else:
        print (n, "è dispari")

print("Finito!")
```

``` title="Esecuzione"
0 è pari
1 è dispari
2 è pari
3 è dispari
4 è pari
5 è dispari
Finito!
```

Notate l'indentazione dell'esempio in cui tutto il blocco `if` è
ripetuto nel `for` e le due `print` fanno parte ognuna di una delle
due parti dell'`if`. Il `print` finale viene eseguito al termine del
ciclo.

La funzione range utilizzata in questo modo può essere utilizzata anche
semplicemente per *contare* le ripetizioni.

Il nome della variabile che si utilizza nel for è assolutamente libero e
casuale: potete scegliere qualsiasi nome ma evitate di sceglierne uno
già utilizzato nel vostro programma, per evitare confusione!!!


``` py title='Scrivi 5 volte "ciao"'
for x in range(5):
    print("ciao")
```


``` py title='Disegna una piramide di "x"'
for i in range(10):
    print( "x" * i )
```


Capiterà spesso di voler gestire una sequenza di numeri un po' più
complessa: ad esempio una sequenza che non inizia da zero, una sequenza
che avanza di 2, un conto alla rovescia...

Per tutte le casistiche possibili occorre studiare i parametri della
funzione `range()`.


!!! tip "Suggerimento"

    La funzione `range()` è una funzione predefinita del linguaggio che crea *"al volo"* una sequenza numerica intera. 


Essa può prendere 1,2,3 parametri! Vediamo i vari casi:

> range( stop )
>
> - la sequenza parte da 0 e avanza di 1:
> - *stop* è il valore finale (non compreso)

Ad esempio:

``` py
range(5) # indica la sequenza (0,1,2,3,4)
```

> range( start , stop )
>
> - *start* è il valore iniziale (compreso)
> - *stop* è il valore finale (non compreso)
> - si avanza di 1

Ad esempio:

``` py
range(2,7) # indica la sequenza (2,3,4,5,6)
```

> range( start , stop , step)
>
> - *start* è il valore iniziale (compreso)
> - *stop* è il valore finale (non compreso)
> - *step* è il valore di avanzamento

Ad esempio:

``` py
range(3,15,2) # indica la sequenza (3,5,7,9,11,13)
```


È più facile di quello che sembra! <br>
Vediamo qualche esempio:


``` py title="Esempio 1"
# c'è un numero solo, è stop!
# Start è predefinito a 0, step è predefinito a 1, quindi...
for i in range(5):
    print(i)
```

``` title="Esecuzione"
0
1
2
3
4
```


``` py title="Esempio 2"
# due numeri, il primo è start, il secondo è stop
# step è predefinito a +1
for i in range(1, 5):
    print(i)
```

``` title="Esecuzione"
1
2
3
4
```


``` py title="Esempio 3"
# si parte da 1, si avanza di 2 fino a 7 (non compreso)!!!
for i in range(1, 7, 2):
    print(i)
```

``` title="Esecuzione"
1
3
5
```


``` py title="Esempio 4"
# si parte da 9, si "avanza" di -2 (quindi si va indietro)
# ci si ferma prima di arrivare a 0
for i in range(9, 0, -2):
    print(i)
```

``` title="Esecuzione"
9
7
5
3
1
```


Altro esempio, con un po' di codice:


``` py title="Esempio 5"
for n in range(1,4):
    q = n**2
    print(q, "è il quadrato di", n)
```

``` title="Esecuzione"
1 è il quadrato di 1
4 è il quadrato di 2
9 è il quadrato di 3
```


Insomma, secondo me più o meno ci siamo. Dopo una trentina di esercizi,
ne sarete convinti anche voi :)


<!-- ###################################################################################################### -->

### Esercizi su for e range (NO IA)


Utilizzate il comando `for ... in range ( ... )` per la risoluzione dei seguenti esercizi:

<br>

------------------------------------------------------------------------------------------


**Esercizio 301**

Visualizzare i numeri da 0 a 19


------------------------------------------------------------------------------------------


**Esercizio 302**

Visualizzare i numeri da 1 a 20


------------------------------------------------------------------------------------------


**Esercizio 303**

Visualizzare i numeri dispari presenti fra 1 e 20


------------------------------------------------------------------------------------------


**Esercizio 304**

Visualizzare i numeri pari presenti fra 1 e 30


------------------------------------------------------------------------------------------


**Esercizio 305**

Visualizzare un countdown che parte da 10 e arriva a 0.


------------------------------------------------------------------------------------------


**Esercizio 306**

Visualizzare un countdown dei numeri pari che parte da 20 e arriva a 0.


------------------------------------------------------------------------------------------


**Esercizio 307**

Chiedere all'utente di inserire un numero intero positivo e visualizzare
un countdown che parte da quel numero fino a 0.


------------------------------------------------------------------------------------------


**Esercizio 308**

Visualizzare la tabellina del 5.


------------------------------------------------------------------------------------------


**Esercizio 309**

Chiedere all'utente un numero intero e visualizzare la tabellina di quel numero.


------------------------------------------------------------------------------------------


**Esercizio 310**

Visualizzare la tabellina del 7 alla rovescia (cioè partendo da 70 e andando indietro fino a 7)


------------------------------------------------------------------------------------------


**Esercizio 311**

Chiedere all'utente un numero intero e visualizzare la tabellina di quel numero alla rovescia.


------------------------------------------------------------------------------------------


**Esercizio 312**

Visualizzare i primi 20 numeri dispari


------------------------------------------------------------------------------------------


**Esercizio 313**

Chiedere all'utente un numero intero e visualizzare i 10 numeri pari
successivi a quel numero. Ad esempio, inserito 17, si dovranno
visualizzare 18, 20, 22, 24, 26, 28, 30, 32, 34, 36.


------------------------------------------------------------------------------------------


**Esercizio 314**

Visualizzare in colonna i numeri da 1 a 100 (i primi 100 numeri).


<!-- ###################################################################################################### -->

## Somma e Conta


Capita spesso (vedrete... capiterà!!!) di dover sommare una sequenza di
numeri oppure di dover contare una sequenza di informazioni in genere.

In questo caso il ciclo for appena studiato torna veramente utile. Si
tratta semplicemente di mettere insieme alcune conoscenze che già
abbiamo. Vediamo dunque i 2 casi (la *somma* e la *conta*) tramite
l'ausilio di 2 esempi


------------------------------------------------------------------------------------------

### Esempio con la somma

In questo esempio voglio fare **la somma dei numeri che vanno da 5 a 12**,
quindi sommare insieme 5, 6, 7, 8, 9, 10, 11, 12 e sapere quanto fa
(senza fare a mente!).

Se vuoi sommare delle quantità vorrai inserire il risultato in una
variabile. Mi sembra abbastanza ragionevole affermare che la variabile
che contiene la somma deve partire da ZERO!

``` python
somma = 0
```

La seconda considerazione da fare è sul ciclo for: se voglio sommare i
numeri fra 5 e 12 devo scrivere un ciclo che parte da 5 (start,
compreso) e avere come stop 13, in modo che si fermi a quello prima,
ovvero 12.


``` python
for s in range(5,13):
    # s va da 5 a 12:
    # la prima volta vale 5, la seconda 6, etc... l'ultima volta 12
```

Terza e ultima considerazione: se voglio sommare tutti questi numeri
devo "aggiungerli tutti" alla (variabile) somma. Man mano che il ciclo
for li scorre li aggiungo dunque ad essa:

``` python
...
somma = somma + s # si può scrivere in maniera compatta: somma += s
```

Questa istruzione aggiunge s al valore attuale di somma e assegna il
nuovo valore calcolato di nuovo alla variabile somma.

Mettendo insieme i 3 pezzi, che spero abbiate compreso, otteniamo:


``` py title="Somma numeri fra 5 e 12"
somma = 0

for s in range(5, 13):
    somma += s

print("la somma dei numeri fra 5 e 12 fa: ", somma)
```


Spero sia tutto chiaro! Come al solito comunque, fra un attimo arrivano gli esercizi ;)


------------------------------------------------------------------------------------------

### Esempio con la conta


In questo secondo esempio voglio **contare i numeri dispari fra 15 e 30**
ovvero sapere quanti sono i numeri 15, 17, 19, 21, 23, 25, 27, 29 (senza
contarli a mano!).

Anche qui ci servità una variabile per "contare" i numeri, che
ovviamente deve partire da ZERO!!


``` python
conta = 0
```

Per scorrere i dispari fra 15 e 30 devo scrivere un for molto semplice:
parte da 15, arriva a 30 e va avanti di 2!


``` python
for c in range(15, 30, 2):
    # In questo modo c varrà 15, 17, 19... fino a 29, il numero prima di 30!
```

Ultima cosa, ogni volta che scorro un numero devo contarlo, cioè aumentare la conta di 1, quindi:


``` python
conta += 1
```

Mettiamo insieme ancora una volta i tre pezzi del ragionamento e otteniamo:


``` py title="Conta dei numeri dispari fra 15 e 30"
conta = 0

for c in range(15, 30, 2):
    conta += 1

print("I numeri dispari fra 15 e 30 sono:", conta)
```


Sinceramente credo che analizzando un pochino gli esempi e ragionando un
po' anche questo concetto sia abbastanza chiaro! Ripeto... in questo
paragrafo niente di nuovo. Solo due tecniche molto comuni che abbiamo
analizzato insieme.

E adesso sotto con gli esercizi!


<!-- ###################################################################################################### -->

### Esercizi su somma e conta (NO IA)


**Esercizio 321**

Visualizzare la somma dei numeri da 1 a 100


------------------------------------------------------------------------------------------


**Esercizio 322**

Contare i numeri che vanno da 10 a 20. (dovrebbe fare 11...)


------------------------------------------------------------------------------------------


**Esercizio 323**

Dato un numero intero chiamato PAOLO, inserito dall'utente, visualizzare la somma dei
numeri da 1 a PAOLO (compreso)


------------------------------------------------------------------------------------------


**Esercizio 324**

Fare la somma di 10 numeri inseriti dall'utente.


------------------------------------------------------------------------------------------


**Esercizio 325**

Dati 2 numeri interi A e B inseriti dall'utente, contare i numeri pari
compresi fra questi, estremi inclusi.


------------------------------------------------------------------------------------------


**Esercizio 326**

Permettere all'utente di inserire 6 numeri interi. Alla fine
dell'inserimento dire quanti numeri dispari positivi sono stati
digitati.


------------------------------------------------------------------------------------------


**Esercizio 327**

Scrivere un ciclo che permetta all'utente di inserire 10 numeri interi.
Alla fine dell'inserimento visualizzare:

- la quantità di numeri pari inseriti
- la somma dei numeri dispari inseriti

Ad esempio, se l'utente inserisce in sequenza i numeri 1, 2, 3, 4, 5,
6, 7, 8, 9, 10 allora il programma dovrà rispondere:

    I numeri pari sono 5.
    La somma dei numeri dispari fa 25.

(infatti i numeri pari sono 2, 4, 6, 8, 10 ovvero 5 numeri. La somma dei
dispari inseriti è 1 + 3 + 5 + 7 + 9 = 25)


------------------------------------------------------------------------------------------


**Esercizio 328**

Chiedere all'utente di inserire due numeri interi da memorizzare nelle
variabili tot e valore.

Permettere all'utente di inserire tot numeri interi, contare quanti di
questi sono più grandi di valore e sommare tutti quelli positivi ma
minori o uguale a valore.

Visualizzare i risultati ottenuti.


<!-- ###################################################################################################### -->

## Istruzione while


L'istruzione while si abbina ad una condizione e ripete il suo blocco di
codice finché questa condizione rimane vera. Vediamo la struttura.


``` py title="Definizione ciclo while"
while condizione:
    # blocco di codice da ripetere se la condizione è vera
    # . . .

# altro codice
```

Vediamo un esempio per provare a chiarire il concetto:


``` python
a = 0
while a < 5:
    print(a)
    a = a + 2
```

``` title="Esecuzione"
0
2
4
```


Le istruzioni for e while permettono di implementare qualsiasi tipo di
iterazione in maniera semplice e lineare. Prendiamo prima un po'
confidenza con queste e poi vediamo casistiche leggermente più
articolate, in cui introdurre alcune istruzioni per modificare il
comportamento dei cicli.


<!-- ###################################################################################################### -->

### Esercizi su while (IA con logica)


**Esercizio 341**

Chiedere all'utente di inserire un numero intero fra 1 e 3. Far ripetere
l'inserimento finché non si è ottenuto il numero nell'intervallo
richiesto


------------------------------------------------------------------------------------------


**Esercizio 342**

Avendo un capitale iniziale C = 100 euro e sapendo che donandolo al
professore questi è in grado di farlo fruttare con un incremento del 15%
annuo, dopo quanti anni esso ha raggiunto o superato il doppio del
capitale iniziale?


------------------------------------------------------------------------------------------


**Esercizio 343**

Chiedere all'utente di inserire numeri interi finché la somma dei
numeri inseriti non superi 20.


------------------------------------------------------------------------------------------


**Esercizio 344**

Chiedere all'utente di inserire numeri interi finché la somma dei pari
inseriti non superi 50.


------------------------------------------------------------------------------------------


**Esercizio 345**

Chiedere all'utente di inserire numeri positivi e crescenti.
L'inserimento si interrompe quando non si inserisce più un numero
maggiore del precedente.


------------------------------------------------------------------------------------------


**Esercizio 346**

Chiedere all'utente di inserire una serie di numeri e terminare
l'inserimento quando l'utente digita lo zero. Visualizzare la somma dei
numeri positivi inseriti.


------------------------------------------------------------------------------------------


**Esercizio 347**

Chiedere all'utente di inserire una serie di numeri e terminare
l'inserimento quando l'utente ne digita due uguali consecutivi.
Visualizzare la quantità di numeri inseriti (l'ultimo doppio conta 1: ad
esempio inseriti 1 , 3 , 4 , 4 saranno stati inseriti 3 numeri).


------------------------------------------------------------------------------------------


**Esercizio 348**

La malattia più contagiosa che sia mai esistita (finora) è il morbillo.
Una persona con il morbillo in un'ora può contagiare fino a 18 persone.

Chiedere all'utente di inserire un numero intero che rappresenta la
quantità di persone di una popolazione, fingere che una persona fra
queste sia ammalata di morbillo e valutare dopo quanti giorni si supera
il 50% di diffusione della malattia (nel caso più grave, ovvero che ogni
ora si contagino 18 persone).


------------------------------------------------------------------------------------------


**Esercizio 349**

Al bar della scuola la pizza costa 1 euro, i panini 1,50 euro e le
brioches salate ripiene 1,80 euro. Mario prende tot euro alla settimana
(non superiore a 10 euro) e ogni giorno della settimana decide cosa
prendere, scalando i soldi dai suoi possedimenti. Verificare se alla
fine della settimana riesce comunque a prendere quello che gli va o è
costretto a fare economia.

Al termine della settimana visualizzare il credito residuo di Mario e se
per almeno un giorno è dovuto vivere in ristrettezze.


------------------------------------------------------------------------------------------


**Esercizio 350**

Decidere il nome di un pezzo e un prezzo iniziale (ad esempio:
"orologio antico", 50 euro) e procedere ad un'asta simulata in cui 2
persone (Anna e Marco) si sfidano alzando ogni volta il prezzo
dell'oggetto. L'asta si interrompe quando uno dei due inserisce un
prezzo minore o uguale al precedente.

Al termine dell'asta dire chi dei due ha acquistato il pezzo e a quale
prezzo.


------------------------------------------------------------------------------------------


**Esercizio 351**

Si supponga che l'andamento della popolazione di un'alga si sviluppi nel
seguente modo: un anno raddoppia l'anno successivo cala di un quarto
(sempre numeri interi, mi raccomando).

Creare un programma che dato un valore iniziale della popolazione
(maggiore di 1) e un valore da raggiungere (maggiore del valore
iniziale) dica quanti anni ci mette quella popolazione a raggiungere o
superare quel valore.


<!-- ###################################################################################################### -->
## Istruzioni per i cicli


Per ognuna delle istruzioni seguenti, vedremo una semplice descrizione
ed un esempio esplicativo prima di "tuffarci" nella moltitudine di
esercizi che fortificheranno la nostra consapevolezza nell'utilizzo
delle stesse. Un unico commento per chiarire la questione: **ognuna di
queste istruzioni funziona indifferentemente con i cicli for o i cicli
while**.

Provare per credere!


<!-- ###################################################################################################### -->
### Istruzione break


L'istruzione `break` provoca un'interruzione del ciclo e un salto
immediato alla prima istruzione seguente. Esempio illuminante


``` python
indovina = 8
print ("Ho pensato un numero fra 1 e 10. Prova a indovinarlo")

while True:
    tentativo = int(input("Che numero è?"))
    if tentativo == indovina:
        print("Incredibile! Hai indovinato!!!")
        break # finito! Esci dal ciclo!
    else:
        print("No, mi spiace! Riprova...")

print("\nok, adesso andiamo avanti")
```

``` title="Esecuzione"
Ho pensato un numero fra 1 e 10. Prova a indovinarlo
Che numero è? 6
No, mi spiace! Riprova...
Che numero è? 7
No, mi spiace! Riprova...
Che numero è? 8
Incredibile! Hai indovinato!!!
ok, adesso andiamo avanti
```

Mi sembra sia semplice da capire e facile da usare. Andiamo avanti.


<!-- ###################################################################################################### -->
### Istruzione continue


L'istruzione continue interrompe l'esecuzione del blocco di codice da
ripetere e salta immediatamente alla prossima iterazione, ricominciando
il blocco iterativo.


``` python
for n in range(1, 8):
    if n % 3 == 0:
        continue # ricomincia il ciclo dalla prossima iterazione
    print ("Numero: ", n)
```

``` title="Esecuzione"
Numero: 1
Numero: 2
Numero: 4
Numero: 5
Numero: 7
```


Anche qui, facile da capire e da utilizzare. Magari è una istruzione che
capiterà di usare poche volte, ma di sicuro non sarà un grande problema
utilizzarla.


<!-- ###################################################################################################### -->

### Istruzione else nei cicli


Una delle caratteristiche peculiari di Python, che lo differenziano
dagli altri linguaggi, è questa cosa di poter utilizzare la clausola
else nei cicli. Il codice nel campo else viene eseguito in due casi
specifici:

1. Abbinato ad un ciclo for, quando la sequenza da scorrere termina.
2. Abbinato ad un ciclo while, quando la condizione diventa False

Vediamo un **esempio con il ciclo for**:


``` py title="Verifica se un numero è primo o no"
numero = int( input("Inserisci numero. Io ti dico se è primo o no: ") )

for divisore in range(2, numero):
    if numero % divisore == 0:
        print (numero,"non è primo, infatti")
        print (numero, " = ", divisore, " * ", numero//divisore )
        break
else: # Indentazione! else è incolonnato al for NON all'if!!!
    print(numero, "è primo")
```

``` title="Prima esecuzione, inserisco 15"
Inserisci numero. Io ti dico se è primo o no: 15
15 non è primo, infatti 
15 = 3 * 5
```

``` title="Seconda esecuzione, inserisco 17"
Inserisci numero. Io ti dico se è primo o no: 17
17 è primo
```


Praticamente il secondo ciclo for, basato sulla variabile i, cerca eventuali divisori del numero. 
Se scorrendo tutti i numeri fra 2 e (numero - 1) non ne trova, allora è un numero primo! Se invece trova
anche un solo divisore, lo visualizza e interrompe il ciclo con il break, rendendo nullo l'else.

Ecco un esempio analogo che utilizza **la clausola else abbinata all'istruzione while**.


``` py title="sette e mezzo"
valoreCarte = 0.0

while valoreCarte <= 7.5:
    # controllo quanto ho e decido se andare avanti o no
    print("In mano hai", valoreCarte)
    risp = input("Vuoi una carta? (s/n)")
    if risp != "s":
        break
    
    # aggiungo la nuova carta
    x = float( input("Dammi una carta: ") )
    valoreCarte += x

else: # Indentazione! else è incolonnato a while NON all'if!!!
    print("Hai sballato, accidenti!!!")

print("In mano hai", valoreCarte)
```

``` title="Prima esecuzione, vado sempre avanti"
In mano hai: 0.0
Vuoi una carta? (s/n) s
Dammi una carta: 5
In mano hai: 5.0
Vuoi una carta? (s/n) s
Dammi una carta: 3
Hai sballato, accidenti!!!
In mano hai 8.0
```

``` title="Seconda esecuzione, mi fermo dopo la prima carta"
In mano hai: 0.0
Vuoi una carta? (s/n) s
Dammi una carta: 6
In mano hai: 6.0
Vuoi una carta? (s/n) n
In mano hai 6.0
```

Spero sia abbastanza chiaro. In generale ci sono altri modi per ovviare
all'utilizzo di questi `for-else` o `while-else`, semplicemente con un
paio di righe di codice in più. Di certo però queste istruzioni sono
molto *pythonic* :)

A voi la scelta per come e quando utilizzarle!


<!-- ###################################################################################################### -->

## Controllo dei valori inseriti


Capita spesso e volentieri di voler controllare il valore che l'utente
inserisce per essere sicuri non solo del tipo, ma anche del "range"
del valore inserito: un numero intero fra 10 e 20, un reale diverso da
0, un carattere maiuscolo, etc...

In questi casi è possibile utilizzare il ciclo while e l'istruzione
break appena studiata, abbinate ad un minimo di ingegno per far
funzionare la cosa.

Facciamo una prova.


``` py title="Esercizio: inserimento di un numero intero fra 1 e 90 (per la tombola)"
# ciclo con condizione sempre vera. Ripete all'infinito
while True:
    # nell'input dobbiamo suggerire all'utente cosa fare...*
    num = int(input("Inserisci un numero fra 1 e 90: "))

    # controllo con interruzione
    if num >= 1 and num <= 90:
        break

# visualizzazione finale
print("Numero inserito:", num)
```

Capito vero? Verifichiamolo con qualche esercizio :)


<!-- ###################################################################################################### -->

### Esercizi sul controllo valori (NO IA)


**Esercizio 361**

Chiedere all'utente di inserire un numero intero fra 1 e 10. Ripetere
l'inserimento finché la condizione non viene soddisfatta. Alla fine,
visualizzare il numero inserito.


------------------------------------------------------------------------------------------


**Esercizio 362**

Chiedere all'utente di inserire un numero intero pari fra 0 e 100.
Ripetere l'inserimento finché la condizione non viene soddisfatta. Alla
fine, visualizzare il numero inserito.


------------------------------------------------------------------------------------------


**Esercizio 363**

Chiedere all'utente di inserire un numero reale negativo. Ripetere
l'inserimento finché la condizione non viene soddisfatta. Alla fine,
visualizzare il numero inserito.


------------------------------------------------------------------------------------------


**Esercizio 364**

Chiedere all'utente di inserire un carattere, fra le maiuscole 'A',
'B', 'C'. Ripetere l'inserimento finché la condizione non viene
soddisfatta. Alla fine, visualizzare il carattere inserito.


------------------------------------------------------------------------------------------


**Esercizio 365: caratteri minuscoli**

Chiedere all'utente di inserire un carattere minuscolo. Ripetere
l'inserimento finché la condizione non viene soddisfatta. Alla fine,
visualizzare il carattere inserito.


------------------------------------------------------------------------------------------


**Esercizio 366**

Chiedere all'utente di inserire 2 numeri reali, di cui il secondo non
nullo (da verificare). Infine visualizzare il rapporto (il risultato
della divisione) fra questi.


------------------------------------------------------------------------------------------


**Esercizio 367**

Predisporre un programma che permetta all'utente di inserire numeri
interi e che si interrompa solo quando l'utente inserisce ZERO. Alla
fine dell'inserimento visualizzare la somma e la media dei valori
inseriti.


------------------------------------------------------------------------------------------


**Esercizio 368: interi, stringhe e congiunzioni (di stringhe)**

Chiedere all'utente di inserire caratteri minuscoli, finché non
inserisce il carattere '!' per terminare. Alla fine si visualizzi
tutti i caratteri inseriti, in una sola riga, separati da spazi.

!!! tip "Suggerimento"

    Create una stringa congiungendo il carattere inserito e uno spazio...


------------------------------------------------------------------------------------------


**Esercizio 369**

Visualizzare la domanda "Hai capito?" e continuare a ripeterla finché
l'utente non dice "sì" (con l'accento sulla ì, mi raccomando...)


<!-- ###################################################################################################### -->
## Esercizio "ragionato" svolto


Questo esercizio è stato pensato perché arrivati a questo punto, in cui
conosciamo tutte le istruzioni base del linguaggio, dobbiamo migliorare
nella nostra capacità di risolvere gli esercizi. Dobbiamo trovare una
strategia che ci permetta di affrontare ogni tipo di esercizio, anche
molto difficile, con la speranza di riuscire a risolverlo.

A questo proposito ho cercato di dividere la mia soluzione in step ben
definiti che dovete assolutamente provare a riprodurre ogni volta che
affrontate un problema un pochino più articolato, come quelli che
inizieranno a capitare da adesso in poi.


------------------------------------------------------------------------------------------
<br>
**STEP 0: lettura del testo dell'esercizio**
<br>

Cominciamo leggendo ***attentamente*** il testo dell'esercizio:

> Dato un numero intero positivo N da parte dell'utente, dire se esso è
> primo oppure no.

Invece di provare a buttare giù codice nella speranza che l'esercizio
"si risolva magicamente", proviamo ad applicare un metodo
"scientifico" per trovare una soluzione.


------------------------------------------------------------------------------------------
<br>
**STEP 1: organizzazione delle conoscenze sul contesto**
<br>

Cosa significa questa cosa? Significa cercare di fare mente locale su
tutto quello che si sa sugli argomenti relativi all'esercizio,
conoscenze che possono aiutarci a risolverlo!!!

Dedicate 5 minuti almeno a questa fase!!!

Iniziamo insieme a ragionarci su, anche rileggendo il testo
dell'esercizio.

La prima cosa da notare è che l'esercizio si divide in 2 parti:

1. Chiedere all'utente di inserire un numero intero positivo N
2. Dire se N è primo oppure no

Mi immagino che siamo tutti sereni con la prima parte che si svolge come
spiegato nel capitolo sul "Controllo dei valori inseriti": ridateci un
occhio se ci sono problemi su questa parte. Scrivo il codice necessario:


``` python
while True:
    N = int(input("Inserisci un numero intero positivo: "))
    if N > 0:
        break
```

La seconda parte è quella più difficoltosa: come si capisce se un numero
è primo? Come si calcola? Cos'è un numero primo???

> Un numero naturale maggiore di 1 si definisce primo se è divisible
> solamente per 1 e per se stesso.<br>
> (Wikipedia, cit.)


Mi sembra che cosa sia un numero primo si sappia... ma per investigare
bene il problema non ci si può esimere dal prossimo step!!!


------------------------------------------------------------------------------------------
<br>
**STEP 2: esempi su valori possibili per l'esercizio**
<br>


Partiamo scrivendo su carta alcuni esempi che possono aiutarci a
riflettere:

- 7 è primo perché è divisibile solo per 1 e per 7. Infatti, nessuno dei numeri fra 2 e 6 divide 7.
- 18 non è primo perché è divisibile per 2, per 3, per 6, per 9...
- 11 è primo perché è divisibile solo per 1 e per 11. Nessun altro numero divide 11
- 25 non è primo perché è divisibile (anche) per 5, oltre ché per 1 e per 25 stesso.


------------------------------------------------------------------------------------------
<br>
**STEP 3: considerazioni desunte dagli esempi**
<br>


Per fare queste considerazioni, più esempi fate prima e meglio è...
Dagli esempi precedenti ho capito che:

- tutti i numeri (primi o no) sono divisibili per 1
- tutti i numeri (primi o no) sono divisibili per se stessi
- Se N è primo, nessun numero fra 2 e N-1 lo divide
- Dato N, se almeno un numero fra 2 e N-1 divide N, allora N non è primo.

Siete d'accordo? Queste considerazioni le ho fatte guardando gli esempi
che mi sono fatto! Fatene anche voi e provate a vedere se quello che ho
scritto vi convince e se vi vengono in mente altre idee.


------------------------------------------------------------------------------------------
<br>
**STEP 4: formulazione di una strategia risolutiva**
<br>


Da questi primi esempi comincio a formulare una ***strategia.***

Dato N:

- scorro tutti i numeri fra 2 e N-1
- vedo se qualcuno di questi divide N
- Se anche uno solo divide N, N non è primo!
- Se nessuno di questi divide N, allora N è primo!

La cosa più semplice da fare mi sembra ***contare*** quanti numeri fra 2
e N-1 dividono N. Se la conta porta ZERO, allora N è primo,
altrimenti NO!

A questo punto ho un altro problema: come contare i divisori di N? Ho
capito che i divisori di N sono tutti i numeri positivi minori di N e
che 1 e N stessi vanno esclusi, perché non sono divisori interessanti.

Provo a organizzare le cose da fare in questo modo:

**Passaggio 1**<br>
Dato N, visualizzo tutti i numeri fra 2 e N - 1

**Passaggio 2**<br>
Dato N, visualizzo quali numeri fra 2 e N - 1 dividono N

**Passaggio 3**<br>
Dato N, conto quanti numeri fra 2 e N -- 1 dividono N

**Passaggio 4 (finale)**<br>
Dato N, faccio lo step 3 e poi guardo il risultato: se la conta è ZERO,
N è primo, altrimenti no.

Attenzione adesso... siete riusciti a figurarvi i passaggi descritti
sopra?!?! Bene! Allora sappiate 2 cose:

1. arrivati qui avete già praticamente risolto l'esercizio
2. la descrizione dei passaggi rappresenta esattamente i commenti che
   servono nel codice!

Capito il concetto?! I commenti che il prof tanto agogna scriviate nelle
vostre risoluzioni sono esattamente questi, ovvero ***i passaggi che
intendete fare per risolvere un quesito***. Come poi li farete, ovvero
con quale codice (un if, un if-else, un for oppure uno while) è
secondario rispetto a questo!


------------------------------------------------------------------------------------------
<br>
**STEP 5: prima stesura del codice**
<br>


Provo a scrivere il codice:

``` py title="Passaggio 1"
# Dato N, visualizzo tutti i numeri fra 2 e N - 1
for div in range(2, N -- 1):
    print (div)
```


``` py title="Passaggio 2"
# Dato N, visualizzo quali numeri fra 2 e N - 1 dividono N
for div in range(2, N -- 1):
    if N % div == 0:
        print (div)
```


``` py title="Passaggio 3"
# Dato N, conto quanti numeri fra 2 e N - 1 dividono N
conta = 0
for div in range(2, N -- 1):
    if N % div == 0:
        conta += 1
```


``` py title="Passaggio 4 (finale)"
# Dato N, faccio lo step 3 e poi guardo il risultato
# se la conta è ZERO, N è primo, altrimenti no.
# . . .

if conta == 0:
    print(N, "è primo")
else:
    print(N, "non è primo")
```

------------------------------------------------------------------------------------------
<br>
**STEP 6: stesura finale del codice**
<br>

Fatto questo, mi basta rimettere insieme tutto il ragionamento e il gioco è fatto!


``` python
# inserimento controllato valore utente
while True:
    N = int(input("Inserisci un numero intero positivo: "))
    if N > 0:
        break

# conta dei divisori "propri" di N
conta = 0

for div in range(2, N - 1):
    if N % div == 0:
        conta += 1

# controllo numero dei divisori propri
if conta == 0:
    print(N, "è primo")
else:
    print(N, "non è primo")
```

------------------------------------------------------------------------------------------
<br>
**STEP 7: test del codice scritto**
<br>


Arrivati a scrivere tutto, non è mica finito!!! Il codice scritto va
testato e controllato! Io direi che sono necessarie almeno 4 esecuzioni
con valori diversi per verificarlo. Se tutto funziona, avete finito. Se
ci sono problemi, bisogna analizzare a ritroso tutti gli step, a costo
di ripartire dallo step 0!!!

In effetti un piccolo errore in questo codice c'è... infatti, facendo
alcune prove, ci si accorge che questo codice riconosce il numero 1 (e tecnicamente... anche tutti i negativi) come
primo, mentre wikipedia (vedi sopra) ci dice che non lo è...

Provate a correggere voi il codice...

Rifate i test per verificare che adesso sia tutto a posto...

Finito!

Spero che abbiate capito il ragionamento svolto e (soprattutto) come
esso si sia sviluppato ragionando a partire dal ***testo del quesito***
e da alcuni ***esempi reali*** che mi sono fatto coi numeri.

Spero di avervi aiutato un po'... Ecco una serie di esercizi in cui
mettervi alla prova!!!


<!-- ###################################################################################################### -->
## Esercizi finali sui cicli (IA con logica)


Gli esercizi elencati qua di seguito non sono semplici applicazioni dei
concetti studiati finora, ma sono i primi esercizi che richiedono una
buona dose di ragionamento e di preparazione per "progettare" la
soluzione dell'esercizio.


------------------------------------------------------------------------------------------


**Esercizio 381**

Acquisire un numero positivo N e calcolarne la radice quadrata intera
(ovvero il massimo intero x tale che x al quadrato sia minore o uguale a
N).


------------------------------------------------------------------------------------------


**Esercizio 382**

Acquisire una sequenza di numeri interi e calcolare la somma di quelli
positivi. Il programma deve terminare non appena l'utente inserisce per
due volte consecutive un valore negativo.


------------------------------------------------------------------------------------------


**Esercizio 383**

Scrivere un programma che acquisisca da tastiera un numero intero
assicurandosi che sia positivo e, successivamente, stampi a video i 5
anni bisestili strettamente superiori al numero acquisito.


------------------------------------------------------------------------------------------


**Esercizio 384**

Visualizzare la Tavola Pitagorica.


------------------------------------------------------------------------------------------


**Esercizio 385: numeri perfetti**

Un numero intero si dice perfetto se risulta uguale alla somma dei suoi
divisori (minori del numero stesso). Ad esempio 6 = 1 + 2 + 3, che sono
i suoi divisori, è un numero perfetto.

Dato un numero intero positivo C, da parte dell'utente, verificare se è
perfetto.


------------------------------------------------------------------------------------------


**Esercizio 386**

Dato un numero F, inserito dall'utente e compreso fra 0 e 12
(verificare), visualizzare il fattoriale di F.


!!! note "Il Fattoriale"

    Il *fattoriale* di un numero intero positivo F si indica con ! ed è
    definito come il prodotto di tutti i numeri da 1 a F. Ad esempio:

    ```
    6! = 1 * 2 * 3 * 4 * 5 * 6 = 720
    ```
    
    Per definizione inoltre abbiamo:

    ```
    0! = 1
    n! = ( n - 1 ) ! * n
    ```

------------------------------------------------------------------------------------------


**Esercizio 387: cornice rettangolare**

Visualizzazione di un rettangolo con cornice "+" e interno "=" di
misure A e B, decise dall'utente


------------------------------------------------------------------------------------------


**Esercizio 388: rettangolo**

Programma che disegna un rettangolo di caratteri di BASE e ALTEZZA
scelti dall'utente. Il rettangolo è formato da un carattere a scelta
come cornice e da un carattere a scelta all'interno.


------------------------------------------------------------------------------------------


**Esercizio 389: MCM**

Inseriti 2 numeri interi positivi (verificare) da parte dell'utente,
calcolare il minimo comune multiplo fra di essi.


------------------------------------------------------------------------------------------


**Esercizio 390: MCD**

Inseriti 2 numeri interi positivi (verificare) da parte dell'utente,
calcolare il Massimo Comun Divisore fra di essi.


------------------------------------------------------------------------------------------


**Esercizio 391: Quadrato Perfetto**

Un quadrato perfetto è un numero della sequenza 1, 4, 9, 16, 25...
ovverosia un numero qualsiasi creato come prodotto per se stesso di un
qualunque numero intero positivo.

Dati dall'utente 2 numeri A, B positivi (da verificare) e tali che A sia
minore o uguale a B, visualizzare il numero di quadrati perfetti
presenti nella sequenza dei numeri [A, B].

Ad esempio, dati A = 6, B = 16, la risposta è 2 perché fra 6 e 16 sono
presenti i quadrati perfetti 9 e 16 stesso.

Dati A = 4 e B = 5, la risposta è 1 perché fra 4 e 5 è presente un solo
quadrato perfetto, cioè 4.


------------------------------------------------------------------------------------------


**Esercizio 392**

Scrivere un programma che riceva in ingresso un numero positivo N e
determini il massimo intero K tale che la somma dei primi K interi sia
minore o uguale a N. Ad esempio, se N=20 allora K risulta 5, infatti

    1 + 2 + 3 + 4 + 5 = 15

mentre

    1 + 2 + 3 + 4 + 5 + 6 = 21


------------------------------------------------------------------------------------------


**Esercizio 393: Fibonacci**

!!! note "La successione di Fibonacci"

    È una sequenza numerica tale che:
    
    - il primo numero è 0
    - il secondo numero è 1
    - il numero successivo si ottiene come somma dei due precedenti
    
    Iterando questo procedimento si ottiene la sequenza 0, 1, 1, 2, 3, 5, 8, 13, 21 ... nota come **Successione di Fibonacci**.


Dato un numero intero N da parte dell'utente (verificare che sia
positivo), visualizzare la successione di Fibonacci da 0 fino
all'ennesimo numero.

Ad esempio, dato N = 8, va visualizzata la successione: 0 , 1 , 1 , 2 , 3 , 5 , 8 , 13.


------------------------------------------------------------------------------------------


**Esercizio 394**

Dopo aver fatto inserire un numero intero positivo dire da quante cifre
è composto il numero. Ad esempio 12345 è composto da 5 cifre.

<br>
<br>
<br>

