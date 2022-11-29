f
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


![[Albero K-appario.svg]]



### Albero k-ario

Un ==albero k-ario== è un albero in cui i figli di un nodo sono etichettati con interi positivi distinti e l'etichette maggiori di k sono assenti. 
Un albero binario è un albero k-ario con k=2 
Un albero k-ario **completo** è un albero k-ario in cui tutte le foglie hanno la stessa profondità e tutti i nodi interni hanno grado k.

![[Es1.svg]]

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

![[Untitled Diagram 1.svg]]

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
Quindi le iterazioni del nostro ciclo while saranno al più $O(n)$ e poiché ogni nodo compare al più una volta in S, lo spazio richiesto è $O(n)$

### Depth First Search (DFS)

```python
def dfs(Node r):
	if r != NIL
		visita il nodo r
		dfs(r.left)
		dfs(r.right)
```

**Teorema**: Se x è la radice di un sottoalbero di n nodi, la chiamata di dfs(r), richiede tempo $\Theta(n)$. 

DIM

VAI A VEDERE DFS NEGLI APPUNTI DI COSTA

## Esercizi

Un nodo di un albero binario è detto centrale se il numero di foglie del sottoalbero di cui è radice, è pari alla somma delle chiavi dei nodi appartenenti al cammino dalla radice al nodo stesso.

Scrivere un algoritmo efficiente che restituisce il numero di nodi centrali. Discutere la complessità e se volessimo modificare l'algoritmo in modo che restituisca l'insieme dei nodi centrali.


```C++
struct Node {
	int key;
	Node *left;
	Node *right;
	Node *p;
	Node(int k, Node *padre, Node *sx=nullptr, Node *rx=nullptr)
	:key{k},p{padre},left{sx},right{dx}{}
}

typedef Node *PNode;

int contaCentrali(Pnode u){
	int numF;
	return contaCentraliAux(u, 0, numF)
}

int contaCentraliAux(PNode u, int sum, int &numF){
	int nodi_c, nodisx, nodidx, numFSx, numFDx;
	if(u == nullptr){
		numF = 0;
		return 0;
	}
	if(u->left==nullptr && u->right==nullptr){
		numF = 1;
		return 0;
	}
	else {
		nodi_sx = contaCentraliAux(u->left, sum+u->key, numF, numFSx);
		nodi_dx = contaCentraliAux(u->right, sum+u->key, numF, numFDx);
		numF = numFSx + numFDx;
		nodi_c = nodisx + nodidx;
	}
	if(numF == sum+u->key){
		return nodi_c+1;
	}
	else {
		return nodi_c;
	}
}
```

2022-11-14

Un cammino è detto **terminabile** se $x_n.left = NIL$ oppure $x_n.right = NIL$. Diciamo perciò che un albero è **3-bilanciato** se tutti i cammini terminabili che partono dalla radice hanno lunghezze che differiscono al più di tre.

Scrivere un algoritmo efficiente che verifica se un albero è 3-bilanciato

```C++

bool 3_Bil(PNode u){
	int min, max;
	3_bil_aux(u, min, max);
	return (max - min <= 3); 
}

int 3_bil_aux(PNode u,int &min,int &max){
	int minsx, maxsx, mindx, maxdx, ;
	if(u == nullptr){
		min = -1;
		max = -1;
		return -1;
	}
	else {
		3_bil_aux(u->left, minsx, maxsx);
		3_bil_aux(u->right, mindx, maxdx);
		min = (minsx <= mindx ? minsx : mindx) + 1;
		max = (maxsx <= maxdx ? maxsx : maxdx) + 1
	}
}
```

**Complessità**:$T(n) = \Theta(n)$

Sia T un albero binario. Progettare un algoritmo che preso in ingresso la radice di un albero e un intero k, che stampi le chiavi contenute nei nodi di T al livello k, procedendo da sinistra verso destra. 

