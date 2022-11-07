
2022-10-25

# Alberi radicati

Un albero radicato è una coppia $T = (N,A)$ dove N è un insieme finito di nodi tra cui si distingue un nodo **r** detto ==radice==.  $A \subseteq N \times N$ è un insieme di coppie di nodi, detti **archi**. In un albero, ogni nodo v (eccetto la radice) ha esattamente un genitore (o padre) **u** tale che $(u,v) \in A$.

Un nodo **u** può avere zero o più figli v tali che abbiamo un arco (u,v) \in A. Il numero degli figli di un nodo è detto ==grado== del nodo. 
![[Pasted image 20221025122359.png]]

- Un nodo senza figli è detto ==nodo foglia==. 
- Un nodo non foglia è un ==nodo interno==. 
- Se due nodi hanno lo stesso padre sono ==fratelli==

Il **cammino** da un nodo u a un nodo v in un albero T è una **sequenza** di nodi $< n_{0}, n_{1}, ... , n_{k} >$ tale che:

- $u_{1} = n_0$
- $u = n_k$
- $< n_{i-1}, n_{i} > \in A$ per ogni $i=1,...,k$

La **lunghezza** di un cammino è il numero degli arch nel cammino $\emptyset$ al $n^0$ di nodi che formano il cammino-1.

 > N.B.
 >  **Un nodo ha  sempre un cammino di lunghezza 0**
 > 

Sia x un nodo in un albero radicato T con radice r. Un nodo qualsiasi y in un cammino che parte dalla radice e arriva a x è detto ==antenato di x==. 


 > N.B.
 >  Ogni nodo è antenato e discendente di se stesso
 > 

Se y è un antenato di x e x != y allora y è un **antenato proprio** di x e x è un **discendente proprio** di y

## Sottoalbero

Il sottoalbero con radice in x è l'albero indotto dai discendenti di x, con radice in x
La ==profondità== di un nodo x è la lunghezza del cammino dalla radice a x.
Un ==livello== di un albero è costituito da tutti i nodi che stanno alla stessa profondità.
L'==altezza== di un nodo è la lunghezza del più lungo cammino che scende dal nodo x ad una foglia. 

### Albero binario

Gli albero binari sono definiti in modo ricorsivo.
- Un albero vuoto è un albero binario
- un albero costituito da un nodo radice da un albero binario detto sottoalbero sinistro della radice e da un albero binario detto sottoalbero destro è una albero binario. 


![[./Albero K-appario.svg]]



### Albero k-ario

Un ==albero k-ario== è un albero in cui i figli di un nodo sono etichettati con interi positivi distinti e l'etichette maggiori di k sono assenti. 
Un albero binario è un albero k-ario con k=2 
Un albero k-ario **completo** è un albero k-ario in cui tutte le foglie hanno la stessa profondità e tutti i nodi interni hanno grado k.

![[Untitled Diagram.svg]]

Esercizio. Trovare il numero di nodi interni di un albero k-ario completo la cui altezza risulta essere k.

Dimostriamo per induzione sull'altezza h dell'albero $foglie(h) = k^h$

**Caso base**: h=0

L'albero è costituito dalla radice 

$k^0 = 1$ ha un'unica foglia che è la radice, vero perché assumiamo che per un albero di altezza h sia vero che $foglie(h) = k^{h}$ e dimostriamo che $foglie(h+1) = k^{h+1}$ per alberi di altezza h+1.

Il numero di nodi di profondità h sono $k^h$ per l'ipotesi induttiva in quanto l'albero di altezza h è un albero completo.

**Ognuno dei nodi di livello h quanti figli ha?** Ha k figli perché l'albero è completo, dunque 
$$k^h * k = k^{h+1}$$
Quindi $foglie(h+1) = k^{h+1}$.

Per calcolare in numero di nodi interni

$$\sum\limits_{i=0}^{h-1} k^{i} = \frac{k^{h-1+1} - 1}{k-1} = \frac{k^{h}-1}{k-1}$$

## Il tipo albero

Dati: un insieme di nodi (di tipo Node) e un insieme di archi
Operazioni: 
- newTree() -> Tree
	- post restituisce un albero vuoto
- treeEmpty(Tree t) -> bool
	- post: restituisce true se l'albero è vuoto, false altrimenti
- padre(Tree t, Node v) -> Node $\cup$ NIL
	- pre: $v \in t$
	- post: restituisce il nodo v se il nodo è diverso dalla radice, oppure NIL se v è la radice
- figli(Tree t, Node v) -> List of Node
	- pre: $v \in t$
	- post: restituisce una lista contenente i figli del nodo v

### Rappresentazione di albero basato su array

Sia T=(N,A) un albero con n nodi numerati da 0 a n-1

