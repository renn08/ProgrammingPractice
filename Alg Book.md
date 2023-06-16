# Alg Book

Dijkstra's algorithm

1. Mark all nodes unvisited. Create a set of all the unvisited nodes called the *unvisited set*.
2. Assign to every node a *tentative distance* value: set it to zero for our initial node and to infinity for all other nodes. During the run of the algorithm, the tentative distance of a node *v* is the length of the shortest path discovered so far between the node *v* and the *starting* node. Since initially no path is known to any other vertex than the source itself (which is a path of length zero), all other tentative distances are initially set to infinity. Set the initial node as current.[[17\]](https://en.wikipedia.org/wiki/Dijkstra's_algorithm#cite_note-17)
3. For the current node, consider all of its unvisited neighbors and calculate their tentative distances through the current node. Compare the newly calculated tentative distance to the one currently assigned to the neighbor and assign it the smaller one. For example, if the current node *A* is marked with a distance of 6, and the edge connecting it with a neighbor *B* has length 2, then the distance to *B* through *A* will be 6 + 2 = 8. If B was previously marked with a distance greater than 8 then change it to 8. Otherwise, the current value will be kept.
4. When we are done considering all of the unvisited neighbors of the current node, mark the current node as visited and remove it from the unvisited set. A visited node will never be checked again (this is valid and optimal in connection with the behavior in step 6.: that the next nodes to visit will always be in the order of 'smallest distance from *initial node* first' so any visits after would have a greater distance).
5. If the destination node has been marked visited (when planning a route between two specific nodes) or if the smallest tentative distance among the nodes in the unvisited set is infinity (when planning a complete traversal; occurs when there is no connection between the initial node and remaining unvisited nodes), then stop. The algorithm has finished.
6. Otherwise, select the unvisited node that is marked with the smallest tentative distance, set it as the new *current node*, and go back to step 3.

Implementation:

```cpp

```



## BFS and DFS

2492

BFS is by nature a non-recursive algorithm, ususally implemented by a queue. DFS is a recursive algorithm, can be either implemented by recursion or by a stack (almost the same as the bfs except using a queue).

How to get max value of a data type

For double and float:

```cpp
double doubleMax = std::numeric_limits<double>::infinity();
```

For int:

```cpp
// std::numeric_limits<int>::infinity() returns 0 instead.
int maxValue = std::numeric_limits<double>::max();
// Or
// Do not use this when do online coding like leetcode, might compile error.
#include <bits/stdc++.h>
int maxValue = std::INT_MAX;
int minValue = std::INT_MIN;

cout << std::numeric_limits<double>::infinity() << endl;
cout << std::numeric_limits<double>::max() << endl;
cout << (std::numeric_limits<double>::infinity() > std::numeric_limits<double>::max()) << endl;
cout << std::numeric_limits<int>::infinity() << endl;
cout << std::numeric_limits<int>::max() << endl;
// Print result:
// inf
// 1.79769e+308
// 1
// 0
// 2147483647
```

## Union Find

2492

Essential elements:

Invariant: Each group should always have only one root.

1. A map to the root from x, typically can be represented by a vector. Need an initialization to map to itself first.
2. Find function, typically recursively find the root of x, for example, until the root of root of ... of x is itself.
3. Union function, make two x the same root, need a merge strategy, for example always take the smaller one as the root. Since union function only merge the root of two x, namely make one of the root as the root of the other, find function will do a job to make these root that are not the ultimate root the ultimate root, typically do this step in recursion, make find faster next time when going through that node.



const T equivalent to T const

union find worst time complexity is log(n), tree height can be derived from total num of node = 2^n, where one node means  it has a height of 0.



## Adjacency List

![](/Users/renn08/Desktop/Job_hunting/Alg Book/Screenshot 2023-03-23 at 2.49.29 PM.png)

recursion version dfs? 1319

adjacent matrix?
