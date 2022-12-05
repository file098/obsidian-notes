# Matrici

Una matrice A di *m* righe e *n* colonne su un campo $K, m, n \in \mathbb{N}$ è una tabella i cui elementi sono $A_{ij} \in K$ dove $1 \leq i \leq m$ è l'indice di riga e $1 \leq j \leq n$ è l'indice di colonna, che si esprime come: 

$$
  A_{m\times n} =
  \left[ {\begin{array}{cccc}
    a_{11} & a_{12} & \cdots & a_{1n}\\
    a_{21} & a_{22} & \cdots & a_{2n}\\
    \vdots & \vdots & \ddots & \vdots\\
    a_{m1} & a_{m2} & \cdots & a_{mn}\\
  \end{array} } \right]
$$

Indichiamo con $M_{m,n}(K)$ l'insieme di tutte le matrici $m x n$ su K. Inoltre indichiamo con $A_i$ la i-esima riga della matrice A e con $A_j$ la sua j-esima colonna. Quindi

- j = colonna
- i = riga

Una sottomatrice di una matrice $A \in M_{m,n} (K)$ è la matrice che si ottiene scartando alcune  righe e/o colonne di A. 

#### Esempio

Sia A una matrice, una sua **sottomatrice** è la matrice 
$$
  B =
  \left ( {\begin{array}{cc}
   -1 & 3 & 0 \\
   1 & 1 & 0 \\
  \end{array} } \right)
$$
ottenuta eliminando l'ultima riga e la prima colonna di $A$

## Matrici quadrate

Una matrice si dice **quadrata** di ordine *n* se è composta da *n* righe e colonne. In tal caso, scriviamo l'insieme delle matrici quadrate su K come M_{m,n}(K) := M_n(K). Se una matrice non è quadrata, è <mark>rettangolare</mark>. 
Sia $A \in M_n(K)$ una matrice quadrata. Gli elementi $a_{ii}, 0 \leq i \leq n$, sono detti elementi diagonali  e formano la <mark>diagonale</mark> di A. 

#### Esempio 
La matrice quadrata $2 \times 2$ su $\mathbb{R}$.
$$A =\left ( {\begin{array}{cc} 1 & -2 \\ \pi & 0 \\ \end{array} } \right)$$ ha com elementi diagonali $a_{11} = 1$ e $a_{22} = 0$. 

Sia $A \in M_n(K)$  una matrice quadrata. La sua <mark>traccia</mark> è definita come la somma dei suoi elementi diagonali, cioè: 
$$tr(A) := \sum^{n}_{i=1}a_{ii}$$

Sia $A \in M_n(K)$  una matrice quadrata. Diciamo che A è simmetrica se per ogni $i,j \in {1,..., n}$ abbiamo $a_{ij} = a_{ji}$

## Matrici diagonali

Sia $A \in M_n (K)$ una matrice quadrata. Diciamo che A è una <mark>matrice diagonale</mark> se $a_{ij} = 0$ per ogni $i \neq j, i \leq i,j \leq n$

Sia $A \in M_n (K)$ una matrice diagonale. Se $a_{ii} = 1$ per ogni $1 \leq i \leq n$, diciamo che A è la matrice identità di ordine *n*. 

#### Esempio 

La matrice $A =\left ( {\begin{array}{cc} 2 & 0 \\ 0 & 0 \\ \end{array} } \right)$ è una matrice diagonale così come $B =\left ( {\begin{array}{cc} 1 & 0 \\ 0 & -\frac{3}{5} \\ \end{array} } \right)$. La matrice identità di ordine 2 è $I =\left ( {\begin{array}{cc} 1 & 0 \\ 0 & 1 \\ \end{array} } \right)$

Sia $A \in M_n (K)$ una matrice quadrata. Diciamo che A è una <mark>una matrice triangolare inferiore</mark> se $a_{ij} = 0$ per ogni $i > j, 1 \leq i,j \leq n$. Diciamo che A è una <mark>matrice triangolare superiore</mark> se $a_{ij} = 0$ per ogni $i < j, 1 \leq i,j \leq n$

