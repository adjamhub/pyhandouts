# Esercizi su GUI complete


## Editor di testo (basato su wx.stc)




### Esercizio Blocco Note


### Esempio di stampa 


---

## Browser (basato su wx.html2)


``` python title="MiniBrowser" hl_lines="2 30"
import wx
import wx.html2

APP_NAME = "Mini Browser"

class Finestra(wx.Frame):

    def __init__(self):
        super().__init__(None, title=APP_NAME)
        panel = wx.Panel(self)
        
        mainLayout = wx.BoxSizer(wx.VERTICAL)
        
        # prima riga -------------------------------------------------
        box1 = wx.BoxSizer(wx.HORIZONTAL)
        
        # la URLBAR e il PULSANTE VAI!!!
        self.urlbar = wx.TextCtrl(panel, value="", style=wx.TE_PROCESS_ENTER)
        self.button = wx.Button(panel,label = "vai")
        
        box1.Add(self.urlbar, proportion=1, flag=wx.ALL, border=5)
        box1.Add(self.button, proportion=0, flag=wx.ALL, border=5)
        
        mainLayout.Add(box1, proportion=0, flag=wx.EXPAND, border=0)
        
        # seconda riga -------------------------------------------------        
        box2 = wx.BoxSizer(wx.HORIZONTAL)
        
        # La WEBVIEW
        self.browser = wx.html2.WebView.New(panel)
        self.browser.Bind(wx.html2.EVT_WEBVIEW_LOADED, self.hoCaricato)
        
        box2.Add(self.browser, proportion=1, flag=wx.ALL|wx.EXPAND, border=5)        
        mainLayout.Add(box2, proportion=1, flag=wx.EXPAND, border=0)

        panel.SetSizer(mainLayout)
        
        # le ultime cose...
        self.button.Bind(wx.EVT_BUTTON, self.loadSite)
        self.urlbar.Bind(wx.EVT_TEXT_ENTER, self.loadSite)


        # la pagina iniziale
        self.caricaSito("https://www.adjam.org/")

        self.SetSize(1200,800)
        self.Centre()

    def loadSite(self,evt):
        url = self.urlbar.GetValue()
        
        # semplice "sanificazione"
        if not url.startswith("http"):
            url = "http://" + url
            
        self.caricaSito(url)
        return

    def caricaSito(self, url):
        self.browser.LoadURL(url)
        return
        
    def hoCaricato(self, evt):
        self.urlbar.SetValue(self.browser.GetCurrentURL())
        self.SetTitle(APP_NAME + " - " + self.browser.GetCurrentTitle())
        return

# ----------------------------------------
if __name__ == "__main__":
    app = wx.App()
    app.SetAppName(APP_NAME)
    
    window = Finestra()
    window.Show()
    
    app.MainLoop()
```


### Esercizio Browser completo, con cronologia e bookmarks
    
### Esercizio PDFViewer



---

## MultiMedia Player (basato su wx.media)


### Video Player


### Audio Player
  
    

---

## Griglia (basato su wx.grid)

### Foglio Elettronico

### Battleship
 

---

## Rich Text Ctrl (basato su wx.richtext)


### Word :)


---
## DA SISTEMARE (DA QUI IN POI!!!)

- wx.ListCtrl

    - File manager ??

---

- DateTime Widgets

    - calendario
    - orologio
    - agenda

---

- Visualizzatore Immagini

    - GIF Viewer (con play/pause/stop)
    - SlideShow (temporizzato)
    - SlideShow (con pulsanti AVANTI/INDIETRO)
