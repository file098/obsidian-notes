2022-10-05

# Complessità 
## Esempi di complessità
### Sequenza 
```
	Block(1)  <-- O(f(n))
	Block(2)  <-- O(g(n))
```
Complessità = $O(f(n) + g(n) ) = O(f(n) + g(n))$

### If-then-else

```
if <cond> then <-- O(f(n))
	ramo-then  <-- O(g(n))
else
	ramo-else  <-- O(h(n))
```
Complessità: $O(f(n) + \text{max}\{g(n), h(n)\})$


### Cicli
```
for i to k
	block  <-- O(f(n))
```
Complessità: $O(k * f(n))$

### While
```
while <cond> do  <-- O(f(n))
	block        <-- O(g(n))
```
N(m) = max numero di iterazioni
Complessità: $O(N(n) (f(n) + g(n)))$

### Esercizio

```
MyAlgorithm (int n) -> int
	if n>1 then
		a = 0
		for i=1 to n                   <-- n * n
			for j=1 to n
				a = (a+1)*j + a/2
		for i=1 to 16
			a = a + MyAlgorithm(n/4)   <-- 16T(n/4)
		return a
	else
		return n
```
Complessità: $T(n) = O(n^2 + 16T(\cfrac{n}{4}))$

## Ricorrenze

### Metodo dell'iterazione
Supponiamo

$$\begin{align} 
T(n) = 
\begin{cases} c + T(\cfrac{n}{2}) & n \geq 2 \\  \\
1 & n=1 \\
\end{cases}
\end{align}$$

$$\begin{align}
T(n) & = c + T(\cfrac{n}{2})\\
& =  c + [ c + T(\cfrac{n}{2}) ] \\
& = 2c + T(\cfrac{n}{2^{2}}) \\
& = 2c + [ c + T(\cfrac{n}{2^3}) ] \\
& = 3c + T(\cfrac{n}{2^{3}}) \\
& \text{riusciamo a intuire il comportamento} \\
& = kc + T(\cfrac{n}{2^{k}})\\
& k = \log_{2}n \\
& = c \log_{2}(n) + T(1) \\
& = c \log_{2}(n) \\
& = O( \log(n)) \\
\end{align}$$


$$\begin{align} 
T(n) = 
\begin{cases} 
9T(\cfrac{n}{3}) + n & n \geq 2 \\
1 & n=1 \\
\end{cases}
\end{align}$$

$$\begin{align}
T(n) & = 9 T(\cfrac{n}{3}) + n \\
& = 9 [ 9T(\cfrac{n}{3^{2}}) + \cfrac{n}{3}]  +n \\
& = 9^{2} T(\cfrac{n}{3^{2}} ) + 3n + n \\
& = 9^{2} [ 9T(\cfrac{n}{3^{3}}) + \cfrac{n}{3^{2}}] + 3n  +n \\
& = 9^{3} T(\cfrac{n}{3^{3}} ) +9n + 3n + n \\
& = 9^{3} T(\cfrac{n}{3^{3}} ) + n(3^{2} + 3^{1} + 3^{0}) \\
& = 9^{k} T(\cfrac{n}{3^{k}} ) + \sum\limits_{i=0}^{k-1} 3^{i} \\
& = 9^{k} T(\cfrac{n}{3^{k}} ) +n \cfrac{3^{k}-1}{2}\
\end{align}$$

dove abbiamo che 
$$
\begin{align}
T(n) & =
\cfrac{n}{3^{k}} = 1 \iff n = 3^{k} \iff k = \log_{3}n \\
& = 9^{\log_{3} n} T(1) + n \cfrac{3^{\log n} -1}{2} \\
& = 3^{\log_{3} n^{2}} + n \cfrac{n-1}{2} \\
& = n^{2} + n \cfrac{n-1}{2} \\
& = \Theta(n^{2})
\end{align}
$$

## Metodo della sostituzione

$$\begin{align} 
T(n) = 
\begin{cases}
1 & n=1 \\
T(\lfloor \cfrac{n}{2} \rfloor + n & n \geq 2 \\
\end{cases}
\end{align}$$

Verifichiamo che $T(n) = O(n)$ e $\exists c > 0 \quad \exists n_{0} \quad \text{t.c.} \quad \forall n \geq n_{0}: \qquad T(n) \leq cn$

**Caso base** $n=1$
$$T(1) = c * 1 \geq 1$$
vero per $\forall c \geq 1$

**Passo induttivo** $n+1$

$$\begin{align} T(n) & = \\
& = T(\lfloor \cfrac{n}{2} \rfloor) + n \\
& \leq c * \lfloor \cfrac{n}{2} \rfloor + n \\
& \leq c * \cfrac{n}{2} + n \\
& = (\cfrac{c}{2} + 1)n \\
& \leq c*n = \cfrac{c}{2} + 1 \leq c \iff 1 \leq \cfrac{c}{2} \iff c \geq 2
\end{align}$$
Quindi $c=2$ e $n_{0} = 1$.

## Teorema Master
Si basa sul concetto di *divide et impera* con questi steps:
1) split
2) risoluzione dei sotto problemi
3) merge

$$\begin{align} 
T(n) & = T_{split}(n) + aT(\cfrac{n}{b}) + T_{merge}(n) \\
& = aT(\cfrac{n}{b}) + f(n)
\end{align}$$

Data $T(n) = aT(\cfrac{n}{b}) +f(n)$ con:
1) $f(n) \geq 0$ per n sufficiente grandi
2) $a \geq 1$
3) $b > 1$

