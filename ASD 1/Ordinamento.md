
%%2022-11-29%%

# Insertion sort

k elementi già ordinati e voglio estendere al k+1-esimo elemento 

```
InsertionSort(array A):
	for j=2 to A.length:
		key = A[j]
		i = j-1
		while i>0 && key < A[i]: \\ pseudo
			A[i+1] = A[i]
			i = i - 1
		A[i+1] = key
```

**Complessità**: $T(n) = O(n^2)$


Teorema: L'algoritmo insertion_sort ordina in loco n elementi eseguendo nel caso peggiore $\Theta(n^2)$.
Il calcolo è eseguito n-1 volte, il numero di confronti è: 

$$\sum\limits_{j=2}^{n} j-1= \sum\limits_{k}^{n-1} k = \cfrac{n-1+1(n-1)}{2} = \frac{n(n-1)}{2} = \Theta(n^2)$$

> **In loco**
> Un ordinamento in loco (o sul posto) è un algoritmo che ordina e in ogni istante al più un numero constante di elementi dell'array di input sono registrati all'interno dell'array
> Cioè non ho bisogno di supporto di una struttura data esterna all'array di input

L'algoritmo è un ordinamento in loco perché un solo elemento è memorizzato all'esterno dell'array e questo unico elemento è key.

Caso migliore: se l'input è ordinato in senso crescente -> $\Theta(n)$
Caso peggiore: se l'input è ordinato in senso decrescente -> $\Theta(n^2)$

