# Python e i numeri reali

Python sembra fare parecchi errori per calcolare i numeri con la
virgola... non sembra preciso... guardate questo esempio:


    1.1 + 2.2 == 3.3
    False (ma come False???)


Ho capito: Python è scemo!

La dispensa è finita :)

No... il problema non è Python, ma la rappresentazione dei numeri reali
**IEEE754** utilizzata dai nostri dispositivi per memorizzare un numero
reale.

Forse in prima l'abbiamo accennata... difficilmente l'abbiamo
studiata... vi ricorderò 2 semplici cose:

-   i computer salvano i dati nelle memorie come sequenze binarie
-   le memorie hanno il brutto difetto di avere uno spazio limitato, *"finito"*

Ora... per capire con un semplice esempio il problema, facciamo un
ragionamento con i numeri decimali.

Immagina di voler memorizzare il valore della frazione `1/4` (un quarto):


    viene 0.25 (facile, finito!!!)


Immagina adesso di voler memorizzare il valore della frazione `1/3`

viene `0.3333333333333333` (facile, ma *infinito*... un problemino in un posto finito)

Certo... tu a occhio hai capito che basta mettere infiniti 3 lì
dietro... ma per quanto ti impegni quella rappresentazione non sarà mai
esattamente `1/3` !!!

A volte, nella traduzione binaria di un numero reale in decimale si
creano situazioni analoghe: numeri che in decimale hanno una
rappresentazione semplice hanno rappresentazione infinita in binario. Di
cui noi (ulteriore problema) possiamo memorizzarne solo un pezzo!

Ecco spiegato l'arcano.

Se vogliamo rappresentazioni precise "all'infinito" (per i numeri
reali razionali) possiamo usare alcuni moduli Python adatti allo scopo:

- [decimal](https://docs.python.org/3/library/decimal.html)
- [fractions](https://docs.python.org/3/library/fractions.html)
- [math](https://docs.python.org/3/library/math.html)

Segui i link indicati e continua tu :wink:

<br>
<br>
<br>

