# Package(s)

Elenco i punti da seguire nell'ordine (più o meno) in cui dovrebbero essere svolti.


## nome pacchetto

Per prima cosa, **scegli bene il nome del pacchetto**. Un nome semplice, possibilmente senza spazi nè maiuscole. Nel proseguio del capitolo, farò
finta di aver scelto il nome `ciccio`. 

Se avete pensato un nome con due o più parole (tipo `distruzione dell'universo`) dovete renderlo un identificatore
semplice, ovvero togliere spazi, articoli e proposizioni (rendendolo ad esempio `DistruzioneUniverso` oppure `distruzione_universo`).


## creazione

Se, come ho detto prima, ho scelto per il mio pacchetto il nome `ciccio`, allora apro il terminale e digito:

``` bash
uv init --package ciccio
```


## rinomina

Se all'inizio non avevo pensato abbastanza bene al nome del pacchetto e adesso voglio cambiarlo, devo eseguire 2 importanti operazioni.
Immaginate che all'inizio, non sapendo bene quale nome scegliere, io abbia creato il pacchetto `provaPack`, di cui ho la seguente struttura:

``` bash
provaPack
├── pyproject.toml
├── README.md
└── src
    └── provapack
        └── __init__.py
```

Andiamo adesso a rinominare il package in 2 mosse:

1) Modificare il nome del pacchetto nel file `pyproject.toml`

2) rinomina la cartella dentro `src`, lasciando inalterata la cartella principale.

Alla fine la struttura sarà la seguente:


``` bash
provaPack
├── pyproject.toml (modificato)
├── README.md
└── src
    └── ciccio
        └── __init__.py
```


## Sistema gli import

Riordina e sistema gli import di ogni file del tuo progetto con la seguente logica:

1) prima gli import della libreria Python Standard (es: random, math, etc...), poi salta una riga

2) poi gli import aggiunti tramite `pip` (es: pygame, platformdirs, etc...), poi salta una riga

3) infine gli import del tuo proprio package (i files dentro `src/my_package` ) inclusi in forma esplicita o implicita. Meglio la forma implicita...


Alla fine sarà una cosa del genere:


``` python title="import(s)"

# libreria Standard
import random
import math

# librerie pip
import pygame
import platformdirs

# moduli del mio package: forma esplicita
from ciccio.nomeModulo import *
# oppure
from ciccio import nomeModulo

# moduli del mio package: forma implicita (con il punto)
from .nomeModulo import *
# oppure
from . import nomeModulo

```


## Gestione files NON di codice

Buona norma organizzare codice e files all'interno della cartella del modulo in maniera sensata. Aggiungete una struttura simile alla seguente:


``` bash
provaPack
├── pyproject.toml
├── README.md
└── src
    └── ciccio
        └── __init__.py
        └── images
            └── file1.jpg
            └── (... le altre immagini...)
        └── sounds
            └── campanella1.mp3
            └── (... gli altri suoni... )
```

Poi aggiungete un file chiamato `resources.py` al vostro progetto, in cui scriverete una cosa tipo questa:


``` python title="resources.py"
from importlib.resources import files

# eventualmente aggiungere tutte le funzioni relative alle cartelle che avete creato in src.
def get_sound(filename: str) -> Path:
    return files(__package__) / "sounds" / filename

def get_image(filename: str):
    return files(__package__) / "images" / filename
```

A questo punto, nel vostro codice, quando avete bisogno di un file, scrivete:

``` python
from .resources import *

fileSfondo = get_image("sfondo.png")
fileAudio = get_sound("sottofondo.mp3")

```


## percorsi dei files con PlatformDirs


Ricordati di aggiungere `PlatformDirs` al tuo package con `uv`:

```bash
uv add PlatformDirs
```

e poi revisiona tutti i percorsi dei files che il tuo package scrive (es: impostazioni, classifica, etc...), riscrivendo il percorso con `PlatformDirs`.<br> 
Eventualmente riguarda il capitolo sui files dove è spiegato il modulo `PlatformDirs`.


## Github: descrizione e README

E' buona norma trovare un momento anche per curare un minimo il repository GitHub, soprattutto sistemando queste due semplici cose!

La descrizione del progetto si può modificare direttamente su GitHub, cliccando sulla rotellina della modifica in alto a dx del progetto (di fianco alla parola **About**).
Scrivete una frase semplice, che descrive sommariamente il gioco ed elenca i vostri cognomi. Ad esempio una cosa tipo: "Una versione di 'Acchiappa la Talpa', by Pippo e Ciccio".

Il file `README.md` fornisce la descrizione che compare a fondo pagina. Va scritto in `markdown`, un linguaggio di rappresentazione semplice e potente. Trovate tonnellate di documentazione online. Potete anche semplicemente scrivere testo semplice. Si può modificare online oppure facendo un commit sul file stesso. Sarebbe molto carino aggiungerci una *pubblicità* per il vostro gioco! Fate uno screenshot, aggiungetelo al progetto e al file README. Spazio alla fantasia...


## File README. Descrizione Operativa!

Aggiungete una interruzione al vostro file README, ad esempio una  `<hr>` e poi producete una descrizione operativa: raccontate come vi siete organizzati per lavorare,
chi ha fatto cosa **in maniera meticolosa**: per ogni file del progetto voglio sapere l'origine e gli autori!!!

Ad esempio:

- Gina ha creato sul sito www.immaginibellissime.com le immagini file1.jpg, file2.jpg. 
- Pino ha scritto insieme alla AI Cancer la funzione spara_a_salve() e la funzione schioppaTutto(). 
- Gina e Pino hanno lavorato insieme a tutte le funzioni del file coso.py, che era stato inizialmente generato tramite l'AI OplaGQT. 
 
Insomma... una cosa del genere...


## Licenza

Ultima revisione della licenza e del contenuto del progetto. 
Di chi é il codice che pubblicate? Avete intestato tutti i file di codice? Dove avete trovato le immagini?? E i suoni??
Qualcuno può prendersela con voi per le cose che state per pubblicare??

Tutti i file python che avete scritto dovrebbero avere una intestazione di questo tipo:

```python
# Nome del modulo - breve descrizione.
# (riga vuota)
# Descrizione più lunga opzionale su più righe,
# che spiega cosa fa il modulo.
# (riga vuota)
# License: See LICENSE file in the project root for details.
# (riga vuota)
# Authors: 
# nome cognome <email>
# nome cognome <email>
```

Se usate l'inglese bene. Altrimenti va bene anche l'italiano. E' il momento di rivalutare la scelta della licenza.
Scegliete una licenza opensource, anche controllando questo sito: <a href="https://choosealicense.com/">Choose a License</a>. Oppure mantenete quella iniziale.

In caso, sostituite il file **LICENSE**. E ricominciate la valutazione di questo punto. 

Oppure andiamo avanti...


## Aggiornate il numero di versione!!

Se fino ad ora abbiamo lavorato alla versione `0.1.0` del nostro progetto, è ora di aggiornare almeno alla versione `0.2.0`!!!
Per farlo basta modificare il file `pyproject.toml` (e fare il commit)! 

Se proprio vi sentite fenomeni, potete *taggare* il commit con l'etichetta `v0.2.0`!

**Finito!!!**
