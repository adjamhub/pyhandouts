# Files


Le operazioni di I/O (input/output) da file e verso file sono operazioni native in Python, che come vedremo, si eseguono con un semplice
comando (nativo, appunto) e che servono per interagire con un generico file presente nel filesystem (quindi sul nostro computer).

Il primo capitolo è dedicato espressamente a comprendere come questo meccanismo funzioni. Nel secondo capitolo, con il modulo `pathlib` si apprende
uno strumento utile alla manipolazione dei percorsi dei file (es: dove si trova la cartella dei download? Voglio creare una cartella sul Desktop di...)
e alla gestione dei file e delle cartelle.


## Files Management

Per interagire con il filesystem del sistema in cui è in esecuzione uno
script, Python mette a disposizione due semplici funzioni predefinite: `open()` e `close()`.
Banalmente, la prima permette di *aprire* un file e lavorarci dentro, mentre la seconda lo *chiude*.

Vediamo nel dettaglio cosa questo significhi:


    file_object = open ( name, mode )


La funzione `open` ha due parametri principali, di cui solo il primo è obbligatorio: 
il nome del file da aprire. Il secondo parametro indica la modalità di apertura: lettura, scrittura o aggiunta a fine file.

Elenchiamo le principali modalità:


| Modo | Descrizione                                                                                                                                                                     |
|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| r    | Modalità di lettura (read).<br> Il file NON sarà modificato da alcuna operazione. Se il file non esiste l'apertura fallisce. <br> **Modo di default**.                          |
| w    | Modalità di scrittura (write). <br> Un file esistente verrà sovrascritto, altrimenti ne verrà creato uno nuovo.                                                                 |
| x    | Modalità di creazione file (non lo so perché x...).<br> Ritorna un errore se il file esiste già. Se funziona, apre il file in scrittura.                                        |
| a    | Modalità di aggiunta a fine file (append). <br> Il file verrà aperto in scrittura, aggiungendo in fondo a ciò che esiste quello che viene scritto. <br> Altrimenti è come write.|


Oltre ad aprire un file per leggerci o scriverci, bisogna anche sapere
come farlo. Le modalità di gestione dei file sono solo due:

| Modo | Descrizione                                                                                                 |
|------|-------------------------------------------------------------------------------------------------------------|
| t    | Modalità testuale. <br> In questa modalità i dati vengono gestiti byte a byte. <br> **Modo di default.**    |
| b    | Modalità binaria. <br> In questa modalità i dati vengono gestiti bit a bit.                                 |

Da queste informazioni si desume che l'apertura generica di un file corrisponde ad una apertura in lettura in modalità testuale: 
qualsiasi altra operazione dovrà essere esplicitata. Per evitare errori, esplicitiamo sempre la modalità di apertura! 
Per quanto riguarda la gestione invece... qui tratteremo solo la gestione testuale :)

Vediamo alcuni semplici esempi:

``` python
# Esempio 1: creazione di un file con testo inserito all’interno
file = open("ciao.txt", "w")
file.write("Ecco qua.\nCapito?")
file.close()
```

In questo primo esempio il file "ciao.txt" inizialmente non esiste.
L'esecuzione del codice lo crea con dentro scritto il testo indicato.
Dopo aver eseguito questo codice, vedrete nella cartella del file python, un file chiamato "ciao.txt" che contiene 2 righe... 
Nella stessa cartella creiamo un nuovo file sorgente con questo codice:

``` python
# Esempio 2: lettura del file "ciao.txt" creato sopra
file = open("ciao.txt", "r")
contenuto = file.read()
file.close()
print(contenuto)
```

Che visualizzerà:

``` 
Ecco qua.
Capito?
```

Penso sia tutto abbastanza intuitivo da capire. Facciamo un esempio con la modalità `append`

``` python
# Esempio 3: aggiunta a fine file
file = open("ciao.txt", "a")
file.write("\nSperiamo di sì")
file.close()
```

Se aprite il file "ciao.txt" **DOPO** aver eseguito il codice sopra, vedrete che il testo è diventato di 3 righe:

