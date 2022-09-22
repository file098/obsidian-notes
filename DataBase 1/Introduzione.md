2022-09-21

# Argomenti modulo 1

- Sistemi per db
- modello dei dati
- progettazione 
- modello razionale
- SQL per la def, manipolazione e consultazione di DB

# Sistema informativo e informatico

2022-09-22

# Basi di Dati

Una base di dati è una raccolta di dati permanenti, gestiti da un elaboratore elettronico, suddivisi in due categorie: 
- Metadati : definiscono lo schema del DB che descrive:
	-  struttura dei dati 
	- restrizioni sui valori ammissibili (**vincoli di integrità**)
	- utenti autorizzati
	-  <mark>definiti prima di creare i dati e indipendentemente dalle applicazioni</mark>
- Dati le rappresentazioni di certi fatti conformi alle definizioni dello schema, con le seguenti caratteristiche: 

## Dati 

### Caratteristiche dei dati 
- sono organizzati in **insiemi omogenei** fra i quali sono definite le **relazioni**, La struttura dei dati e le relazioni sono descritte nello schema usando i meccanismi di astrazioni del modello dei dati adottato.
- sono **molti**, in assoluto e rispetto ai metadati, e non possono essere gestiti in memoria temporanea.
- sono **permanenti**, continuano ad esistere finché non sono rimossi esplicitamente.
- sono **utilizzabili contemporaneamente** da utente diversi.
- sono **protetti** sia da accesso da parte di utenti non autorizzati, sia da corruzione dovuta a malfunzionamenti hardware e software
- sono accessibili mediante **transazioni**, unità di lavoro atomiche che non possono avere effetti parziali.

### DBMS

Definizione: una DBMS è un sistema centralizzato o distribuito che offre opportuni linguaggi/strumenti per: 
- definire lo schema della DB
	- definito usando il modello dei dati adottato dal DBMS 
	- interrogabile con le stesse modalità prevista per i dati
- scegliere le strutture dati per la memorizzazione dei dati
- memorizzare i dati rispettando i vincoli definiti nello schema 
- recuperare e modificare i dati interattivamente (linguaggio di interrogazione o query language) da programmi

### Architettura dei DBMS centralizzati 
Il meccanismo di astrazione fondamentale è la <mark>relazione (tabella)</mark> cioè un insieme di record con campi di tipo elementare.

| name    | matricola | citta   | anno di nascita |
| ------- | --------- | ------- | --------------- |
| verdi   | 882754    | padova  | 1987            |
| bianchi | 882742    | roma    | 1998            |
| zeeri   | 553311    | treviso | 1999            |

 
Lo schema specifica le tabelle: 
- nome 
- struttura degli elementi 

Nella tabella la **matricola** è la <mark>chiave primaria</mark> della tabella

### Funzionalità dei DBMS

Deve fornire: 
- linguaggio per la definizione della base di dati
- linguaggi per l'uso dei dati
- meccanismi per il controllo dei dati
- strumenti per il responsabile della base di dati 
- strumenti per lo sviluppo dell applicazioni

#### Linguaggio per la definizione di DB

La descrizione della DB è indipendente dalle applicazione che al usano
Tre diversi livelli di descrizione dei dati (schemi):
1. livello vista logica: fornisce all'utente la vista della base di dati, è possibile definire viste differenti
2. livello logico: descrizione della struttura e vincoli della base di dati
3. livello fisico: raccoglie le informazioni per la memorizzazione dei dati (più basso)


#### Livello fisico

Descrive lo schema fisico o interno

#### Livello logico

Descrive come deve apparire la struttura della base di dati ad una certa applicazione


**Indipendenza fisica**: i programmi applicativi non devono essere modificati in seguito a modifiche dell'organizzazione fisica dei dati, per esempio
- strutture dati ausiliarie
- modifica della distribuzione
Se si deve risalire spesso agli studenti che hanno sostenuto un particolare esame: 

```sql
CREATE INDEX IndiceIdeC ON Esami (IdeC);
```

**Indipendenza logica**: i programmi applicativi non devono essere modificati in seguito a modifiche dello schema logico
- difficile da ottenere
- richiederà la ridefinizione della schema esterno

Esempio: per suddividere la collezioni degli studenti part-time e full-time:

```sql
CREATE TABLE StudentiFull (...);
CREATE TABLE StudentiPart (...);

CREATE VIEW Studenti AS 
	SELECT * FROM StudentiFull
	UNION
	SELECT * FROM StudentiPart;

```