$$
  A =
  \left ( { \begin{array}{ccc}
   \color{red} 1 & \color{cyan} 0 & \color{cyan}0 \\
   \color{red} -1 & \color{red} 2 & \color{cyan} 0 \\
   \color{red} 0 & \color{red} 1 &\color{red}  0 \\
  \end{array} } \right)
$$
## Somma di matrici

Siano  $A, B \in M_{m,n} (K)$. Definiamo la somma matriciale di A e B la matrice $S := A + B \in M_{m,n} (K)$ tale che $s_{ij} = a_{ij} + b_{ij}$ per ogni $1 \leq i \leq m$ e $1 \leq j \leq n$.

Possiamo sommare solo matrici delle stesse dimensioni. 

#### Esempio
$$
A =
  \left ( {\begin{array}{cc}
   2 & 1 & 0 \\
   0 & -1 & 2 \\
  \end{array} } \right)   \qquad \qquad
B =
  \left ( {\begin{array}{cc}
   0 & 0 & 1 \\
   1 & 0 & -1 \\
  \end{array} } \right) \qquad \qquad
A + B = 
  \left ( {\begin{array}{cc}
   2 &1&1 \\
   1&-1&1 \\
  \end{array} } \right)
$$

## Prodotto di matrici

Siano $A, B \in M_{m,n} (K)$. Definiamo la <mark>prodotto matriciale</mark> di A e B la matrice $P := AB \in M_{m,n} (K)$ tale che
$$\sum_{l=1}^{n}a_{il}\times b_{lj}, \quad 1\leq i \leq m, 1 \leq j \leq k$$
A e B possono avere dimensioni diverse, ma il numero di colonne di A deve corrispondere al numero di righe di B. Se in particolare $A, B \in M_{n,n} (K)$ è possibile calcolare sia AB che BA ma tipicamente $AB \neq BA$, ovvero il **prodotto matriciale non è commutativo**. 

#### Esempio 
$$
A =
  \left ( {\begin{array}{cc}
   2 & 1 & 0 & 1 \\
   0 & 1 & 1 & 3 \\
  \end{array} } \right)   \qquad \qquad
B =
  \left ( {\begin{array}{cc}
   1 & -1 & -1 \\
   0 & 1 & 0 \\
	1 & 2 & 0 \\
	0 & 3 & 0 \\
  \end{array} } \right) \qquad \qquad
AB = 
  \left ( {\begin{array}{cc}
   2 & -4 & -2 \\
   1& 12 & 0 \\
  \end{array} } \right)
$$

(vedi appunti su quaderno per il procedimento)

### Prodotto di una matrice per uno scalare ed altre proprietà

Siano $A \in M_{m,n} (K), c \in K$. Definiamo il <mark>prodotto di una matrice per uno scalare</mark> tra A e *c* la matrice $cA \in M_{m,n} (K)$ tale che
$$ca_{ij} = c \times a_{ij}, \quad 1\leq i \leq m, 1 \leq j \leq n$$ Se A, B e C sono tre matrici delle giuste dimensioni, e $c \in K$, valgono le seguenti proprietà:
- $A(B + C) = AB + AC$ e $(A+B)C = AC+BC$
- $c(AB) = (cA)B$
- $(AB)C = A(BC)$
- Sia *l* la matrice identità e *O* la matrice nulle (tutte le entrate sono zeri) delle giuste dimensioni. Allora $IA = AI = A$ e $AO = OA = O$. (funziona come il prodotto normale)

### Matrici trasposte e simmetriche 

Sia $A \in M_{m,n} (K), c \in K$. La <mark>matrice trasposta</mark> di A è la matrice $A^T \in M_{m,n} (K)$ tale che, indicando con $a_{ij}^T$ gli elementi di $A^T$. 

$$
A =
  \left ( {\begin{array}{cccc}
   1 & 1 & 0 & -1 \\
   0 & 0 & 1 & 1 \\
   2 & 1 & -3 & 0 \\
  \end{array}} \right) 