``` 
Ecco qua.
Capito?
Speriamo di sì
```

Se avete osservato i 3 esempi proposti avrete notato che:

-   la funzione `write()` scrive su file la stringa esatta che gli viene fornita come parametro senza aggiungere spazi 
    o andare a capo (come ad esempio fa la print())
-   la funzione `read()` copia su una stringa tutto il contenuto del file in una volta sola.

Se vogliamo leggere il file di testo riga per riga abbiamo due possibilità:

1.  il ciclo for
2.  la funzione readline()

``` python
# Esempio 4: lettura delle righe con ciclo for
file = open("ciao.txt", "r")
for riga in file:
    print(riga)
file.close()
```

Che (ancora una volta) visualizzerà:

``` 
Ecco qua.
Capito?
Speriamo di sì
```

Stesso risultato lo si ottiene con la funzione `readline()` che, come dice il nome, legge una linea del file di testo. 
Il difetto di questa seconda modalità è che devi sapere quante righe contiene il file...

``` python
# Esempio 5: lettura delle righe con funzione readline()
file = open("ciao.txt", "r")
riga1 = file.readline()
print(riga1)
riga2 = file.readline()
print(riga2)
riga3 = file.readline()
print(riga3)
file.close()
```

Che (per l'ennesima volta) visualizzerà:

``` 
Ecco qua.
Capito?
Speriamo di sì
```

!!! warning "Attenzione!"
    
    La visualizzazione degli ultimi due esempi non è proprio... corretta!!! Se eseguite gli ultimi due spezzoni di codice vedrete infatti delle righe vuote in più...
    
    Se volete capire perché... ragionate sul funzionamento della print e sul fatto che le righe dei file finiscono (ma comprendono) il carattere *a capo* `\n`
    

Basta con gli esempi! Ma fra un attimo iniziamo con gli esercizi ;)



### File Objects


Un file object non è nient’altro che una variabile a cui è stato assegnato l’abbinamento con un file tramite la funzione open(). Se ad esempio scrivo:

``` python
file = open( "file.txt", "w" )
```

allora f diventa un file object!
Questo tipo di variabile presenta alcune caratteristiche che permettono al programmatore di investigare sullo stato della relazione fra la variabile (e quindi il programma) e il file.
Le caratteristiche esposte sono:

| Caratteristica  | Descrizione                                 | Esempio              |
|-----------------|---------------------------------------------|----------------------|
| file.name       | Contiene il nome del file                   | "file.txt"           |
| file.mode       | Contiene il modo di apertura del file       | "w"                  |
| file.closed     | Indica se il file è chiuso oppure no        | False                |


Queste possono essere utilizzate ad esempio per verificare se è possibile scrivere sul file oppure se il file è già stato chiuso.

``` python
if file.closed :
    print("impossibile interagire con il file!")
else:
    if file.mode == "w" or file.mode == "a":
        file.write("ciao")
    else:
        print("file non aperto in scrittura!")
```

Spero sia abbastanza chiaro. Nel dubbio… lo sapete già! Funzioni `dir()` ed `help()` !!!



### Esercizi sui files


**Esercizio 701**

Scrivere un programma che chiede all’utente di digitare il proprio nome e poi salva la stringa digitata sul file "stringa.txt".

------------------------------------------------------------

**Esercizio 702**

Scrivere un programma che carica in lettura il file "stringa.txt" creato nell’esercizio precedente e ne visualizza 
il contenuto sullo schermo (dovrebbe visualizzare la stringa digitata prima).

------------------------------------------------------------

**Esercizio 703**

Scrivere un programma che chiede all’utente di digitare un numero intero e poi salva il numero digitato sul file "intero.txt".


!!! tip "Suggerimento"
    
    La lettura e scrittura da file funziona sempre e solo con le stringhe, quindi quando si lavora con interi bisogna ricordarsi di convertirli 
    in stringhe quando si scrive su file e riconvertirli in interi quando si leggono da file.

------------------------------------------------------------

