%%2022-10-19%%

# Linguaggi Relazionali

Insieme di operatori su relazioni che danno come risultato relazioni e si definiscono come:
- operatori primitivi
- operatori derivati
- altri operatori
Non si usa direttamente come linguaggio di interrogazione dei DBMS ma come rappresentazione interna delle interrogazioni

Calcolo relazionale: linguaggio dichiarativo ti tipo logico del quale è stato derivato SQL

## Operatori Primitivi


### Proiezione

Proiezione ($\pi$) data R(x) con $(A_1, ... , A_n) \subseteq x$ 

$$\pi_{(A_1, ... , A_n)} (R)$$
Elimina gli attributi diversi da $A_m$:

$$\pi_{(A_1, ... , A_{n)} (R)}= \{t.A_{1}, ... ,t.A_{m} |  t \in \mathbb{R} \}$$

**Cioè elimino colonne della mia tabella e anche i duplicati**

Se $\pi_{(A_1, ... , A_n)} (R)$ è superchiave, la cardinalità della mia proiezione è uguale a $n$.

### Proprietà 

Se L1 e L2 sono due insiemi di attributi con $L1 \subseteq L2$:

$$\pi_{L1}(\pi_{L2}(R)) = \pi_{L1}(R)$$

Per esempio se avessimo una tabella con 

| nome | cognome | corso | matricola | provincia |
| ---- | ------- | ----- | --------- | --------- |
  
L'operatore $\pi_{Nome,Matricola,Provincia}(Studenti)$ va a prendere solo le colonne indicate quindi 

| nome | matricola | provincia |
| ---- | --------- | --------- |

  
### Restrizione

$$\sigma_{\phi}(R) = \{ t | t \in \mathbb{R} \land \phi(t) \}$$

**Va a fare un taglio orizzontale, inverso della proiezione.**

### Prodotto

$$R \times S$$

Siano R e S due relazioni con attributi distinti $A_{1}, ..., A_{n}$ e $B_{1}, ..., B_{m}$

$$R \times S = \{ t.A_{1}, ..., t.A_{n}, u.B_{1}, ..., u.B_{n}  | t \in \mathbb{R} \land u \in S \}$$
**Non ci possono essere dei duplicati.**


## Esercizio 

Trovare il nome degli studenti che hanno superato l'esame di BD con 30

$$\pi_{Nome}(\phi_{Materia='BD' \land Voto=30}( \phi_{Matricola=Candidato}(Studenti \times Esami)))$$

Che può essere scritto così:
$$\pi_{Nome}(\phi_{Materia='BD' \land Voto=30 \land Matricola=Candidato}(Studenti \times Esami)))$$

## Operatori derivati

### Giunzione o Join

$$R \bowtie S$$
Siano R e S due relazioni con attributi distinti $A_{1}, ..., A_{n}$ e $B_{1}, ..., B_{m}$

ovvero
$$R \bowtie S = \phi_{A_{i}=b_{j}}(R \times S)$$
$$R \times S = \{ t.A_{1}, ..., t.A_{n}, u.B_{1}, ..., u.B_{n}  | t \in \mathbb{R} \land u \in S \land t.A_{i} = u.B_{j} \}$$

Sia $R(YX)$ e $S(ZX)$ con $X$ attributi comuni, $R \bowtie S$ restituisce una relazione con attributi $Y \times X$ tale che 

$$t \in R \bowtie S \iff t[YX] \in R \quad e \quad t[ZX] \in S$$


%%2022-11-09%%

Voglio l'insime degli studenti con i loro esami, inclusi gli studenti che non hanno sostenuto esami.

$$Studenti \bowtie_{Matricola = Candidato}^{\leftarrow} Esami$$

### Divisione

Divisione: date le relazioni R(XY) e S(Y) si vuole produrre una relazione T(X) tale  
che una ennupla t è in T se e solo se per ogni s in S la ennupla <t, s> appare in R.

$$R \div S$$

Esempio: matricola degli studenti che hanno fatto tutti gli esami che ha fatto Anna  
Rossi (matr. 76366).

esami di Anna Rossi:

$$ES\_AR= \pi_{Materia}(\phi_{Candidato=76366}(Esami))$$
esami studenti con matricola
$$ES = \pi_{Candidato,Materia}(Esami)$$

Questa divisione è applicabile se $ES \div ES\_{AR} \quad ES_{AR}\neq \emptyset$

Quindi

$$R \div S = \{ t | t \in \Pi_{x} (R) \land \forall x \in S < t,s > \in R \}$$
sui numeri 

$$r \div s = max\{t | t*s \leq r \} \iff $$
Quindi possiamo dire che la divisione è equivalente a:
$$R \div S \equiv \Pi_{x}(R) - (\Pi_{x}(R)_{X}S- R)$$

#### Esercizio  
Query per  
- studenti che hanno fatto un sottoinsieme degli esami di Anna Rossi  
	- $AL\_PIU= \Pi_{Matricola}(Studenti) - p(\Pi_{Candidato}( ES - \Pi_{Candidati}(ES) \times ES\_AR)))$