```C++
void stampaLivello(PNode u, int k){
	if(u !== nullptr){
		if(k == 0){
			count << u->key
		}
		else {
			stampaLivello(u->left, k-1);
			stampaLivello(u->right, k-1);
		}
	}
}
```

**Complessità in funzione di k**: 
$$\begin{align}
T(k) = 
\begin{cases}
 c & k =0 \\
 \cfrac{T(k-1)+ T(k-1) +d}{2T(k-1) + d} & k>0
\end{cases}
\end{align}$$

Dato un albero binario con i nodi bianchi e neri, scrivere una funzione efficiente che calcoli il numero di nodi aventi lo stesso numero di discendenti bianchi e neri (nodo stesso è discendente di se stesso)

```C
typedef struct Node {
	struct node* left;
	struct node* right;
	char* colore;
} *Node;


int nodiBN(PNode u){
	int bianco, nero;
	return auxcolore(u, &bianco, &nero);
}

int auxcolore(Node u, int *numB, int *numN){
	int risSx, risDx, numBSx, numBDx, numNSx, numNDx;
	// Caso base: il caso in cui il nodo è vuoto
	if(u == NULL){
		*numN = 0; 
		*numB = 0;
		return 0;
	}
	else {
		
		rissx = auxcolore(u->left, &numBSx, &numNSx);
		risdx = auxcolore(u->right, &numBDx, &numNDx);
		// scorro l'albero fino alla foglia e rissx e risdx messi a 0
		// una volta arrivato alla foglia viene eseguito il resto del codice 
		*numB = numBSx + numBDx;
		*numN = numNSx + numNDx;
	}

	if(strcmp(u->colore, "bianco") == 0)){
		(*numB)++;
	}
	else {
		(*numN)++;
	}
	// controllo se i discendenti hanno il numero di B e N uguali e ritorno quanti nodi lo hanno
	if(*numB == *numN){
		return risSx + risDx + 1;
	}
	else {
		return risSx + risDx;
	}
}
```

2022-11-15

### Albero binario bilanciato

Un albero viene detto binario bilanciato se la sua altezza è $h=O(\log n)$ dove n è il numero di nodi.
Albero completo -> albero bilanciato
Albero bilanciato -/> albero completo

### Albero binario di ricerca

Un albero binario di ricerca è un albero binario che soddisfa la seguente proprietà:
> **Proprietà di ricerca**
>  sia x un nodo in un albero binario di ricerca. Se y è un nodo nel sottoalbero sinistro di x, allora $y.key \leq x.key$ e se y è invece un nodo nel sottoalbero destro di x allora $y.key \geq x.key$

![[Albero di ricerca.svg]]

Questa proprietà ci permette di elencare in ordine **non decrescente** le chiavi di un albero binario di ricerca visitando l'albero in ordine simmetrico. 

```C 
Node Tree_search(Node x, Elem k){
	// Restituisce un nodo con chiave k, se esiste, oppure NIL
	if (x == null || x->key == k){
		return x;
	}
	else {
		if(x.key > k){
			tree_search(x->left, k);
		}
		else {
			tree_search(x->right, k);
		}
	}
}
```

**Correttezza**: possiamo tagliare lo spazio di ricerca perciò le proprietà degli alberi binari di ricerca assicurano che nel sottoalbero destro non ci sono nodi con chiavi minori di x.key. In maniera analoga si taglia il sottoalbero sinistro perché la proprietà assicura che non ci sono nodi con chiavi minori di x.key in tale albero. 

**Complessità**: I nodi incontrati durante la ricorsione formano un cammino verso il basso dalla radice del mio albero, quindi il mio tempo di esecuzione è $O(h)$ dove $h$ è l'altezza del mio albero. 
- Se l'albero è bilanciato allora $O(\log n)$
- Se l'albero è fortemente sbilanciato allora $O(n)$

