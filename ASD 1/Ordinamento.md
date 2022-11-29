
%%2022-11-29%%

# Insertion sort

k elemente già ordinati e voglio estendere al k+1-esimo elemnto 

```
InsertionSort(array A):
	for j=2 to A.length:
		key = A[j]
		i = j-1
		while i>0 && key < A[i]: \\ pseudo
			A[i+1] = A[i]
			i = i - 1
		A[i+1] = key
		