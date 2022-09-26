# Gestione degli eventi

Una volta iniziato il Main Event Loop le applicazioni wxPython sono in
grado di intercettare gli eventi utente, come ad esempio un click su un
pulsante o sulla tastiera o un movimento del mouse. Tutte questi eventi
sono catalogati negli oggetti, ovvero ogni widget sa quali eventi
intercettare: ad esempio un pulsante saprà intercettare un click su di
esso, una linea di testo sarà in grado di capire quando ci scrivi
dentro, etc...

Deciso l'evento a cui rispondere (ad esempio, un click su pulsante) è possibile
abbinare a questo una funzione, in modo che quando l'evento accade, la funzione venga eseguita!

Per farlo dobbiamo utilizzare la funzione **Bind**:

``` python
widget.Bind ( EVENTO, FUNZIONE )
```

Vediamo un esempio di codice di una Finestra con un grosso pulsante
dentro: al click sul pulsante viene eseguita una funzione e... provate
a copiare il codice e ad eseguirlo per vedere cosa succede!

``` python
import wx

class Esempio(wx.Frame):

    def __init__(self):
        super().__init__(None, title="Cliccami")
               
        pulsante = wx.Button(self, label="Chiudi tutto")
        pulsante.Bind(wx.EVT_BUTTON, self.chiudi)

    def chiudi(self, evt):
        self.Close()

# ----------------------------------------
if __name__ == "__main__":
    app = wx.App()
    window = Esempio()
    window.Show()
    app.MainLoop()
```

Ok... con questo esempio abbiamo capito che un pulsante, ovvero la widget **wx.Button** intercetta il click 
con l'evento **wx.EVT_BUTTON**. 

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

Ok... adesso invece parto con i dubbi... stavolta con un elenco in ordine sparso?

- Come si fa a sapere quali (altri) eventi può gestire una widget? (Sugg: leggi la documentazione)
- Dove sta la documentazione? (qui ci sono le dispense del prof, su <https://docs.wxpython.org> trovi la documentazione ufficiale)
- E... se voglio mettere 2 pulsanti? (fra qualche riga ci arriviamo)
- E se voglio mettere un pulsante... piccolo? (in realtà lo sai già...)
- E... se voglio far fare qualcos'altro al mio programma quando clicco il pulsante? (sugg: studia!)

Basta così con le domande per adesso... prima di passare a presentare tutte le widgets vediamo altre due cose molto importanti sugli eventi


<!-- ############################################################################################################## -->
## Identificare le widgets


Immaginate una applicazione con tanti pulsanti (una tastiera virtuale, una calcolatrice, etc...). Capita spesso in questi casi di collegare
più oggetti alla stessa funzione. Ma come si può distinguere quale pulsante (o più in generale quale widget) ha scatenato l'evento?

***Come si fa ad identificare una widget?***


> Ogni oggetto grafico wxPython dispone di un **ID** identificativo!


Vediamo un semplice esempio con due pulsanti che cliccati richiamano entrambi la stessa funzione!


``` python
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

La libreria wxPython identifica in maniera automatica tutte le widget con un ID sempre diverso e sempre **negativo**: 
la prima widget creata sarà quella con ID -1, la seconda quella con ID -2 e così via...

**Se volete impostare voi l'ID di una widget usate solo numeri positivi crescenti**: in questo modo sarete sicuri di non fare
confusione con gli ID assegnati automaticamente alle widget da wxPython e di non sbagliarvi da soli mettendo due volte lo stesso ID!


<!-- ############################################################################################################## -->
## Bloccare gli eventi


Può essere utile sapere che in alcuni casi possiamo bloccare gli eventi
e le naturali risposte delle applicazioni ad essi: il caso tipico in
programmazione per questa problematica è quando l'utente prova a
chiudere un editor con il file non ancora salvato! In quel caso
l'applicazione blocca la chiusura suggerendo di salvare prima il file!
Nella libreria wxPython è possible bloccare un evento con la funzione
**Veto()**, da applicare all'evento da bloccare.

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
        else:
            # blocca l'evento
            evt.Veto()

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


