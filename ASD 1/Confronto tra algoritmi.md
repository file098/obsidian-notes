2022-09-27

# Confronto tra algoritmi

Una funzione $f(n)$ si dice che appartiene alla classe 
$$O(g(n)) = \begin{align}
\begin{cases}
f(n) \quad | \\
& \exists c > 0 \\
& \exists n_0 \in \mathbb{N} \quad \text{t.c.} \quad \forall n \geq n_0: \\
& &  f(n) \leq c * g(n) \\
\end{cases}
\end{align}$$



## O grande
> **_Notazione_**
> $$f(n) = O(g(n))$$

Stiamo dicendo che f appartiene a $O$.

Dimostriamo che $\frac{1}{2}n^{2}- 3n = O(n^2)$
$$\exists c > 0 \quad \exists n_{0} \in \mathbb{N} \quad \text{t.c.} \quad \forall n \geq n_0$$
$$\frac{1}{2}n^{2}- 3n \leq c * n^2$$
$$\frac{1}{2}n - 3 \leq c * n$$
$$\frac{1}{2}n - cn \leq 3$$
$$(\frac{1}{2} - c)n \leq 3$$
$$c \geq \frac{1}{2} > 0 \qquad \forall n \geq 1$$

Quindi $c = \cfrac{1}{2}$ e $n_0 = 1$

## Omega

$$\Omega(g(n)) =\begin{align}
\begin{cases}
f(n) \quad | \\
& \exists c > 0 \\
& \exists n_0 \in \mathbb{N} \quad \text{t.c.} \quad \forall n \geq n_0: \\
& & c * g(n) \leq f(n) \\
\end{cases}
\end{align}$$

> **_Notazione_**
> $$f(n) = \Omega(g(n))$$

Dimostriamo che $\frac{1}{2}n^{2}- 3n = \Omega(n^2)$
$$\exists c > 0 \quad \exists n_{0} \in \mathbb{N} \quad \text{t.c.} \quad \forall n \geq n_0$$
$$c * n^{2}\leq \frac{1}{2}n^{2}- 3n$$
$$ c * n \leq \frac{1}{2}n - 3$$
$$\frac{1}{2}n - cn \leq 3$$
$$n\left(\frac{1}{2} - c\right)\geq 3$$
$$c \geq \frac{1}{2} > 0 \qquad \forall n \geq 1$$

supponendo che $\frac{1}{2} - c > 0 \qquad [c < 1/2]$

si ha: $n \geq \cfrac{3}{\cfrac{1}{2} - c} = \cfrac{6}{1-2c}$ scegliamo che $c = \cfrac{1}{14}$ si ottiene $n \geq \cfrac{6}{1 - \frac{1}{7}} = 7$


## Theta

$$\Theta(g(n)) =\begin{align}
\begin{cases}
f(n) \quad | \\
& \exists c_{1} > 0 \quad \exists c_{2} > 0 \\
& \exists n_0 \in \mathbb{N} \quad \text{t.c.} \quad \forall n \geq n_0: \\
& & c_1 * g(n) \leq f(n) \leq c_{2}* g(n) \\
\end{cases}
\end{align}$$

> **_Notazione_**
> $$f(n) = \Theta(g(n))$$

### Proprietà 
$$f(n) = \Theta(g(n)) \iff f(n) = O(g(n)) \land \Omega(g(n))$$
Quindi: $\frac{1}{2}n^{2}- 3n = \Theta(n^2)$

## Esercizi
$$\sqrt{n+10} = \Theta(\sqrt{n})$$

$$\exists c_1, c_2 > 0 \qquad \exists n_0 \in \mathbb{N} \quad t.c. \quad \forall n \geq n_0$$
$$c_{1} \sqrt{n} \leq \sqrt{n+10} \leq c_{2} \sqrt{n}$$

$$c_{1}^2 n \leq n+10 \leq c_{2}^2 n$$
1) 
$$c_{1}^{2} n \leq n+10 \iff (c_{1}^{2} - 1)n \leq 10$$
se $c_{1}^{2} - 1 \leq 0 \quad (c_{1}^{2} \leq 1, c_{1} \leq 1)$ vera per $\forall n \geq 1$

2) 
$$c_{1}^{2} n \geq n+10 \iff (c_{1}^{2} - 1)n \geq 10$$
se $c_{1} \geq 1: n \geq \cfrac{10}{c_{2}^{2} - 1}$

Proviamo $c_2 = \sqrt{2} \quad (> 1)$ si ha che $n \geq 10$

## Esempi
--- 
$$n! = O(n^n)$$
Infatti:
$$
\begin{align}
n!
& = 1 * 2 * 3 ... n \\
& \leq n * n * n ... n \\
& = n^n
\end{align}$$ 
$\log{n} = O(n)$
--- 

$$n! = \Omega(2^n)$$
Infatti:
$$
\begin{align}
n!
& = 1 * 2 ... n \\
& \geq 1 * 2 * 2 ... 2 \\
& = 2^{n-1}
\end{align}$$
Quindi: $2^{n-1} \leq n1 \quad \forall n \geq 1$
Da cui:
$$\cfrac{1}{2} 2^{n}= n! \quad \forall n \geq 1$$
$$c = \cfrac{1}{2} \qquad n_0 =1$$

--- 
$\log n! = O(n \log n)$
Infatti:
$$
\begin{align}
\log n! =\\
& =\log \prod_{i=1}^{n} i \\
& =\sum\__{i=1}^{n} \log i\\
& \leq n \log n \\
\end{align}$$

## Proprietà

$$f(n) = O(g(n)) \iff g(n) = \Omega(f(n))$$
Dim: $(\implies)$

Ipotesi:

