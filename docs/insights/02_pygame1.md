# PyGame

`pygame` è un modulo Python, disponibile su `PyPi` che implementa la <a href="https://www.libsdl.org/" target="_blank">libreria SDL</a>.

Questa fornisce accesso cross-platform alle componenti hardware multimediali, come suono,
video, mouse, tastiera, joystick, etc...

Per installare la libreria `pygame` su Thonny, cercate dal sistema di gestione dei pacchetti
il nome corrispondente e cliccate (incredibilmente) INSTALLA!!!


<!-- ################################################################################# -->
## Fare cose con PyGame

Cominciamo dal programma assolutamente minimo, che però in realtà contiene già parecchie
cosine su cui riflettere!

``` py
# Primo programma

# importa ed inizializza la libreria pygame
import pygame

pygame.init()

# lo screen
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

    # Update display content
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

Una cosa che a me piace molto è quella di dare la possibilità di uscire semplicemente premendo il tasto `ESC`: questa funzionalità si può ottenere aggiungendo opportunamente il seguente codice!

``` py
# DENTRO il FOR che gestisce gli eventi...
# Se l'evento è la pressione di un tasto...
# ... e il tasto è il tasto ESC.. esc(i)!
if event.type == pygame.KEYDOWN:
    if event.key == pygame.K_ESCAPE:
        running = False
```

Ragionate su come inserire il codice e testatelo finché non funziona! Quando premi ESC, il gioco deve terminare!

!!! tip "suggerimento"

    Potrebbe essere carino impostare l'uscita dal gioco con il tasto Q (QUIT), oppure
    con un tasto a propria scelta! 
    
    L'elenco completo dei codici relativi ai tasti si trova
    qui: [pygame keys](https://www.pygame.org/docs/ref/key.html#module-pygame.key)
    

## Aggiungere scritte

``` py
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH,SCREEN_HEIGHT))

# Definizione dei font: Quello "grosso" e quello "giusto"
Titlefont = pygame.font.SysFont('Impact', 70)
Normalfont = pygame.font.SysFont('Impact', 30)

# oggetto_testo = oggetto_font.render(stringa, True (non serve a una gibba), colore, sfondo)
game_end = Titlefont.render("Hai Perso!", True, "red","black")
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


## Aggiungere forme

``` py
import pygame

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

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

``` py
import pygame   

pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) 
pygame.display.set_caption("Rettangolo che si muove") 

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
        if event.type == pygame.KEYDOWN and event.key == pygame.K_s:
            speed += 1
        if event.type == pygame.KEYDOWN and event.key == pygame.K_a:
            speed -= 1
            
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
    pygame.draw.rect(screen, "red", (x, y, w, h)) 
    pygame.display.flip()  

pygame.quit()
```

## Nemici e Collisioni


In questa parte del tutorial cercherò di aggiungere nemici in posti più o meno casuali e di controllare le collisioni fra
questi e il giocatore!

``` py
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
        if event.type == pygame.KEYDOWN and event.key == pygame.K_s:
            speed += 1
        if event.type == pygame.KEYDOWN and event.key == pygame.K_a:
            speed -= 1
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


## Lavorare con le Immagini

Questo pezzetto di codice presuppone che abbiate nella stessa cartella due immagini:

- pere.jpg, lo sfondo con le pere
- mosca.png, la mosca con bordo trasparente

``` py
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


## Aggiungere suoni

Per far vedere come fermare e far ripartire una musichetta ho implementato anche la pausa :)

``` py
import pygame

pygame.init()   

pygame.mixer.init() 
pygame.mixer.music.load("zanzara.mp3") 
pygame.mixer.music.set_volume(0.5) 
pygame.mixer.music.play()

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


## Aggiungere pulsanti



<br>
<br>
<br>



