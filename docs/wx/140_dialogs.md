# Dialogs

Le finestre di dialogo sono strumenti indispensabili della
programmazione con GUI attuale. Esse permettono una comunicazione
bidirezionale fra l'applicazione e l'utente con la prima che tramite
esse mostra all'ultimo informazioni ritenute importanti o richiede
scelte senza le quali non si può procedere oltre.

!!! tip "Suggerimento"

    La caratteristica delle finestre che le porta ad essere considerate
    finestre di dialogo è quella di essere finestre **modali**, ovvero
    finestre che si sovrappongono alle finestre principali e non possono in
    alcun modo essere ignorate.

    Questa condizione si ottiene utilizzando in una finestra la funzione
    **ShowModal()** al posto della classica funzione **Show()**.


Esempi banali di finestre di dialogo sono la finestra di errore, la
finestra di selezione file, quella per selezionare i font oppure i
colori. Vediamole una per una, con un piccolo esempio per comprenderne
al meglio il funzionamento.


<!-- ####################################################################################################################################### -->
## Message Dialogs


> **Documentazione ufficiale <a href="https://docs.wxpython.org/wx.MessageDialog.html" target="_blank">wx.MessageDialog</a>**
> 
> Finesta di dialogo per un messaggio, un avvertimento o una domanda da porre all'utente.


Sevono per inviare un messaggio esclamativo, di avvertimento, di
richiesta o di errore. Tramite la selezione di pulsanti sotto, si può
ottenere un feedback dall'utente per assicurarsi abbia recepito il
messaggio.

<br>

``` python
MessageDialog( parent , message , caption=TITOLO , style=STILE )
```

<br>

I pulsanti di una MessageDialog possono essere i seguenti:

| Valore     | Descrizione                                  |  Valore di ritorno          |
|------------|----------------------------------------------| ----------------------------|
| wx.OK      | Pulsante OK. Combinabile con CANCEL          |  wx.ID_OK                   |
| wx.CANCEL  | Pulsante CANCEL. Combinabile con OK o YES_NO |  wx.ID_CANCEL               |
| wx.YES_NO  | Pulsanti Sì e No. Combinabile con CANCEL     |  wx.ID_YES oppure wx.ID_NO  |
| wx.HELP    | Mostra il pulsante AIUTO                     |  wx.ID_HELP                 |


Se non si preme nessun pulsante, ad esempio uscendo dalla finestra di
dialogo con `ESC`, oppure con l'icona di chiusura, essa ritorna il
valore `wx.ID_NONE`.

<br>

Lo stile può contenere uno dei seguenti valori. Essi sono sovrapponibili
ai pulsanti con la tecnica del *pipe* (il simbolo `|`), come per i flag
dei Sizer.


| Stile                | Descrizione                              |
|----------------------| -----------------------------------------|
| wx.ICON_EXCLAMATION  | Mostra un icona di allerta               |
| wx.ICON_ERROR        | Mostra una icona di errore               |
| wx.ICON_HAND         | Come wx.ICON_ERROR                       |
| wx.ICON_INFORMATION  | Mostra una icona informativa             |
| wx.ICON_QUESTION     | Mostra una icona a un punto di domanda   |


Vediamo qualche esempio semplice semplice:


``` python
#  Messaggio informativo
dial = wx.MessageDialog(None, "Ora della merenda", "Info", wx.OK | wx.CANCEL)
if dial.ShowModal() == wx.ID_OK:
    # fai merenda

# Messaggio di errore
dial = wx.MessageDialog(None, "Biscotti non disponibili", "Errore", wx.OK | wx.ICON_ERROR)
dial.ShowModal()

# Messaggio di domanda
dial = wx.MessageDialog(None, "Ti andrebbe un mandarino?", "Domanda", wx.YES_NO | wx.ICON_QUESTION)
if dial.ShowModal() == wx.ID_YES:
    # mangia il mandarino

# Messaggio di avvertimento
dial = wx.MessageDialog(None, "Troppa nutella all'orizzonte", "Esclamazione", wx.OK | wx.ICON_EXCLAMATION)
dial.ShowModal()
```