```C
// pre: x è un nodo del mio albero T
Node TreeMax(Node x){
// post: mi restituisce il nodo con chiave massima nel sottoalbero radicato in x
	while(x->right != null){
		x = x->right
	}
	return x;
}

// pre: x è un nodo del mio albero T
Node TreeMin(Node x){
// post: mi restituisce il nodo con chiave minima nel sottoalbero radicato in x
	while(x->left != null){
		x = x->left
	}
	return x;
}
```

**Complessità**: $T(n) = O(h)$

```C
Iterative_Tree_Search(Node x, Elem k){
	while (x != null && x.key != k){
		if(k < x.key){
			x = x->left;
		}
		else {
			x = x->right;
		}
	}
	return x;
}
```


#### Predecessore e Successore

Dato un albero binario di ricerca voglio determinare dato un nodo il suo predecessore e il suo successore nell'ordine stabilito in una lista simmetrica. Se tutte le chiavi sono distinte, il successore di un nodo x non è altro che il nodo con la più piccola chiave che è maggiore di x.key.

Distinguiamo due casi:
- x ha un figlio destro: succ(x) è il minimo del sottoalbero destro di x
- x non ha un figlio destro: succ(x) se esiste, è l'antenato più prossimo di x il cui figlio sinistro è anche antenato di x. Per trovarlo si risale da x verso la radice fino ad incontrare la prima svolta a destra

Se x è il massimo restituisce NIL


```C
// pre: x è un nodo dell'albero T
Node tree_successor(Node x){
	if(x->right != null){
		return tree_minimum(x->right); // O(h)
	}
	else {
		y = x.p;
		while (y != null && x == y.right){ // O(h)
			x = y;
			y = y.p;
		}	
		return y;
	}
}
```

**Complessità**: $T(n) = O(h)$ perché si segue un cammino che scende o che sale ma siamo sempre in una situazione di seguire un cammino. 

#### Inserimento

```C
// T.root contiene il nodo radice
void insert(Tree T, Node z){
	// post: inserisce z in T mantenendo la proprietà di ricerca
	y = null; // padre di x
	x = T.root;
	while(x != null){
		y = x;
		if(z.key < x.key){
			x = x->left;
		}
		else {
			x = x->right;
		}
	}
	z.p = y;
	
	if(y == null){
		T.root = z;
	}
	else {
		if(z.key < y.key){
			y.left = z;
		}
		else {
			y.right = z;
		}
	}
} 
```
**Complessità**: $T(n) = O(h)$ perché si segue un cammino dalla radice verso il basso. 


%%2022-11-22%%

Esercitazione 1

#### Cancellazione

Si possono distinguere tre casi con difficoltà crescente:
- Foglia: se z non ha figli, modifichiamo suo padre (z.p) per sostituire z con NIL
- Un unico figlio: stacchiamo il nodo z creando un collegamento tra suo figlio (z.child) e suo padre (z.p)
- Due figli: troviamo il successore y di z che deve trovarsi nel sotto-albero destro di z e facciamo in modo che y assuma la posizione di z nell'albero

Per spostare i sotto-alberi si usa:

```python
def trasplant(Tree T, Node u, Node v):
	# sostituisce il sottoalbero con radice nel nodo u con
	# il sottoalbero con radice nel nodo v
	if u.p == null:
		T.root = v
	else:
	 if u == u.p.left:
		 u.p.left = v
		else:
			u.p.right = v
	if v != null:
		v.p = u.p
```

```python
# pre: il nodo z appartiene all'albero T
def delete(Tree T, Node z):
	if z.left == null:
		trasplant(T, z, z.right)
	else:
		if z.right == null:
			trasplant(T, z, z.left)
		else:
			y = tree_minimum(z.right) # O(h)
			if y.p != z:
				trasplant(T, y, y.right)
				y.right = z.right
				z.right.p = y
			trasplant(T, z, y)
			y.left = z.left
			y.left.p = y
```

**Complessità**: $T(n) = O(h)$ con h = altezza dell'albero

