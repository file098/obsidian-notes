2023-02-15

%%libro consigliato: Fondamenti di basi di dati albano ghelli orsini%%

# Dipendenza funzionale 

Sia $R(T)$ uno schema di relazione e siano X , Y due insiemi di attributi  
non vuoti tali che $X \cup Y \subseteq T$ , una **dipendenza funzionale** è un qualsiasi  
vincolo della forma X → Y .

Un’istanza r di R(T ) **soddisfa** la dipendenza funzionale X → Y se e solo  
se ogni coppia di ennuple in r che coincide su X coincide anche su Y .  
Formalmente chiediamo $$\forall t1, t2 \in r : t1[X ] = t2[X ] \rightarrow t1[Y ] = t2[Y ]$$
Scriveremo $R(T,F)$ per indicare uno schema di relazione $R(T)$ con le dipendenze funzionali F che tutte le sue istanze valide devono soddisfare. 

![[Pasted image 20230215130119.png]]

> La terza condizione non soddisfa la dipendenza perché posso avere persone diverse con lo stesso numero di telefono. 


Sia R(T , F ) uno schema di relazione. Diciamo che F **implica logicamente** 
la dipendenza funzionale X → Y , indicato con F |= X → Y , se e solo se  
ogni istanza valida di R(T , F ) soddisfa anche X → Y .

Sia $F = \{  CodiceLibro -> Titolo, CodiceLibro -> NomeUtente \}$ allora: 
$$F \models CodiceLibro \rightarrow Titolo,NomeUtente$$
$$F \models CodiceLibro \rightarrow CodiceLibro$$

## Assiomi di Armstrong 

Teorema:
$$F \vdash X \rightarrow Y \iff F \models X \rightarrow Y$$



2023-02-17

## Chiavi & Copertura canonica


### Chiavi ed Attributi Primi  
  
> Dato una schema di relazione $R(T , F )$, un insieme di attributi $X \subseteq T$ è una superchiave di R se e solo se $X \rightarrow T \in F^{+}$

> Una chiave è una superchiave minimale, cioè una superchiave tale che nessuno dei suoi sottoinsiemi propri sia a sua volta una superchiave.  
  
> Un attributo è primo se e solo se appartiene ad almeno una chiave.


### Verifica superchiave

![[Pasted image 20230217143058.png]]

Trovare una chiave
Dato R(T,F) è possibile trovare una chiave in tempo polinomiale. 
```python
def FindKey(R(T,F)):
	k <- T
	for all A in T do
		if (k/{A})+ = T then
			k <- k / {A}
		return k
```

Sia $G = {AB → C , E → A, A → E , B → F }$. Costruiamo una chiave  
come segue:  
1. $K_0 = BD$, perché né B né D sono derivabili da altri attributi  
2. abbiamo $A \notin BD_{+}^{G} = BDF$ , quindi $K_1 = ABD$  
3. abbiamo $C \notin ABD_{+}^{G} = ABCDEF$ , quindi la chiave non cambia  
4. abbiamo $E \notin ABD_{+}^{G} = ABCDEF$ , quindi la chiave non cambia  
5. abbiamo $F \notin ABD_{+}^{G} = ABCDEF$ , quindi la chiave non cambia  
Si noti che l’algoritmo potrebbe ritornare $K_1$ già al passo 3.

### Trovare l'insieme della chiavi

Dato $R(T , F )$, trovare tutte le chiavi ha costo esponenziale, perché ogni  
sottoinsieme di T è potenzialmente una chiave. Esiste però un algoritmo  
piuttosto ottimizzato per la ricerca di tutte le chiavi.

> $X :: (Y)$
> Rappresentiamo i candidati da testare nella forma $X :: (Y )$, una forma compatta per descrivere tutti gli insiemi $X \cup Z$ con $Z \subseteq Y$


### Verifica di primalità 

Dato $R(T , F )$, il problema di verificare se un attributo $A \in T$ è primo ha  
complessità esponenziale:  
- più precisamente, si può dimostrare che è un problema NP-completo  
- ciò implica che non esistono soluzioni significativamente più efficienti di generare tutte le possibili chiavi!  
- questo è l’approccio che useremo per trovare l’insieme degli attributi primi quando sarà necessario

#### Forma canonica

Sia $X \rightarrow Y \in F$ . L’attributo A ∈ X è **estraneo**  $\iff X / \{A\} \rightarrow Y \in F^{+}$.  
  
> La dipendenza X → Y ∈ F è ridondante $\iff X → Y \in (F / \{X → Y \})^{+}$.  
  
F è in forma canonica se e solo se per ogni $X \rightarrow Y \in F$ :  
1. $|Y | = 1$;  
2. X non contiene attributi estranei;  
3. $X → Y$ non è ridondante

G è una copertura canonica di F se e solo se $F \equiv G$ e G è in forma canonica.  

> **Teorema**  
> Per ogni insieme di dipendenze F esiste una copertura canonica.  

La dimostrazione è costruttiva: definiamo un algoritmo per produrre una  
copertura canonica. Si osservi che uno stesso insieme di dipendenze può  
avere più coperture canoniche.

2023-02-23

sick day 

2023-02-24

# Decomposizione di schemi

Dato uno schema R(T,F) una sua **decomposizione** è un insieme di schemi $p = \{ R_{1} (T_{1}, F_{1}), ... , R_{n}(T_{n}, F_{n}) \}$ tale che $U_{i} T_{i} = T, \forall i: T_{i} \neq \emptyset$ e $\forall i:F_{i} = \pi_{T_{i}} (F)$.
Visto che gli $F_{i}$ sono determinati da $F$ e dai $T_{i}$, per la leggibilità scriveremo una decomposizione di R(T,F) solo come $p=\set{R_{1}(T_{1}),...,R_{n}(T_{n})}$. 

### Proprietà

Non tutte le decomposizioni sono desiderabili: 

1. perdita di informazione: la decomposizione va ad introdurre dei dati spuri, che possono inficiare la correttezza di alcune query
2. perdita di dipendenze: a decomposizione perde alcune dipendenze funzionali, andando ad alterare la semantica dei dati rappresentati

Proprietà desiderabili: una buona decomposizione dovrebbe eliminare le  
anomalie, ma preservare i dati e le dipendenze. 

![[Pasted image 20230224141654.png]]

Sia $p=\set{R_{1}(T_{1}),R_{2}(T_{2})}$ una decomposizione di $R(T,F)$ si ha che $p$ preserva i dati $\iff T_{1} \cup T_{2} \rightarrow T_{1} \in F^{+}$ oppure $T_{1} \cup T_{2} \rightarrow T_{2} \in F^{+}$.

Questo permette di ricondurre il problema di determinare se una certa decomposizione binaria preserva i dati al problema dell’implicazione, che ha costo **polinomiale**.

