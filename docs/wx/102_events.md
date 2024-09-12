# Gestione degli eventi

Una volta iniziato il ***Main Event Loop***, le applicazioni wxPython sono in
grado di intercettare gli eventi utente, come ad esempio un click su un
pulsante o sulla tastiera o un movimento del mouse. 

Tutte questi eventi sono catalogati negli oggetti, ovvero ogni widget sa quali eventi
intercettare: ad esempio un pulsante saprà intercettare un click su di
esso, una linea di testo sarà in grado di capire quando ci scrivi
dentro, etc...

Deciso l'evento a cui rispondere (ad esempio, un click su pulsante) è possibile
abbinare a questo una funzione, in modo che quando l'evento accade, la funzione venga eseguita!

Per farlo dobbiamo utilizzare la funzione **Bind**:

``` python
widget.Bind ( EVENTO, FUNZIONE_EVENTO )
```

Vediamo un esempio di codice di una Finestra con un grosso pulsante
dentro: al click sul pulsante viene eseguita una funzione e... provate
a copiare il codice e ad eseguirlo per vedere cosa succede!

``` py title="Eseguire una funzione al click di un pulsante" hl_lines="9 11"
import wx

class Esempio(wx.Frame):

    def __init__(self):
        super().__init__(None, title="Cliccami")
               
        pulsante = wx.Button(self, label="Chiudi tutto")
        pulsante.Bind(wx.EVT_BUTTON, self.funzioneEvento)

    def funzioneEvento(self, evt):
        self.Close()

# ----------------------------------------
if __name__ == "__main__":
    app = wx.App()
    window = Esempio()
    window.Show()
    app.MainLoop()
```

!!! note "Funzioni Evento"

    Le funzioni che possono essere collegate con un Bind ad un evento si dicono `funzioni evento`.
    Questo tipo di funzioni ha sempre (e solo) due parametri:
    
    - `self`, poiché sono sempre funzioni membro di una classe
    - `evt`, che rappresenta l'evento che le ha scatenate.


Provate a sostituire la funzione `self.Close()` con altre funzioni tipo:

- `self.Maximize()`: massimizza la finestra
- `self.Iconize()`: riduce a icona la finestra
- `self.Move(0,0)`: sposta la finestra nel punto (0,0)
- `self.SetSize(400,300)`: ridimensiona la finestra
- etc...

Ormai avete capito tutto... io nel dubbio scrivo un pò di deduzioni a partire da questi esempi...

1. L'oggetto che rappresenta un pulsante si chiama `wx.Button`.
2. L'evento predefinito per un pulsante è il click su di esso: questo evento, per un pulsante, si chiama `wx.EVT_BUTTON`.
3. Probabilmente (ed è proprio così) se una widget si chiamasse `wx.Pippo`, il suo evento predefinito si chiamerebbe `wx.EVT_PIPPO`
4. Le funzioni che rispondono agli eventi hanno tutte la struttura `nomeFunzione (self, event)`.


!!! tip "Come si fa a sapere quali (altri) eventi può gestire un pulsante (wx.Button)?"

    Leggi la documentazione ufficiale della classe **<a href="https://docs.wxpython.org/wx.Button.html" target="_blank">wx.Button</a>**)


<!-- ############################################################################################################## -->
## Identificare le widgets


La libreria `wxPython` mette a disposizione una serie di funzionalità utili per identificare una widget. Vediamo le principali soluzioni offerte:


***Indentificare la widget che ha scatenato un evento***


La funzione evento prende come parametro l'evento che l'ha scatenata. Questo può ritornare l'evento che l'ha generato tramite la funzione `evt.GetEventObject()`.
Vediamo:


``` py title="Identificare la widget che ha generato un evento" hl_lines="11 12"
import wx

class Esempio(wx.Frame):

    def __init__(self):
        super().__init__(None, title="Cliccami")     
        pulsante = wx.Button(self, label="Fai Qualcosa")
        pulsante.Bind(wx.EVT_BUTTON, self.funzioneEvento)

    def funzioneEvento(self, evt):
        # btn è il pulsante che ha generato l'evento
        btn = evt.GetEventObject()
        btn.SetLabel("Fatto!")
        return

# ----------------------------------------
if __name__ == "__main__":
    app = wx.App()
    window = Esempio()
    window.Show()
    app.MainLoop()
```


