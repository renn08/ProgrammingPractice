# DP

https://leetcode.com/explore/learn/card/dynamic-programming/

## When to use dp?

1. The problem can be broken down into "overlapping subproblems" - smaller versions of the original problem that are **re-used** multiple times. (overlapping here means re-used, re-used is where duplicated calculation operations are saved), for example in divide and conquer, sub-problem are not overlapping, instead independent, so divide and conquer are much more easier to be parallelized.
2. The problem has an "optimal substructure" - an optimal solution can be formed from optimal solutions to the overlapping subproblems of the original problem. (the formula for f(n) can be determined by some subproblem of f(n))

## Some characteristics of using dp

1. find the max or min of something
2. future decisions depends on the earlier decisions.

## Top down or bottom up?

1. Usually, a bottom-up algorithm will be faster than the equivalent top-down algorithm as there is some overhead with recursive function calls. However, sometimes, a top-down dynamic programming approach will be the better option, such as when only a fraction of the subproblems need to be solved.

## Conversion from top down to bottom up

1. When converting a top-down solution to a bottom-up solution, we can still use the same base case(s) and the same recurrence relation. However, bottom-up dynamic programming solutions iterate over all of the states (starting at the base case) such that all the results necessary to solve each subproblem for the current state have already been obtained before arriving at the current state. So, to convert a top-down solution into a bottom-up solution, we must first find a logical order in which to iterate over the states.

   ## On state variables

   - An index along some input. This is usually used if an input is given as an array or string. This has been the sole state variable for all the problems that we've looked at so far, and it has represented the answer to the problem if the input was considered only up to that index - for example, if the input is nums = [0, 1, 2, 3, 4, 5, 6]nums = [0, 1, 2, 3, 4, 5, 6], then dp(4)dp(4) would represent the answer to the problem for the input nums = [0, 1, 2, 3, 4]nums = [0, 1, 2, 3, 4].
   - A second index along some input. Sometimes, you need two index state variables, say ii and jj. In some questions, these variables represent the answer to the original problem if you considered the input starting at index ii and ending at index jj. Using the same example above, dp(1, 3)dp(1, 3) would solve the problem for the input nums = [1, 2, 3]nums = [1, 2, 3], if the original input was [0, 1, 2, 3, 4, 5, 6][0, 1, 2, 3, 4, 5, 6].
   - Explicit numerical constraints given in the problem. For example, "you are only allowed to complete kk transactions", or "you are allowed to break up to kk obstacles", etc.
   - Variables that describe statuses in a given state. For example "true if currently holding a key, false if not", "currently holding kk packages" etc.
   - Some sort of data like a tuple or bitmask used to indicate things being "visited" or "used". For example, "bitmaskbitmask is a mask where the ��ℎ*i**t**h* bit indicates if the ��ℎ*i**t**h* city has been visited". Note that mutable data structures like arrays cannot be used - typically, only immutable data structures like numbers and strings can be hashed, and therefore memoized.

   mutable data structure like array cannot be hashed. immutable data structure like number or strings can be hashed.

## Procedures

1. identify if it is indeed a problem that can be solved by dp? (Max of min of something or word break is that possible, or the counting dp that ask for how many distinct ways are there etc.) Mostly try to think if it can be solved by greedy algorithm, (try to think a counterexample and prove we cannot use greedy.)
2. Think of how many state vars we need to represent the state what what that state's value represent?

## Counting DP

counting dp that ask for how many distinct ways are there. Instead of using max or min in the recurrance relationship, counting dp do operations between prev states for example sum the prev states' value to get the current state value.

1. base case might be a bit tricky need to analyze. Usually not 0 (unlike other types of questions).

## Optimizations on DP

1. Use bottom up usually better than top down but not always.
2. Use the least possible dims to represent states (one side of state reduction, another side is to reduce necessary cached states while dim of state var are the same, see 5.).
3. Use some pre-calculated memo to avoid iterations to find the suboptimal.
4. Iterations to optimize when calculating a moving min and the min of previous calculated range is done except for the current value, so we can maintain a previous min and compare with the current one to gain current real min. (example [188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/) optimiation on the most inside loop)
5. Optimize the space complexity by using less size of memo (avoid storing elements that we do not need anymore.) For example, fibonacci, f(n) = f(n - 1) + f(n - 2), when using bottom up, we only need to remember two previous number. So we can actaully improve memo to be only remember prev two number, so now space complexity is O(1).

## Kadane's Algorithm

To find the maximum sum subarray. State is the max sum subarray end at the current index.  Update best along the iteration. And iterate all number as the end once and we consider all the possibility and find the final result. Review LC918.

## Pathing Problem

Typically we can use dp when moving is constrained in a way that prevents moving "backward", here "backward" does not means real backward to the visited position but also has the trend to move backward, for example, go right and go down and then again go up, then we  are possible to go back to the visited position by just another move. So the valid case are for example, we are only allowed to move right and move down.

DP solves path problem that do not "backward". If all four directional is allowed then that should be a problem to be solved by BFS or DFS or graph.



