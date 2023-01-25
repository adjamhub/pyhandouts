# Primi concetti

wxPython è un toolkit Python cross-platform per la creazione di
applicazioni con GUI e che espone una lunga lista di widgets per i
compiti più disparati. Le sue classi sono organizzate in moduli che pian
piano andremo a studiare: per adesso ci basterà sapere che le classi
principali sono disponibili nel modulo **wx**, lo stesso che abbiamo
importato nell'esempio *Hello, World!*.

Capisco che arrivato a questo punto, prima di andare avanti, è
necessario che io faccia una pausa e spieghi una serie di termini che ho
utilizzato qua e là e che probabilmente ancora non conoscete.

* ***toolkit*** <br>
  Letteralmente "cassetta degli attrezzi", rappresenta l'insieme di strumenti necessari per eseguire un compito. 
  Il compito del toolkit wxPython è la creazione di applicazioni grafiche, gli strumenti che utilizza sono classi Python.

* ***GUI*** <br>
  Acronimo di *Graphical User Interface*, indica la capacità di alcune applicazioni di interagire con gli utenti 
  tramite la modalità WIMP (e adesso spiego WIMP...)

* ***cross-platform*** <br>
  Rappresenta la capacità di alcuni software di essere utilizzati su vari sistemi operativi. 
  Per quanto riguarda wxPython essa è disponibile su tutti i sistemi operativi desktop, in particolare è sicuramente 
  disponibile su Windows, Mac OS e Linux.

* ***Widget*** <br>
  Si tratta di un generico oggetto grafico. Nel contesto wxPython si tratta di una classe wxPython che implementa 
  un oggetto grafico, ad esempio la classe che implementa un pulsante (e quindi il pulsante), la classe che implementa una finestra, 
  una checkbox, etc...

Benissimo! Detto questo passiamo a reimplementare l'unico esempio che abbiamo finora visto e ragioniamoci un pò sù


<!-- ####################################################################################### -->
## Widget Derivata


Riguardiamo l'esempio iniziale ***Hello, World!*** con la differenza che, invece di istanziare direttamente la classe `wx.Frame`
verrà creata una classe derivata a partire da questa.

Questa sarà la modalità operativa con cui lavoreremo fino a nuovo ordine! Per meglio comprendere quanto da ora in poi eseguirete
con obbedienza e rassegnazione, in questo esempio banale troverete tantissimi commenti:


``` python
# IMPORTA LA LIBRERIA wxPython (modulo wx)
import wx

# --------------------------------------------------------
# QUI SI DEFINISCE LA CLASSE LaMiaPrimaFinestra (derivata dalla classe wx.Frame)
class LaMiaPrimaFinestra(wx.Frame):

    def __init__(self):
        super().__init__(parent=None, title="La mia prima finestra")
        # ... (altro codice)...

# --------------------------------------------------------

# QUI SI UTILIZZA LA CLASSE LaMiaPrimaFinestra DEFINITA SOPRA
if __name__ == "__main__":

    # si crea un oggetto Applicazione.
    # Ce ne sarà sempre uno (e solo uno) in ogni applicazione.
    # Gestisce l'interazione con l'esterno (l'utente e il sistema operativo)
    app = wx.App()
 
    # si definisce un oggetto della classe LaMiaPrimaFinestra
    # Gi oggetti grafici principali (le finestre) vengono creati nascosti e quindi devono essere mostrati
    window = LaMiaPrimaFinestra()
    window.Show()
    
    # si avvia il "Main Event Loop"    
    app.MainLoop()
```

!!! note "Main Event Loop"

    Il **Main Event Loop** o *ciclo principale degli eventi* è uno stato di
    grazia in cui si pone ogni applicazione grafica dopo aver disegnato le
    proprie widgets.

    In questo particolare stato di colloquio perenne tra il sistema
    operativo, l'utente e l'applicazione stessa, quest'ultima diventa in
    grado di intercettare gli eventi che accadono nel sistema (un click su
    un pulsante, un movimento del mouse, la carta della stampante che
    finisce, la rete che si sconnette, etc...) e di rispondere
    (eventualmente) eseguendo una funzione tra quelle disponibili fra gli
    oggetti che la compongono.


