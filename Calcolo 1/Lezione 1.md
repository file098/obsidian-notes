<date>19/9/2022</date>


# Insiemistica 

## Operazioni tra insiemi

- Unione: $A \cup B = \{ x \in X | (x \in A ) \lor (x \in B)\}$
	- prende tutti gli elementi dei due insiemi

- Intersezione: $A \cap B = \{ x \in X | (x \in A) \land (x \in B)\}$
	- prende gli elementi condivisi

- Complementare: $A^c = \{x \in X | x \notin A\}$

- Differenza: $A / B = \{ x \in X | x \in A \land x \notin B\}$

- Prodotto cartesiano: $A\times B = \{(x,y) | x \in A \land y \in B\}$
	- $A = \{a1, a2, a3\} \quad B = \{10, 20\}$
	- $A \times B = \{(a1,10), (a1,20), (a2,10), (a2,20), (a3,10), (a3,20)\}$

![[Pasted image 20220919093733.png]]

Dimostriamo che $A \cup B = A \iff B \subseteq A$

Andiamo a vedere $A \cup B = A \Leftarrow B \subseteq A$

Sappiamo che $A \cup B = A$ è verificata.
Prendiamo $b \in B$ e supponiamo per assurdo che $b \notin A$. Questo è assurdo perché $b \in A \cup B = A$. Quindi deve essere $\forall b \in B \Rightarrow b \in A$, cioè $B \subseteq A$

Sappiamo che $B \subseteq A$ è verificata.
Mostriamo che $A \cup B = A$ cioè $A \cup B \subseteq A$ e $A \subseteq A \cup B$. 
Sia $x \in A \cup B$ quindi per definizione $x \in A \lor x \in B$. Ma $B \subseteq A$ e si ha allora $x\in A$ e $A \cup B \subset A$. Inoltre si ha sempre che $A \subseteq A \cup B$, quindi $A \cup B = A$.

#### Esercizi 
Dimostrare le seguenti proprietà:
- $A \cap ( B \cup C)  = (A \cup B) \cap (A \cup C)$
- $A \cup ( B \cap C)  = (A \cap B) \cup (A \cap C)$



## Assiomi dei numeri reali

L'insieme dei numeri reali $\mathbb{R}$ può essere definito come l'insieme che soddisfa i seguenti quattro assiomi:
1. **Somma**
	- L'addizione (+) in $\mathbb{R}$ gode delle seguenti proprietà
		- commutativa
		- associativa
		- esistenza dell'elemento neutro
		- esistenza dell'opposto
	- Si dice che $(\mathbb{R} ,+)$ è un *gruppo commutativo*. Si può dimostrare che l'elemento neutro è unico. Si può dimostrare che l'opposto di un numero è unico. 
1. **Prodotto**
	 - Il prodotto $(*)$ in $\mathbb{R}$ gode delle seguenti proprietà
		- commutativa
		- associativa
		- esistenza dell'elemento neutro
		- esistenza dell'reciproco
	- Si dice che $(\mathbb{R} ,+, *)$ è un *corpo commutativo o campo*. Si può dimostrare che l'elemento neutro è unico. Si può dimostrare che il reciproco di un numero è unico. 
3. **Ordinamento**
4. **Completezza**