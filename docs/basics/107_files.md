# Files

!!! warning

    Questa parte della documentazione non è ancora pronta.

    Usa la documentazione in PDF reperibile
    [qui](https://www.adjam.org/next/index.php/s/egW7AnHxcif8n27?path=%2FPYTHON)


Per interagire con il filesystem del sistema in cui è in esecuzione uno
script, Python mette a disposizione due semplici funzioni predefinite:
[open()]{.title-ref} e [close()]{.title-ref}. Banalmente, la prima
permette di \"aprire\" un file e lavorarci dentro, mentre la seconda lo
\"chiude\".

Vediamo nel dettaglio cosa questo significhi:

``` 
file_object = open ( name, mode )
```

La funzione open ha due parametri principali, di cui solo il primo è
obbligatorio: il nome del file da aprire. Il secondo parametro indica la
modalità di apertura: lettura, scrittura o aggiunta a fine file.

Elenchiamo le principali modalità:

  Modo      Descrizione
  --------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  r         Modalità di lettura (read). Il file NON sarà modificato da alcuna operazione. Se il file non esiste l'apertura fallisce. **Modo di default**.
  \-\-\--   \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
  w         Modalità di scrittura (write). Un file esistente verrà sovrascritto, altrimenti ne verrà creato uno nuovo.
  \-\-\--   \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
  x         Modalità di creazione file (non lo so perché x...). Ritorna un errore se il file esiste già. Se funziona, apre il file in scrittura.
  \-\-\--   \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
  a         Modalità di aggiunta a fine file (append). Il file verrà aperto in scrittura, aggiungendo in fondo a ciò che esiste quello che viene scritto. Altrimenti è come write.

Oltre ad aprire un file per leggerci o scriverci, bisogna anche sapere
come farlo. Le modalità di gestione dei file sono solo due:

  Modo      Descrizione
  --------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  t         Modalità testuale. In questa modalità i dati vengono gestiti byte a byte. **Modo di default.**
  \-\-\--   \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
  b         Modalità binaria. In questa modalità i dati vengono gestiti bit a bit.

Da queste informazioni si desume che l'apertura generica di un file
corrisponde ad una apertura in lettura in modalità testuale: qualsiasi
altra operazione dovrà essere esplicitata. Per evitare errori,
esplicitiamo sempre la modalità di apertura! Per quanto riguarda la
gestione invece\... qui tratteremo solo la gestione testuale :)

Vediamo alcuni semplici esempi:

``` python
# Esempio 1: creazione di un file con testo inserito all’interno
f = open("ciao.txt", "w")
f.write("Ecco qua.\nCapito?")
f.close()
```

In questo primo esempio il file \"ciao.txt\" inizialmente non esiste.
L'esecuzione del codice lo crea con dentro scritto il testo indicato.
Dopo aver eseguito questo codice, vedrete nella cartella del file
python, un file chiamato \"ciao.txt\" che contiene 2 righe\... Nella
stessa cartella creiamo un nuovo file sorgente con questo codice:

``` python
# Esempio 2: lettura del file "ciao.txt" creato sopra
f = open("ciao.txt", "r")
str = f.read()
f.close()
print(str)
```

Che visualizzerà:

``` 
Ecco qua.
Capito?
```

Penso sia tutto abbastanza intuitivo da capire. Facciamo un esempio con
la modalità \"append\"

``` python
# Esempio 3: aggiunta a fine file
f = open("ciao.txt", "a")
f.write("\nSperiamo di sì")
f.close()
```

Se aprite il file \"ciao.txt\" DOPO aver eseguito il codice sopra,
vedrete che il testo è diventato di 3 righe:

``` 
Ecco qua.
Capito?
Speriamo di sì
```

Se avete osservato i 3 esempi proposti avrete notato che:

-   la funzione **write()** scrive su file la stringa esatta che gli
    viene fornita come parametro senza aggiungere spazi o andare a capo
    (come ad esempio fa la print())
-   la funzione **read()** copia su una stringa tutto il contenuto del
    file in una volta sola.

Se vogliamo leggere il file di testo riga per riga abbiamo due
possibilità:

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

Stesso risultato lo si ottiene con la funzione readline() che, come dice
il nome, legge una linea del file di testo. Il difetto di questa seconda
modalità è che devi sapere quante righe contiene il file\...

``` python
# Esempio 5: lettura delle righe con funzione readline()
file = open("ciao.txt", "r")
str = file.readline()
print(str)
str = file.readline()
print(str)
str = file.readline()
print(str)
file.close()
```

Che (per l\'ennesima volta) visualizzerà:

``` 
Ecco qua.
Capito?
Speriamo di sì
```

Basta con gli esempi! Ma fra un attimo iniziamo con gli esercizi ;)