<br>

!!! warning "Attenzione!"

    Ovviamente va individuato il giusto momento per visualizzare una MessageDialog: 
    **abusare di finestre modali è considerato fastidioso e maleducato.**

<br>


**Esercizio 401**

Visualizzate una finestra con un pulsante che quando premuto visualizza
un messaggio informativo a vostro piacere.


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 402**

Visualizzate una finestra vuota. Quando si clicca per chiuderla appare
il messaggio di domanda "Sicuro di voler chiudere?". Se l'utente
risponde No, la finestra non si chiude.


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 403**

Visualizzare una finestra con una SpinCtrl con valori da -10 a +10. Se
l'utente seleziona 0, appare un messaggio di avvertimento.

<br>

<!-- ####################################################################################################################################### -->
## Dir Dialogs


> **Documentazione ufficiale <a href="https://docs.wxpython.org/wx.DirDialog.html" target="_blank">wx.DirDialog</a>**
> 
> Finesta di dialogo per selezionare una cartella.


Servono per selezionare una cartella (presente o no) nel proprio computer.


``` python
# seleziona una dir e poi visualizza la scelta
dlg = wx.DirDialog(None, 'Seleziona la cartella delle immagini')
if dlg.ShowModal() != wx.ID_OK:
    return

# la stringa che contiene il percorso della cartella selezionata
percorso = dlg.GetPath()
# ...
```

<br>

**Esercizio 411**

Visualizzare una finestra con un pulsante ed una etichetta di testo
inizialmente vuota. Cliccando il pulsante si apre la DirDialog che
permette di selezionare la cartella. Se l'utente preme OK nella
etichetta di testo si visualizzi il percorso selezionato.


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 412**

Visualizzare una finestra con un pulsante. Cliccando il pulsante si apre
una DirDialog con la possibilità di selezionare cartelle non esistenti.
Se l'utente ne seleziona una non esistente, il programma la crea (Sugg:
ricordate il modulo Pathlib???)

<br>

<!-- ####################################################################################################################################### -->
## File Dialogs


> **Documentazione ufficiale <a href="https://docs.wxpython.org/wx.FileDialog.html" target="_blank">wx.FileDialog</a>**
> 
> Finesta di dialogo per la selezione file, in apertura o salvataggio.


La classe FileDialog crea una finestra di selezione file.
Analogamente alle DirDialog, servono per selezionare un file (esistente o no) nel proprio computer.



``` py title="ESEMPIO 1: SELEZIONA FILE DA APRIRE"
dlg = wx.FileDialog(None, "Apri File", style=wx.FD_OPEN)
if dlg.ShowModal() == wx.ID_CANCEL:
    return

# la stringa che contiene il percorso del file da aprire
percorso = dlg.GetPath()
```


``` py title="ESEMPIO 2: SELEZIONA PERCORSO FILE SU CUI SALVARE"
dlg = wx.FileDialog(None, "Salva File", style=wx.FD_SAVE)
if dlg.ShowModal() == wx.ID_CANCEL:
    return

# la stringa che contiene il percorso del file su cui fare salva
percorso = dlg.GetPath()
```

<br>

**Esercizio 421**

Visualizzare una finestra con un pulsante ed una etichetta di testo
inizialmente vuota. Cliccando il pulsante si apre la FileDialog che
permette di selezionare un file per l'apertura. Se l'utente preme OK
nella etichetta di testo si visualizzi il percorso del file selezionato.


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 422**

Visualizzare una finestra con un pulsante. Cliccando il pulsante si apre
una FileDialog in modalità salva. Se l'utente ne seleziona uno non
esistente, il programma lo crea vuoto (Sugg: ricordate il modulo
Pathlib???)


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 423**

Visualizzare una finestra con un pulsante ed una etichetta di testo
inizialmente vuota. Cliccando il pulsante si apre una FileDialog in
modalità apri. Se l'utente seleziona un file di testo e preme OK, il
contenuto del file viene visualizzato nell'etichetta.