abbiamo il teorema **master**

Sia $d = \log_{b} a$

**Caso 1**
$$\begin{align}
f(n) &= O(n^{d-\epsilon}) \quad \exists \epsilon > 0 \\
& \Rightarrow T(n) = \Theta(n^{d})
\end{align}$$

**Caso 2**
$$\begin{align}
f(n) &= O(n^{d}) \\
& \Rightarrow T(n) = \Theta(n^{d} \log n)
\end{align}$$

**Caso 3**
$$\begin{align}
f(n) &= \Omega(n^{d+\epsilon}) \quad \exists \epsilon > 0 \land \exists c >1 \quad t.c. \quad af(\cfrac{n}{b}) \leq cf(n) \\
& \Rightarrow T(n) = \Theta(f(n))
\end{align}$$

### Esempi
$$T(n) = T(\cfrac{n}{2}) + c$$
- $a=1$
- $b=2$
- $d=\log_{2} 1 = 0$
- $f(n) = c$
- $g(n) = n^0$

Quindi caso 2, dunque  $T(n) = \Theta(\log n)$

$$T(n)= 9T(\cfrac{n}{3})+n$$
- $a=9$
- $b=3$
- $d=\log_{3} 9 = 2$
- $f(n) = n$
- $g(n) = n^{2}$

Quindi caso 1, $f(n) = O(n^{d - \epsilon}) \implies T(n) = \Theta(n^{d})$
$$\begin{align}
f(n) & = \\
& = O(n^{2- \epsilon}) \\
& = O(n^{2-1}) \\
& = O(n) \\
\\
&\text{quindi} \quad \epsilon=1
\end{align}$$

Dunque $T(n) = \Theta(n^{2})$

### Dimostrazione teorema master

$$T(n) = aT(\cfrac{n}{b}) + f(n)$$

![[Pasted image 20221011150521.png]]

1) al livello $i \geq 0$:
	-  numero di nodi = $a^{i}$
2) al livello i:
	- dimensionalità = $\cfrac{n}{b^{i}}$ 
3) tempo al livello $i$:
	- $f(\cfrac{n}{b^{i}})$

Quindi mettendo tutto insieme otteniamo
$$T(n) = \sum\limits_{i=0}^{\text{liveli}} a^{i} f(\cfrac{n}{b^{i}})$$

dove il numero di livelli è $\cfrac{n}{b^{i}} \rightarrow n = b^{i} \rightarrow i=\log_{b}n$


$$\text{n nodi foglia} = a^{\log_b n}$$

$$\begin{align} a^{\log_{b}n} & = \\
& = (a^{\log_{a} n})^{\log_{b} n} \\
& = n^{\log_{b} a}
& = n^{d}
\end{align}$$

$$\begin{align} 
\sum\limits_{i=0}^{\log_{b} n} a^{i} & =\\
& = \cfrac{a^{\log_{b}n}}{a-1} \\
& = \cfrac{a * a^{\log_{b}n} -1}{a-1} \\
& = \cfrac{a * a^{d} -1}{a-1} \\
& = \Theta(n^{d}) \\
\end{align}$$

#### Caso 1 dim

Vogliamo dimostrare che: $$f(n) = O(n^{d - \epsilon})$$

$$\begin{align}
a^{i} f(\cfrac{n}{b^{i}}) & = \\
& = a^{i} O\left((\cfrac{n}{b^{i}})^{d - \epsilon}\right) \\
& = O\left( a^{i} (\cfrac{n}{b^{i}})^{d - \epsilon}\right) \\
& = O\left( a^{i} \cfrac{n^{d- \epsilon}}{(b^{i})^{d} (b^{i})^{- \epsilon}} \right) \\
& = O\left((b^{i})^{\epsilon} n^{d - \epsilon} \right) \\
& = O\left((b^{\epsilon})^{i} n^{d - \epsilon} \right) 
\end{align}$$

$$\begin{align}
T(n) & = \sum\limits_{i=0}^{\log_{b}n} a^{i} f(\cfrac{n}{b^{i}})\\
& = O\left( \sum\limits_{i=0}^{\log_{b}n} (b^{\epsilon})^{i} n^{d - \epsilon} \right)\\
& = O\left( n^{d - \epsilon} \sum\limits_{i=0}^{\log_{b}n} (b^{\epsilon})^{i} \right)\\
& = O\left( n^{d - \epsilon} \sum\limits_{i=0}^{\log_{b}n} \cfrac{(b^{\epsilon})^{\log_{b}n +1} -1}{b^{\epsilon} -1} \right) \\
& = O\left( n^{d - \epsilon} \cfrac{(b^{\epsilon}) n^{\epsilon} -1}{b^{\epsilon} -1} \right) \\
& = O(n^{d - \epsilon} n^{\epsilon}) \\
& = O( n^{d}) \\
\end{align}$$

Quindi abbiamo
$$T(n) = O(n^{d})$$

#### Caso 2 dim

Vogliamo dimostrare che
$$f(n) = \Theta(n^{d})$$

$$\begin{align} T(n) & = \Theta(n^{d} \log n) \\
& = \sum\limits_{i=-}^{\log n} a^{i} f \left( \cfrac{n}{b^{i}} \right) \\ \end{align}$$

$$\begin{align} f \left( \cfrac{n}{b^{i}} \right)  & = a^{i} \Theta \left( \cfrac{n}{(b^{i})^{d}} \right) \\
& = a^{i} \Theta \left( \cfrac{n}{b^{i}} \right) \\ \end{align}$$


#### Caso 3 dim


