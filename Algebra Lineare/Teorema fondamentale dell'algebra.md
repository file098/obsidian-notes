# Teorema fondamentale dell'algebra

Sia $p(z) = a_n z^n + a_{n-1} z^{n-1} + a_1 z + a_0$ un polinomio di grado $n \in \mathbb{N}$ a coefficienti $a_0, ..., a_n \in \mathbb{C}$. Allora $p(z)$ ammette $n$ zeri complessi contati con la loro molteplicità.

## Forma polare di un numero complesso

Un numero complesso $z \in \mathbb{C}$ può essere scritto in forma **polare** come

$$ z = |z|(\cos\theta + i \sin\theta), \theta \in [0, 2\pi)$$

## Potenza di un numero complesso

### Proposizione Formula di De Moivre

Sia $z = |z|(\cos\theta + i \sin\theta) \in \mathbb{C}$. Allora per ogni $n \in \mathbb{N}$ si ha

$$ z^n = |z|(\cos n\theta + \sin n\theta) $$

### Formula di Eulero

Per ogni $\theta \in \mathbb{R}$ si ha

$$e^{i\theta} = \cos \theta + i \sin \theta \in \mathbb{C}$$

Valgono dunque le seguenti proprietà:

- $|e^{i\theta}| = 1$

- $e^{n\theta} = e^{-i\theta}$

- $e^{i(\theta + 2k \pi)} = e^{i\theta}, k \in \mathbb{N}$

### Corollario di Eulero

$$e^{i\pi} + 1 = 0$$

### Formula esponenziale di un numero complesso

In generale osserviamo che $e^{x+iy} = e^x * e^{iy}$

Per ogni $z \in \mathbb{C}$, si ha $e^z \neq 0$ non è mai nullo! (ma può essere un numero reale negativo)

Un numero complesso $z \in \mathbb{C}$ può essere scritto in **forma esponenziale** come

$$ z = |z|e^{i\theta}, \theta \in [0,2\pi)$$

L'angolo $\theta$ è chiamato l'**argomento** di $z$. La forma esponenziale si ottiene banalmente dalla forma polare.

ula esponenziale di un numero complesso

In generale osserviamo che $e^{x+iy} = e^x * e^{iy}$

Per ogni $z \in \mathbb{C}$, si ha $e^z \neq 0$ non è mai nullo! (ma può essere un numero reale negativo)

Un numero complesso $z \in \mathbb{C}$ può essere scritto in **forma esponenziale** come

$$ z = |z|e^{i\theta}, \theta \in [0,2\pi)$$

L'angolo $\theta$ è chiamato l'**argomento** di $z$. La forma esponenziale si ottiene banalmente dalla forma polare.

### Radici complesse dell'unità

Per il teorema formale dell'algebra, esistono _n_ soluzioni dell'equazione (1)
$$z^n = 1$$
In particolare, abbiamo il seguente risultato che caratterizza con precisione le radici dell'unità

#### Proposizione

Per ogni $n \in \mathbb{N}$, l'equazione (1) ammette n soluzioni distinte

Dato $z^n = 1$, ne consegue che $|z| = 1$. Dunque

$$z^n = (\cos \theta + i \sin\theta)^n = \cos n \theta + i \sin n \theta = e^{in\theta}$$

da cui 

$$ e^{in\theta} = 1 \rightarrow e^{in\theta} = \cos 2k\pi + i\sin 2k\pi = e^{2ik\pi}, k \in \mathbb{N}$$

Ne consegue

$$in\theta = 2ik\pi \rightarrow \theta = \frac{2k\pi}{n}, k \in \mathbb{N}$$

### Radici di un numero complesso

$\phi$ rappresenta un piccolo "shift" nell'angolo preso in considerazione, quindi $\theta$ e qualcosa rappresentato da $\phi$

Per ogni $n \in \mathbb{N}$ e $w = |w|e^{i\phi} \in \mathbb{C}$, l'equazione $z^n = w$ ammette *n* soluzioni distinte

$$\omega_k = \sqrt{|w|e^{i\theta_k}}$$ 

dove $\theta_k = \frac{\phi}{n} + \frac{2k\pi}{n}, k = 0, ..., n-1$


