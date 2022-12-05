# Gruppi e campi

## Operazione su un inseme

Sia X un insieme non vuoto ($X \neq 0$) e sia

$$ X \times X = {(x,y) : x,y \in X}$$

il prodotto cartesiano di X con sé stesso. Un operazione binaria \* su X è una funzione

$$ _ : X \times X \rightarrow X, (x,y) \rightarrow x _ y$$

Esempi

Sia $X = \mathbb{N}$. L'operazione _somma_ è un operazione su X, mentre l'operazione _differenza_ non lo è

## Gruppo abeliano

Sia $X \neq 0$ e sia $*$ un'operazione su X. Chiamiamo $(X,*)$ un **gruppo abeliano**t se:

1. per ogni $x,y,z \in X$ abbiamo $(x *y)* z = x *(y* z)$ (proprietà associativa)
2. per ogni $x,y \in X$ si ha $x *y = x* y$ (proprietà commutativa)
3. esiste un elemento $n \in X$ tale che $n * x = x$ per ogni $x \in X$ (esistenza dell'elemento neutro)
4. per ogni $x \in X$ esiste un elemento $x' \in X$ tale che $x' * x = n$ (esistenza dell'inverso)

Esempi

$(\mathbb{N}, +)$ e $(\mathbb{N}, *)$ non sono gruppi abeliani
$(\mathbb{Z}, +)$ è un gruppo abeliano con elemento neutro 0, $(\mathbb{Z},*)$ non è un gruppo abeliano

## Campo

Sia $X \neq 0$ e siano $+$ e $*$ le operazioni di somma e prodotto su $X$.
Chiamiamo $(X, +,*)$ un campo se:

1. $(X, +)$ è un gruppo abeliano con elemento neutro $O_X$
2. $(X / \{O_X\}, +)$ è un gruppo abeliano
3. per ogni $x, y, z \in X$ si ha $x *(y+z) = x*y + x*z$ (proprietà distributiva di $*$ rispetto a $+$)

si parla di inverso se l'operazione è la moltiplicazione $x' * x = 1_X$ di opposti se l'operazione è la somma $x' + x = 0_X$

Esempi

$(\mathbb{Q}, +, *)$ e $(\mathbb{R}, +,*)$ sono campi. Anche $(B, +_B, *_B)$ è un campo

Esercizio

Siano T = {0,1,2} e S = {0,1,2,3}. Si considerino le operazioni $+_T, *_T, +_S, *_S$ definite analogamente $a +_B *_B.$
$(T, +_T, *_T)$ e $(S, +_S, *_S)$ sono campi?

## Unità immaginaria

Si definisce unità immaginaria il numero _i_ tale che
$$i^2 = -1$$

in altre parole $i := \sqrt{-1}$

Esempi

Considerando l'unità immaginaria, l'equazione $x^2 + 2 = 0$ ammette ora due soluzioni:
$x = \pm \sqrt{-2} = \pm \sqrt{2i^2} = \pm \sqrt{2}$

### Coniugio

Proprietà del coniugio

$$ \bar {\bar{z}} = z \\
\bar{z} + z = 2Re(z) \\
z - \bar{z} = 2Im(z)i \\
z * \bar{z} \in \mathbb{R}\_{\leq 0}$$

## Il campo $\mathbb{C}$

$\mathbb{C}, +, *$ è un campo. In particolare, dato un numero compreso $z = x + iy$, il suo inverso moltiplicativo è:

$$ z^{-1} = \frac{x}{x^2 + y^2}-i\frac{y}{x^2 + y^2}$$

$\mathbb{C}$ non è un campo ordinato! Non esiste un ordinamento naturale, quindi non ha senso prendere due numero complessi e compararli uno a l'altro. Quindi i numeri complessi non sono comparabili in disequazioni.

Esiste una corrispondenza biunivoca tra numeri complessi ed elementi in $\mathbb{R}^2$. Dato infatti $z = x + iy$, associamo:
$$ z \in \mathbb{C} \rightarrow (x,y) \in \mathbb{R}^2$$

Infatti possiamo rappresentare un numero complesso nel **piano di Gauss**, il cui asse delle ascisse è l'**asse reale** e l'asse delle ordinate è l'**asse immaginario**.

Il modulo di un numero complesso $z = x + iy$ è
$$ |z| := x^2 + y^2 = \sqrt{z * \bar{z}}$$
