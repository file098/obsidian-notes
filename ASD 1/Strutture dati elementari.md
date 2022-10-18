2022-10-17

# Strutture dati elementari

## Che cos'è un tipo di dato?
È un modello matematico che consiste in una collezione di valori sui quali sono ammesse certe operazioni. Dobbiamo conoscere cosa un'operazione deve fare ma **non come** un'operazione deve essere realizzata **né** come gli elementi possono essere organizzati in modo tale da rendere le operazioni efficienti e la collezione stessa occupi poco spazio in memoria. 

Una ==**struttura dati**== è una particolare organizzazione delle informazioni che permette di supportare in modo efficiente le operazioni di un tipo di dato, e quindi di conseguenza specifica come organizzare i dati e come realizzare le operazioni definite per un certo tipo di dato. 

Le strutture dati possono essere classificate in tre diversi criteri:
1) Disposizione dei dati
	- lineare: organizzati in sequenze
		- array, liste, pile, code, ...
	- non lineare: non organizzati in sequenze
		- alberi, grafi, ...
2)  numero
	 - statiche: il numero di elementi della struttura rimane costante nel tempo
		 - array, ...
	 - dinamiche: il numero di elementi può aumentare o diminuire nel tempo
		 - liste, ...
3) tipo
	 - omogenee: i dati sono tutti dello stesso tipo
	 - non omogenee: i dati non sono tutti dello stesso tipo


## Dizionario

Un ==**dizionario**== rappresenta il concetto matematico di relazione univoca R:D -> C fra gli elementi di un insieme D (*dominio*) e gli elementi di un insieme C (*codominio*). Gli elementi del dominio sono detti ==**chiavi**== e gli elementi del codominio ==**valori**==.  
Quindi un dizionario è un insieme di coppie chiave-valore. 

### Tipo di dato: Dizionario

> **Dati**: un insieme **S** di coppie (chiave, valore)

**Operazioni**:
- search (Dizionario S, Chiave K) -> Elemento $\cup$ {NIL}
	- Post: restituisce il valore associato alla chiave K se presente in **S**, **NIL** altrimenti
- insert (Dizionario S, Valore V, Chiave K)
	- Post: associa il valore V alla chiave K
- delete (Dizionario S,Chiave K)
	- Pre: k è presente in S
	- Post: rimuove la coppia con chiave K dalla collezione S


### Realizzazione attraverso array ordinati

Usiamo array ordinati perché algoritmi basati sulla ricerca binaria risultano particolarmente efficienti.

**Dati**: un array A di dimensione *n* contenente un record con due campi (Key, Info). Devono essere ordinati in base alla chiave. 

A : | 1,-3 | 3,15 | 5,-3 | 9,10 | 15, 0 |


 Qual'è il costo in termini di spazio della nostra struttura? $S(n) = \Theta(n)$

```python
def search(Dizionario A, Chiave k):
	i = search_index(A,k,1,A.length) 
    # restituisce l'indice della cella che contiene la chiave K se esiste, altrimenti -1
	
	if i == -1
		return NIL
	else 
		return A[i].info

def search_index(Dizionario A, Chiave k, int inizio, int fine):
	# se k è presente in A, restituisce l'indice della cella dove K si trova, altrimenti -1
	if fine < inizio
		return -1
	else 
		med = floor((inzio + fine) / 2)
		if A.[med].key == k
			return med
		else 
			if A[med].key > k
				return search_index(A, k, inzio, med-1)
			else 
				return search_index(A, k, med-1, fine)
					
```

$$\begin{align}T(n) &= 
\begin{cases} \Theta(1) && n = 0 \\
\\
T(\cfrac{n}{2}) + \Theta(1) && n > 0  \\ 
\end{cases}
\end{align}$$

**Complessità**: Secondo caso del Master theorem: $\Theta(\log n)$

2022-10-18

```python
def insert(Dizionario A, Elem v, Chiave k):
	i = 1
	while i <= A.length and A[i].key < k # Theta(n)
		i = i + 1
	if i <= A.length and A[i].key == k
		A[i].info = v
	else
		# crea un nuovo array con la dimensione voluta e copia il contenuto delle celle interesse (minimo fra vecchia dimensione e nuova dimensione) dal vecchio al nuovo spazio
		reallocate(A, A.length+1) # O(n)
		A.length = A.length + 1
		for j = A.length downto i+1
			A[j] = A[j-1]
		A[i].key = k
		A[i].info = v
```