***Identificare una widget tramite un Id***


> La libreria wxPython identifica in maniera automatica tutte le widget con un ID sempre diverso e sempre **negativo**


È comunque possibile impostare un identificativo a scelta, con una importante raccomandazione: **scegliete ID positivi e crescenti**.
Partite da 1 e andate avanti: in questo modo sarete sicuri di non fare confusione con gli ID assegnati automaticamente alle widget 
da wxPython e di non sbagliarvi da soli mettendo due volte lo stesso ID!

Nel prossimo esempio abbiamo due pulsanti (con ID impostato) collegati alla stessa funzione. L'id permette di distinguere quale dei due ha
scatenato l'evento.


``` py title="Esempio con funzione GetId" hl_lines="15 16"
import wx

class Esempio(wx.Frame):

    def __init__(self):
        super().__init__(None, title="2 pulsanti, 1 funzione")

        # i due pulsanti sono identificati con ID 1 e 2
        pulsante1 = wx.Button(self, label="pulsante 1", pos=(5,5), size=(100,30), id=1)
        pulsante2 = wx.Button(self, label="pulsante 2", pos=(120,5), size=(100,30), id=2)
        pulsante1.Bind(wx.EVT_BUTTON, self.faiQualcosa)
        pulsante2.Bind(wx.EVT_BUTTON, self.faiQualcosa)

    def faiQualcosa(self, evt):
        # la funzione GetId ci dice l'ID della widget che ha scatenato l'evento
        id = evt.GetId()
        print("Hai cliccato il pulsante con ID =", id)
        return

# ----------------------------------------
if __name__ == "__main__":
    app = wx.App()
    window = Esempio()
    window.Show()
    app.MainLoop()
```


***Recuperare una widget conoscendo il suo Id***


Vi risparmio qualunque esempio, ma immaginate di avere assegnato gli Id da 1 a 10 ad altrettante widgets. Per riottenere
una qualsiasi delle widgets in oggetto, basta eseguire la funzione `FindWindow(id)`


``` python hl_lines="2"
# per ottenere la widget con ID = 5
widget = self.FindWindow(5)
``` 

<!-- ############################################################################################################## -->
## Gestire l'evento Close()


La funzione `Close()`, che abbiamo già precedentemente incontrato, provoca la chiusura
di una finestra. In realtà però, essa genera un evento di chiusura per la finestra (CloseEvent),
che poi questa potrà gestire per *programmare* la sua chiusura.

Il caso tipico in programmazione per questa problematica è quando l'utente prova a
chiudere un editor con il file non ancora salvato! In quel caso
l'applicazione blocca la chiusura suggerendo di salvare prima il file!

Nell'esempio che segue la finestra che appare è chiudibile dall'utente
(con scorciatoia, cliccando sulla x in alto, etc..) solo se
massimizzata.

``` python
import wx

class Esempio(wx.Frame):

    def __init__(self):
        super().__init__(None, title="Massimizza per chiudere")        
        self.Bind(wx.EVT_CLOSE, self.chiudi)

    def chiudi(self, evt):
        if (self.IsMaximized()):
            self.Destroy()
        return

# ----------------------------------------
if __name__ == "__main__":
    app = wx.App()
    window = Esempio()
    window.Show()
    app.MainLoop()
```

Come al solito... copiate e provate!

!!! warning "Attenzione!"
    Quando ci si connette all'evento **wx.EVT_CLOSE** (e tipicamente... solo in questo caso) è necessario chiudere la finestra utilizzando 
    la funzione `Destroy()` invece della funzione `Close()`. 
    
    Infatti: funzione `Close()` ---> evento `wx.EVT_CLOSE` ---> bind alla funzione chiudi ---> funzione `Close()` ---> CICLO INFINITO!


Ok, definiti gli eventi più semplici e capito come collegarli alle
widget, vediamo le widgets e i layout per creare delle applicazioni con
un look consistente.

<br>
<br>
<br>


