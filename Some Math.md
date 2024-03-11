# Some Math

## XOR

^: 

a ^ b = c

| a    | b    | c    |
| ---- | ---- | ---- |
| 0    | 0    | 0    |
| 1    | 0    | 1    |
| 0    | 1    | 1    |
| 0    | 0    | 0    |

1. Commutative: a^b = b^a
2. Not associative: (a^b)^c might != a^(b^c)
3. Cancellation property: a^b^b = a (Useful)



## >> and <<

a >> 1 the original value of a is not changed. So we need to do a = a >> 1.

## Quick Select Algorithm

For example fine the kth largest element in an unsorted array. We used partition to eliminate a part of the array and do partition recursively on the to be probed other half until we find the pivot is just at the idx we want.

Average O(n): each partition always select randomly and on near median (normal distribution), so each partition narrow the search range by half, so $$\frac{n}{2} + \frac{n}{4} + \frac{n}{8} + ... = n$$ -> O(n)

Worst O(n): we choose every element to be the pivot but until the last we find that's locate on the kth largest, so O(n ^ 2)

Best O(1): on first pivot we are lucky and found it.

partition function maintains a left and right for range and a pivot for pivot value, return the pivot right idx. we use a fill ptr and a iterate ptr, if encounter elem (at i) smaller than pivot value, we swap i with fill and increment fill, in the end (i reaches end) fill left is all elem that are smaller than pivot value, so we swap pivot and fill to put pivot value at the right spot and we are done.



