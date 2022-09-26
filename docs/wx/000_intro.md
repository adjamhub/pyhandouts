# La libreria grafica wxPython


<!-- ########################################################################################################################################### -->
## Introduzione

**wxPython** (<https://wxpython.org/>) è una libreria grafica open source, adatta alla creazione di GUI (interfacce grafiche) per sistemi Windows, Mac e Linux.

WxPython deriva dal toolkit **wxWidgets** (<https://wxwidgets.org>), libreria grafica C++ con una tradizione più che ventennale. 
Con la versione 4.x che noi utilizzeremo (codenamed *Phoenix*) ha subìto una profonda revisione e modernizzazione, fino a diventare la libreria
grafica preferita dallo stesso [von Rossum](https://it.wikipedia.org/wiki/Guido_van_Rossum) (l'inventore di Python). 
E chissà che presto non diventi la libreria grafica predefinita!

Si presenta come una libreria Python 3.x completamente orientata agli oggetti e quindi sarà di immediato utilizzo per tutti noi, 
non appena avremo introdotto la sua struttura e gli oggetti principali.


<!-- ########################################################################################################################################### -->
## Installazione

La libreria wxPython è una libreria OOP Python in tutto e per tutto. 
La trovate come tantissime altre sul **Python Package Index** ([pypi.org](https://pypi.org)) e per installarla
seguite questi semplici passaggi.

Aprite [Thonny](https://thonny.org) e accedete al suo gestore dei pacchetti:

![image](images/wxpython_install_0.jpg)

Da lì digitate la stringa **wxpython** e cliccate su *Cerca in PyPi*:

![image](images/wxpython_install_1.jpg)

A questo punto vi basta semplicemente cliccare **INSTALLA** e aspettare :)

![image](images/wxpython_install_2.jpg)

Quando il download e l'installazione sono finiti, passiamo a verificare il funzionamento del tutto con un Hello Wordl!


<!-- ########################################################################################################################################### -->
## Hello World!


Vediamo innanzitutto un primo assaggio di codice, il famoso programma *Hello World!* per la libreria wxPython:

``` python
# si importa la libreria wx
import wx

# si crea un oggetto Applicazione
app = wx.App()

# si crea una finestra con titolo "Hello, World!"
window = wx.Frame(parent=None, title="Hello, World!")
window.Show()

# si avvia il "Main Event Loop"
app.MainLoop()
```

!!! tip "Hello World Programs"

    Gli *Hello World Programs* sono programmi che scrivono (o mostrano)
    semplicemente la scritta "Hello, World!".

    Sono tipicamente i primi programmi che si vuole scrivere in un qualsiasi
    linguaggio di programmazione e servono soprattutto a vedere la struttura
    e la sintassi del linguaggio, oltre che ad assicurarsi che tutto
    funzioni.


Il risultato dell'esecuzione di quel codice è questo!

![image](images/first_wxpython_code.jpg)


Se avete visto anche voi una finestra grigia vuota con il titolo "Hello, World!" significa che l'installazione e il primo programma sono andati
a buon fine e siete pronti per studiare la libreria wxPython (a partire dalla prossima pagina!).

<br>
<br>
<br>

