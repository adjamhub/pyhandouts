# ESP32

ESP32 è un microcontrollore con Wifi e bluetooth integrato, oltre che un'interfaccia programmabile per la gestione di vari sensori collegati ad esso.<br>
È possibile programmarlo con un linguaggio chiamato `MicroPython` che, come si intuisce facilmente dal nome, rappresenta un sottinsieme del linguaggio `Python`.<br>
Rappresenta uno dei mattoni fondamentali dell'evoluzione dell'informatica e delle telecomunicazioni conosciuta con il nome di <a href="https://it.wikipedia.org/wiki/Internet_delle_cose" target="_blank">Internet of Things</a>

--- immagine ---

!!! tip "Domanda"

    Sapete qual è l'editor Python più semplice ed adatto per la programmazione di microcontrollori basati su MicroPython??
    
    Se avete risposto <a href="https://thonny.org" target="_blank">Thonny</a>, avete dato la risposta esatta!!!

<!-- ################################################################################# -->
## Thonny vs ESP32

Thonny è l'editor perfetto per questo tipo di lavoro! È stato scritto all'universitù di Tartu espressamente per questi due obiettivi:

1. fornire un editor semplicissimo per imparare a programmare in Python
2. fornire una interfaccia semplice per la gestione di dispositivi programmabili

--- immagine ---

Vediamo come si fa.

## MicroPython Firmware (importante)

La prima cosa da fare quando si programma un ESP32 con MicroPython è caricare su di esso il firmware MicroPython, che conterrà l'interprete e le librerie 
di base per l'esecuzione del codice che andremo a scrivere.

Questa operazione va fatta per prima e solo un'unica volta!!!

Il sito ufficiale di MicroPython è (incredibilmente): <a href="https://micropython.org" target="_blank">https://micropython.org</a>

Scaricate fra le releases il seguente file binario:

--- immagine ---

Blah blah

## "Hello, World!"

Connetti il tuo ESP32 al computer e cambia l'interprete Python a `MicroPython (ESP32)`.

Scrivi il tuo difficilissimo codice:

``` py
print("Hello, World!")
```

e salva il file come `HelloWorld.py` dentro la memoria dell'ESP32. Per farlo:

Clicca sul pulsante APRI:

--- immagine ---

Seleziona `MicroPython device`

--- immagine ---

Esegui il codice, premendo `F5` oppure selezionando l'azione `Run current script`

Se vuoi fare in modo che il tuo dispositivo esegua il tuo codice continuamente non appena viene acceso (così come fanno tutti i dispositivi: televisori, forni, macchine del caffè, etc...) apri il file `boot.py` e modificalo come segue:

''' py
# codice per eseguire il file HelloWord.py
```


<br>
<br>
<br>

