# Scipy

FIXME!!!

<!-- ################################################################################# -->
## Modulo NumPy

Il modulo NumPy serve per operazioni matematiche con sequenze di numeri.
E qui molti di voi staranno già progettando di saltarlo a piè pari...
tranquilli però! E per 2 ottimi motivi: il primo è che i calcoli da
fare... li fa lui (il modulo NumPy), il secondo è che questo modulo fa
da base per molti altri moduli più \"divertenti\"... allora due parole
su questo... ci toccano!

Installato il modulo da PyPi per includerlo nei nostri script basterà
come al solito:

import numpy as np \# di solito il nome \"numpy\" si abbrevia in \"np\"

In pratica NumPy gestisce una specie di lista numerica, chiamata array,
con (e su) cui è in grado di fare operazioni matematiche molto
velocemente (molto più che salvando i dati su una normale lista).

Si prende una lista qualsiasi e la si traduce in un array NumPy in un
attimo:

lista = \[1,2,3,4,5\]

arr = np.array(lista)

print(arr) \# i numeri vengono elencati senza virgole

\[1 2 3 4 5\]

Per visualizzare il primo elemento:

print( arr\[0\] )

1

Nel caso di un array di 2 dimensioni (fatto da elementi che sono a loro
volta liste):

arr2D = np.array ( \[ \[1 , 3 , 5 \] , \[ 2 , 4 , 6 \] \] )

print(arr2D\[0,1\]) \# visualizza il secondo elemento della prima lista

3
