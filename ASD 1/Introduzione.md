2022-09-19

# Numeri di Fibonacci
Vogliamo scrivere un algoritmo che descriva la formula di Fibonacci.

$$F_n = \begin{equation}
		  \begin{cases}
		  1, ... \quad \text{se} \quad n=1,2 \\
		  F_{n-1} + F_{n-2} \quad \text{se} \quad n \geq 3 \\
		  \end{cases}
		\end{equation}$$

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

$$T(n) = \begin{equation}
		  \begin{cases}
		  1 \qquad \text{se} \qquad n=1,2 \\
		  2 + T_{n-1} + T_{n-2} \qquad n \geq 3 \\
		  \end{cases}
		\end{equation}$$


# Albero delle ricorsioni

COPIA APPUNTI SLIDES SU ALBERI !!!!!!!!!!!!!!!!!!!!!!!!!!!!

Complessità dei Fib2 = $T(n) = i(T_n) *2 f(T_n)$ dove i = n nodi interni e f = foglie

