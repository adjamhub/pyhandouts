# PyGame

`pygame` è un modulo Python, disponibile su `PyPi` che implementa la <a href="https://www.libsdl.org/" target="_blank">libreria SDL</a>.

Questa fornisce accesso cross-platform alle componenti hardware multimediali, come suono,
video, mouse, tastiera, joystick, etc...

Per installare la libreria `pygame` su Thonny, cercate dal sistema di gestione dei pacchetti
il nome corrispondente e cliccate (incredibilmente) INSTALLA!!!


!!! note "PyGame: sito e documentazione ufficiale"

    Attualmente non ve ne frega nulla, me ne rendo conto. Ma lasciatemi scrivere qui un paio di info utili!
    
    Il sito ufficiale della libreria PyGame è [https://www.pygame.org/](https://www.pygame.org/)

    Il sito della documentazione ufficiale è [https://www.pygame.org/docs/](https://www.pygame.org/docs/)



<!-- ################################################################################# -->
## Fare cose con PyGame

Cominciamo dal programma assolutamente minimo, che però in realtà contiene già parecchie
cosine su cui riflettere!

``` py title="Primo programma"
# importa ed inizializza la libreria pygame
import pygame

pygame.init()

# lo screen (con titolo)
screen = pygame.display.set_mode( (800, 600) )
pygame.display.set_caption("Il mio primo gioco con PyGame!")

# facile...
running = True

while running:
    # serve a gestire la X di chiusura in alto
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
            
    # colora lo schermo di verde
    screen.fill("green")

    # aggiorna il contenuto dello schermo
    pygame.display.flip()

# Chiude pygame
pygame.quit()
```

Questo codice crea un rettangolo verde, di grandezza 800x600 pixel, con titolo "Il mio primo gioco con PyGame!".

Quando clicchi sulla X rossa in alto, il gioco si chiude tranquillamente. Per verificare che sia così, potreste aggiungere una print in fondo. Oppure provare a modificare colore e dimensione della finestra principale!

Vediamo pezzo per pezzo cosa abbiamo scritto:

- `import pygame`... ormai dovremmo aver capito. Importa la libreria pygame

- `pygame.init()`. Inizializza la libreria pygame. Permette il funzionamento di tutto il resto

- `screen ...` è una variabile che contiene una `PyGame Surface`, una superficie (un... rettangolo) gestito da PyGame per fare le cose. Questo in particolare, sarà il nostro schermo.

- `screen.fill("color")`: prende come parametro una stringa o una tupla RGB. Colora lo sfondo della surface.

- `pygame.display.flip()`: aggiorna il contenuto dello schermo. Senza questa funzione ripetuta nel loop non funziona nulla!!!

Per adesso basta così con le spiegazioni.... proviamo ad andare avanti con il codice!!!


## Uscire con il tasto ESC

Una cosa che a me piace molto è quella di dare la possibilità di uscire semplicemente premendo il tasto `ESC`: 
questa funzionalità si può ottenere aggiungendo il seguente codice!


``` py title="Uscire con il tasto ESC" hl_lines="14 15 16 17 18"
import pygame

pygame.init()

screen = pygame.display.set_mode( (800, 600) )
pygame.display.set_caption("Il mio primo gioco con PyGame!")

running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        # Se l'evento è la pressione di un tasto...
        # ... e il tasto è il tasto ESC.. esc(i)!
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                running = False
            
    screen.fill("green")
    pygame.display.flip()

pygame.quit()
```


Ragionate su come modificare il codice per fare qualunque cosa alla pressione di un tasto qualsiasi!


!!! tip "suggerimento"

    Potrebbe essere carino impostare l'uscita dal gioco con il tasto Q (QUIT), oppure
    con un tasto a propria scelta! 
    
    L'elenco completo dei codici relativi ai tasti si trova
    qui: [pygame keys](https://www.pygame.org/docs/ref/key.html#module-pygame.key)
    

## Aggiungere scritte

In questa parte del tutorial, vedremo come è possibile aggiungere una scritta (o più di una) su pygame.

Si tratta semplicemente di selezionare un oggetto font (Ad esempio "Times", 12) e utilizzarlo per fare il render (cioè il disegno) della scritta che ci interessa. 
Il risultato sarà un `rettangolo` di una certa dimensione e colore, che andrà disegnato (con `blit`) su un qualche punto dello schermo.


``` py title="Aggiungere scritte" hl_lines="11 12 13 15 16 17 29 30"
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH,SCREEN_HEIGHT))
pygame.display.set_caption("Aggiungere scritte") 

# Definizione dei font: Quello "grosso" e quello "giusto"
Titlefont = pygame.font.SysFont('Impact', 70)
Normalfont = pygame.font.SysFont('Impact', 30)

# oggetto_testo = oggetto_font.render(stringa, True, colore, sfondo (opzionale) )
game_end = Titlefont.render("Hai Perso!", True, "red")
close_tip = Normalfont.render("Click ESC to exit", True, "blue","yellow")

running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
            running = False
            
    screen.fill("white") 
    screen.blit(game_end, (100,100))
    screen.blit(close_tip, (100,300))
    pygame.display.flip()

pygame.quit()
```

## Aggiungere pulsanti


È possibile creare pulsanti semplicemente modificando il comportamento delle scritte in due modi:

1. reagendo (ad esempio, cambiando colore) quando ci passi sopra con il mouse
2. eseguendo una qualche operazione quando viene fatto click sopra di esse

Il codice sotto fa esattamente questo!

- Crea una scritta bianca su sfondo rosso disegnata in un opportuno rettangolo inserita in qualche punto sullo schermo.

- Modifica il colore di sfondo del rettangolo che rappresenta il pulsante quando il mouse ci passa sopra (nell'esempio ho scelto il blu)

- Reagisce quando si clicca nell'area del pulsante eseguendo una qualche porzione di codice (in questo caso, semplicemente facendo ESCI!)


``` py title="Aggiungere Pulsanti" hl_lines="10 11 12 18 19 26 27 28 29 33 34 35 36 37"
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

font = pygame.font.SysFont('Arial',30) 
textRect = font.render('Esci' , True , "white") 
buttonRect = pygame.Rect(SCREEN_WIDTH // 2, SCREEN_HEIGHT //2, 140, 40)
    
running = True

while running:

    # posizione del mouse
    mPos = pygame.mouse.get_pos() 
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
            running = False
        # quando clicchi SOPRA il pulsante... FAI QUALCOSA!!!
        if event.type == pygame.MOUSEBUTTONDOWN: 
            if buttonRect.collidepoint(mPos):
                running = False
                
    screen.fill("yellow")
    
    # ANIMAZIONE DEL PULSANTE (cambia colore quando ci passi sopra)
    buttonColor = "red"
    if buttonRect.collidepoint(mPos):
        buttonColor = "blue"
    button = pygame.draw.rect(screen,buttonColor,buttonRect) 
    
    screen.blit(textRect , (SCREEN_WIDTH //2 + 50, SCREEN_HEIGHT// 2) )
    
    pygame.display.flip()


pygame.quit()
```


## Aggiungere forme geometriche


L'esempio di questo pezzo di codice ha un puro scopo didattico, cioè quello di mostrare come si creano e posizionano
alcune figure geometriche su pygame.

Se pensate ad un gioco e avete bisogno di una figura geometrica particolare... adesso non potete fingere di non sapere come si fa!!!!



``` py title="Aggiungere forme geometriche" hl_lines="22 23 24 26 27 28 30 31 32 34 35 36 38 39 40"
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Aggiungere forme geometriche") 

running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
            running = False
            
    screen.fill("white")
    
    # cerchio ROSSO di raggio 80 al centro dello screen
    # c è il "rettangolo" che contiene il cerchio disegnato
    c = pygame.draw.circle(screen, "red", (SCREEN_WIDTH//2, SCREEN_HEIGHT//2), 80)
    
    # rettangolo BLUE che va dal punto (600,400) lungo 180, largo 100
    # r è il rettangolo che contiene il rettangolo disegnato
    r = pygame.draw.rect(screen, "blue", (600, 400, 180, 100))
    
    # linea VERDE dal punto... al punto ... di spessore ...
    # l è il "rettangolo" che contiene la linea disegnata 
    l = pygame.draw.line(screen, "green", (600, 100), (700, 300), 8)
    
    # ellisse VIOLA contenuto nel rettangolo che parte da (100,400) lungo 60, largo 90. Di spessore...
    # el è il rettangolo che contiene l'ellisse disegnata
    el = pygame.draw.ellipse(screen, "purple" , (100, 400, 60, 90), 8)
    
    # poligono GIALLO (riempito) che collega i punti...
    # pol è il rettangolo che contiene il poligono disegnato
    pol = pygame.draw.polygon(screen, "yellow",((146, 0), (291, 106),(236, 277), (56, 277), (0, 106)))
    
    pygame.display.flip()

pygame.quit()
```


## Muovere un rettangolo


In questa parte del tutorial iniziamo davvero a fare le cose sul serio!!!

In questo pezzo di codice vediamo come si muove un rettangolo dentro allo schermo comandandolo con le frecce!

Il mio rettangolo parte dal centro (guarda la posizione iniziale) ed ha un *movimento di coda* in quanto gira il retro 
quando si curva in una direzione (guarda come inverto le dimensioni w,h).

Alla fine ogni volta si ripittura lo schermo di nero e si disegna il rettangolino nella posizione ove dovrebbe trovarsi.


``` py title="Muovere un rettangolo" hl_lines="11 12 13 15 16 17 19 20 34 35 36 37 38 39 40 41 42 43 44 45 48"
import pygame   

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) 
pygame.display.set_caption("Rettangolo che si muove") 

# posizione iniziale
x = SCREEN_WIDTH // 2
y = SCREEN_HEIGHT // 2

# dimensioni rettangolo
w = 40
h = 20

# velocità di spostamento
speed = 8

running = True

while running: 
    pygame.time.delay(10) 
    
    for event in pygame.event.get(): 
        if event.type == pygame.QUIT: 
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
            running = False
            
    keys = pygame.key.get_pressed() 
    if keys[pygame.K_LEFT] and x > 0: 
        w,h = 40,20
        x -= speed 
    if keys[pygame.K_RIGHT] and x < SCREEN_WIDTH - w: 
        w,h = 40,20
        x += speed 
    if keys[pygame.K_UP] and y > 0: 
        w,h = 20,40
        y -= speed 
    if keys[pygame.K_DOWN] and y < SCREEN_HEIGHT - h: 
        w,h = 20,40
        y += speed 
    
    screen.fill("black")
    player = pygame.draw.rect(screen, "red", (x, y, w, h)) 
    pygame.display.flip()  

pygame.quit()
```

Se per voi è tutto chiaro quello che succede qui sopra, vi sfido ad aggiungere una funzionalità: il controllo della velocità! Con un tasto (a vostra scelta) si accelera,
con un altro si rallenta!

Buon divertimento!!!


## Nemici e Collisioni


Adesso è il momento di aggiungere dei nemici... o meglio... degli ostacoli! Questi appariranno ogni tanto in posti più o meno casuali 
e noi andremo a controllare le (eventuali) collisioni fra il giocatore e questi!

Per far funzionare una cosa del genere dobbiamo organizzare un pò di cose:

1. un evento che capiti ogni TOT ms che ci permetta, quando si scatena, di fare qualcosa (ad esempio: aggiungere un nemico)

2. una lista che ci ricordi l'elenco (soprattutto... la posizione) di **tutti i nemici presenti** sul campo di gioco

3. per ogni elemento nemico, il controllo della eventuale collisione con il giocatore

Osservate bene il codice qui sotto!

``` py title="Nemici e Collisioni" hl_lines="12 13 14 15 17 18 38 39 40 41 60 61 62 63 64 65 66 67 68"
import pygame   
import random

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) 
pygame.display.set_caption("Rettangolo che si muove con nemici a caso") 

# crea un nuovo (tipo di) evento (da gestire nel for degli eventi sotto)
# che verrà scatenato ogni TOT ms
ADD_ENEMY = pygame.USEREVENT + 1
pygame.time.set_timer(ADD_ENEMY, 1000)

# l'elenco dei nemici
enemies = []

# info utili per il rettangolo giocatore:
# (x,y) la posizione, (w,h) la dimensione, speed... indovina!!!!!
x = SCREEN_WIDTH // 2
y = SCREEN_HEIGHT // 2
w = 40
h = 20
speed = 8

running = True

while running: 
    pygame.time.delay(10) 
    
    for event in pygame.event.get(): 
        if event.type == pygame.QUIT: 
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
            running = False
        if event.type == ADD_ENEMY:
            posx = random.randint(0,SCREEN_WIDTH - 20)
            posy = random.randint(0,SCREEN_HEIGHT - 20)
            enemies.append( (posx,posy) )
            
    keys = pygame.key.get_pressed() 
    if keys[pygame.K_LEFT] and x > 0: 
        w,h = 40,20
        x -= speed 
    if keys[pygame.K_RIGHT] and x < SCREEN_WIDTH - w: 
        w,h = 40,20
        x += speed 
    if keys[pygame.K_UP] and y > 0: 
        w,h = 20,40
        y -= speed 
    if keys[pygame.K_DOWN] and y < SCREEN_HEIGHT - h: 
        w,h = 20,40
        y += speed 
    
    screen.fill("black") 
    player = pygame.draw.rect(screen, "red", (x, y, w, h)) 
    
    # in questo caso i nemici sono fermi: sono ostacoli
    for posx,posy in enemies:
        # en è il rettangolo disegnato 
        en = pygame.draw.rect(screen, "white", (posx, posy, 20, 20)) 
        
        # se questo rettangolo "collide" con il punto (x,y) ove si trova il giocatore...
        if player.colliderect(en):
            print("HAI PERSO!")
            running = False

    pygame.display.flip()  

pygame.quit() 
```

!!! tip "Collisioni!!"

    Puoi controllare se un punto attraversa un'area, se due rettangoli si sovrappongono, se un punto passa dentro un rettangolo... praticamente ogni
    tipo di incrocio fra oggetti!!!
    
    la documentazione per ognuno di questi la trovi qui: <a href="https://www.pygame.org/docs/ref/rect.html" target="_blank">Documentazione pygame.Rect</a>


## Lavorare con le Immagini

Questo pezzetto di codice presuppone che abbiate nella stessa cartella due immagini:

- pere.jpg, lo sfondo con le pere
- mosca.png, la mosca con bordo trasparente

``` py title="lavorare con le immagini" hl_lines="11 12 14 15 47 48 50 51"
import pygame

pygame.init()   

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) 
pygame.display.set_caption("Lavorare con le Immagini") 

imgSfondo = pygame.image.load("pere.jpg") 
imgSfondo = pygame.transform.scale(imgSfondo,(SCREEN_WIDTH,SCREEN_HEIGHT))

imgMosca = pygame.image.load("mosca.png") 
imgMosca = pygame.transform.scale(imgMosca,(30,30))

x = SCREEN_WIDTH // 2
y = SCREEN_HEIGHT // 2

width = 30
height = 30

speed = 8

running = True

while running:  
    
    pygame.time.delay(10)
    
    for event in pygame.event.get(): 
        if event.type == pygame.QUIT: 
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
            running = False

    keys = pygame.key.get_pressed() 
    if keys[pygame.K_LEFT] and x > 0: 
        x -= speed 
    if keys[pygame.K_RIGHT] and x < SCREEN_WIDTH - width: 
        x += speed 
    if keys[pygame.K_UP] and y > 0: 
        y -= speed 
    if keys[pygame.K_DOWN] and y < SCREEN_HEIGHT - height: 
        y += speed
    
    # invece di screen.fill("white")
    screen.blit(imgSfondo,(0,0) )
    
    # invece di pygame.draw.rect(screen, "red", (x, y, width, height)) 
    screen.blit(imgMosca,(x,y))
    
    pygame.display.flip() 

# 
pygame.quit()
```

!!! note "Modificare le immagini"

    Sarebbe fighissimo se la mosca si girasse nella direzione opportuna di volo!!! Per farlo non serve modificare l'immagine (il file "mosca.png") 
    ma solo l'oggetto immagine (imgMosca).
    
    Per sapere come, controlla tutta la documentazione qui: <a href="https://www.pygame.org/docs/ref/transform.html" target="_blank">Documentazione pygame.transform</a>


## Aggiungere suoni

Per far vedere come fermare e far ripartire una musichetta ho implementato anche la pausa :)

``` py title="Aggiungere suoni" hl_lines="5 6 7 8 45 48"
import pygame

pygame.init()   

pygame.mixer.init() 
pygame.mixer.music.load("zanzara.mp3") 
pygame.mixer.music.set_volume(0.5) 
pygame.mixer.music.play()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) 
pygame.display.set_caption("Lavorare con le Immagini e i suoni") 

imgSfondo = pygame.image.load("pere.jpg") 
imgSfondo = pygame.transform.scale(imgSfondo,(SCREEN_WIDTH,SCREEN_HEIGHT))
imgMosca = pygame.image.load("mosca.png") 
imgMosca = pygame.transform.scale(imgMosca,(30,30))

x = SCREEN_WIDTH // 2
y = SCREEN_HEIGHT // 2

width = 30
height = 30

speed = 8

running = True
paused = False

while running:  
    
    pygame.time.delay(10)
    
    for event in pygame.event.get(): 
        if event.type == pygame.QUIT: 
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
            running = False
        # PREMI "P" per mettere in pausa (o uscire dalla pausa)
        if event.type == pygame.KEYDOWN and event.key == pygame.K_p:
            if paused:
                paused = False
                pygame.mixer.music.play()
            else:
                paused = True
                pygame.mixer.music.pause()
            
    if paused:
        continue

    keys = pygame.key.get_pressed() 
    if keys[pygame.K_LEFT] and x > 0: 
        x -= speed 
    if keys[pygame.K_RIGHT] and x < SCREEN_WIDTH - width: 
        x += speed 
    if keys[pygame.K_UP] and y > 0: 
        y -= speed 
    if keys[pygame.K_DOWN] and y < SCREEN_HEIGHT - height: 
        y += speed
    
    # invece di screen.fill("white")
    screen.blit(imgSfondo,(0,0) )
    
    # invece di pygame.draw.rect(screen, "red", (x, y, width, height)) 
    screen.blit(imgMosca,(x,y))
    
    pygame.display.flip() 

# 
pygame.quit()
```


<br>
<br>
<br>