![[./Untitled Diagram 1.svg]]

P: vettore d di dimensione r le cui celle sono coppie (info,parent)%%da rivedere%%

$\forall v \in [0,n-1]$ 
$P[v].info$ è il contenuto informativo
$P[v].parent = u$ se e solo se vi è un arco $(u,v) \in A$
Se v è la radice $P[v].parent == -1$
P.length contiene il numero di nodi dell'albero

```python
 def padre(Tree P, Node v):
	 if P[v].parent == -1:
		 return NIL
	else: 
		retrun P[v].parent
```

```python
 def figli(Tree P, Node v):
	 l = crealista()
	 for i=0 to P.length-1:
		 if P[i].parent == v:
			 inserisci i in l
	return l
```

2022-11-07

#### Vettore posizionale

Alberi k-ario completo con k>=2
Ogni nodo ha una posizione prestabilita sulla struttura 
Sia T = (N,A) un albero k-ario completo
P è un vettore di dimensione n tale che
P[v] contiene l'informazione associata al nodo v
O è la posizione della radice
i-esimo figlio di v è in posizione $k*v+1+i$ dove $i \in \{0,...,k-1\}$
padre del nodo f è in posizione $(f \neq 0)$ 

$$\begin{align}
& k*v+1 \leq f \leq kv+1+k-1 \\
& k*v \leq f-1 \leq kv+k-1 \\
& v \leq \frac{f-1}{k} \leq v+ \frac{k-1}{k} < v+1 \\
& v = \frac{f-1}{k}
\end{align}$$

Lo spazio per un albero con n elementi è $\Theta(n)$.
P.length può contenere il numero di nodi
P.k grado dei nodi

```python
def padre(Tree P, Node v):
	if v==0
		return NIL
	else
		return floor((v-1)/P.k)
```

Complessità: $T(n) = \Theta(1)$

```python
def figli(Tree P, Node v):
	l = creaLista()
	if v*P.k + 1 >= P.length:
		return l
	else:
		for i=0 to P.k-1:
			inserisci P.k*v+1+i in l
		return l
```

Complessità: $T(n) = O(k)$


### Rappresentazione basata su strutture collegate


**Dati**: ogni nodo è rappresentato attraverso un record che contiene l'informazione associata al nodo, contiene un puntatore al padre e altri puntatori per accedere ai figli.

#### Puntatore ai figli

Se ogni nodo ha grado k al più k, possiamo mantenere in ogni nodo un puntatore a ciascuno dei possibili k figli.

Un nodo x ha:
- x.p puntatore al padre
- x.left puntatore al figlio sinistro
- x.right puntatore al figlio destro
- x.key informazione del nodo

![[Albero Puntatori.svg]]

T.root punta alla radice
Lo spazio richiesto è $\Theta(n*k)$ e se k è costante $\Theta(n)$.

```python
def figli(Tree P, Node v):
	l = creaLista()
	if v.left != NIL:
		insersci v.left in l
	if v.right != NIL:
		insersci v.right in l
	return l
```

**Se k è limitato da una grande costante ma la maggior parte dei figlio sono NIL c'è uno spreco di memoria.**

Lista figli: Se il numero di figli non è noto a priori allora è possibile associare a ciascun nodo la lista dei puntatori ai suoi figli

![[Lista dei figli.svg]]


#### Figlio Sinistro - Fratello Destro

**Dati**: Ogni nodo x ha le seguenti informazioni:
- x.key contiene l'informazione
- x.p puntatore al padre
- x.left_child puntatore al figlio più a sinistra del nodo
- x.right_sibling puntatore al nodo immediatamente alla sua destra

Se il nodo x ha x.left_child == NIL è un nodo foglia
Se il nodo x è il figlio più a destra di suo padre allora x.right_sib == NIL

![[Filgi,Fratelli.svg]]

```python
def padre(Tree T, Node v):
	return v.p
```

```python
def figli(Tree T, Node v):
	l = creaLista()
	iter = v.left_child
	while iter != NIL:
		inserisci iter in l
		iter = iter.right_sib
	return l
```

**Complessità**: $T(n) = \Theta(grado(v))$

# Algoritmi su alberi

## Visite di alberi

### Visita generica

```python
def visitaGenerica(Node r):
	S = {r}
	while S != {} :
		estrai un nodo da S
		visita il nodo u
		S = S unito {figli di u}
```

**Teorema**: l'algoritmo di visita applicato alla radice di un albero con n nodi termina in $O(n)$ iterazioni e lo spazio usato è $O(n)$.

DIM: inserimento/cancellazione da S sono eseguite in O(n)

Ogni nodo verrà inserito ed estratto da S ==una sola volta== perché un albero non si può tornare ad un nodo a partire dai suoi figli. 

