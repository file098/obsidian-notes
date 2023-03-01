2023-03-01

# Forma normale di Boyce-Codd (BCNF)

> **Definizione**
>Uno schema di dipendenze funzionali è in BCNF $\iff$ per ogni dipende funzionale $X \rightarrow Y \in F^{+}$ tale che $Y \nsubseteq X$ si ha che $X$ è superchiave.

Si può dimostrare che è possibile sostituire $F^{+}$ con $F$ nella definizione"verificare se uno schema è in BCNF ha perciò costo **polinomiale**. 

Si consideri $Prodotti(\{Articolo, Magazzino, Quantità, Indirizzo\}, F)$ con $F = \{Articolo, Magazzino \rightarrow Quantità, Magazzino \rightarrow indirizzo \}$. Dato che $\{ Magazzino \}^{+}_{F} = \{Magazzino, Indirizzo\}$, lo schema non è in BCNF.

![[Pasted image 20230301123712.png]]

Una dipendenza che viola BCNF è detta **anomalia**. Nel nostro esempio abbiamo una dipendenza anomala Magazzino -> Indirizzo. 

L’eliminazione di anomalie è tipicamente basata sulla decomposizione di  
schemi mal definiti in schemi più piccoli, equivalenti ma più disciplinati.

## Conversione in BCNF

L'algoritmo di conversione in BCNF è anche detto algoritmo di **analisi**, perché decompone lo schema originale fino a normalizzazione.

1. Se $R(T,F)$ è già in BCNF, ritorno $\set{R(T,F)}$
2. altrimenti seleziona $X \rightarrow Y \in F$ che viola BCNF. Calcola gli insiemi di attributi $T_{1} = X_{F}^{+}$ e $T_{2} = X \cup (\frac{T}{T_{1}})$
3. calcola le proiezioni $F_{1} = \pi_{T_{1}}(F)$ e $F_{2} = \pi_{T_{2}}(F)$
4. decompone ricorsivamente $R_{1}(T_{1},F_{1})$ e $R_{2}(T_{2},F_{2})$ in $p_1$ e $p_{2}$
5. Ritorna la loro unione $p_{1} \cup p_{2}$


### Correttezza della conversione

10/23  
Correttezza della Conversione in BCNF  
L’algoritmo di conversione in BCNF termina quando non ci sono più dipendenze anomale. Per garantire che ciò avverrà, dimostriamo che tutti gli schemi con solo due attributi sono in BCNF. Consideriamo R(AB, F ) e sia X → Y ∈ F . Dimostriamo che in nessun caso viene violata BCNF:  
1. Se $X = \{A\}$, ho due casi. Se $B \notin Y$ , allora $Y \subseteq X$ e la dipendenza è banale. Se invece $B \in Y$ , allora X è una superchiave.  
2. Se $X = \{B\}$, il caso è simmetrico al precedente.  
3. Se $X = \{A, B\}$, allora $Y \subseteq X$ e la dipendenza è banale.

### Proprietà 

Vantaggi:

- BCNF garantisce l’assenza di anomalie  
+ L’algoritmo di conversione in BCNF preserva i dati  
+ Verificare se uno schema è in BCNF ha costo polinomiale  

Difetti:

- L’algoritmo di conversione in BCNF ha costo esponenziale, perché richiede di calcolare le proiezioni delle dipendenze
- L’algoritmo di conversione in BCNF non preserva le dipendenze

# 3NF 

> **Definizione**
>Uno schema relazionale R(T,F) è in **3NF** $\iff$ per ogni dipendenza $X \rightarrow Y \in F^{+}$ tale che $Y \nsubseteq X$ si ha che $X$ si ha che $X$ è una superchiave oppure tutti gli attributi di $Y/X$ sono primi

Per ogni definizione ogni schema in BCNF è anche in 3NF, ma non viceversa

## Conversione in 3NF

L’algoritmo di conversione in 3NF è anche detto algoritmo di sintesi,  
perch ́e basato sulla generazione di nuovi schemi più piccoli.  
Sia $R(T , F )$ lo schema di partenza:  
1. Costruisci $G$ , una copertura canonica di $F$  
2. Sostituisci in $G$ ciascun insieme di dipendenze $X → A_{1}, . . . , X → A_{n}$ con una singola dipendenza $X \rightarrow A_{1} ... A_{n}$  
3. Per ogni $X \rightarrow Y \in G$ , crea un nuovo schema $S_{i}(XY)$  
4. Elimina ogni schema contenuto in un altro schema  
5. Se la decomposizione non contiene alcuno schema i cui attributi costituiscano una superchiave per $R$, aggiungi un nuovo schema $S(W)$ dove $W$ è una chiave di $R$.

### Esempio 

Sia $R(\{A, B, C , D\}, \{AB \rightarrow C , C \rightarrow D, D \rightarrow B\})$, osserviamo che  
l’insieme delle dipendenze è già in forma canonica. 
Otteniamo quindi:  

- $R1(\{A, B, C \})$ tramite $AB \rightarrow C$  
- $R2(\{C , D\})$ tramite $C \rightarrow D$  
- $R3(\{B, D\})$ tramite $D \rightarrow B$  

Nessuno schema è contenuto in un altro, quindi nessuno di essi viene  
eliminato. Poiché $\{A, B, C\}$ è una superchiave di $R$, non è necessario  
aggiungere altri schemi. 

