2023-02-20
# Introduzione

Un applicazione ha bisogno: 
- insieme dinamico
- ogni elemento ha un chiave estratta da un'universo $U \in \{ 0,1,...,\omega-1\}$
- nessun elemento ha la stessa chiave

Si può utilizzare un array la cui dimensione è $T[0,...,\omega-1]$
- ogni posizione del mio array corrisponde ad una chiave in $U$
- se c'è l'elemento $x$ con chiave $k$, allora $T[k]$ contiene un puntatore all'elemento $x$
- se l'elemento non è presente $T[k] = NIL$, inserisco l'elemento in $T[k]$

Le operazioni da implementare sono:

## Operazioni su tabella indirizzamento diretto

### Ricerca
```python 
def direct_address_search(T,k):
	return T[k]
```
complessità: $\Theta(1)$

### Inserimento
```python
def direct_address_insert(T,x):
	T[x.key] = x
```
complessità: $\Theta(1)$

### Cancellazione
```python
def direct_address_delete(T,x):
	T[x.key] = NIL
```
complessità: $\Theta(1)$

**Vantaggio**: operazioni in tempo costante
**Svantaggio**: Lo spazio utilizzato è proporzionale a $\omega=|U|$ e  non al numero n di elemento effettivamente associati -> spreco di memoria 

## Tabelle hash

Quando l'insieme delle chiavi da memorizzare è molto più piccolo dell'universo U (tutte le possibili chiavi), allora una tabella hash richiede molto meno spazio di una tabella ad indirizzamento diretto.

### Caratteristiche

una tabella hash ha le seguenti caratteristiche: 
- lo spazio può essere ridotto a $\Theta(k)$ dove k è l'insieme delle chiavi memorizzate
- **il tempo di esecuzione della ricerca sarà nel caso medio costante, ma nel caso peggio lineare**

invece di memorizzare un elemento con chiave k nella cella k, si usa una funzione $h$ e si memorizza l'elemento nella cella $h(k)$. $h$ si chiama funzione hash. 

$h: U \rightarrow \{ 0,1,...,m-1 \}$ dove la dimensione della tabella hash è generalmente più piccola di $|U|$.

### Collisioni

Le tabelle hash posso soffrire del fenomeno delle <mark>collisioni</mark>. Quando un elemento da inserire è mappato in una cella già occupata, si verifica una collisione, quindi occorre andare a trovare delle politiche per la gestione delle collisioni. 

Può succedere che ci siano collisioni quando il numero di chiavi in U risulta essere più grande di m. 

$$| U | > m$$ Accade sicuramente che ci siano delle collisioni se k (elementi effettivamente memorizzati) è maggiore di k.

$$|k| > m$$

### Liste di collisioni (concatenamento)

Si mettono tutti gli elementi associati alla stessa cella in una lista concatenata.
- La cella j contiene un puntatore alla testa della lista di tutti gli elementi memorizzati che sono mappati nella posizione j
- se non ci sono elementi la cella j contiene NIL

#### Operazioni con il concatenamento

Ipotesi:
- l'operazione della funzione hash ha tempo costante
- si suppone che l'elemento non sia presente nella lista


##### Inserimento

```python
def direct_address_insert(T,x):
	inserisce x in testa alla lista T[h(x.key)]
```


> Se necessario controllare se l'elemento è presente, occorre fare una ricerca ed eventualmente inserire l'elemento. La complessità dipende dalla funzione di ricerca.

Complessità: $\Theta(1)$

##### Cancellazione

```python
def direct_address_delete(T,x):
	cancella x dalla lista T[h(x.key)]
```

> Poiché si fornisce direttamente il puntatore all'elemento x da cancellare. non è necessaria alcuna ricerca.

In presenza di liste doppie il tempo di esecuzione nel caso peggiore è $\Theta(1)$. 
**Se le liste sono singolarmente concatenate la cancellazione costa quanto la ricerca**.

##### Ricerca

```python
def direct_address_search(T,k):
	cercare un elemento con chiave k sulla lista T[h(k)]
```

Il tempo di esecuzione nel caso peggiore risulta essere proporzionale alla lunghezza della lista nella cella di $h(k)$.

Complessità: $\Theta(n)$

###### Studio & Analisi

Voglio andare a valutare il tempo di esecuzione delle ricerca di un elemento con chiave k. 
Il caso peggiore si verifica quando tutte le chiavi sono inserite nella stessa cella -> unica lista di lunghezza n
Il caso medio **dipende dal modo in cui la funzione hash distribuisce mediamente le chiavi fra le n celle**. 
Il caso migliore si realizza quando la funzione hash soddisfi l'<mark>hashing uniforme semplice</mark>:
	qualsiasi elemento ha la stessa probabilità di essere mandato in una delle qualsiasi m celle, indipendentemente da dove sono mandate gli altri elementi $\forall i \in [0,...,m-1] \quad Q(i) = \cfrac{1}{m}$ dove $Q(i)$ e la probabilità che una chiave finisca nella cella $i$.
	
> **Fattore di carico**
> il fattore di carico di una tabella hash costituita da *m* celle e *n* chiavi è $\alpha = \cfrac{n}{m}$ 

Sotto l'ipotesi di hashing uniforme semplice, indichiamo con $nj$ la lunghezza della lista $T[j]$ 
Il valore medio di $nj$ è $\cfrac{ n_{0} + n_{1} + ... + n_{m-1}}{m}= \cfrac{n}{m} = \alpha$


> **Teorema**
> in una tabella hash in cui le collisioni sono risolte con il metodo di concatenamento una ricerca senza successo richiede tempo $\Theta(1+\alpha)$, nell'ipotesi che la funzione goda dell'hashing uniforme semplice

> **Teorema**
> in una tabella hash in cui le collisioni sono risolte con il metodo di concatenamento una ricerca con successo richiede tempo $\Theta(1 + \alpha)$.

Se $n = O(m)$ abbiamo che $\alpha = \frac{n}{m} = \frac{O(m)}{m} = O(1)$

**Se n cresce le prestazione possono degradare**.


2023-02-21

### Indirizzamento aperto

## Funzione hash
 