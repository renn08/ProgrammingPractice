# Sliding window and subarrays

## Count subarrays with bounded criteria

See the Leetcode list here: https://leetcode.com/problemset/all/?listId=ph7cmn4h&page=1 (typical: [1248. Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/))

This kind of problem (similar: 2444): 

count subarray with number satisfied a bounded criteria, process each idx and update valid range (start - bounded start - bounded end - end) treate end idx as end of candidates subarrs each new end that has valid range (maintained start - end) we add bounded criteria first idx - start + 1 of new subarrs into result. (do this step at the end since we might update in the current round)

## Monotonic deque (queue or stack) to solve moving range max and min

typical question: [1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit](https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/)

Monotonic deque:   

Some important property: 

1. if in dq, the prev one is the first one on the left (reverse direction of adding elements) larger (for max dq) smaller (for min dq) than current. And if in dq, means process to current position, no value is larger than them on their right (or they will be poped).
2. num in dq follows the order of adding into dq., so it's like current max candidate follows the order of adding them. So if we want to find some element's first larger number of num appears first in left or right direction. The process of adding and removing in monotonic queue is to first eliminate these 凹element in decreasing monQ(max front) and 凸element in increasing monQ(min front), and these element prev in q is guaranteeded to be larger than them (to avoid complication, we added a inf at first so that in situation 1 2, 1 will find 2 and the number directly after that number, also the next to be added is larger than that, so we find the first appear larger left and right we just compare them. And After  This is what we can do:

monotonic deque to record range max and min: 

when changing range: 

1. move right ptr, add right range:

   pop end < newly added make a non-increasing mon q, max candidate

​     pop end > newly added make a non-decreasing mon q, min candidate

2. move left ptr, shrink left range:

​     check cur left value, if match, pop q front. Then move left ptr



Some great stack problem: 