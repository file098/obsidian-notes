
%%2022-11-29%%

## Insertion-sort

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

![[Pasted image 20221205114444.png]]

%%2022-12-05%%

## Merge-sort

Algoritmo basato sulla strategia del divide et impera

Per la funzione di mergesort abbiamo queste caratteristiche:

Inizialmente p=1  e r=A.length

- impera: ordina i due sottoarray in modo ricorsivo, utilizzando mergesort. Se il problema è sufficientemente piccolo si risolve piccolo
- combina: fondo insieme i due sottoarray **ordinati** per generare un singolo vettore ordinato $A[p...r]$

```python
def mergesort(array A, int p, int r):
	if p<r:
		med = floor((p+r)/2) # divide
		mergesort(A,p,med) 
		mergesort(A,med+1,r)
		merge(A,p,q,r) # fondere le porzioni ordinate
```

Per la funzione di merge abbiamo le seguenti caratteristiche:

- $p \leq q < r$
- il sottoarray $A[p..q]$ è ordinato e il sottoarray $A[q+1,r]$ è ordinato. Nessuno dei due è vuoto per la condizione di p,q e r

```python
def merge(array A, int p, int q, int r):
	n1 = q - p + 1
	n2 = r - q
	# crea gli array L[1...n1+1] e R[1...n2+1]
	for i=1 to n1:
		L[i] = A[p+i-1]
	for j=0 to n2:
		R[j] = A[q+j]
	L[n1+1] = infinito #carta sentinella che contiene un valore più grande di tutti
	R[n2+1] = infinito # carta sentinella
	i = 1; # primo elmeneto
	j = 1;
	for k=p to r:
		if L[i] <= R[j]:
			A[k] = L[i]
			i++;
		else
			A[k] = R[j]
			j++;
```

$INV \equiv$ il sottoarray $A[p...k-1]$ contiene **ordinati** i $k-p$ elementi più piccoli di $L[1...n_1+1]$ e $R[1...n_2+1]$. Inoltre, $L[i]$ e $R[j]$ sono i più piccoli elementi dei loro array che non sono stati ancora copiati in A.

![[Pasted image 20221205144502.png]]

Alla fine del ciclo, k=r+1 e vale il nostro invariante. $INV[ \cfrac{r+1}{k} ] \equiv$ il sottoarray A[p-r] contiene ordinati i  r+1-p elementi più piccoli \land L[1...n1+1] e R[1...n2+1]. Inoltre L[i] e R[j] sono i più piccoli elementi dei loro array che non sono stati copiati in A.
Il vettore A[p...r] è ordinato e gli 


**Complessità**: $T(n) = T(\frac{n}{2}) + T(\frac{n}{2}) + \Theta(n)$.

$$\begin{align} T(n) =
\begin{cases}  O(1) & n \leq 1 \\
2T\left(\frac{n}{2}\right) + \Theta(n)&  n>1 \\
\end{cases}
\end{align}
$$
Utilizziamo il master theorem:

$$\begin{align} 
&f(n) = \Theta(n) \\
&n^{\log_{2}2} = n \\
&f(n) = \Theta(n) \\
&T(n) = \Theta(n \log n)
\end{align}
$$

> **Nota**
> Il tempo di calcolo del mergesort dipende dal numero degli elementi e non trae beneficio da l'ordine iniziale degli elementi. 
> Un ottimizzazione che viene fatta è usare l'insertion-sort per input di piccole dimensioni. 


## Quick-sort

È un algoritmo basato sulla tecnica del divide et impera.
Per ordinare un vettore $A[p...r]$, p=1 e r=A.length
1) divide: partiziona l'array di partenza in due sottoarray, e questi sottoarray vanno da A[p...q-1] e A[q+1,...r] (eventualmente vuote) tali che ogni elemento nella prima porzione di A[p...q-1] è minore o uguale di A[q] (**pivot**) che a sua volta è minore o uguale ad ogni elemento di A[q+1...r]. L'indice q è il risultato della funzione `partition()` e l'elemento A[q] è chiamato **pivot**. 
2) impera: ordina i due sottoarray che A[p...q-1] e A[q+1...r] chiamando ricorsivamente la procedura `quick-sort`. Se il problema è sufficiente piccolo (0 o 1 elemento), risolve direttamente 
3) combina: non esegue nulla dato che l'array è già ordinato sul posto dopo le chiamate ricorsive