**Esercizio 704**

Scrivere un programma che carica in lettura il file "intero.txt" creato nell’esercizio precedente e salva il suo contenuto, 
convertito in intero, su una variabile. Visualizzare la variabile e verificare il suo tipo con la funzione `type()`.

------------------------------------------------------------

**Esercizio 705**

Scrivere un programma che chiede all’utente di digitare un numero reale e poi salva il numero digitato sul file "reale.txt".

------------------------------------------------------------

**Esercizio 706**

Scrivere un programma che carica in lettura il file "reale.txt" creato nell’esercizio precedente e salva il suo contenuto, convertito in reale, su una variabile. 
Visualizzare la variabile e verificare il suo tipo con la funzione type().

------------------------------------------------------------

**Esercizio 707**

Creare una lista contenente i nomi di alcuni animali, visualizzarla sullo schermo e poi andare a copiarne il contenuto nel file "animali.txt" avendo cura di mettere 
ogni animale in una nuova riga.<br>
Eseguito il codice verificare che il file è effettivamente ben formato con un animale per riga.

------------------------------------------------------------

**Esercizio 708**

Aprire in lettura il file "animali.txt" creato nell’esercizio precedente in lettura e leggere il contenuto riga per riga visualizzando ogni volta l’animale "estratto".

------------------------------------------------------------

**Esercizio 709**

Aprire il file "animali.txt" in modalità "append" (aggiunta a fine file). Chiedere all’utente di inserire il nome di un animale e procedere all’inserimento nel file. 
Ripetere l’operazione 2 o 3 volte, aggiungendo ogni volta l’animale inserito nel file.<br>
Terminato l’inserimento, chiudere il file e ripetere il codice dell’esercizio precedente per visualizzarne il contenuto.

------------------------------------------------------------

**Esercizio 710**

Creare un file chiamato "parola.txt" nella stessa cartella del codice di questo esercizio, digitando al suo interno una parola qualsiasi. 
Provare ad aprire il file in modalità "x" per verificare se è possibile andarlo a sovrascrivere. 
Ripetere l’operazione in modalità "w" e infine controllare il contenuto del file.

------------------------------------------------------------

**Esercizio 711: area rettangolo**

Implementare un software che legge dal file "lati.txt" due valori reali per la base e l'altezza di un rettangolo, visualizza i dati su schermo, 
calcola e visualizza l’area del rettangolo e salva il valore calcolato nel file "area.txt".

------------------------------------------------------------

**Esercizio 712: secondi trascorsi**

Implementare un software che legge dal file "secondi.txt" un valore intero che rappresenta i secondi trascorsi dalla mezzanotte di un dato giorno e che trasforma questo valore, 
visualizzandolo su schermo in ore:minuti:secondi. Ad esempio, se il valore caricato dal file "secondi.txt" fosse 4000 (uguale a 3600, 1 ora, + 360, 6 minuti, + 40), 
il programma scriverebbe su video 1 : 6 : 40.<br>
I numeri vanno poi memorizzati nello stesso formato nel file "orario.txt".

------------------------------------------------------------

**Esercizio 713: stringhe**

Dichiarare una lista di 5 stringhe e procedere ad un salvataggio su file delle parole, una per riga.

------------------------------------------------------------

**Esercizio 714: media dei numeri**

Dato un file denominato "numeri.txt" contenente esattamente 10 numeri interi, caricarne il contenuto su una lista, procedere al calcolo della media aritmetica dei numeri inseriti, 
visualizzare il risultato a video e salvarlo nel file "media.txt".

------------------------------------------------------------

**Esercizio 715: ricerca elementi**

Dato un file "sequenza.txt" analogo a quello dell’esercizio precedente, caricare i dati su una lista, visualizzare i dati a video, chiedere un numero intero da cercare 
all’utente e procedere alla ricerca di tutte le posizioni della lista ove questo numero si trovi.<br>
Scrivere tutte le posizioni trovate riga per riga nel file "posizioni.txt". Se il numero non viene mai trovato, si inserisca nel file la scritta maiuscola "NON TROVATO".

