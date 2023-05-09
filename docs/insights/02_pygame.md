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
    

## Aggiungiamo una pallina mobile al suo interno

Questa pallina sarà posizionata dentro lo schermo e sarò possibile muoverla con i tasti freccia!

``` py
# Primo programma

# importa ed inizializza la libreria pygame
import pygame


pygame.init()

SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

# lo screen
screen = pygame.display.set_mode( (SCREEN_WIDTH, SCREEN_HEIGHT) )
pygame.display.set_caption("Il mio primo gioco con PyGame!")

# -----------------------------------------------------------------------
# la pallina
pallina = pygame.sprite.Sprite()
pallina.surf = pygame.Surface((50, 50))
pallina.surf.fill("green")
pallina.rect = pygame.draw.circle(pallina.surf, "red", (25,25), 25)
# -----------------------------------------------------------------------

# facile...
running = True

while running:
    # serve a gestire la X di chiusura in alto
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
            
        # quando premi ESC, esc(i)!!!
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                running = False

    # L'insieme dei tasti premuti dall'utente..
    pressed_keys = pygame.key.get_pressed()
    
    # Qui si muove la pallina a seconda delle frecce cliccate.
    # Attenti al sistema di riferimento!!!
    if pressed_keys[pygame.K_UP]:
        pallina.rect.move_ip(0, -1)

    if pressed_keys[pygame.K_DOWN]:
        pallina.rect.move_ip(0, 1)

    if pressed_keys[pygame.K_LEFT]:
        pallina.rect.move_ip(-1, 0)

    if pressed_keys[pygame.K_RIGHT]:
        pallina.rect.move_ip(1, 0)
    
    # Questo codice MANTIENE LA PALLINA DENTRO LO SCHERMO!!!
    if pallina.rect.left < 0:
        pallina.rect.left = 0

    if pallina.rect.right > SCREEN_WIDTH:
        pallina.rect.right = SCREEN_WIDTH

    if pallina.rect.top <= 0:
        pallina.rect.top = 0

    if pallina.rect.bottom >= SCREEN_HEIGHT:
        pallina.rect.bottom = SCREEN_HEIGHT

                
    # colora lo schermo di verde
    screen.fill("green")

    # disegna gli oggetti sullo schermo
    screen.blit(pallina.surf, pallina.rect)

    # Flip the display
    pygame.display.flip()


# Chiude pygame
pygame.quit()

```
<br>
<br>
<br>

