
Restituire il cognome di uno studente e del suo tutor. Se lo studente non ha un tutor, restituisce 'Non ha tutor'

```SQL
/* restituisce il primo studente */
SELECT s.Cognome COALESCE(t.Cognome, 'Non ha tutor')
FROM Studenti s LEFT JOIN Studenti t ON s.Tutor = t.Matricola
```

Restituire il cognome degli studenti che non sono tutor

```SQL
/*snt = studente non tutor*/
SELECT s.Cognome
FROM Studenti snt LEFT JOIN Studenti s ON snt.Matricola = s.Tutor
WHERE s.Tutor IS NULL
			s.Matricola IS NULL
``` 


Studenti con il nome che inizia per 'A' e termina per 'a' oppure 'i'

```SQL
/*snt = studente non tutor*/
SELECT *
FROM Studenti 
WHERE Nome LIKE 'A%a' or Nome LIKE 'A%i'
``` 

Stessa query con le Regrex

```SQL
/*snt = studente non tutor*/
SELECT *
FROM Studenti 
WHERE REGEXP_LIKE (Nome, '^A.*(a|i)$’)
``` 



## Sottoselect

Se il risultato di una sottoselect è:
- NULL -> UNKNOWN
- vuoto -> UNKNOWN
- più valori -> ERRORE

Studenti che vivono nella stessa provincia dello studente con matricola 71346,  
escluso lo studente stesso
```SQL
SELECT
FROM Studenti s
WHERE s.Matricola <> '71346' AND 
			s.Provincia = ( SELECT Provincia
											FROM Studenti
											WHERE Matricola = '71346' )
```

stessa query ma senza sottoselect 

```SQL
SELECT altri.*
FROM Studenti s JOIN Studenti altri USING(Provincia)
/* USING() prende il valore della provincia solo sui valori presi dalla join */ 
WHERE s.Matricola = '71346' AND altri.Matricola <> '71346'
```
	

## Quantificazione Esistenziale

Gli studenti con almeno un voto > 27
```SQL
SELECT *
FROM Studenti s
WHERE EXISTS (SELECT *
							FROM Esami e 
							WHERE s.Matricola = e.candidato AND e.Voto > 27)
```


```SQL
SELECT *
FROM Studenti s
WHERE EXISTS e IN Esami WHERE e.Candidato = s.Matricola:
												e.Voto > 27
```


## ANY

Per ogni tupla (o combinazione di tuple) t della select esterna  
- calcola la sottoselect
- verifica se Expr è in relazione Comp con almeno uno degli elementi ritornati  
dalla select

Exp Comp ANY(Sottoselect)
- true se esiste un valore c restituito dalla sottoselect che è in relazione Comp con Exp cioè Exp Comp  v è vera
- false se nella sottoselect se tutti i valori restituiti sono diversi da NULL e non esiste un valore v tale che Exp Com v sia vera
- UNKNOWN se nella sottoselect ci sono valori NULL e per tutti i valori v diversi da NULL restituiti dalla sottoselect abbiamo che Exp Comp è false

```SQL

SELECT *  
FROM Studenti s  
WHERE s.Matricola=ANY (SELECT e.Candidato  
											FROM Esami e  
											WHERE e.Voto >27)
```

## FORALL 

Non esiste l'operatore FORALL ma ci si può arrivare usando le leggi di De Morgan

```SQL
SELECT * 
FROM Studenti s  
WHERE NOT EXISTS (SELECT *  
									FROM Esami e  
									WHERE e.Candidato = s.Matricola AND e.Voto <> 30)
```

%%2022-12-07%%

Cani(Cod, Nome, Razza*, Madre*, Padre*, AnnoNasc, AnnoMorte, Istruttore*)  
Madre FK(Cani), Padre FK(Cani), Razza FK(Razze), Istruttore FK(Istruttori)  
Dare il nome di ogni cane che ha entrambi i genitori e i loro genitori della sua  
stessa razza

```SQL
CREATE VIEW StessaRazza(Cane, Padre, Madre, Razza)
AS SELECT c.Id p.Id m.Id c.Razza
	FROM Cani c JOIN Cani p ON c.Padre = p.Id
		JOIN Cani m ON c.Madre = m.Id 
	WHERE c.Razza = p.Razza AND c.Razza = m.Razza

SELECT c.Nome
# il cane che sto considerando
FROM Cani c JOIN StessaRazza sameRace ON c.Id = sameRace.Cane
	JOIN StessaRazza p ON c.Padre = p.Cane
	JOIN StessaRazza m ON c.Madre = m.Cane
```

## Vincoli di integrità 

vincoli intrareferenziali: vincoli che valgono sulla tabella stessa.
```SQL


VincoloTabella := UNIQUE (Attributo {, Attributo})  
	| CHECK (Condizione) |  
	| PRIMARY KEY (Attributo {, Attributo})  
	| FOREIGN KEY (Attributo {, Attributo})  
	REFERENCES Tabella [(Attributo {, Attributo})]  
	[ON DELETE CASCADE | NO ACTION | SET DEFAULT | SET NULL ]  
	[ON UPDATE CASCADE | NO ACTION | SET DEFAULT | SET NULL ]
```


# chiedi alla prof Differenza tra WITH e VIEW e la loro "durata"

per ogni nazione restituire il numero di medaglie d'oro da le donne e da gli uomini nella disciplina sci. Se una nazione non ha vinto medaglie di un certo tipo, restituire 0. 


```SQL
SELECT a.Nazione, SUM(CASE WHEN a.Sesso = 'm' AND m.Codice IS NOT NULL THEN 1 ELSE 0) AS NumMaschi, SUM(CASE WHEN a.Sesso = 'f' AND m.Codice IS NOT NULL THEN 1 ELSE 0) AS NumMaschi
FROM Atleti a JOIN Medaglie m ON a.IdAtleta = m.IdAtleta AND m.Sport = 'Sci' AND m.Tipo = 'oro'\\
GROUP BY a.Nazione 
