2022-10-05

# Complessità 

## Sequenza 
```
	Block(1)  <-- O(f(n))
	Block(2)  <-- O(g(n))
```
Complessità = $O(f(n) + g(n) ) = O(f(n) + g(n))$

## If-then-else

```
if <cond> then <-- O(f(n))
	ramo-then  <-- O(g(n))
else
	ramo-else  <-- O(h(n))
```
Complessità: $O(f(n) + \text{max}\{g(n), h(n)\})$


## Cicli
```
for i to k
	block  <-- O(f(n))
```
Complessità: $O(k * f(n))$

## While
```
while <cond> do  <-- O(f(n))
	block        <-- O(g(n))
```
N(m) = max numero di iterazioni
Complessità: $O(N(n) (f(n) + g(n)))$

## Esempio

```
MyAlgorithm (int n) -> int
	if n>1 then
		a = 0
		for i=1 to n                   <-- n * n
			for j=1 to n
				a = (a+1)*j + a/2
		for i=1 to 16
			a = a + MyAlgorithm(n/4)   <-- 16T(n/4)
		return a
	else
		return n
```
Complessità: $T(n) = O(n^2 + 16T(\cfrac{n}{4}))$