<br>

<!-- ####################################################################################################################################### -->
## Colour Dialogs


> **Documentazione ufficiale classi per la gestione dei colori:**
> 
> **<a href="https://docs.wxpython.org/wx.ColourDialog.html" target="_blank">wx.ColourDialog</a>**: Finesta di dialogo per selezionare un colore dalla tavolozza nativa del SO.<br>
> **<a href="https://docs.wxpython.org/wx.ColourData.html" target="_blank">wx.ColourData</a>**: Informazioni sui colori in utilizzo su una applicazione.<br>


Le finestre di dialogo per la selezione dei colori si utilizzano tramite
la loro classe ausiliaria `wx.ColourData` che mantiene le
informazioni iniziali necessarie per la selezione dei colori e (dopo
l'esecuzione della dialog) il colore selezionato dall'utente.

``` python
# ...
datiIniziali = wx.ColourData()
dialog = wx.ColourDialog(self, datiIniziali)
if dialog.ShowModal() != wx.ID_OK:
    return

datiFinali = dialog.GetColourData()
coloreSelezionato = datiFinali.GetColour()
# ...
```

<br>

**Esercizio 431**

Visualizzare una finestra con un pulsante ed una etichetta di testo
inizialmente vuota. Cliccando il pulsante si apre una ColourDialog che
permette di selezionare un colore. Visualizzarlo come stringa nella
etichetta.


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 432**

Visualizzare una finestra con un pulsante ed una etichetta di testo
inizialmente vuota. Cliccando il pulsante si apre una ColourDialog che
permette di selezionare un colore. Colorare lo sfondo dell'etichetta
del colore selezionato.


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 433**

Visualizzare una finestra con un pulsante ed una etichetta di testo con
la scritta "Colore selezionato". Cliccando il pulsante si apre una
ColourDialog che permette di selezionare un colore. Colorare il testo
dell'etichetta con il colore selezionato.

<br>

<!-- ####################################################################################################################################### -->
## Font Dialogs


> **Documentazione ufficiale classi per i font:**
> 
> **<a href="https://docs.wxpython.org/wx.FontDialog.html" target="_blank">wx.FontDialog</a>**: Finesta di dialogo per selezionare un font dalla finestra nativa del SO.<br>
> **<a href="https://docs.wxpython.org/wx.FontData.html" target="_blank">wx.FontData</a>**: Informazioni sui Font in utilizzo su una applicazione.<br>



Le finestre di dialogo per la selezione dei font si utilizzano tramite
la loro classe ausiliaria `wx.FontData` che mantiene le
informazioni iniziali necessarie per la selezione dei font e (dopo
l'esecuzione della dialog) il font selezionato dall'utente. (Questa
frase mi sembra di averla già sentita...)

``` python
# ...
datiIniziali = wx.FontData()
dialog = wx.FontDialog(self, datiIniziali)
if dialog.ShowModal() != wx.ID_OK:
    return

datiFinali = dialog.GetFontData()
fontSelezionato = datiFinali.GetChosenFont()
# ...
```

<br>

**Esercizio 441**

Visualizzare una finestra con un pulsante ed una etichetta di testo
inizialmente vuota. Cliccando il pulsante si apre una FontDialog che
permette di selezionare un font. Visualizzarlo come stringa nella
etichetta.


------------------------------------------------------------------------------------------------------------------------------------------


**Esercizio 442**

Visualizzare una finestra con un pulsante ed una etichetta di testo con
la scritta "Font selezionato". Cliccando il pulsante si apre una
FontDialog che permette di selezionare un font. Utilizzarlo come font
dell'etichetta.


!!! tip "Suggerimento"

    Se volete una presentazione generica di tutte le finestre di dialogo
    comuni presenti nella libreria *wxPython* ecco il link che
    fa per voi: <https://docs.wxpython.org/common_dialogs_overview.html>.


<br>
<br>
<br>

