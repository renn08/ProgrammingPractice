# Sliding window

Let's do the LC in a DFS way.

Today our focus is sliding window.

https://leetcode.com/tag/sliding-window/

1. Iterate through all the possiblities (usually end of the window as the iterator), and determine when to shrink left and when to update result.
2. 

- [x] 3
- [x] 30
- [x] <span style="color:red">76</span>: Read problem carefully and when to shrink on left is the most important thing.
- [x] 159
- [x] 187
- [x] 209
- [x] 219
- [x] 220: bucket category for fixed value Diff problem. (see bucket sort), check this bucket and adj buckets. Use whole division to calcalculate bucket.
- [x] 239
- [x] 340: can use int arr[256] to do a char count map, since 256 is the number of ascii char at most. (normal char 0-127, but have special chars from 128 - 255).
- [x] <span style="color:red">395</span>: if sliding window bound and size is not clear, we can see if that problem can be devide and conquer into window size of different value.
- [x] <span style="color:red">424</span>: a fake medium, should be hard. maintain window size as the max result we currently have so we don't need to consider every substring with different end start from length < max result we already had.
- [x] 438
- [x] <span style="color:red">480</span>: two number balanced heap (min and max) with lazy deletion (no explicit deletion, delete deleted node only they are at top)
- [ ] 487
- [ ] 567
- [ ] 632
- [ ] 643