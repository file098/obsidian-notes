
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