\qquad \qquad
A^T =
  \left ( {\begin{array}{cccc}
   1 & 0 & 2 \\
   1 & 0 & 1 \\
	0 & 1 & -3 \\
	-1 & 1 & 0 \\
  \end{array} } \right)
$$

Sia $A \in M_{m,n} (K), n \in \mathbb{N}$. A è una matrice simmetrica se e solo se $A = A^T$.

Essendo un equivalenza, la proposizione predente è di fatto una definizione alternative di matrice simmetrica (la più comune). Alcune proprietà della trasposizione, nell'ipotesi che le operazioni abbiano senso (matrici di giuste dimensioni).
- $(A^T)^T = A$
- $(A + B)^T = A^T + B^T$
- $(AB)^T = B^T A^T$
- $(cA)^T = cA^T, c \in K$


## Matrice inversa

Sia $A \in M_{m,n} (K), c \in K$. A è detta <mark>matrice invertibile</mark> se esiste una matrice $B \in M_{m,n} (K)$ detta <mark>matrice inversa</mark>,  tale che $AB = BA = I$ dove *l* è la matrice identità di ordine *n*. In tal caso, scriveremo $B = A^{-1}$.

Siano $A, B \in M_n(K), n \in \mathbb{N}$
1. se A è invertibile, la sua inversa $A^{-1}$ è unica
2. se A e B sono invertibili, abbiamo $(AB)^{-1} = B^{-1}A^{-1}$

#### Combinazioni lineari di righe

Sia $A \in M_{m,n} (K), c \in K$. e siano $A_1, ... , A_m$ le sue righe. Una <mark>combinazione lineare</mark> $L \in M_{1,n} (K)$ delle righe di A è 
$$L = \alpha_1A_{1,:} + ... + \alpha_mA_m$$
dove $\alpha_1,...,\alpha_m \in K$.

Sia $A = \left ( {\begin{array}{cccc} 1 & 2 \\ -4 & 0 \\ 0 & 1 \\ \end{array}} \right)$. Scegliendo $\alpha_1=1,\alpha_2 = -\frac{1}{2}, \alpha_3=0$ abbiamo la combinazione lineare $L = (3 \quad 2)$. 

#### Indipendenza lineare di righe

Sia $A \in M_{m,n} (K), c \in K$. Le sue righe $A_1, ... , A_m$ si dicono <mark>linearmente indipendenti</mark> se, cercando coefficienti $\alpha_1, ..., \alpha_m \in K$ tali che
$$\alpha_1A_{1,:} + ... + \alpha_mA_{m,:} = O$$
dove $O \in M_{1,n}(K$) è  la matrice nulla, se l'unica soluzione possibile è $\alpha_1 = ... \alpha_m = 0$. 

Se le righe di una matrice non sono linearmente indipendenti, allora sono linearmente dipendenti. Vista da un'altra prospettiva, se le righe sono linearmente dipendenti allora possiamo esprimete una riga come combinazione lineare delle altre.

## Teorema di Binet

Siano $A, B \in M_2 (K)$. Allora $det(AB) = det(A)det(B)$. Scriviamo $A = \left ( {\begin{array}{cccc} a & b \\ c & d\\ \end{array}} \right)$ e $B = \left ( {\begin{array}{cccc} a' & b' \\ c' & d'\\ \end{array}} \right)$. da cui $AB = \left ( {\begin{array}{cccc} aa' + bc' & ab' + bd' \\ ca' + dc' & cb' + dd' \\ \end{array}} \right)$. È sufficiente verificare dunque la testi $det(AB)$ ovvero:
$$(aa' + bc')(ab' + bd') - (ca' + dc')( cb' + dd') = (ad - bc)(a'd'-b'c')$$

Sia $A = \left ( {\begin{array}{cccc} a & b \\ c & d\\ \end{array}} \right) \in M_2(K)$. A è <mark>invertibile</mark> se e solo se $det(A) \neq 0$ ed in tal caso 

