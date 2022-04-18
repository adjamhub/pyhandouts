# Funzioni

!!! warning

    Questa parte della documentazione non è ancora pronta.

    Usa la documentazione in PDF reperibile
    [qui](https://www.adjam.org/next/index.php/s/egW7AnHxcif8n27?path=%2FPYTHON)



# Funzioni in Python

Il termine \"*funzione*\" viene utilizzato in programmazione con un
significato analogo a quello della matematica: una funzione è una
procedura che può ricevere valori come argomenti e restituire un
***unico*** valore come risultato. Nel linguaggio comune si dice anche
che una funzione ***ritorna*** un valore.

La sintassi generale per le funzioni in Python è così strutturata:

def nome_funzione ( parametri ) :

\# blocco di codice che implementa la funzione

\# codice...

\# la funzione ritorna un valore con l'istruzione return

Come al solito, cominciamo con un semplice esempio per capire il
funzionamento:

def isPositive ( number ) :

if number \> 0 :

return True

return False

numero = float(input(\"Inserisci un numero: \"))

if isPositive(numero):

print(\"Hai inserito un numero positivo\")

Alcune considerazioni banali:

-   la funzione si chiama \"isPositive\"
-   la dichiarazione della funzione inizia con la clausola def
-   eventuali parametri della funzione vanno fra parentesi tonde
-   PRIMA la funzione si dichiara (una volta), POI si può usare (quante
    volte ti pare)

Altro esempio banale:

def somma (a , b) :

return a + b

print(\"27 + 35 = \" , somma(27,35) )

print(\"12 + 5 = \" , somma(12,5) )

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
\"divertiamoci\" con una valanga di esercizi da svolgere!!!

## Parametri delle funzioni

I parametri di una funzione sono quelle variabili indicate tra parentesi
nella sua dichiarazione e che prendono i valori che vengono inseriti in
essa al momento della sua chiamata.

Capisco lo sconcerto... riprovo con un esempio:

\# la variabile \"nome\" è il parametro della funzione saluta()

def saluta (nome):

return \"ciao \" + nome

Quando poi la funzione viene chiamata i parametri prendono dei valori:

\# il valore \"ciccio\" sarà inserito nel parametro \"nome\"

\# della funzione \"saluta()\"

print( saluta(\"ciccio\") )

ciao ciccio

Se la funzione prende più di un parametro, Python fornisce 2
possibilità:

1.  **l'inserimento ordinato** dei valori
2.  **l'inserimento nominale** dei valori

Partiamo come al solito definendo una funzione di prova e verificando
cosa succede:

\# la funzione ritorna parola ripetuta per un certo numero di volte

\# (con uno spazio di separazione in mezzo, ma non alla fine):

\# ripeti(\"ciao\", 3) ritorna \"ciao ciao ciao\"

def ripeti(parola, numero):

res = (parola + \" \" ) \* (numero - 1) + parola

return res

Nella chiamata con inserimento ordinato dei valori basta inserire i dati
nell'ordine della definizione: prima la parola e poi il numero:

*print( *ripeti (\"ciao\", 4) ) \# scrive \"ciao ciao ciao ciao\"

mentre se si inseriscono i dati nell'ordine errato si va incontro ad un
errore:

*print( *ripeti (3, \"ciao\") ) \# ***ERRORE***

Se lo si desidera è anche possibile procedere ad un **inserimento
nominale**, indicando cioè il nome della variabile in cui inserire il
valore: in questo caso, l'ordine di inserimento non conta.

*print( *ripeti (parola = \"ciao\" , numero = 3) ) \# ciao ciao ciao

print( ripeti (numero = 3 , parola = \"ciao\") ) \# ciao ciao ciao

È inoltre possibile passare alle funzioni alcuni **valori di default**:
questi vengono utilizzati se la funzione viene chiamata senza i valori
da passare ai parametri o ignorati in presenza di essi.

\# definizione della funzione \"saluta\" con valore di default
\"ciccio\"

\# per il parametro nome

def saluta(nome = \"ciccio\"):

return \"ciao \" + nome

Allora è possibile scrivere in fase di chiamata:

saluta() \# ritorna la stringa \"ciao ciccio\"

saluta(\"pippo\") \# ritorna la stringa \"ciao pippo\"

Spero sia chiaro, a me perlomeno sembra così.

## Esercizi sulle funzioni

Esercizio 501

Scrivere una funzione che calcola l\'area di un rettangolo e una che ne
calcola il perimetro, date la base e l\'altezza.

Esercizio 502

Scrivere una funzione che calcola l\'area di un cerchio e una che
calcola la sua circonferenza. Entrambe richiedono (ovviamente) come
parametro il raggio del cerchio.

Esercizio 503: triangoli rettangoli

Scrivere 3 funzioni relative ai triangoli rettangoli. Tutte e tre
prendono come parametri la lunghezza reale dei cateti e calcolano
rispettivamente:

• l'ipotenusa

• l'area

• il perimetro.

Utilizzare la funzione \"ipotenusa\" all'interno della funzione
\"perimetro\".

Esercizio 504: potenze

Dati un parametro per la base e uno (intero) per l'esponente,
implementare la funzione potenza. Attenzione ai valori negativi degli
esponenti.

(Per implementare questa funzione **non** potete usare la sintassi
Python base\*\*esp, ma dovete "scrivere" i calcoli da fare)

Esercizio 505: MCD

Scrivere una funzione che, dati due numeri interi positivi come
parametri, ritorna il Massimo Comun Divisore fra questi.

**Esercizio 506: mcm**

Scrivere una funzione che, dati due numeri interi positivi come
parametri, ritorna il minimo comune multiplo fra questi.

**Esercizio 507: carattere**

Scrivere una funzione che, dato un carattere, ritorna la stringa
\"vocale\", \"consonante\", \"cifra\" o \"alfanumerico\" a seconda del
carattere passato.

**Esercizio 508: inverti stringa**

Scrivere una funzione che, data una stringa, ritorna la stringa
rovesciata. Ad esempio fornito \"ciao\" come parametro, la funzione
ritorna la stringa \"oaic\".

**Esercizio 509: palindroma**

Scrivere una funzione che, data una stringa, dice se è palindroma oppure
no. Una stringa palindroma (ad esempio: \"anna\") si legge uguale in
entrambi i versi. Ritornare True o False a seconda che la stringa sia
palindroma oppure no.

**Esercizio 510: farfallese**

Scrivere una funzione che, data una stringa, ritorna la stringa
convertita in farfallese. In farfallese ogni vocale viene seguita da una
f + la vocale ripetuta. Ad esempio la stringa \"ciao\" in farfallese
diventa \"cifiafaofo\".

# Moduli Python

Tutte le variabili e le funzioni che si possono definire nell'interprete
Python vengono ovviamente perse alla sua chiusura. Per evitare ciò ed
eseguire i nostri programmi Python ogni volta che lo vogliamo,
utilizziamo gli script: proviamo con l'interprete il codice che
scriviamo e alla fine lo salviamo in uno script in modo tale che una
intera procedura possa essere ripetuta in un attimo, senza dove scrivere
(di nuovo) una riga di codice.

Se, andando avanti, scriveremo programmi più complicati, ci renderemo
conto che è possibile dividere in più file il codice, organizzarlo in
funzioni e utilizzarne alcune parti magari per altri programmi simili.

Per supportare questa idea divina, Python ha un modo per inserire le
definizioni in un file e usarle in uno script o in un\'istanza
interattiva dell\'interprete, semplicemente richiamandolo. Tale concetto
viene chiamato ***modulo***; le definizioni da un modulo possono essere
importate in altri moduli o nello script principale, il \"programma\".

Un modulo è un file contenente definizioni e definizioni Python. Il nome
del file è il nome del modulo con il suffisso .py aggiunto. Ad esempio,
dato il file \"pippo.py\" esso produrrà un modulo chiamato \"pippo\".
Semplice :)

Per capire meglio il concetto, facciamo una prova! Immaginiamo di voler
costruire un modulo che contenga alcune delle funzioni che abbiamo
scritto precedentemente e che riteniamo utili, ad esempio, la funzione
***isPrime(num****ber****)*** che verifica se *number* è un numero primo
oppure no e le funzioni ***unit(num****ber****)***,
***dec(num****ber****)*** e ***cent(num****ber****)*** che, dato un
numero, restituiscono rispettivamente unità, decine e centinaia dello
stesso.

Il modulo si chiamerà \"provaModulo\", quindi creiamo un file chiamato
\"provaModulo.py\" e scriviamoci dentro le implementazioni delle
funzioni elencate sopra.

\# File \"p*rovaModulo*.py\"

def isPrime(number):

if number \<= 1:

return False

for i in range(2, number - 1):

if number % i == 0:

return False

return True

def unit(number):

\# vai avanti\...

Fatto questo, nel nostro programma potremo accedere al modulo
\"provaModulo\" e alle funzioni e variabili in lui definite utilizzando
il seguente codice:

\# File \"*testProvaModulo*.py\"

\# questo unico comando permette di \"importare\" nel nostro programma

\# il modulo \"provaModulo\" appena creato

import p*rovaModulo*

n = int( input(\"Inserisci un numero intero. Io ti dirò se è primo: \")
)

\# per accedere alle funzioni definite nel modulo p*rova*,

\# dobbiamo utilizzare la notazione puntata

if provaModulo.isPrime(n):

print(\"primo\")

else

print(\"NON primo\")

Tutto qua! Spero sia chiaro :)

## Esercizio svolto sui moduli

Implementare un modulo, chiamato \"ControlloInteri\" contenente le
funzioni per verificare se un numero intero è positivo, se è pari, se è
primo. Testare il risultato in un file esterno.

Soluzione

Per implementare un modulo con alcune funzioni dentro che possa essere
riutilizzato ogni volta si voglia, dato il nome del modulo (es:
ControlloInteri), basterà creare il file \"ControlloInteri.py\".

\# File \"ControlloInteri.py\"

\# restituisce True se il numero è positivo, False altrimenti

def positivo ( num ):

if num \> 0:

return True

return False

\# restituisce True se il numero è pari, False altrimenti

def pari ( num ):

if num % 2 == 0:

return True

return False

\# restituisce True se il numero è primo, False altrimenti

def primo ( num ):

for n in range(2, num):

if num % n == 0:

return False

return True

Fatto questo, il \"modulo\" ControlloInteri è pronto per essere
utilizzato :)

Ci basta creare un nuovo file nella stessa cartella e provare ad usarlo.

\# File \"*testControlloInteri*.py\"

\# serve per richiamare l'utilizzo del modulo \"ControlloInteri\"

import ControlloInteri

n = int ( input(\"Inserisci intero: \") )

\# ogni volta che ci serve una funzione del modulo, dobbiamo

\# scrivere Modulo.Funzione( parametri )

if ControlloInteri.positivo(n):

print(\"positivo\")

else:

print(\"non positivo\")

if ControlloInteri.pari(n):

print(\"pari\")

else:

print(\"dispari\")

if ControlloInteri.primo(n):

print(\"primo\")

else:

print(\"non primo\")

Tutto qua!

E adesso gli esercizi ;)

## Esercizi sui moduli Python

Per ognuno degli esercizi qui sotto proposti occorre implementare il
modulo citato accanto al numero dell'esercizio, implementare al suo
interno le funzioni elencate e predisporre un file chiamato
\"testNomeModulo.py\" che importa lo stesso e propone almeno 3 test con
valori diversi per ognuna delle funzioni implementate nel modulo.

Esempio: modulo \"esempio\"

Raddoppia

la funzione prende un numero intero e restituisce il suo doppio.

Dimezza

la funzione prende un numero intero e restituisce la sua metà.

+----------------------+--------------------------------------------------+
| \# File *esempio*.py | \# File \"testEsempio.py\"                       |
|                      |                                                  |
| def raddoppia(num):  | import *esempio*                                 |
|                      |                                                  |
| d = num \* 2         | a = 3                                            |
|                      |                                                  |
| return d             | print(\"a = \", a)                               |
|                      |                                                  |
| def dimezza(num):    | print(\"raddoppia = \", *esempio*.raddoppia(a) ) |
|                      |                                                  |
| d = num / 2          | print(\"dimezza = \", *esempio*.dimezza(a) )     |
|                      |                                                  |
| return d             | . . . (altri 2 esempi) . . .                     |
+----------------------+--------------------------------------------------+

**Esercizio 521: modulo \"SequenzeNumeriche\"**

Minori di un elemento

Creare una funzione che, data una sequenza numerica (tupla o lista) e un
numero qualsiasi, conta quanti numeri nella sequenza sono minori del
numero.

Somma degli elementi

Creare una funzione che, data una sequenza numerica (tupla o lista),
restituisce la somma dei numeri della sequenza.

Media degli elementi

Creare una funzione che, data una sequenza numerica (tupla o lista),
restituisce la media aritmetica dei numeri della sequenza.

Esercizio 522: modulo \"ManipolazioneStringhe\"

LunghezzaStringa

La funzione prende una stringa come parametro e ritorna il numero di
caratteri di cui è composta (la sua lunghezza)

ContaLettera

La funzione prende una stringa e una lettera come parametro e ritorna il
numero di volte in cui la lettera è presente all\'interno della stringa

TutteMaiuscole

La funzione prende una stringa come parametro e ritorna la stringa
trasformata in maiuscolo

TutteMinuscole

La funzione prende una stringa come parametro e ritorna la stringa
trasformata in minuscolo

InvertiMaiuscoleMinuscole

La funzione prende una stringa come parametro e ritorna la stringa con
maiuscole e minuscole invertite.

InizialiMaiuscole

La funzione prende una stringa come parametro e ritorna la stringa
trasformata in minuscolo con le iniziali di ogni parola maiuscole

Esercizio 523: modulo \"PianoCartesiano\"

quadrante

La funzione prende due numeri x, y che rappresentano le coordinate del
punto P nel piano cartesiano e restituisce un numero corrispondente al
quadrante nel quale esso si trova, ovvero un numero fra 1 e 4.
Restituisce 0 nel caso che il punto sia su uno degli assi cartesiani.

Distanza dall'origine

La funzione prende due numeri x, y che rappresentano le coordinate del
punto P nel piano cartesiano e restituisce la distanza del punto P
dall'origine degli assi, ovvero dal punto O di coordinate (0,0).

Distanza fra due punti

La funzione prende quattro numeri xP, yP, xQ, yQ che rappresentano le
coordinate dei punto P e Q nel piano cartesiano e restituisce la
distanza fra loro.

Esercizio 524: modulo \"CifreNumeriche\"

unita

La funzione prende un numero come parametro e restituisce la cifra delle
unità. Ad esempio unita(23) restituisce 3, unita(8174.56) restituisce 4.

decine

La funzione prende un numero come parametro e restituisce la cifra delle
decine. Ad esempio decine(23) restituisce 2, decine(8174.56) restituisce
7.

centinaia

La funzione prende un numero come parametro e restituisce la cifra delle
centinaia. Ad esempio centinaia(23) restituisce 0, centinaia(8174.56)
restituisce 1.

migliaia

La funzione prende un numero come parametro e restituisce la cifra delle
migliaia. Ad esempio migliaia(23) restituisce 0, migliaia(8174.56)
restituisce 8.

decimi

La funzione prende un numero come parametro e restituisce la cifra dei
decimi. Ad esempio decimi(23) restituisce 0, decimi(8174.56) restituisce
5.

centesimi

La funzione prende un numero come parametro e restituisce la cifra dei
centesimi. Ad esempio centesimi(23) restituisce 0, centesimi(8174.56)
restituisce 6.

Esercizio 525: modulo \"FunzioniNumeriche\"

sommaDivisori

La funzione prende un numero intero come parametro e restituisce la
somma dei suoi divisori propri (ovvero dei divisori minori del numero
stesso)

listaDivisori

La funzione prende un numero intero come parametro e restituisce la
lista dei suoi divisori propri (ovvero dei divisori minori del numero
stesso)

isPrime

La funzione prende un numero intero come parametro e restituisce True se
il numero è primo, false altrimenti. (sugg: se un numero è primo il suo
unico divisore proprio è 1...)

perfetto

La funzione prende un numero intero come parametro e restituisce True se
il numero è perfetto, False altrimenti (un numero si dice perfetto se e
solo se è uguale alla somma dei suoi divisori propri)

nthPrime

La funzione prende un numero intero come parametro e restituisce
l'ennesimo numero primo. Ad esempio dato 3, la funzione restituisce 5
perché, essendo i numeri primi 2, 3, 5, 7, 11, etc... 5 è il terzo
numero primo.

SemiPrimo

La funzione prende un numero intero come parametro e restituisce True se
il numero è semiprimo, False altrimenti. Un numero si dice semiprimo se
è esprimibile come prodotto di due numeri primi. Ad esempio 6 = 2\*3 è
semiprimo, 7 = 7\*1 non è semiprimo, infatti 1 non è primo.

# Moduli della libreria standard

Ovviamente l'utilità dei moduli non è solo organizzativa, ma...
storica!!! Immaginate se qualcuno avesse raccolto tutte le funzioni più
\"fighe\" scritte in Python e le avesse catalogate in gruppi omogenei;
ad esempio le funzioni aritmetiche, le funzioni per le stringhe, le
funzioni per data e ora e così via.

Beh... qualcuno lo ha fatto! Ed ha creato la ***Python Standard
Library***.

Essa non è nient'altro che una collezione di moduli, inclusi per
semplicità in qualunque installazione Python, che quindi possiamo
utilizzare semplicemente scrivendo \"import nomeModulo\".

Fighissimo!

Faccio alcuni esempi in una tabella con il nome corretto del modulo e
una descrizione sommaria. Elenco i moduli più comuni:

  ---------- ------------------------------------------
  random     Generazioni di numeri \"pseudo-casuali\"
  math       Operazioni matematiche comuni
  datetime   Gestione Data e Ora
  pathlib    Accesso a file e directories
  csv        Lettura e Scrittura su file csv
  ...        \...
  ---------- ------------------------------------------

Se questi elencati non vi bastano e siete curiosi su quanti ce ne siano
effettivamente, provate a consultare la documentazione ufficiale:
<https://docs.python.org/3/library/index.html>.

Ancora non vi basta? Bene! Allora sappiate che ci sono altre migliaia di
moduli pieni zeppi di funzioni utili per gli incarichi più disparati,
già catalogati e liberi di essere utilizzati da chiunque! La differenza
con i precedenti è che questi non fanno parte della Python Standard
Library, ma sono elencati semplicemente nel ***Python Package Index***
(<https://pypi.org/>). Se vi serve uno di questi moduli dovete
scaricarlo e installarlo nel vostro computer prima di poterlo
utilizzare. L'ultimo capitolo di questa dispensa, chiamato Moduli PyPi
parla proprio di questo!

Di seguito vediamo alcuni esempi con moduli della ***Python Standard
Library*** che possono ritornare molto utili in varie occasioni. La
documentazione ufficiale (in inglese) di ogni modulo è inserita nello
stesso: per ottenerla, dato il modulo \"NomeModulo\", basta scrivere
nell'interprete:

\>\>\> import NomeModulo

(adesso per leggere TUTTA la documentazione del modulo)

\>\>\> help(NomeModulo)

. . .

(oppure per elencare le funzioni disponibili)

\>\>\> dir(NomeModulo)

. . .

(e poi trovata la \"funzione interessante\", leggere solo di lei)

\>\>\> help(NomeModulo.funzioneInteressante)

. . .

Molto facile e veloce. Un po\' meno facile quando si tratta di leggere
la documentazione associata, ma quello è uno scoglio che dobbiamo
superare :)

Ricordate che ogni funzione elencata va utilizzata precedendola con il
nome del modulo e che le funzioni che iniziano con il doppio underscore
( ad esempio: \_\_funzione\_\_) vanno ignorate.

Proviamo!!!

## Modulo Random

Serve per operazioni che richiedono una certa \"casualità\", anche se il
termine corretto sarebbe \"pseudocasualità\"... Ad esempio:

\# estrai numero della tombola

import random

n = random.randint(1, 90)

\# n sarà un numero \"casuale\" fra 1 e 90. Ambo! ;)

Il modulo random ritorna utile anche quando si lavora con le sequenza
(tuple, liste, stringhe, dizionari): in particolare vorrei evidenziare 3
metodi:

-   randint

    prende 2 parametri e ritorna un numero pseudo-casuale compreso fra
    questi con entrambi gli estremi inclusi.

-   choice

    applicato ad una sequenza generica ritorna un elemento casuale della
    stessa (utile per le estrazioni)

-   shuffle

    funziona solo con le liste e serve per mescolare la lista passata
    come parametro. Ovviamente non ritorna valori.

Vediamo alcuni esempi:

lista = \[ 1, 2, 3, 4, 5\]

random.choice(lista) \# estrae un numero, ad esempio: 4

random.shuffle(lista) \# mischia la lista

print(lista) \# \[4, 3, 2, 1, 5\]

Non è affatto difficile! Provate a fare i seguenti esercizi aiutandovi
con la documentazione integrata.

**Esercizio 531 (randint)**

Riempire una lista con 5 numeri casuali fra 1 e 90 diversi fra loro.
Pronta la cartella della tombola!!!

Esercizio 532 (randint)

Generare 5 numeri casuali fra 0 e 1 con 2 cifre esatte dopo la virgola
(sugg: genera interi fra 0 e 100, dividi per\...)

Esercizio 533 (choice)

Dichiarare una tupla contenenti l'elenco dei cognomi della classe ed
estrarne uno con choice. Chi esce sarà interrogato!!!

Esercizio 534 (choice)

Creare una lista contenente i numeri da 1 a 10 ed estrarre un numero con
choice. Provvedere successivamente ad eliminare il numero estratto dalla
lista e visualizzare la stessa.

Esercizio 535 (shuffle)

Dichiarare una lista contenente l'elenco dei cognomi della classe (in
ordine alfabetico) e mischiarla con shuffle. Visualizzare la lista
mescolata: quello sarà l'ordine delle interrogazioni!!!

Esercizio 536 (shuffle)

Creare una lista contenente i numeri da 1 a 10 e mescolarla.
Visualizzare la lista nel nuovo ordine ottenuto e successivamente
riordinarla.

## Modulo Math

Contiene tutte le funzioni matematiche utili per le operazioni su
esponenziali, logaritmi, trigonometria, etc...

\# esempi di operazioni varie

import math

math.log(10) \# logaritmo in base e di 10

math.cos(math.pi) \# coseno di 90 gradi (pi greco radianti)

math.factorial(5) \# fattoriale di 5, ovvero 5! = 1 \* 2 \* 3 \* 4 \* 5

math.sqrt(12) \# radice quadrata di 12

math.gcd(345,678) \# Massimo Comun Divisore

math.lcm(345,678) \# Minimo Comune Multiplo

ceil/floor/trunc \# RTFM

. . .

\# variabili definite in math:

\# math.e = 2.718281828459045 (numero di Nepero)

\# math.inf = inf (più infinito)

\# math.nan = nan (not a number. PS: hai combinato qualcosa)

\# math.pi = 3.141592653589793 (pi greco)

Esercizio 541 (sqrt)

Scrivere una funzione che calcola le soluzioni dell\'equazione di
secondo grado Ax^2^ + Bx + C = 0.

In particolare la funzione prende come parametri i coefficienti A, B, C
dell\'equazione e restituisce la lista delle soluzioni reali della
stessa.

La lista può contenere 0, 1, 2 soluzioni (anche coincidenti) a seconda
dei casi.

Esercizio 542 (sqrt, floor)

Scrivere una funzione per calcolare la radice quadrata intera di un
numero. La radice quadrata intera di un numero x è il più grande intero
n tale che n \* n \<= x.

Provate a scrivere questa funzione con l'aiuto del modulo math (facile)
e provate a scriverne una analoga senza (un po\' più complicato)

Esercizio 543 (gcd , lcd)

Scrivere una funzione che prende numeratore e denominatore di una
frazione e ritorna una tupla di 2 valori contenenti numeratore e
denominatore ridotti ai minimi termini. Ad esempio, la funzione
riduci(15,6) ritorna la tupla (5,2).

Esercizio 544 (gcd , lcd)

In una piazza si trova il capolinea di tre linee di tram: A, B, e C. Il
tram A parte ogni TOT_A minuti, il tram B ogni TOT_B minuti, il tram C
ogni TOT_C minuti. Ogni quanti minuti i 3 tram si ritrovano al capolinea
insieme? Implementare la funzione calcolaMinuti(TOT_A, TOT_B, TOT_C) che
ritorna il numero di minuti che bisogna aspettare per avere di nuovo i 3
tram insieme al capolinea.

## Modulo DateTime

Contiene le funzioni per la manipolazione di data e ora. Contiene 4
classi diverse a cui si accede con l'operatore PUNTO (.):

-   la classe ***Date*** per la gestione della data, con giorno, mese ed
    anno;
-   la classe ***Time*** per la gestione dell'orario, con ore, minuti,
    secondi e microsecondi;
-   la classe ***DateTime*** per la gestione di Data e Ora: praticamente
    è la classe unione delle due precedenti;
-   la classe ***TimeDelta*** per il calcolo delle differenze di tempo.

Vediamo alcuni esempi per chiarire i concetti espressi. Primo esempio
relativo all'utilizzo dell'operatore punto: ***(modulo DateTime) .
(classe \"una delle 4 elencate sopra\")***:

import datetime

\# nell'ordine: anno, mese, giorno

scopertaAmerica = datetime.date(1492, 10, 12)

\# nell'ordine: ore, minuti, secondi

oraDellaPausa = datetime.time(16, 40, 00)

\# nell'ordine: anno, mese, giorno, ore, minuti, secondi

uomoSullaLuna = datetime.datetime(1969, 7, 20, 20, 18, 00)

Successivamente vedremo uno o due esempi che coinvolgono la classe
TimeDelta. Per visualizzare informazioni sulle classi in oggetto
ricordatevi di utilizzare le funzioni dir() e help():

help(datetime.date)

help(datetime.time)

\...

Una delle cose più semplici da fare con queste classi è ottenere ora e
data correnti:

\# Per la classe Date, possiamo ottenere il giorno odierno

oggi = datetime.date.today() \# vale 2019-05-23

\# La classe Time NON ha un metodo per l'ora corrente.

\# Dobbiamo usare la classe DateTime

adesso = datetime.datetime.now() \# vale 2019-05-23 19:26:03.478039

Una volta impostata una data o un'ora è possibile accedere ai valori dei
campi che la caratterizzano:

print(\"Anno: \", adesso.year)

print(\"Mese: \", adesso.month)

print(\"Giorno: \", adesso.day)

print(\"Ore: \", adesso.hour)

print(\"Minuti: \", adesso.minute)

print(\"Secondi: \", adesso.second)

**L'accesso ai valori dei campi che caratterizzano una variabile Date o
DateTime o Time è sempre in sola lettura**.

Questo significa che possiamo visualizzare i valori come fatto qui
sopra, ma non possiamo utilizzare questi campi per modificare una data.

Per essere completamente espliciti, non è possibile fare operazioni tipo
le seguenti:

dataAcaso = datetime.datetime(2022, 6, 4, 13, 0, 0)

dataAcaso.year = 2020 **\# ERRORE**

dataAcaso.hour = 12 **\# ERRORE. (capito? Non si può\...)**

Le date non sono fatte per essere modificate. Invece di cambiarne una...
create un'altra variabile!

Per visualizzare date, ore o data con ora a piacimento, tutte e tre le
classi mettono a disposizione la funzione ***strftime()*** che prende
l'oggetto Data (o Ora, o Data e Ora) e ritorna una stringa
personalizzata, secondo i seguenti parametri (ho messo solo i
principali...):

  ----------- -------------------------------------------------- -----------
  Parametro   Descrizione                                        Esempio
  %a          Giorno della settimana (breve)                     Wed
  %A          Giorno della settimana                             Wednesday
  %w          Giorno della settimana come numero: 0 è Domenica   3
  %d          Giorno del mese: 01-31                             31
  %b          Nome del mese (breve)                              Dec
  %B          Nome del mese                                      December
  %m          Mese come numero: 01-12                            12
  %y          Anno (breve, 2 cifre)                              18
  %Y          Anno                                               2018
  %H          Ore: 00-23                                         17
  %M          Minuti: 00-59                                      41
  %S          Secondi: 00-59                                     08
  %%          Per visualizzare %                                 \%
  ----------- -------------------------------------------------- -----------

Qualche esempio è meglio di molte spiegazioni:

print( oggi.strftime(\"%d-%m-%Y\") )

23-05-2019

print( adesso.strftime(\"Sono le %H:%M\") )

Sono le 19:26

print( adesso.strftime(\"%A\") )

Thursday

È facile capire che in ogni tipologia di dato potete usare solo i
parametri relativi ad esso: ovvero con un oggetto date, i parametri
relativi ad ore, minuti o secondi non vanno bene, mentre con un oggetto
time non vanno quelli sul giorno, il mese, etc... su un oggetto datetime
funzionano tutti!!!

### Differenze di tempo (TimeDelta)

Ok, domanda a bruciapelo. Da quanto tempo l'uomo è andato sulla Luna? Da
quanti anni? Da quanti giorni??

Le differenze di tempo sono materia per la classe TimeDelta; un elemento
della classe stessa si ottiene facendo una differenza tra due elementi
di tipo DateTime o Date (**non Time... attenti!!!**)

print(adesso -- uomoSullaLuna)

18205 days, 12:42:12.510824

Ok... in giorni è quello. Ma... in anni? Settimane? Ore? Minuti?
Secondi? In questo caso occorre fare un po\' di calcoli: si fa la
differenza fra 2 date (o 2 datetime, NON due time), si utilizza la
funzione ***total_seconds()*** che ritorna i secondi totali e poi si fa
qualche divisione...

diff = adesso -- uomoSullaLuna

secondiTotali = **int(**diff.total_seconds()**) \# int() per
arrotondare\...**

minutiTotali = secondiTotali // 60

oreTotali = minutiTotali // 60

giorniTotali = oreTotali // 24

settimaneTotali = giorniTotali // 7

anniTotali = giorniTotali // 365 \# più o meno\...

Prendiamo un po\' confidenza con il modulo grazie ad un po\' di esercizi
:)

**Esercizio 551 (now)**

Visualizzare la data e l'ora corrente, scrivendo la frase \"Oggi è il
GG/MM/AAAA e sono le ore HH:MM\"

Esercizio 552 (\...)

Data l'ora di adesso e inserito dall'utente l'ora di fine lezione
calcolare il numero di minuti mancanti.

Esercizio 553 (tuple, weekday)

Chiedere all'utente di inserire la data di nascita e visualizzare il
giorno della settimana in cui è nato.

Esercizio 554 (\...)

Chiedere all'utente di inserire due numeri per giorno e mese dell'anno
corrente e calcolare quante settimane sono passate dall'inizio dell'anno
a quella data.