------------------------------------------------------------

**Esercizio 716: ordinamenti**

Scrivete un programma che legge dal file "sequenza.txt" una sequenza di interi, la ordina in modo crescente e la salva ordinata sul file "ordinati.txt".

------------------------------------------------------------

**Esercizio 717**

Creare un file chiamato "settings.txt" contenente una serie di righe del tipo chiave = valore (ad esempio: nome=Andrea, cognome=Diamantini…). 
Importare i dati dal file e caricarli in un dizionario creato appositamente con la parte prima dell’uguale "strizzata" degli spazi come chiave e la parte dopo l’uguale, 
"strizzata" di spazi e newline come valore.



## Modulo Pathlib

    
Il modulo Pathlib permette di ricavare informazioni sui percorsi ove si trovano file e directories all’interno del sistema operativo che esegue lo script Python in oggetto. 
In particolare, di solito viene utilizzato l’oggetto Path importato dalla libreria pathlib.


``` python
from pathlib import Path

# il file "song.mp3" della cartella "musica" su C: in Windows 
canzone = Path("C:/musica/song.mp3")
print("Percorso della canzone:", canzone)

# la cartella corrente (dove abbiamo salvato questo file Python)
cur = Path.cwd()
print( "Cartella corrente:", cur )

# la HOME utente
# "C:\Users\utente" su Windows, "/home/utente" su Mac/Linux
homePath = Path.home()
print( "Home dir:", homePath )

# il percorso del Desktop
# il simbolo / congiunge i percorsi
desktop = home / "Desktop"
print( "Il percorso del Desktop:", desktop )
```


Negli esempi trattati sopra sono evidenziate alcune funzionalità:

  - un percorso può essere descritto tramite una stringa, con il simbolo `/` (slash) come separatore di percorsi
  - Un Path indica un percorso che non deve per forza deve esistere... anzi tra le funzionalità di Path c'è quella di verificare se un percorso esiste ed eventualmente crearlo

