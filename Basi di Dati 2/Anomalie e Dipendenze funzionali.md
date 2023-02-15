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

