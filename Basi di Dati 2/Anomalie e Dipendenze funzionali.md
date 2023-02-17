2023-02-15

%%libro consigliato: Fondamenti di basi di dati albano ghelli orsini%%

## Dipendenza funzionale 

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

### Assiomi di Armstrong 

Teorema:
$$F \vdash X \rightarrow Y \iff F \models X \rightarrow Y$$



2023-02-17

## Chiavi & Copertura canonica


### Chiavi ed Attributi Primi  
  
> Dato una schema di relazione $R(T , F )$, un insieme di attributi $X \subseteq T$ è  
una superchiave di R se e solo se $X \rightarrow T \in F^{+}$

> Una chiave è una superchiave minimale, cioè una superchiave tale che  
nessuno dei suoi sottoinsiemi propri sia a sua volta una superchiave.  
  
> Un attributo è primo se e solo se appartiene ad almeno una chiave.


### Verifica superchiave

![[Pasted image 20230217143058.png]]

Trovare una chiave
Dato R(T,F) è possibile trovare una chiave in tempo polinomiale. 
```
function FindKey(R(T,F))
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



