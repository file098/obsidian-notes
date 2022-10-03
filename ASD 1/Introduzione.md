2022-09-19

# Numeri di Fibonacci

Vogliamo scrivere un algoritmo che descriva la formula di Fibonacci.

$$F_n = 
\begin{align}
  \begin{cases}
  &1, ... & \text{se} \quad n=1,2 \\
  &F_{n-1} + F_{n-2} & \text{se} \quad n \geq 3 \\
  \end{cases}
\end{align}$$


2022-09-20

## Formula di Binet

$$\forall n \geq 1 \qquad F_n = \frac{1}{\sqrt{5}} (\phi^n - \hat{\phi}^n)$$
Dimostrare la formula di Binet:

> **_NOTE:_**  Per le dimostrazioni con numeri interi, è consigliata la tecnica di dimostrazione per induzione

> **_NOTE_**: $\phi$ è la sezione aurea

Induzione su $n$

Base: $n=1$

$$n =1 \qquad F_1 = \frac{1}{\sqrt{5}} (\phi - \hat{\phi})$$

$$$\frac{1}{\sqrt{5}} * (\frac{1 + \sqrt{5}}{2} - \frac{1 - \sqrt{5}}{2} )$$

$$\frac{1}{\sqrt{5}} * (\frac{ 1 - 1 + \sqrt{5} - \sqrt{5}}{2}) = 1$$

Base: $n = 2$
$$n =2 \qquad F_1 = \frac{1}{\sqrt{5}} (\phi^2 - \hat{\phi}^2)$$

$$\frac{1}{\sqrt{5}} [(\frac{1 + \sqrt{5}}{2})^2 - (\frac{1 - \sqrt{5}}{2})^2 ]$$

$$\frac{1}{\sqrt{5}} (\frac{1 + 2 \sqrt{5} + 5 - 1 - 2 \sqrt{5} +5}{4}) = \frac{1}{\sqrt{5}} \frac{4 \sqrt{5}}{4} = 2$$

Passo induttivo $n \geq 3$

$$\forall k \leq n -1$$

$$F_k = \frac{1}{\sqrt{5}} (\phi^k - \hat{\phi}^k)$$
Definizione della formula, ora sostituiamo i campi
$$F_{n}= F_{n-1}+ F_{n-2}$$

$$\frac{1}{\sqrt{5}} (\phi^{n-1}- \hat{\phi}^{n-1}) + \frac{1}{\sqrt{5}} (\phi^{n-2}- \hat{\phi}^{n-2})$$

$$\frac{1}{\sqrt{5}}[ (\phi^{n-1}+\phi^{n-2}) - (\hat{\phi}^{n-1} - \hat{\phi}^{n-2})]$$

Siamo arrivati ad un punto in cui la dimostrazione comincia a sembrare il caso iniziale, dove la differenza è solo nei termini di $\phi$. 
Se potessimo dimostrare che $(\phi^{n-1}+\phi^{n-2}) = \phi^n$ e $(\hat{\phi}^{n-1} - \hat{\phi}^{n-2}) = \hat{\phi^n}$ avremmo completato la dimostrazione. 

$$\begin{equation}
  \begin{cases}
   \phi^{n} = \phi^{n-1}+\phi^{n-2} \\
   \hat{\phi^{n}}= \hat{\phi}^{n-1} - \hat{\phi}^{n-2} \\
  \end{cases}
\end{equation}$$
ci rendiamo conto che dividendo tutto per $\phi^{n-2}$ otteniamo
$$\begin{equation}
  \begin{cases}
  \phi^{2} = \phi + 1\\
  \hat{\phi}^{2} = \hat{\phi} + 1 \\
  \end{cases}
\end{equation}$$
ed è vera per definizione di $\phi$ e $\hat{\phi}$, quindi la dimostrazione è vera e finita


### Algoritmo 
Scriviamo l'algoritmo ora che abbiamo la formula di Binet

```F#
Fib1(int n) -> int 
	return 1/5*(phi^n - hat_phi^n)
```

**Complessità**: T(n) = 1
**Correttezza**: <mark>No</mark>. Il teorema di Binet utilizza numeri razionali, dunque in una macchina, che usa numero approssimati, i valori non saranno sempre corretti.

L'implementazione precedente produce i seguenti risultati:
- n=3 -> 1.9999 -> 2 GIUSTO
- n=16 -> 986.698 -> 987 GIUSTO
- n=18 -> 2583.1 -> 2583 ERRATO

#### È possibile scrivere un algoritmo corretto?

```F#
Fib2(int n) -> int
	if(n <= 2) then return n
	else
		return Fib2(n-1) + Fib2(n-2)
```