![[Pasted image 20221205152950.png]]

```python
def quicksort(array A, int p, int r):
	q = partition(A,p,r)
	quicksort(A, p, q-1)
	quicksort(A, q+1, r)

def partition(array A, int p, int r):
	x = A[r]
	i = p-1
	for j=p to r-1:
		if A[j] <= x:
			i++;
			swap(A[i], A[j])
	swap(A[i+1], A[r])
	return i+1
```

%%2022-12-06%%

**Complessità `partition`**: $T(n) = \Theta(n) \qquad n = r-p+1$

**Complessità**: 
$$\begin{align} T(n) =
\begin{cases}  O(1) & n \leq 1 \\ \\
\\
T(k) + T(n-1-k) + \Theta(n)&  n>1 \\
\end{cases}
\end{align}
$$

> **Note**
> il tempo di esecuzione dipende <u>fortemente</u> dalla scelta del nostro pivot, quindi dal partizionamento del sottoarray


### Caso peggiore
un sottoarray contiene n-1 elementi, quindi fortemente sbilanciato e già ordinato
$$\begin{align}
T(n) & = \\
& = T(n-1) + T(0) + \Theta(n) \\
& = T(n-1) + \Theta(n) = T(n-1) + cn \\
& = T(n-1)+cn = T(n-2)+c(n-1) + cn \\
& = \sum\limits^{n}_{i=1} ci \\
& = c \sum\limits_{i=1}^{n} \\
& = \frac{c(n(n+1))}{2} \\
& = \Theta(n^{2}) \\
\end{align}$$
### Caso migliore
i sottoarray sotto bilanciati 
$$T(n) = 2T\left(\frac{n}{2}\right)+ \Theta(n) = \Theta(n \log n)$$
### Caso medio
supponiamo che il nostro algoritmo produca sempre una ripartizione proporzionale a 9-a-1.

l'altezza dell'albero è $\log_{\cfrac{10}{9}} n$
$$\begin{align}
T(n) = & \\
& = T\left(\frac{n}{10}\right)+ T\left(\frac{9n}{10}\right) + cn \\
& cn \implies \text{costi a livello più alto delle ricorrenze} \\
& = O(n \log n)
\end{align}$$

Qualsiasi proporzionalità costante $T(n) = T(\alpha n) + T(i - \alpha) + cn \quad 0<\alpha<1 \quad e \quad c>0$ produce un albero di ricorsione di profondità $\Theta(n \log n)$ dove il costo di ogni livello è limitato superiormente da $O(n)$. Il tempo di esecuzione è quindi $O(n \log n)$.

#### Sistema di ricorrenze

Le partizioni si alternano tra buone (lucky) e cattive (unlucky).

$L(n) = 2U\left(\frac{n}{2}\right)+ \Theta(n)$
$U(n) = L(n-1) + \Theta(n)$

$L(n) = 2\left(L (\frac{n}{2} -1\right)+ \Theta(n)) + \Theta(n) = 2L\left(\frac{n}{2} - 1\right)+ \Theta(n) = \Theta(n \log n)$

### Ottimizzazioni


#### Quick-sort randomizzato

Prestazione 3-4 volte più veloce su input di grandi dimensioni del merge-sort

Invece di scegliere A[r] (ultimo elemento) come pivot, scambieremo l'elemento A[r] con un elemento **scelto casualmente** da la parte di vettore che noi stiamo andando a ordinare. 


```python 

def randomized_quicksort(array A, int p, int r):
	if p<r
		q = randomized_partition(A,p,r)
		randomized_quicksort(A, p, q-1)
		randomized_quicksort(A, q+1, r)
		
def randomized_partition(Array A, int p, int r):
	i = random(p,r)
	swap(A[i], A[r])
	return partition(A, p, r)
```


Vantaggi:
**Assunzioni chiavi distinte**
1) tempo di esecuzione è indipendente dall'ordinamento dell'input
2) nessuna assunzione sulla distinzione dell'input
3) nessun specifico input può portare al caso pessimo
4) il caso peggiore è determinato solamente dal generatore di numeri casuali


#### Altre ottimizzazioni

Utilizzare l'insertion-sort su vettori di piccole dimensioni 