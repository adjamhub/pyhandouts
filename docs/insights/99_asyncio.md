# asyncio

<!-- tutorial basato su https://medium.com/pythoniq/master-asyncio-in-python-a-comprehensive-step-by-step-guide-4fc2cfa49925  -->

Prima c'erano Python `threading` e Python `multiprocessing`... o librerie di terze parti come `Twisted` e `Tornado`... adesso
si utlizza `asyncio`.

La libreria `asyncio` è predefinita in Python sin dalla versione `3.7`!!! Se volete utilizzarla (e in molti casi... fate molto bene!!)
dovete solo aver cura di avere una versione recente di Python installata.

!!! note "Documentazione ufficiale"

    La documentazione ufficiale di `asyncio` è disponibile nella documentazione ufficiale di Python. Link veloce per i più pigri:
    <a href="https://docs.python.org/3/library/asyncio.html" target="_blank">Clicca qui!</a>.<br>
    Questo piccolo tutorial serve solo come introduzione al discorso...


`asyncio` è un framework asincrono di I/O che permette di scrivere codice concorrente tramite la sintassi `await` e `async`.
Si basa sui concetti di **event loop** e di **coroutines** per la gestione delle operazioni asincrone.<br>
Vediamoli:

## Event Loop
L'**event loop** (letteralmente, il ciclo degli eventi) è il concetto alla base del modello di esecuzione di asyncio.
Quando viene attivato, esso si occupa di pianificare e gestire le operazioni di I/O e le attività (asincrone) definite nelle coroutines e di alternarsi
con il sistema operativo nel controllo dell'hardware: in questo modo si mantiene il sistema fluido (cioè in esecuzione di operazioni non bloccanti).

## Coroutines
Le **coroutine**(s) non sono altro che funzioni asincrone, ovvero definite con la sintassi `async def`. La loro caratteristica principale, rispetto
alle normali funzioni è che hanno la facoltà di restituire il controllo all'*event loop* tramite l'utilizzo della keyword `await`, permettendo ad altre
operazioni di essere eseguite nel frattempo.


``` py title="Esempio base: saluto asyncrono"
import asyncio

async def saluta(nome, delay):
    """ Aspetta {delay} secondi (asincrono) e poi saluta {nome}"""
    await asyncio.sleep(delay)
    print(f"Ciao, {nome}!")

async def main():
    """ esegue TOT operazioni 'contemporaneamente'!!! """

    # asyncio.gather permette di eseguire 'insieme' un gruppo di operazioni asincrone
    await asyncio.gather(
        saluta("Andrea", 2),
        saluta("Barbara", 1),
        saluta("Cristina", 3),
    )

if __name__ == "__main__":
    # codice per avviare l'event loop
    asyncio.run(main())
```

## Task(s)
Un **task asyncio** è una coroutine in programma per l'esecuzione e gestita in maniera indipendente.

``` py title="Creazione ed esecuzione di task asincroni"
import asyncio

async def operazioneLunga(n):
    print(f"Inizio operazione {n}")
    await asyncio.sleep(n)
    print(f"Fine operazione {n}")

async def main():
    # asyncio.create_task... fa quello che dice!
    task1 = asyncio.create_task(operazioneLunga(2))
    task2 = asyncio.create_task(operazioneLunga(4))

    # aspetta il completamento dei task
    await task1
    await task2

if __name__ == "__main__":
    asyncio.run(main())
```

## Gestione errori e Timeout

Con tutta la buona volontà di portare avanti e terminare più operazioni possibili contemporaneamente, è praticamente
certo che prima o poi qualcosa andrà storto... bisogna rendere il codice più robusto possibile, ovvero in grado di gestire al meglio
ogni eventuale problematica incontrata.

Le soluzioni offerte da Python sono tipicamente due:

- la gestione delle eccezioni tramite il codice `try... except`: questa vale sempre!!!
- l'impostazione di un timeout per le coroutine in esecuzione (oltre il quale non possono andare): questa vale solo per asyncio!!!

Per gestire ogni problema al meglio bisognerebbe considerare entrambi gli approcci. Vediamo un esempio di codice semplice e ben commentato!


``` py title="Se non finisci entro 2 secondi, muori!"
import asyncio

async def fai_in_fretta():
    """ aspetta 5 secondi e via! """
    try:
        await asyncio.sleep(5)
        print("Fatto!")
    except asyncio.CancelledError:
        print("Operazione cancellata!!!")

async def main():
    task = asyncio.create_task(fai_in_fretta())

    try:
        # concede al massimo 2 secondi di tempo per l'esecuzione del task
        await asyncio.wait_for(task, timeout=2)
    except asyncio.TimeoutError:
        print("Time OUT")
        task.cancel()
        await task

if __name__ == "__main__":
    asyncio.run(main())
```



## Asyncio Networking

La libreria `asyncio` rende molto semplice lavorare con le operazioni I/O di rete. L'esempio sotto presenta un **echo server**
(una applicazione che ripete tutto quello che dici) che utilizza le classi asyncio `StreamReader` e `StreamWriter`


``` py title="async(io) echo server"
import asyncio

async def echo(reader, writer):
    while True:
        data = await reader.read(100)
        if not data:
            break

        writer.write(data)
        await writer.drain()

    writer.close()
    await writer.wait_closed()

async def main():
    server = await asyncio.start_server(echo, "127.0.0.1", 8888)

    async with server:
        await server.serve_forever()

if __name__ == "__main__":
    asyncio.run(main())
```


!!! tip "Debugging"
    Per fare il debug di una applicazione basata su asyncio, ti basta inserire la riga
    `asyncio.set_debug(True)` prima di eseguire l'*event loop*. <br>
    Fornirà all'applicazione la possibilità di essere controllata al meglio!!!



## 3rd party libraries

Vista la grande qualità per cui asyncio si è subita distinta, sono immediatamente state implementate librerie specifiche, basate su di essa per i casi
più disparati:

- `aiohttp`, una libreria che implementa framework HTTP client/server
- `aiomysql`, una libreria asincrona per interagire con il database MySQL e MariaDB
- `AsyncSSH`, una libreria asincorna per implementare un client o un server SSH
- `aiodns`, un semplice DNS resolver basato su asyncio
- `aioping`, una libreria asincrona per il protocollo ICMP (su cui si basa ping)
- `asynctest`, una libreria per i test su funzioni e librerie asincrone-

Molti (ma non tutti) sono genericamente indicati su questo strano sito:
<a href="https://github.com/timofurrer/awesome-asyncio" target="_blank">Awesome AsyncIO</a>.
Trovare esempi in rete di utilizzo di queste librerie diventa ogni giorno più facile.


## Best Practices


- Usa `async def` per definire una coroutine e `await` per metterla in pausa.
- Usa `asyncio.gather()` o `asyncio.create_task()` per eseguire coroutine in maniera concorrente.
- Gestisci le eccezioni nei blocchi `try... except`.
- Usa `asyncio.wait_for()` per impostare timeout alle coroutines.
- Chiudi sempre le risorse, come i file o le connessioni di rete, quando non le usi più.
- Usa librerie di terze parti basate su asyncio per le migliori performance su compiti specifici.
- Usa il *debug mode* di asyncio per controllare il codice.

<br>
<br>