**Complessità**: $T(n) = O(1) + i*d +O(n) + (n-i+1)d = O(1) + nd + d + O(n) = O(n)$

```python
# pre: la chiave k è presente nel nostro dizionario
def delete(Dizionario A, Chiave v):
	i = search_index(A, k, 1, A.length) # Theta(log n)
	for j=i to A.length-1 # O(n-1)
		A[j] = A[j+1]
	reallocate(A, A.length-1) #O(n)
	A.length = A.length - 1
```

**Complessità**: $T(n) = \Theta(\log n) + (n-i)d + O(n) = O(n)$

#### Reallocate

Tecnica del raddoppiamento e dimezzamento.
Si mantiene un array di dimensione $h$, dove per ogni $n>0$, $h$ soddisfa questa condizione: $n \leq h < 4n$
Le prime *n* celle dell'array contengono gli elementi delle collezioni, mentre il contenuto delle altre celle è indefinito. 
- Inizialmente, quando n è 0, poniamo $h=1$
- Ogniqualvolta *n* supera $h$, l'array viene riallocato raddoppiando la dimensione $(h = 2h)$
- Ogniqualvolta *n* scende a $\cfrac{h}{4}$, l'array viene riallocato dimezzando la dimensione ($h = \cfrac{h}{2}$)
Quindi: $S(n) = \Theta(h) = \Theta(n)$

#### Analisi ammortizzata

Al posto di analizzare ogni singola operazione, analizziamo il costo medio dell'esecuzione di un operazione su una certa struttura dati.

Assumiamo di partire da un vettore inizialmente di dimensione 1 e vogliamo eseguire *n* insert. Sia $c_i$ il costo dell'i-esimo inserimento 

$$\begin{align} c_{i} & = \begin{cases} i & & \exists k \quad \text{t.c.} \quad  
 i=2^{k}+1   \\ \\
1 & & \text{altrimenti}
\end{cases}\end{align}$$

Il costo degli *n* inserimenti è:
$$\begin{align}
C(h) & = \\
& = \sum\limits_{i=1}^{n} c_{i} \\
& = n + \sum\limits_{k=0}^{\log_{2}n} 2^{k} \\
& = n + \cfrac{2^{\lfloor log_{2} n \rfloor + 1} -1}{2-1} \\
& = n + 2n -1 \\
& \leq 3n \\
& = 3n / n \qquad \text{divido per n per trovare il costo medio di un operazione} \\
& = 3 \\
& = O(1) \\
\end{align}$$

Quindi $T(n) = O(1)$



### Realizzazione attraverso record e puntatori

> **Dati**: un insieme **S** di coppie (chiave, valore, next, prev)

Una collezione L di *n* record contenenti (key, info, next, prev) dove next e prev sono puntatori al successivo e al precedente record della collezione. Un attributo L.head punta al primo elemento della lista, se L.head == NIL allora la lista è vuota. 

Lo spazio della collezione è: $S(n) = \Theta(n)$.

```python 
def insert(Dizionario L, Elem v, Chiave k):
	p.next = L.head
	if L.head != NIL
		L.head.prev = p
	p.rev = NIL
	L.head = p
```

**Complessità**: $T(n) = O(1)$

```python
def search( Dizionario L, Chiave k):
	x = L.head
	while x != NIL and x.key != k:
		x = x.next
	if x != NIL:
		return x.info
	else:
		return NIL
```

**Complessità**: $T(n) = O(n)$

**Correttezza**: è restituita la prima occorrenza della chiave k

#### Invariante

Un asserzione (formula) che deve essere vera prima, dopo ed ad ogni iterazione del ciclo. Occorre dimostrare tre proprietà:
 - **inizializzazione**: la mia asserzione è vera prima della prima iterazione del ciclo
 - **conservazione**: se la mia asserzione è vera prima di un iterazione del ciclo, rimane vera prima della successiva iterazione 
	 - $INV \land \text{Guardia} \implies INV$ (dopo l'esecuzione del corpo del ciclo)
 - **conclusione**: quando il ciclo termina, l'invariante fornisce un utile proprietà che aiuta a dimostrare che l'algoritmo è corretto
	 - $INV \land \neg \text{Guardia} \implies \text{asserzione finale}$

**Funzione di terminazione**: è una funziona a valori naturali strettamente decrescente ad ogni iterazione del ciclo.

$INV$ = gli elementi da L.head ad x escluso, hanno la chiave diversa da k

