# Other Algs

Boyer–Moore majority vote algorithm:https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm
To find the majority (not mode, majority is consumes more than 50% of a group while mode is the highest frequency), don't need to keep track of a hashmap (size continuously growing) . But not guarantee to find the majority, need to verify at the second pass: /
counter example to only one pass can find majority:
1 0 1 0 1 0 5

will treat 5 as the majority while actually no majority elem inside. (need second pass count and compare with n / 2 (should be larger than this take floor))

Basic idea is if find other candidate vote, decrease the current candidate's votes since that means the advantages of it over other candidates. When that advanatages become zero, we can select the new candidate. But one problem is one pass might not select the real mode. We need second pass to verify.

## Find the next permutation lexigraphically

Thanks to a guy named Narayana Pandita (an indian guy from 14th century), we have: https://en.wikipedia.org/wiki/Permutation#Generation_in_lexicographic_order

1. find the largest k such that a[k]<a[k+1], if no such index, the permuatation is the last permutation(reverse the array)
2. find the largest l > k such that a[k]<a[l]
3. swap elem at l and k
4. reverse array from k+1 to end

03/11/2024 4:12am read an article from geeksforgeeks and developed an explanation for that alg so I can now grasp it instead of "purely" memorized it.

Here is the great explanation: https://www.geeksforgeeks.org/next-permutation/

From obervation we can find we must exchange some element in the array. And all permutation has an non-dec suffix from right to left. If is non-dec, we won't exchange any elements in it, since it only makes num smaller, so pivot is the first element that is left to non-dec seq from right and then we would exchange on this pivot with some number in the non-dec seq to find the next larger permutation for the following reasons(or proof):

1. Cannot change in non-dec seq since it makes num smaller.
2. If change outside of non-dec seq, then it need at least one digit more significant than the pivot which is obviously if make larger would be larger than exchange one digit in non-dec seq with pivot.

so we exchange a num in non-dec seq and the num on pivot then which num in non-dec seq we choose to make the the num larger but among all these choices it's the smallest one. So we need to find a larger than pivot digit(to exchange and make the num larger), the best one would be count from the left start of the right-start non-dec seq the digit that is the last one that is larger than pivot digit since it satisfies the least larger.

After the exchange, it's still not done. Since it's non-dec, if we reverse the after-change non-dec seq (now still non-dec since we find the least larger and exchange later one would <=), it will be the smallest num that is larger than original num.

Corner case: 321 last permutation we cannot find the pivot, so just skip other steps and reverse the non-dec suffix it become 123.