> **Teorema**
> Le operazioni search, minimum, maximum, succ e prev, insert e delete possono essere realizzate nel tempo $O(h)$ in un albero binario di ricerca di altezza h.
> **Cercare di mantenere bilanciato l'albero binario di ricerca perché questo fa si che tutte le operazioni abbiano tempo di esecuzione di $\log n$** 


#### Creazione albero
```python
	def buildBST(Arr A):
		t = newTree()
		for i=1 to A.length:
			u = creaNodo(A[i]) # u.key = A[i] a.left & a.right = null
			Tree_Insert(t,u)
		return T
```

**Complessità**:
$$\begin{align}
 \sum\limits_{i=0}^{n-1} (c + di) & = \\
& = cn + d  \sum\limits_{i=0}^{n-1} i \\
& =  cn + d \cfrac{n-1}{n-1+1}{2} \\
& = cn + d \frac{n(n-1)}{2} \\
& = \Theta(n^{2})
\end{align}$$

```python
# ipotesi: A è ordinato
def buildBSTOtt(Arr A):
	t = newTree()
	t.root = buildBTSOTTAux(A, 1, A.length, null)
	return t


def buildBTSOTTAux(Arr A, int inf, int sup, Node padre):
	if(inf > sup):
		return null
	else: 
		elementoCentrale = floor((inf+sup)/2)
		r = creaNodo(A[elementoCentrale])
		r.p = padre
		r.left = buildBTSOTTAux(A, inf, elementoCentrale-1, r)
		r.right = buildBTSOTTAux(A, elementoCentrale+1, sup, r)
		return r
```

%%2022-11-28-%%

# Esercizi d'esame

## Esercizio 1

Dato un albero binario di ricerca, scrivere un algoritmo efficiente che restituisca il numero di elementi che occorrono una sola volta e analizzarne la complessità.

![[Es1.svg]]

```C++

int contaDistinti(PTree T){
	PNode iter; 
	if(T->r == nullptr){
		return 0;
	}
	else {
		iter = tree_minimum(T);
		numDist = 0;
		count = 1;
		prevValue = iter->key;
		iter = succ(iter);
		while(iter-> != nullptr){
			if(iter->key == value){
				count++;
			}
			else {
				if(count == 1){
					numDist++;				
				}
				count = 0;
				prevValue = iter->key;
			}
			iter = succ(iter);
		}
		// controllare l´ ultimo elemento perché non viene controllato nel while
		if(count == 1){
			numDist++;
		}
		return numDist;
	}
}
```
**Complessità**

L'attraversamento simmetrico di un albero binario di ricerca di n nodi può essere implementato trovando l; elemento minimo dell'albero con la procedura Tree_minimum e poi, effettuando n-1 chiamate di Tree_succ(). Dimostrare che questo algoritmo viene eseguito ne tempo $\Theta(n)$

Dim
Le chiamate a Tree_minimum seguita da n-1 chiamate a Tree_succ esegure esattamente una cista simmetrica come fa la procedura ricorsiva INORDER. Infatti INORDER stampa prima Tree_minimum e poi definizione il  Tree_succ di un nodo è il prossimo nodo di una visita simmetrica. L'algoritmo ha tempo di esecuzione perché:
- richiede \Omega(n) per effettuare le n chiamate di procedura
- attraversare ognuno dei n-1 archi al più 2 volte, che richiede $O(n)$.
Sia (u,v) un generico arco.
Partiamo dalla radice, dobbiamo attraversare l'arco (u,v) da u a v.
L'unico modo di attraversarlo "downward" è nella procedura.
Tree_minimum mentre "upwards" è nella procedura Tree_succ quando il nodo a cui applico Tree_succ non ha sotto-albero destro. 


## Esercizio 2

Sia T un albero binario di ricerca contente n chiavi intere distinte. Sia k una chiave di T. Si consideri il problema di eliminare da T tutte le chiavi maggiori di k



## Esercizio 3