!!! tip "I percorsi delle cartelle principali"

    Dopo qualche anno a parlare del modulo Pathlib, ho capito che gli studenti non hanno bene idea dell'organizzazione dei files in un Sistema Operativo.
    
    Cerchiamo di farla semplice: da una parte troviamo il Sistema Operativo Windows (che fa come gli pare), dall'altra tutto il resto del mondo (Linux, BSD, MacOS, iOS, Android)
    che segue una linea comune.
    
    ---
    
    **Windows**
    
    Il sistema operativo Windows gestisce gli HD in maniera unica: ogni HD viene abbinato ad una lettera, ma per motivi storici di solito si parte da C: (se hai 3 dischi saranno C: D: E:)
    
    In uno di questi, di solito C:, c'è il sistema operativo vero e proprio, nella cartella `C:\Windows`. Gli utenti hanno ognuno uno spazio personale (una *home*): queste cartelle
    si trovano tutte nel percorso `C:\Users` e si chiamano con il relativo nome utente (la home dell'utente pippo sarà `C:\Users\pippo`)
    
    All'interno della *home* ci sono alcune cartelle importanti per l'organizzazione dei file dell'utente. Le cartelle:
    
    - `Documents`: la cartella dei documenti
    - `Downloads`: la cartella dove vanno a finire i download
    - `Desktop`: la cartella che corrisponde al Desktop utente
    - etc...
    
    Quindi ad esempio, il desktop dell'utente pippo si trova nella cartella `C:\Users\pippo\Desktop`.
    
    ---
    
    **Linux, Mac, BSD, etc...**
    
    Tutti gli altri sistemi operativi uniscono tutti gli HD montati sul proprio PC in un unico spazio comune che identificano con il simbolo `/` e chiamano `root` (radice).
    
    Le cartelle degli utenti si trovano nella cartella `/home` e si chiamano ovviamente con il nome utente. 
    Ad esempio lo spazio personale dell'utente ciccio sarà nel percorso `/home/ciccio`.
    
    Le cartelle importanti per l'utente si chiamano allo stesso modo, quindi ad esempio, la cartella Downloads di ciccio si troverà su `/home/ciccio/Downloads`

    ---
    
    **Una partenza comune: `Path.home()`**
    
    In qualsiasi OS, Python identifica la cartella personale tramite la funzione Path.home(), così che (ad esempio) il Desktop di qualunque utente si trovi nel percorso:
    
    ``` py
    percorsoDesktop = Path.home() / "Desktop"
    ```
    
    Molto intelligente :smile:

L’oggetto Path espone fra le altre le seguenti funzioni:

| Funzione              | Descrizione                                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------|
| `cwd()`               | Ritorna il percorso della cartella corrente. Restituisce un Path.                                                    |
| `exists()`            | Verifica se il percorso attuale esiste oppure no. Restituisce un valore boolean.                                     |
| `glob(pattern)`       | Ritorna la lista di tutti i file e le cartelle presenti nel Path e che rispettano il pattern.                        |
| `home()`              | Ritorna il percorso della cartella utente (la `home`, vedi sopra). Restituisce un Path.                              |
| `is_dir()`            | Ritorna True se il path attuale è una cartella, False altrimenti.                                                    |
| `is_file()`           | Ritorna True se il path attuale è un file, False altrimenti.                                                         |
| `iterdir()`           | Ritorna la lista di tutti i file presenti nel Path.                                                                  |
| `mkdir()`             | Crea la cartella abbinata al percorso del Path.                                                                      |
| `open(mode)`          | Apre il file indicato nel Path in modalità "mode". Ritorna un file object come fa la funzione predefinita "open()"   |
| `rename(target)`      | Rinomina il Path al percorso indicato nel Path "target".                                                             |
| `rmdir()`             | Rimuove la cartella abbinata al percorso del Path (solo se la cartella è vuota).                                     | 
| `unlink()`            | Rimuove un file (solo se è un file). <br> **Attenti a quello che fate, per favore!!!**                               |

!!! note

    Per vedere **tutte** le funzioni offerte dall'oggetto Path:
    
    ``` py
    >>> dir(Path)
    ```

    (Ma questo lo sapevate già...)


Vediamo alcuni esempi per capire il funzionamento delle funzioni più "ostiche": 
ovviamente ognuno di questi esempi dovrebbe iniziare con l’import dell’oggetto Path dalla libreria pathlib.


``` python
From pathlib import Path
```

<br>

**Esempio 1: verificare se nella Home è presente un file chiamato "pippo"**

``` python
percorso = Path.home()
pippo = percorso / "pippo"
if pippo.exists():
    print("pippo esiste")
    if pippo.is_file():
        print("ed è un file")
    if pippo.is_dir():
        print("ed è una cartella")
else:
    print("pippo non esiste")
```

<br>

**Esempio 2: elenco dei file *.txt presenti nel Desktop dell’utente "pippo"**

``` python
desk = Path.home() / "Desktop"
for f in desk.glob("*.txt"):
    print(f, "(file)")
```

<br>

!!! note "Pattern"

    Il parametro pattern della funzione glob è una stringa che ammette la wildcard * dove per wildcard (in informatica) si intende il carattere 
    che può sostituire qualunque altro, anche molti. <br>
    Così il pattern "*.txt" rappresenta tutti i file che finiscono per ".txt", il pattern "\*" rappresenta tutti i file con qualunque nome, 
    il pattern "a*" rappresenta tutti i file che iniziano per "a" e così via.


<br>

**Esempio 3: elenco del contenuto della home con suggerimento a fianco**

``` python
home = Path.home()
for f in home.iterdir():
    if f.is_file():
        print(f, "(file)")
    elif f.is_dir():
        print(f, "(dir)")
    else:
        print(f, "(boh)")    
``` 

<br>


**Esempio 4: creazione, cambio nome ed eliminazione di una cartella nella home utente**

``` python
home = Path.home()

# creazione della cartella "ciao" nella home
# ATTENZIONE!!! mkdir da errore se la cartella esiste già... bisogna controllare!!!
cartellaCiao = home / "ciao"
if not cartellaCiao.exists():
    cartellaCiao.mkdir()

# cambio nome della cartella "ciao" in "salve" nella home
cartellaSalve = home / "salve"
cartellaCiao.rename(cartellaSalve)

# eliminazione della cartella "salve"
cartellaSalve.rmdir()
```

<br>

**Esempio 5: creazione del file "pippo.txt" nel Desktop**

``` python
desktop = Path.home() / "Desktop"
filePath = desktop / "pippo.txt"
file = filePath.open("w")
file.write("Ciao Pippo")
file.close()
```

Grazie alla funzione `open()` dell’oggetto Path possiamo creare o aprire in lettura file in un percorso a nostra scelta. O a scelta dell’utente.
Adesso tocca a voi provare il codice degli esempi e poi procedere con gli esercizi!


### Esercizi


------------------------------------------------------------

**Esercizio 731**

Scrivere un programama che elenca tutto il contenuto del proprio Desktop e verificare per ogni elemento se esso è un file oppure una cartella.

------------------------------------------------------------

**Esercizio 732**

Scrivere un programma per creare sul Desktop una cartella di nome "prova".<br>
All'interno di essa dovrà essere inserito un file di nome "pippo.txt".<br>
Dentro al file "pippo.txt" ci deve essere inserita una frase qualsiasi a scelta dell'utente.<br>

------------------------------------------------------------

**Esercizio 733**

Creare sul proprio Desktop un file di nome "gatto".
Chiedere all'utente di inserire una parola (ad esempio: "cane") e rinominare il file precedentemente creato da "gatto" alla parola inserita dall'utente.

------------------------------------------------------------

**Esercizio 733 bis**

Chiedere all'utente se vuole eliminare il file dell'esercizio precedente. Se sì, eliminarlo. Se il file non è più presente, comunicare all'utente
che il file non è più presente sul Desktop.

------------------------------------------------------------

**Esercizio 734**

Scrivere un programma creare una cartella di nome "cartella" sul Desktop e al suo interno un file vuoto di nome "file".

Procedere ad eliminare la cartella "cartella", verificando che è impossibile farlo se prima non si elimina ogni file al suo interno.

------------------------------------------------------------

**Esercizio 735**

Creare sul Desktop la cartella “esercizio”.
Al suo interno generare un file chiamato “numeri.txt” contenente 10 numeri casuali compresi fra 1 e 100. I numeri vanno scritti in colonna (uno sotto l’altro).

Creare dentro la cartella “esercizio” un file chiamato “sommaPari” contenente la somma dei numeri pari contenuti nel file “numeri.txt”.

------------------------------------------------------------

**Esercizio 736**

Chiedere all'utente di inserire una stringa.<br>
Visualizzare l’elenco di tutti i file con estensione `txt` oppure `py` presenti nella propria cartella Downloads al cui interno è presente la stringa inserita.

------------------------------------------------------------

**Esercizio 737**

Creare un programma per ripulire la cartella dei Downloads.<br>
Prima visualizza la stringa: *"Nella cartella Downloads ci sono TOT files. Vuoi cancellarli?" (T) Sì, tutti. (U) guardiamoli uno per volta (N) No* <br>
Se l’utente seleziona T, cancella tutto e via.<br>
Se seleziona N, non fare niente <br>
Se seleziona U, per ogni file visualizza il nome e chiedi: "Vuoi cancellarlo? (S/N)"

------------------------------------------------------------

**Esercizio 738 (Sposta Files)**

Crea sul Desktop una cartella chiamata ESERCIZI. Cerca i files Python presenti nella tua cartella Documenti e spostali nella cartella ESERCIZI.

!!! tip "Suggerimento: per spostare un file"
    
    1. lo apri, 
    2. copi il contenuto, 
    3. lo chiudi, 
    4. crei il file con lo stesso nome nella nuova cartella, 
    5. ci copi il contenuto, 
    6. elimini il vecchio file


<br>
<br>
<br>

