# Python requests

Il venerabile modulo `requests` è lo standard *de facto* in Python per realizzare, gestire, analizzare richieste e risposte HTTP.
Questa libreria non fa parte della dotazione ufficiale standard e va quindi installata, tramite l'interfaccia di Thonny o tramite il
comando:

``` sh
pip install requests
```

!!! tip "Il protocollo HTTP"

    Se siete qui a studiare il modulo `requests`, si presuppone abbiate
    già una discreta conoscenza del protocollo HTTP.
    
    In caso contrario... molte cose rimarranno oscure e/o meccaniche.
    

La sintassi di base del modulo è strutturata nel modo seguente:

``` python
import requests

# method è una funzione generica per uno dei metodi HTTP: get, post, put, head ... etc...
response = requests.method( URL , options )
```

## Richieste GET

Vedi: https://realpython.com/python-requests/

<br>
<br>
<br>

