# Spazi vettoriali
Sia V un insieme, chiamiamo i suoi elementi <mark>vettori</mark>. Diciamo che *V* è uno **spazio vettoriale** su $\mathbb{R}$ se sono definite due operazioni:

1. $+ : V \times V \rightarrow V, (u,v) \rightarrow u + v$ (somma)
2. $\mathbb{R} \times V \rightarrow V, (c,v) \rightarrow cv$ (prodotto per uno scalare)

tali che valgano i seguenti fatti

1. $(V, +)$ è un gruppo abeliano. Indichiamo con 0 l'elemento neutro della somma (il **vettore nullo**).
2. per ogni $c_1, c_2, \in \mathbb{R}$ e $v_1, v_2, \in V, c_1(v_1+v_2) = c_1v_1 + c_2v_2$ e $(c_1 + c_2)v_1 = c_1v_1+c_2v_1$ (proprietà distributiva)
3. per ogni $c_1, c_2, \in \mathbb{R}$ e $v_1 \in V, c_1(c_2v) = (c_1 c_2)v$  (proprietà associativa)
4. per ogni $v \in V, 1v = v$ e $0v = \pmb 0$

#### Esempio 
Sia $n \in \mathbb{N}$. L'insieme $\mathbb{R}^n$ è uno spazio vettoriale su $\mathbb({R}$, u cui vettori sono n-uple di numero reali. Per convenzione, se non viene specificato altro, intenderemo sempre gli elementi di $\mathbb{R}^n$ come vettori colonna del tipo:

$$  u =
	  \left ( {\begin{array}{cc}
	   1 \\
	   2 \\
	  \end{array} } \right) \in \mathbb{R}^2,
	v = 
		\left ( {\begin{array}{c} 1 \\ 0 \\ 7 \\ -9 \\ \end{array}} \right) \in \mathbb{R}^4	  
$$

scrivendo quindi $\pmb{u} = (1,-2)^T$ e $\pmb{v} = (1,0,7,-9)^T$. Possiamo interpretare tali vettori come matrici colonna, e tornerà comodo ma concettualmente sono oggetti differenti.

## Prodotto matrice-vettore di $\mathbb{R}^n$

Considerato lo spazio vettoriale $\mathbb{R}^n$. Data una matrice $A \in M_{m,n}$ ed un vettore $\pmb v \in \mathbb{R}^n$ possiamo parlare di **prodotto di matrice-vettore**.
$$M_{m,n}(R) \times \mathbb{R}^n \rightarrow \mathbb{R}^n, (A, \pmb{v}) \rightarrow A \pmb{v}$$ In pratica per calcolare tale prodotto è sufficiente calcolare il prodotto matriciale tra A e v è pensato come una matrice $n \times 1$.

## Sottospazio vettoriale

Sia V uno spazio vettoriale. Un sottoinsieme $W \subseteq V$ è detto un **sottospazio vettoriale** se è chiuso rispetto alla somma e al prodotto per uno scalare, ovvero: 

1. se $\pmb{u,v} \in W$ allora $\pmb{u + v} \in W$
2. se $c \subset \mathbb{R}, \pmb{v} \subset W$, allora $c\pmb{v} \subset W$

Un sottospazio vettoriale è esso stesso uno spazio vettoriale.

Sia V uno spazio vettoriale. Allora V e $\{0\}$ sono sottospazi di V.

$$span(\pmb{v,w}) = \{ 2\alpha_1 - \alpha_2, 0)^T | \alpha_1, \alpha_2 \in \mathbb{R}\}$$

#### Esempio
Sia $V = \mathbb{R}^3$ e siano$\pmb{v} = (2,0,0)^T, \pmb{w} = (0,-1,0)^T$. Allora,
$$span(\pmb{v,w}) = \{ (2\alpha_1, - \alpha_2,0)^T | \alpha_1, \alpha2 \in \mathbb{R}\}$$

indica il piano z = 0 dello spazio cartesiano, infatti qualsiasi vettore del tipo (x,y,0)^T vi appartiene.

Sia $V = \mathbb{R}^3$ e siano$\pmb{v} = (2,0,0)^T, \pmb{w} = (-1,0,0)^T$. Allora,
$$span(\pmb{v,w}) = \{ (2\alpha_1 - \alpha_2,0,0)^T | \alpha_1, \alpha2 \in \mathbb{R}\}$$

indica l'asse x dello spazio cartesiano. Se nell'esempio precedente due vettori generavano un piano, qui generano una retta.


### Prodotto scalare di $\mathbb{R}^2$

Sia $V = \mathbb{R}^2, \pmb{v} = (v_1, ..., v_n)^T, \pmb{w} = (w_1, ... w_n)^T \in V$. Definiamo il <mark>prodotto scalare</mark> tra v e w come:

$$V \times V \rightarrow \mathbb{R}, \pmb{v * w} = \sum^{n}_{i=1} v_iw_i$$

Se $\pmb{v*w} = 0$, diciamo che sono **ortogonali**. Definiamo inoltre la **norma** di $||v||  = \sqrt{\pmb v * v}$
