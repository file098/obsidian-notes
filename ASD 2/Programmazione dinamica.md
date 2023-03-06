2023-03-06

# Problema dell'asta

In quanti modi posso tagliare un'asta di lunghezza *n*?

in ogni posizione $i=1...n$ posso decidere di tagliare o non tagliare, questo fa si che ottenga $n^{n-1}$ modi di tagliare. Usando il metodo della forza bruta, quindi andando a esprimere esplicitamente tutti i i possibili tagli non è efficiente -> $\Theta(n^{n-1})$.

Il ricavo massimo $r_{n}$ per un'asta di lunghezza n può essere espresso in modo ricorsivo:
- $r_{0}= 0$
- $r_{n} = \text{max} \set{p_{n}, r_{1} + r_{n-1}, r_{2} + r_{n-2}, ... r_{n-1} + r_{1}}$

Quando la soluzione ottima è esprimibile come combinazione di soluzioni ottime di sottoproblemi, si dice che vale la **proprietà della sottostruttura ottima**.

Caratterizzazione più semplice:
- tagliare un pezzo in modo definitivo (il pezzo a sinistra)
- suddividere ulteriormente la parte rimanente

Quindi abbiamo:
- $r_{0}$
- $r_{n} = \text{max} \set{p_{i} + r_{n-i}}$ ($i=n$ -> nessun taglio)


**input**: 
- $p[i...m]$: $m \geq n$ vettore di prezzi, p[i] prezzo per lunghezza i ($\geq 0$)
- $n$: lunghezza massima $r_{n}$ 

**output**: ricavo massimo $r_{n}$

```python 
def Cut_Rod(p,n):
		if n == 0:
			return 0;
		else: 
			q = -1 #inizializzato a valore impossibile per il controllo (-inf)
			for i=1 to n:
				q = max(q, p[i] + Cut_Rod(p,n-i))
			return q
```

T(n) è il numero di chiamate di `Cut_Rod` quando la chiamata viene fatta con il secondo parametro uguale a *n*.

$$\begin{align} &T(n) = 
\begin{cases}
1 & n=0 \\
1 + \sum\limits_{i=1}^{n} T(n-i) & n>0 \\
\end{cases}  \\
& T(n) = 1 + \sum\limits_{i=1}^{n} T(n-i) \\
& \text{facciamo un cambio di variabile dove n-i} \rightarrow \text{j}\\
& T(n) = 1 + \sum\limits_{j=0}^{n} T(j) = 2^{n}\\
\end{align}$$

La dimostriamo per induzione su *n*.

$(n=0) = T(0) = 1= 2^{0}$

Assumiamo che per *n* $T(n) = 2^{n}$ e la dimostriamo per $n+1$

$T(n+1) = 1 + \sum\limits_{j=0}^{n+1-1} T(j) = 1 + \sum\limits_{j=0}^{n-1} T(j) + T(n) = T(n) + T(n) = 2T(n)$

Quindi otteniamo $2 * 2^{n} = 2^{n+1}$

**Complessità**: esponenziale! $O(2^{n})$.

![[albero delle soluzioni 1.svg]]

Abbiamo la situazione in cui delle soluzioni come il 2 e il  4 vengono calcolati più volte, risultando in uno spreco di computazione.


## Aspetti della programmazione dinamica

Se:
- i sottoproblemi distinti sono di numero polinomiale
- ciascuno si risolve in tempo polinomiale (data la soluzione di sottoproblemi)

memorizzando le soluzioni ed evitando di ricalcolarle, si ottiene un algoritmo polinomiale a costo di un po' più di utilizzo di spazio.

Ci sono due possibilità:
1. top-down:
	- ricordando in una tabella (vettore, hash) le soluzione di problemi già risolti (memorization)
2. bottom-up:
	- ordina i sottoproblemi in base alla dimensione iniziando dai problemi più piccoli, e memorizzando le soluzioni ottenute

### Top-down

```python
def memorized-cut-rod(p,n):
	# Sia r[0,n] un nuovo vettore dove r[i]=ricavo ottimo per lunghezza i
	for i=0 to n:
		r[i] = -1
	return memorized-cut-rod-aux(p,n,r)


def memorized-cut-rod-aux(p,j,r):
	if r[j] < 0:
		if j==0:
			return 0
		else:
			q = -1
			for i=1 to j:
				q = max(q,p[i] + memorized-cut-rod-aux(p,j-i,r))
			r[j] = q
	return r[j]
```

**Complessità**: una chiamata ricorsiva precedentemente risolto si risolve in tempo costante. Dunque si giunge al ramo `else` **una sola volta** per ciascun sottoproblema $j=1,...,n$
Per risolvere un sottoproblema di dimensione *j*, il ciclo `for` effettua *j* iterazioni. Quindi il numero totale di iterazioni di questo ciclo for per tutte le chiamate ricorsive di memorized-cut-rod è: $\sum\limits^{n}_{j=1} j = \dfrac{n(n+1)}{2} = \Theta(n^{2})$  , quindi il costo della memorized-cut-rod = $\Theta(n) + \Theta(n^{2}) = \Theta(n^{2})$ nel caso peggiore. 

### Bottom-up