$$\begin{align} \exists c > 0 \quad \exists n \in \mathbb{N} \quad \text{t.c.} \quad \forall n \ge n_{0}:\\
& f(n) \leq c * g(n) \end{align}$$

Tesi: 

$$
\begin{align}
\exists c' > 0 \quad \exists n_{0}' \in \mathbb{N} \quad \text{t.c.} \quad \forall n \ge n_{0}': \\
& c*f(n) \leq g(n) 
\end{align}
$$


Si ponga: $c' = \cfrac{1}{c} > 0$

$$n_{0}'= n_{0}$$

### Proprietà transitiva

Se $f(n) = O(g(n))$ e $g(n) = O(h(n))$

allora: $f(n) = O(h(n))$

Ipotesi:
$$\begin{align} \exists c_1 > 0 \quad \exists n_1 \in \mathbb{N} \quad \text{t.c.} \quad \forall n \ge n_{1}:\\
& f(n) \leq c_1 * g(n) \end{align}$$

Ipotesi:
$$\begin{align} \exists c_2 > 0 \quad \exists n_2 \in \mathbb{N} \quad \text{t.c.} \quad \forall n \ge n_{2}:\\
& f(n) \leq c_2 * g(n) \end{align}$$

Tesi:
$$\begin{align} \exists c_3 > 0 \quad \exists n_3 \in \mathbb{N} \quad \text{t.c.} \quad \forall n \ge n_{3}:\\
& f(n) \leq c_3 * g(n) \end{align}$$

$$
\begin{align}
& n_3 = \text{max}\{n_1, n_2\} \quad \forall n \geq n_{3} \\
& f(n) \leq c_1 g(n) \land g(n) \leq c_{2}h(n) \\
& f(n) \leq c_{1}c_{2}h(n) \\
\end{align}$$
2022-10-05 

## Osservazioni

$$
\lim_{n \rightarrow \infty} \cfrac{f(n)}{g(n)} = 
\begin{cases}  
o & \implies & f(n) = O(g(n)) \\
l \qquad (0 < l < \infty) & \implies & f(n) = \Theta(g(n))  \\
\infty & \implies & f(n) = \Omega(g(n))
\end{cases}
$$


1) $o(g(n)) \cap \Omega(g(n)) = \emptyset$
2) $\omega(g(n)) \cap O(g(n)) = \emptyset$

Dimostrazione (1) per assurdo:

Partiamo con la supposizione che $\color{red} \exists f(n) \in o(g(n)) \cap \Omega(g(n))$
Quindi:
$$
\begin{align}
\forall c > 0 \quad \exists n_{0}\in \mathbb{N} \quad t.c. \quad \forall n > n_{0} \quad f(n) < c * g(n) \\
\exists c' > 0 \quad \exists n_{0}' \in \mathbb{N} \quad t.c. \quad \forall n > n_{0}' \quad c' * g(n) < f(n)   \\
\end{align}
$$

se e solo se $n \geq max\{n_{0}, n_{0}'\}$ si avrebbe $\color{red} f(n) < c' * g(n) \leq f(n)$ il che è assurdo perché avrei trovato un numero strettamente minore di se stesso. 

**Proposizione**

Se $\lim_{n \rightarrow \infty} \cfrac{f(n)}{g(n)} = l \quad (0 < l < \infty)$ allora $f(n) = \Theta(g(n))$.

> **Nota**
> Se il limite del rapporto produce un valore costante, allora f(n) e g(n) sono uguali asintoticamente

Esempio: 

$1 + \sin(n)n = O(n)$ dove:
- $f(n) = 1 + \sin(n)n$
- $g(n) = O(n)$

Sappiamo che $-1 \leq \sin(n) \leq 1$ dal comportamento della funzione seno.

$$
\begin{align}
\forall n \geq 1: \\
& 0 \leq (1 + \sin(n)) \leq 2 \\
& 0 \leq (1 + \sin n)n \leq 2n & & \text{verificato}
\end{align}
$$
Vediamo come si comporta con il limite

$$
\lim_{n \rightarrow \infty} \cfrac{(1 + \sin n)n}{n} = (1 \sin n)
$$
dove il limite non esiste perché è una funzione armonica. 

## Polinomi

Osserviamo $3n^{3} + 2n^{2}+6n+5=\Theta(n^{3})$


$$
\begin{align}
\lim_{n \rightarrow \infty} \cfrac{3n^{3} + 2n^{2}+6n+5}{n^{3}} = \\
\lim_{n \rightarrow \infty} 3 + \cfrac{2}{n} + \cfrac{6}{n^{2}}+ \cfrac{5}{n^{3}} = 3 \\
\end{align}$$

> **Nota**
> Si va a cercare il termine dominante e gli altri possono essere trascurati
> Ex: $27n^{2} + n^{2} \log n + \sqrt{n} + \log n^{2} = \Theta(n^{2} \log n)$

### Proprietà

Forma compatta: $f(n) + o(f(n)) = \Theta(f(n))$

Forma estesa:

$$

\begin{align}
g(n) = \Theta(f(n)) \Longleftarrow

\begin{cases}
    g(n) = f(n) + h(n) \\ \\
    h(n) = o(f(n))
\end{cases} 

\end{align} 

$$
$$
\lim_{n \rightarrow \infty} \cfrac{g(n)}{f(n)} = \lim_{n \rightarrow \infty} \cfrac{f(n) + h(n)}{f(n)} = \lim_{n \rightarrow \infty} 1 + \cfrac{h(n)}{f(n)} = 1
$$
perché $\cfrac{h(n)}{f(n)}$ tendo a 0 dato che $f(n)$ tende a infinito e cresce più velocemente di $h(n)$.

