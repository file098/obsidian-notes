2022-10-03

# Progettazione e Modellazione


La progettazione di una base di dati consiste in due basi:
1) analisi dei requisiti 
2) progettazione dei requisiti
	- trasposizione in uno *schema concettuale*
3) progettazione logica
	- creazione di uno *schema logico*, quindi un modella realmente utilizzabile nel DB (modello relazionale)
4) progettazione fisica
	- creazione di un modello che va ad archiviare il modello con informazioni sulla memorizzazione dei dati

## Cosa si modella?


Progettare una base di dati significa progettare la:
- struttura dei dati
- applicazioni

La progettazione della struttura die dati è l'attività fondamentale

Richiede di specificare un modella della realtà d'interesse (**universo del discorso**) quanto più fedele, per questo ci concentreremo sulla modellazione.

Un **modello astratto** è la rappresentazione formale di idee e conoscenze relative a un fenomeno.
Aspetti di un modello:
- il modello è la rappresentazione di certi fatti
- la rappresentazione è data con un linguaggio formale
- il modello è il risultato di un processo di interpretazione, guidato dalle idee e conoscenze possedute dal soggetto che interpreta
![[Pasted image 20221006133319.png]]
Ciascuna di queste fasi è concentrata sulla modellazione. 

## Modellazione concettuale

### Aspetti del problema
Quale conoscenza del dominio del discorso si rappresenta?  (aspetto ontologico)  
Con quali meccanismi di astrazione si modella?  (aspetto logico)  
Con quale linguaggio formale si definisce il modello?  (aspetto linguistico)  
Come si procede per costruire un modello?  (aspetto pragmatico)

La modellazione è strutturata in quattro tipi di idee:
- conoscenza concreta
	- i fatti
- conoscenza astratta
	- struttura e vincoli sulla conoscenza concreta
- conoscenza procedurale
	- le operazioni di base
	- le operazioni degli utenti
- comunicazioni
	- come si comunicherà con il sistema informatico

### Conoscenza concreta

Sono fatti specifici che si vogliono rappresentare come le entità con le loro proprietà, le collezioni di entità omogenee e le associazioni fra entità. Le **entità** sono ciò di cui interessa rappresentare alcuni fatti (o **proprietà**) come oggetti concreti, oggetti astratti o eventi. 
- Es: un libro, una descrizione bibliografica, un prestito

Le **proprietà** si distinguono dalle entità poiché sono fatti che interessano solo  
in quanto descrivono caratteristiche di determinate entità  
- Es: indirizzo che interessa solo in quanto indirizzo di un utente

Una proprietà è una coppia <Attributo, valore di un certo tipo>. 

Classificazione di una proprietà:
- atomica o strutturata
- univoca/multi valore
- totale/parziale

Esempi:
- nome (atomica, univoca, totale)
- residenza = [indirizzo, cap, città] (strutturata)
- recapiti telefonico = (multi valore, parziale)

**Tipi di entità**:  ogni entità ha un tipo che ne specifica la natura (identifica caratteristiche: proprietà e dominio relativo). Ad esempio **Antonio** ha tipo persona con proprietà: 
- Nome: `string`
- Indirizzo: `string`

**Collezione** (classe): un insieme variabile nel tempo di entità omogenee, ad esempio: *Studenti*: insieme di tutti gli studenti nel dominio del discorso.

Spesso le collezioni di entità sono organizzate in una gerarchia di **specializzazione/generalizzazione** (si parla anche di sottoclassi e superclassi). Per esempio nella DB della biblioteca la collezione degli `Utenti` può essere considerata una generalizzazione di `Studenti` e `Docenti`. 
Due importanti caratteristiche delle gerarchie:
- **ereditarietà** delle proprietà
- **inclusione**: se la collezione C1 specializza C2 gli elementi di C1 sono un sottoinsieme degli elementi di C2
La classe degli *studenti* universitari è una generalizzazione delle classi:
	-  matricole e laureandi
	- studenti in corso e studenti fuori corso
	- studenti veneziani e studenti fuori sede

Un'**istanza di associazione** è un fatto che correla due o più entità, stabilendo un legame logico tra di loro.
- la descrizione bibliografica con titolo "Basi di dati" *riguarda* il documento con collocazione "D3-55-2"
- l'utente "Tizio" ha *in prestito* una copia della "Divina Commedia"

Un **associazione** R(X,Y) fra due collezioni di entità X ed Y è un insieme di istanze di associazione tra elementi di X e Y, che varia in generale nel tempo. Il prodotto cartesiano (X x Y) è detto **dominio** dell'associazione. 
Un associazione è caratterizzata dalle seguenti proprietà strutturali:
- molteplicità (o cardinalità)
- totalità