**Complessità**: 
| n   | T(n)      |
| --- | --------- |
| 1   | 1         |
| 2   | 1         |
| 3   | 2+1+1 = 4 |
| 4   | 2+4+1 = 7 |

$$
T(n) = 
	\begin{align}
	  \begin{cases}
	    &1 \qquad \text{se} & n=1,2 \\
	    &2 + T_{n-1} + T_{n-2} & n \geq 3 \\
	  \end{cases}
	\end{align}$$


## Albero delle ricorsioni

COPIA APPUNTI SLIDES SU ALBERI !!!!!!!!!!!!!!!!!!!!!!!!!!!!


Formula generale: $T(n) = 2 * i(T_{n}) + f(T_{n})$ dove $i = \text{n}$ nodi interni e $f = \text{foglie}$ di $T(n)$. 

--- 

2022-09-27

#### Proposizione 1:
Sia $T_n$ l'albero di ricorsione relativo alla chiamata $\text{Fib2}(n)$, allora il numero di foglie di $f(T_n) = F_n$ cioè il numero di nodi foglia è uguale al n-esimo numero di Fibonacci. 

Dimostrazione: 

Passo induttivo $n \geq 3$

![[Pasted image 20220927124402.png]]

#### Proposizione 2:
Sia $T$ un albero dove i nodi interni hanno esattamente 2 figli, allora: il numero di nodi interni è sempre uguale al numero di foglie - 1

$$i(T) = f(T)-1$$

**Dimostrazione**: induzione su numero di noti di T

- caso base 1,2
- passo induttivo con $n \geq 3$
	- $\hat{T} = f(T) - 1 + i(T)$
	- $i(\hat{T}) = f(\hat{T} -1)$
	- obiettivo: $i(T) = f(T)-1$

![[Pasted image 20220927171321.png]]

Dobbiamo dimostrare che $i(T_{n}-1) = f(T_{n}-1)$

Consideriamo l'albero di partenza e aggiungiamo due foglie ad un nodo foglia già esistente: $f(T_{n}) = f(T_{n-1}) + 2$.
e di conseguenza anche il numero di nodi viene aggiornato: $i(T_{n)}= i(T_{n-1}) +1$.
Sappiamo che: 
- $i(T_n) = i(\hat{T_{n}}) + 1$
- $f(T_n) = f(\hat{T_n}) + 2$


$$
\begin{align}
& i(T_{n}) =  f(T_{n}) - 1 \\
& \text{aggiungiamo le due foglie} \\
& = f(\hat{T_{n}}) - 1 + 2 \\
& = f(\hat{T_{n}}) + 1
\end{align}
$$
e facciamo lo stesso per i nodi

$$
\begin{align}
& f(T_{n}) - 1 = i(T_{n})\\
& f(T_{n}) - 1 = i(\hat{T_{n}}) + 1 \\
& f(T_{n}) - 1 = i(\hat{T_{n}}) + 1 \\
\end{align}
$$

Quindi abbiamo 
$$i(\hat{T_{n})} + 1 = f(\hat{T_{n})} + 2$$
$$

$$

<mark>Forma completa</mark>: $T(n) = 2(F_n - 1) + F_n = 3F_{n} - 2 \approx F_n$  

#### Proposizione 3:
$$\forall n \geq 6 \qquad F_{n} \geq 2^{\frac{n}{2}}$$
**Dimostrazione**:
- base $n=6,7$
- passo induttivo $n \geq 8$
	- obiettivo: $F_{n} \geq 2^{\frac{n}{2}}$
	- $F_n = F_{n-1} - F_{n-2}$
	- $F_{n-1}\geq n^\frac{n-1}{2}$ e lo stesso vale per $F_{n-2}$


## Algoritmo Iterativo

```pseudo
Fib3(int n) -> int


alloca spazio per array di n interi F
F[1] = 1; F[2] = 1;
for i = 3 to n
	F[i] = F[i-1] + F[i-2]
return F[n] 
```

Complessità temporale: $T(n) = 3 + (n-1) + (n-2) = 2n \approx n$
Complessità spaziale: n


```pseudo
Fib4(int n) -> int
a = 1, b = 1
for i = 3 to n
	c = a + b
	a = b
	b = c
return c
```

Complessità temporale = $T(n) \approx n$
Complessità spaziale: 3


## Analisi algoritmi 

|      | correttezza | complessità temp    | complessità spaziale |
| ---- | ----------- | ------------------- | -------------------- |
| fib1 | no          | costante            | costante             |
| fib2 | si          | esponenziale: $2^n$ | lineare              |
| fib3 | si          | lineare             | lineare              |
| fib4 | si          | lineare             | costante             |
