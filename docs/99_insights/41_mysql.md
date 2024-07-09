# Python & MySQL


Per sviluppare applicazioni in Python con interazione con un DBMS
servono sostanzialmente 2 cose:

-   un modulo Python per il collegamento con il DBMS
-   l'installazione di un DBMS per il testing dell'applicazione


<!-- ################################################################################# -->
## Modulo Python

Il modulo necessario per le implementazioni che vedremo si chiama "MySQL
Connector". Per l'installazione dello stesso basta utilizzare pip, con
il comando indicato sotto


    $ pip install mysql-connector


oppure dalla linea di comando, invocando l'interprete Python


    $ python -m pip install mysql-connector


I comandi elencati funzionano sicuramente su Linux e Mac. Su Windows
dipende da come è stata fatta l'installazione di Python e in particolare
se l'eseguibile Python è stato inserito nel PATH.

Se così non fosse bisogna spostarsi con la console della riga di comando
fino alla cartella di installazione di Python ed eseguire il comando
sopra da lì.

Ad esempio se l'installazione è stata fatta su `C:\Python`, allora il comando va
eseguito in quella cartella.

Per verificare che l'installazione del modulo è andata a buon fine basta
aprire l'interprete Python e provare a importare il modulo:


    >>> import mysql.connector


Se Python non si lamenta di nulla, siamo pronti per il prossimo step :)



<!-- ################################################################################# -->
## Installazione DBMS

Per testare il codice che scriveremo dobbiamo installare un DBMS.
Bene... installeremo MariaDB! Cioè... come scusa? Non installiamo MySQL?
E tutti discorsi fatti fino ad ora? E... il titolo di questa dispensa???

Provo a spiegare con una frase: ***MariaDB è un software libero nato
come fork di MySQL e studiato come Drop-In Replacement dello stesso***.
Credo che come spiegazione sia un po' criptica ma sufficientemente
esaustiva :)

Se volete maggiori informazioni sulle motivazioni della scelta, vi
rimando alla loro pagina wikipedia:
<https://it.wikipedia.org/wiki/MariaDB>.

Per installare MariaDB basta seguire le istruzioni che trovate nel loro
sito ufficiale: <https://mariadb.org/>


### Connessione al DB

Cominciamo stabilendo una connessione fra il nostro script Python e il database:

```python
import mysql.connector

pydb = mysql.connector.connect(
    host="localhost",
    user="username",
    passwd="password",
    database="dbname"
)
```

Ovviamente se c'è un problema qualunque nella connessione questo pezzo di codice fallirà.
E sarà inutile andare avanti...


<!-- ################################################################################# -->
## DDL execution

DDL (Data Definition Language) è quella parte di codice SQL che serve
per la definizione dei dati. Per estrema semplicità dirò semplicemente
che DDL si riferisce ai comandi SQL `CREATE` (ad esempio: CREATE
TABLE...), `ALTER`, `DROP`.

Questo tipo di comandi non ritornano "valori" o tabelle come risultato,
ma generano semplicemente una risposta del tipo "OK, tutto fatto!"
oppure "Mannaggia, qualcosa è andato storto!!!".

Per eseguire questo tipo di comandi abbiamo bisogno di un "cursore" che
si occupi di attualizzare l'istruzione descritta.


```python
pycur = pydb.cursor()
pycur.execute("CREATE TABLE if not exists tbl_seven(number int);")
```


## DML execution

DML (Data Manipulation Language) è quella parte di codice SQL che serve
per la manipolazione dei dati. Per estrema semplicità dirò semplicemente
che DML si riferisce ai comandi SQL `INSERT`, `UPDATE`, `DELETE`.


Questo tipo di operazioni sulle tabelle del database non modifica in
alcun modo la struttura dello stesso, ma si occupa semplicemente di
andare ad aggiungere, modificare, eliminare dati dalla tabella.

Per eseguire i comandi abbiamo ancora bisogno di un cursore. Vediamo
l'esempio:

Inserimento di un valore

```python
pycur = pydb.cursor()

for n in range(1,11):
    sql = 'INSERT INTO tbl_seven(number) VALUES (' + str(n*7) + ')'
    pycur.execute(sql)

    # per applicare l'aggiornamento dei dati, va fatto il commit sul DB
    pydb.commit()
```

<!-- ################################################################################# -->
## QL execution

QL (Query Language) è quella parte di codice SQL che serve per
l'interrogazione dei dati. Per estrema semplicità dirò semplicemente che
QL si riferisce al comando SQL `SELECT`.

Questo tipo di operazioni sulle tabelle del database genera come
risultato una tabella "provvisoria" contenente il risultato
dell'interrogazione.

Neanche a dirlo, per eseguire i comandi abbiamo ancora bisogno di un
cursore. Vediamo l'esempio:

```python
pycur = pydb.cursor()

sql = "SELECT number FROM tbl_seven WHERE number % 2 = 0"
pycur.execute(sql)

results = pycur.fetchall()

for r in results:     
    print(r)
```

Tutto qua!

Rimane da provare e sperimentare un po'...

<br>
<br>
<br>