$$A^{-1} = \frac{1}{det(A)} \left ( {\begin{array}{cccc} a & -d \\ -c & a\\ \end{array}} \right)$$

### Determinante: forma generale

Sia $A \in M_n (K)$. Definiamo la **matrice aggiunta dell'elemento $a_{ij}$** la matrice $A^{(i,j)} \in M_{n-1} (K)$, sottomatrice di A, che si ottiene eliminando la i-esima riga e la j-esima colonna di A, $1 \leq i,j \leq n$. 

Calcolo della determinante di una matrice quadrata $2 \times 2$.
$$det \left ( {\begin{array}{cccc} a & b \\ c & d\\ \end{array}} \right) = (a*d)-(b*c)$$

#### Risultato del Teorema di Laplace 

Sia $A \in M_n (K)$. Il determinante di A può essere calcolato in modo *induttivo* in entrambi i seguenti modi 
1. fissata una riga $i \in {1,...,n}$ scriviamo $det(A):= \sum^{n}_{j=1} (-1)^{i+j} a_{ij} det(A^{(i,j)})$
2. fissata una colonna $j \in {1,...,n}$ scriviamo $det(A):= \sum^{n}_{i=1} (-1)^{i+j} a_{ij} det(A^{(i,j)})$

### Regola di Sarrus per il determinante

Esiste una strategia per il calcolo del determinante che è valido **esclusivamente** per matrici $3 \times3$ ed è la cosiddetta <mark>regola di Sarrus</mark>.

Data una matrice $A = \left ( {\begin{array}{cccc} a & b & c \\ d & e & f \\ g & h & i \end{array}} \right)$, allora il suo determinate può essere calcolato come $det(A) = aei + bfg + cdh - afh - dbi - ceg$. 

![[Screenshot from 2022-08-23 11-08-45 1.png]]

## Rango di una matrice 

Sia $A \in M_n (K)$. Il <mark>rango</mark> della matrice A, che denotiamo come $rg(A)$ è il numero massimo di righe (o equivalentemente di colonne) di A che sono linearmente indipendenti. 
Di conseguenza, $rg(A) \geq min\{m,n\}$

#### Esempio
 Sia $A = \left ( {\begin{array}{cccc} a & b & c \\ d & e & f \\ \end{array}} \right)$. Innanzitutto, abbiamo $rg(A) \geq 2$. Le prime due colonne sono linearmente indipendenti quindi $rg(A) = 2$ (sappiamo che non può essere 3, in questo caso lo si vede perché $A_{:,3} = 2A_{:.1} - A_{:,2})$.

### Minori e rango, orlati

Sia $A \in M_n (K)$. La matrice A ha rango k se:
1. tutti i suoi minori di ordine k sono diversi da 0
2. tutti i suoi minori di ordine k+1 sono nulli

In quanto segue, vediamo come si può evitare di calcolare molti minori della matrice

Sia $A \in M_n (K)$ e sia $B \in M_n (K)$ una sottomatrice di ordine $k$ di $A$, ottenuta selezionando $k$ righe e $k$ colonne. Un <mark>orlato</mark> di $B$ è una sottomatrice $B'$ di A di ordine $k+1$ che si ottiene aggiungendo una riga ed una colonna a $B$. 

#### Esempio
Sia $A = \left ( {\begin{array}{cccc} 0 & 0 & 3 & 4 \\ -1 & \frac{1}{2} & 0 & 1\\ 6 & -5 & 1 & 0 \\ \end{array}} \right)$

### Teorema degli orlati

Sia $A \in M_n (K)$. La matrice A ha rango k se e solo se:
1. esiste una sottomatrice $B$ di ordine $k$ tale che $det(B) \neq 0$
2. tutti gli orlati di $B$ di ordine $k+1$ hanno determinante nullo

Questo risultato è ottimo, perché consente di calcolare il rango di una matrice senza dover calcolare troppi minori. 

