2023-03-08

I vincoli possono essere specificati in fase di creazione di una tabella:  

```sql
CREATE TABLE Nome  
	"(" Attributo Tipo [ Vincolo {, Vincolo}]  
	{, Attributo Tipo [Vincolo {, Vincolo}]}  
	[, VincoloTabella {, VincoloTabella}] ")"  
```

I vincoli vengono poi controllati dal sistema quando si effettuano certe  
operazioni che possono violarli. Vedremo che questo è un punto delicato!  
La sintassi evidenzia due tipi di vincoli: su attributi e su tuple.

## Unique

Data una tabella R(T ) ed un insieme di attributi X ⊆ T , possiamo  
specificare che nessuna coppia di tuple in R(T ) coincida su tutti gli  
attributi in X , a meno che uno di essi non sia NULL.  
Example  
```Sql 
CREATE TABLE Movies (  
	title CHAR(100) NOT NULL,  
	year INT,  
	length INT,  
	genre CHAR(10),  
	UNIQUE (title, year)  
)
```