In questo modo impareremo a strutturare ogni finestra in una classe e se
necessario a strutturare i nostri progetti dividendo ogni classe in un
file diverso, in modo da favorire al massimo l'organizzazione
fortemente orientata agli oggetti e tutti le buone cose che ne derivano
(organizzazione del codice, chiara divisione dei compiti fra le classi,
semplicità nel riutilizzare il codice, etc..)


<!-- ####################################################################################### -->
## Dimensione e posizionamento


Se vogliamo modificare la **dimensione** di una finestra possiamo farlo in 2 modi: 
o fornendo una dimensione iniziale nel costruttore della stessa, oppure utilizzando la funzione `SetSize(width, height)`. 

Faccio notare che tutte le misure sono espresse in pixel.

``` python
import wx

app = wx.App()   
window = wx.Frame(None, title="Finestra 800x600", size=(800,600))
window.Show()
app.MainLoop()
```

...oppure...

``` python
import wx

app = wx.App()   
window = wx.Frame(None, title="Finestra 800x600")
window.SetSize(800,600)
window.Show()
app.MainLoop()
```

Entrambi i metodi sono semplici ed efficaci. Dal punto di vista operativo, il metodo `SetSize()` può essere chiamato all'interno della funzione
`__init__` quando si definisce una finestra derivata.

In maniera analoga, se vogliamo specificare il **posizionamento** della finestra all'interno dello schermo possiamo 
specificare la posizione iniziale nel costruttore o eseguire successivamente la funzione `Move(x,y)`

``` python
import wx

app = wx.App()   
window = wx.Frame(None, title="Finestra al punto (5,5)", pos=(5,5))
window.Show()
app.MainLoop()
```

...oppure...

``` python
import wx

app = wx.App()   
window = wx.Frame(None, title="Finestra 800x600")
window.Move(5,5)
window.Show()
app.MainLoop()
```

Anche qui, dal punto di vista operativo, eseguiremo questo codice nel costruttore della classe grafica derivata o
all'interno della funzione `__init__`.

Un'ultima cosa, semplice e molto utile può essere quella relativa al posizionamento automatico con la funzione `Centre()`,
che posiziona automaticamente la finestra al centro dello schermo:

``` python
import wx

app = wx.App()

window = wx.Frame(None, title="Finestra Centrata")

# esegui questo codice, poi commenta la riga qui sotto e rieseguilo
window.Centre()
window.Show()

app.MainLoop()
```

Adesso avanti! Il prossimo step è quello di interagire un pò con l'applicazione! 
Inserire un pulsante e fargli fare qualcosa! 

Prima però... una doverosa precisazione!!!


## Documentazione Ufficiale

La libreria wxPython contiene circa 1000 classi grafiche, molte delle quali sono collegate fra loro tramite ereditarietà. 

Questa informazione è decisiva anche dal punto di vista della documentazione: ad esempio, le funzioni di posizionamento e ridimensionamento viste sopra, vengono
dalla classe `wx.Window` da cui la classe `wx.Frame` deriva, così come ogni oggetto grafico della libreria wxPython (avete letto bene,,, tutti!!!!).<br>
Questo significa che tutte le classi hanno questi metodi e che voi già da qualche minuto sapete *spostare* e *ridimensionare* ogni oggetto grafico!!!

Da un altro punto di vista, in questa dispensa introdurremo (non studieremo approfonditamente... introdurremo) una cinquantina circa fra gli oggetti grafici più importanti.
Qualsiasi funzionalità o caratteristica interessante che non viene descritta nella dispensa sarà da ricercare nella documentazione ufficiale!!!

**La documentazione ufficiale wxPython si trova sul sito <a href="https://docs.wxpython.org/" target="_blank">https://docs.wxpython.org/</a>**.

Da lì, dovrete imparare a cercare le classi che vi interessano, capire per ognuna da quali classi deriva, quali sono i suoi metodi, le sue proprietà, le sue caratteristiche principali.

Per comodità, metto qui i link diretti alle due classi che abbiamo studiato finora:

- **<a href="https://docs.wxpython.org/wx.App.html" target="_blank">wx.App</a>**: Gestisce le applicazioni con GUI implementate tramite wxPython.

- **<a href="https://docs.wxpython.org/wx.Frame.html" target="_blank">wx.Frame</a>**: Finestra vuota generica, con barra del titolo, bordi e ridimensionamento funzionanti.

Provate a curiosare un pò e a capire come ricercare informazioni.

Buon lavoro!!

<br>

