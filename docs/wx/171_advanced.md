# Widgets avanzate


In questo capitolo andiamo ad introdurre alcune widgets molto potenti per realizzare programmi
specializzati in determinati ambiti! 

Iniziamo a gustare la potenza della OOP e delle librerie integrate!!!



<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## Griglia per foglio di calcolo


Modulo wx.grid


---

**Esercizio: Foglio Elettronico**

blah blah

---

**Esercizio: Battleship**

blah blah


---


<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## Editor di documenti stiloso


Modulo wx.stc


---

**Esercizio: Blocco Note con wx.stc**

blah blah

---


<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## Browser per la navigazione internet


Modulo wx.html2


``` python title="MiniBrowser" hl_lines="2 15"
import wx
import wx.html2

APP_NAME = "Mini Browser"

class Finestra(wx.Frame):

    def __init__(self):
        super().__init__(None, title=APP_NAME)
        panel = wx.Panel(self)

        mainLayout = wx.BoxSizer(wx.VERTICAL)
        
        # La WEBVIEW
        self.browser = wx.html2.WebView.New(panel)
        self.browser.Bind(wx.html2.EVT_WEBVIEW_LOADED, self.hoCaricato)
        mainLayout.Add(self.browser, proportion=1, flag=wx.ALL|wx.EXPAND, border=5)
        
        # la pagina iniziale
        self.browser.LoadURL("https://www.adjam.org/")

        panel.SetSizer(mainLayout)
        self.SetSize(1200,800)
        self.Centre()

    def hoCaricato(self, evt):
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

---

**Esercizio: Browser completo, con cronologia e bookmarks**

blah blah

---

**Esercizio: PDFViewer**

blah blah


---



<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## Media Player


Modulo wx.media


---

**Esercizio: Video Player**

blah blah

---

**Esercizio: Audio Player**
  
blah blah
    

---


<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## Rich Text Ctrl 


Modulo wx.richtext


---

**Esercizio: Word :)**

blah blah

---




<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## DA SISTEMARE

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

<br>
<br>
<br>
