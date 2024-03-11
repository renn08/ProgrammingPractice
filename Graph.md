# Graph(CHECK TODOS)

## Basic Knowledges

**Negative Weight Cycle**: In a “weighted graph”, if the sum of the weights of all edges of a cycle is a negative value, it is a negative weight cycle. 

**Degree of a Vertex**: the term “degree” applies to unweighted graphs. The degree of a vertex is the number of edges connecting the vertex. 

**In-Degree**: “in-degree” is a concept in directed graphs. If the in-degree of a vertex is d, there are d directional edges incident to the vertex.

**Out-Degree**: “out-degree” is a concept in directed graphs. If the out-degree of a vertex is d, there are d edges incident from the vertex. 

## Disjoint Set

(Union find)

1. quick find: so root array actually store the real root(cannot root any more "root"). That makes find() to be O(1) but union to be O(n), since when joining node x and node y, for example we are making y's root node to be x's root node, so we need to find all node that has root to be y's root node change their root node to be x's root node. Also check connected is O(1) since it is just check if for x and y find(x) == or not find(y).

   ```pesudo
   union(x, y):
   	rootx = find(x)
   	rooty = find(y)
   	for all node i:
   		if find(i) == rooty:
   			root[i] = rootx
   ```

2. quick union: Instead union takes lesser time (worst case O(n)) and find takes O(n). So union just makes root[y] = root[x]. But when we do find, we need to find recursively until the root of x is x means x is the ultimate root node. That can at most take O(n) time. Check connected will also be O(n) since it is check if find(x) == find(y).

   ```pesudo
   find(x):
   	if (x == root[x])
   		return x
   	return find(root[x])
   	
   union(x,y):
   	rootx = find(x)
   	rooty = find(y)
   	if (rootx != rooty):
   		root[rootx] = rooty
   ```

   2. is usually faster than 1. quick union faster than quick find. For example combining N elements, faster find need exactly O(n^2) while faster union will need worst O(n^2) since sometimes union takes O(1), so faster union (updating real root node in recursive find) is usually better.

   ## Union by rank

   merge the shorter tree under the taller tree and assign the root node of the taller tree as the root node for both vertices to make recursively find to go through less level and saved time.

   Let rank denote the height of the root (max distance from root to leaf). 

```pesudo
init:
	rank all to 0
	root all to itself
	
find(x): // since it's a balanced tree right now, O(logn)
	if (x == root[x])
		return x
	return find(root[x])
	
union(x,y): // O(logn)
	rootx = find(x)
	rooty = find(y)
	if (rootx != rooty):
		if (rank[rootx] > rank[rooty]):
			root[rooty] = rootx // do not change height
		else if (rank[rootx] < rank[rooty]):
			root[rootx] = rooty
		else: // same height tree union would cause the root has height + 1
			root[rootx] = rooty
			rank[rooty]++
// connected check will also be O(logn)
```

## Path compression optimization

That is just the following in find():

```pesudo
find(x):
	if (x == root[x]):
		return x
	return root[x] = find(root[x]) // this is path compression, update the real "root" when we are trying to find it (all elem along the way has their real "root" updated, we adding shortcuts to the real "root"). Therefore we compress the path and find will be faster next time of calling it.
	
// another implementation:
find(x):
	if (x != root[x]):
		root[x] = find(root[x])
	return x
```

## Optimized union find using rank and path compression

```pesudo
init:
	rank all to 0
	root all to itself
	
find(x): // since it's a balanced tree right now, O(alpha(n)) alpha is inverse Ackermann function which grows extremely slowly with n, so nearly constant for practical use but not constant because recursive find will trigger sometimes and that depends on size
	if (x != root[x])
		root[x] = find(root[x])
	return x
	
union(x,y): // O(alpha(n))
	rootx = find(x)
	rooty = find(y)
	if (rootx != rooty):
		if (rank[rootx] > rank[rooty]):
			root[rooty] = rootx // do not change height
		else if (rank[rootx] < rank[rooty]):
			root[rootx] = rooty
		else: // same height tree union would cause the root has height + 1
			root[rootx] = rooty
			rank[rooty]++
// connected check will also be O(alpha(n))
```

## Union Find with Weights

See problem 399. Evaluate Division, check the detailed explanation in https://leetcode.com/problems/evaluate-division/editorial/:Approach 2: Union-Find with Weights

**Intuition**

As we mentioned before, the problem can also be solved with the **Union-Find** data structure and algorithm.

> As a reminder, the [Union-Find](https://en.wikipedia.org/wiki/Disjoint-set_data_structure) data structure, also known as *Disjoint Set*, is used to track a set of elements partitioned into a number of disjoint (non-overlapping) subsets.
> The Union-Find data structure is often applied to solve the **graph partition** problem, where we partition a graph into a set of inter-connected subgraph.

Given the above description, it is not immediately evident that how we can apply the algorithm in this problem.
To get familiar with the Union-Find data structure, we would recommend one to check out another problem called [Largest Component Size by Common Factor](https://leetcode.com/problems/largest-component-size-by-common-factor/),
where we can apply the Union-Find algorithm in a more ***canonical\*** way.

![graph example](https://leetcode.com/problems/evaluate-division/Figures/399/399_graph_example.png)

One thing is clear though. Thanks to the characteristic of the Union-Find data structure, we can easily determine whether the nodes of `a` and `c` belong to the same *group* in the above graph, which accomplishes the first task that we need to perform, *i.e.* determining if there exists a path between two nodes.

However, one important task is missing, which is how can we calculate the cumulative product along the path, with the Union-Find data structure.

> As a spoiler alert, it suffices to adapt the Union-Find data structure and algorithm a little bit.

**Customized Union-Find Data Structure**

The name of Union-Find data structure is originated from the fact that it mainly consists of two operations: `Union()` and `Find()` defined as follows:

- `Find(x)`: get the identity of the group that the element x belongs to.
- `Union(x, y)`: merge the two groups that the two elements belong to respectively.

Now, here are the adaptions that we will do.
Or more precisely, here are a few **behaviors** that our *customized* Union-Find data structure would possess at the end.

First of all, essentially we will build a *table* which contains an entry for each node in the graph, with the help of Union-Find.

The entry is defined as `key -> (group_id, weight)`.
For example, initially, given a node `a`, its entry in the table would look like `'a' -> ('a', 1)`, where the first `'a'`indicates the id of the node, the second `'a'` indicates the id of the group that the node belongs to, and finally the value `1` indicates the weight of the node.

With the above definitions, the tasks become simple.
Given two nodes (variables `a` and `b`) with entries as `(a_group_id, a_weight)` and `(b_group_id, b_weight)` respectively, to evaluate the query of ab=?\frac{a}{b} = ?*b**a*​=?, we only need to perform the following two calculations:

- `a_group_id == b_group_id`: If so, they belong to the same group, *i.e.* there exists a path between them.
- `a_weight / b_weight`: If the above condition holds, by dividing over the ***relative\*** weights that are assigned to the variables, we then can obtain the result of ab\frac{a}{b}*b**a* at the end.

> Now it all boils down to how we can build the above table with the help of Union-Find algorithm.

Again, let us look at the same example we presented before.

We have two equations as input, namely ab=2, bc=3\frac{a}{b} = 2, \space \frac{b}{c} = 3*b**a*=2, *c**b*=3.

- Initially, the entries for each variable would look like the following, where the `group_id` of each variable is the variable itself and the `weight` of each variable is `1`.
  Each variable forms a group on its own, since there is no relationship among them at the moment.

![init state](https://leetcode.com/problems/evaluate-division/Figures/399/399_union_find_init.png)

- Now if we process the equation ab=2\frac{a}{b}=2*b**a*=2, by joining (**Union** operation) the two groups that the variables `a` and `b` belong to, we would obtain the results as shown in the following graph.
  More precisely, we attach the group of dividend `a` to the one of the divisor `b`.
  Meanwhile, we would also update the *relative* weight of the group `a` to reflect the ratio between the two variables.

![second state](https://leetcode.com/problems/evaluate-division/Figures/399/399_union_find_ab.png)

- Similarly, we continue to process the equation of bc=3\frac{b}{c}=3*c**b*=3, by joining (**Union** operation) the groups of `b` and `c` together.
  Similarly, we attach the group of dividend `b` to the one of divisor `c`.
  And also we update the weight of the group `b` to reflect the ratio between the two variables.

![third state](https://leetcode.com/problems/evaluate-division/Figures/399/399_union_find_bc.png)

- As one might notice, there is some inconsistency in the above graph, *i.e.* the `group_id` of the variable of `a` should then be `c` and the weight of the variable `a` should be `6` rather than `2`.
  Indeed, these inconsistencies are expected.
  The **magic** happens when we invoke the **Find** operation on the variable `a`, where a *chain* reaction would be triggered to update the `group_id` and `weight` along the chain, as follows:

![final state](https://leetcode.com/problems/evaluate-division/Figures/399/399_union_find_ac.png)

> Once the **lazy** evaluation of `find()` is triggered, the states of the nodes along the chain would then be updated, and eventually they become consistent.

The mechanism of update is fairly similar with the DFS traversal, as one will see more in detail in the implementation later.

**Algorithm**

Now that we have defined the behaviors for the desired Union-Find data structure, let us put them down into implementation.

The overall interfaces of our Union-Find data structure remain the same. We will implement two functions: `find(variable)` and `union(dividend, divisor, quotient)`.

- `find(variable)`: the function will return the `group_id` that the variable belongs to. Moreover, the function will update the states of variables along the chain, if there is any discrepancy.
- `union(dividend, divisor, quotient)`: this function will attach the group of dividend to that of the divisor, if they are not already the same group. In addition, it needs to update the weight of the dividend variable accordingly, so that the ratio between the dividend and divisor is respected.

We present a sample implementation of the above two functions in the later section, which is inspired from the post of [WangQiuc](https://leetcode.com/problems/evaluate-division/discuss/270993/Python-BFS-and-UF(detailed-explanation)) in the discussion forum.
Concise the implementation might be, it might be tricky to wrap one's head around it.
One might want to refer to the step-wise example we showed before.

Once we implement the above two functions, we then solve the problem in two steps:

- Step 1): we iterate through each input equation, and invoke the `union(dividend, divisor, quotient)` on each of them, in order to build the Union-Find data structure.
- Step 2): we evaluate the query one by one. The evaluation is just as intuitive as our first approach, which can be broken down into the following cases:
  - case 1): Either of the variables did not appear in the input equations. The query is not valid. We then return `-1.0` as the result.
  - case 2): If both variables are valid, we then apply the `find(variable)` to obtain the tuple of `(group_id, weight)` for each variable. If they are not of the same group, *i.e.* there is no chain of division between them, we then return `-1.0` as the result.
  - case 3): Finally if both variables are of the same group, then we simply perform the division between their `weights` as the result.

```java
class Solution {

    public double[] calcEquation(List<List<String>> equations, double[] values,
            List<List<String>> queries) {

        HashMap<String, Pair<String, Double>> gidWeight = new HashMap<>();

        // Step 1). build the union groups
        for (int i = 0; i < equations.size(); i++) {
            List<String> equation = equations.get(i);
            String dividend = equation.get(0), divisor = equation.get(1);
            double quotient = values[i];

            union(gidWeight, dividend, divisor, quotient);
        }

        // Step 2). run the evaluation, with "lazy" updates in find() function
        double[] results = new double[queries.size()];
        for (int i = 0; i < queries.size(); i++) {
            List<String> query = queries.get(i);
            String dividend = query.get(0), divisor = query.get(1);

            if (!gidWeight.containsKey(dividend) || !gidWeight.containsKey(divisor))
                // case 1). at least one variable did not appear before
                results[i] = -1.0;
            else {
                Pair<String, Double> dividendEntry = find(gidWeight, dividend);
                Pair<String, Double> divisorEntry = find(gidWeight, divisor);

                String dividendGid = dividendEntry.getKey();
                String divisorGid = divisorEntry.getKey();
                Double dividendWeight = dividendEntry.getValue();
                Double divisorWeight = divisorEntry.getValue();

                if (!dividendGid.equals(divisorGid))
                    // case 2). the variables do not belong to the same chain/group
                    results[i] = -1.0;
                else
                    // case 3). there is a chain/path between the variables
                    results[i] = dividendWeight / divisorWeight;
            }
        }

        return results;
    }

    private Pair<String, Double> find(HashMap<String, Pair<String, Double>> gidWeight, String nodeId) {
        if (!gidWeight.containsKey(nodeId))
            gidWeight.put(nodeId, new Pair<String, Double>(nodeId, 1.0));

        Pair<String, Double> entry = gidWeight.get(nodeId);
        // found inconsistency, trigger chain update
        if (!entry.getKey().equals(nodeId)) {
            Pair<String, Double> newEntry = find(gidWeight, entry.getKey());
            gidWeight.put(nodeId, new Pair<String, Double>(
                    newEntry.getKey(), entry.getValue() * newEntry.getValue()));
        }

        return gidWeight.get(nodeId);
    }

    private void union(HashMap<String, Pair<String, Double>> gidWeight, String dividend, String divisor, Double value) {
        Pair<String, Double> dividendEntry = find(gidWeight, dividend);
        Pair<String, Double> divisorEntry = find(gidWeight, divisor);

        String dividendGid = dividendEntry.getKey();
        String divisorGid = divisorEntry.getKey();
        Double dividendWeight = dividendEntry.getValue();
        Double divisorWeight = divisorEntry.getValue();

        // merge the two groups together,
        // by attaching the dividend group to the one of divisor
        if (!dividendGid.equals(divisorGid)) {
            gidWeight.put(dividendGid, new Pair<String, Double>(divisorGid,
                    divisorWeight * value / dividendWeight));
        }
    }
}
```



**Complexity Analysis**

Since we applied the Union-Find data structure in our algorithm, we would like to start with a statement on the time complexity of the data structure, as follows:

> **Statement**: If MM*M* operations, either Union or Find, are applied to NN*N* elements, the total run time is O(M⋅log⁡N)\mathcal{O}(M \cdot \log {N})O(*M*⋅log*N*), when we perform unions arbitrarily instead of by size or rank.

One can refer to the [Wikipedia](https://en.wikipedia.org/wiki/Disjoint-set_data_structure) for more details.

In our case, the maximum number of elements in the Union-Find data structure is equal to twice of the number of equations, *i.e.* each equation introduces two new variables.

Let NN*N* be the number of input equations and MM*M* be the number of queries.

- Time Complexity: O((M+N)⋅log⁡N)\mathcal{O}\big( (M+N) \cdot \log N \big)O((*M*+*N*)⋅log*N*).

  - First of all, we iterate through each input equation and invoke `union()` upon it. As a result, the overall time complexity of this step is O(N⋅log⁡N)\mathcal{O}\big(N \cdot \log N \big)O(*N*⋅log*N*).
  - As the second step, we then evaluate the query one by one. For each evaluation, we invoke the `find()` function at most twice. Therefore, the overall time complexity of this step is O(M⋅log⁡N)\mathcal{O}\big(M \cdot \log N \big)O(*M*⋅log*N*).
  - To sum up, the total time complexity of the algorithm is O((M+N)⋅log⁡N)\mathcal{O}\big( (M+N) \cdot \log N \big)O((*M*+*N*)⋅log*N*).
  - Note, as compared to the DFS/BFS search approach, Union-Find data structure is more **efficient** for the repetitive/redundant query scenario.
  - Once we evaluate a query with Union-Find, all the subsequent repetitive queries or any query that has the overlapping with the previous query in terms of variable group could be evaluated in **constant time**.
    For instance, in the above example, once the query of ac\frac{a}{c}*c**a*​ is evaluated, if later we want to evaluate ab\frac{a}{b}*b**a*​, we could instantly obtain the states of variables `a` and `b` without triggering the chain update again.
    While for DFS/BFS approaches, the cost of evaluating each query is independent for each other.

- Space Complexity: O(N)\mathcal{O}(N)O(*N*)

  - The space complexity of our Union-Find data structure is O(N)\mathcal{O}(N)O(*N*) where we maintain a state for each variable.
  - Since the `find()` function is implemented with recursion, there would be some additional memory consumption in function call stack, which could amount to O(N)\mathcal{O}(N)O(*N*).
  - To sum up, the total space complexity of the algorithm is O(N)+O(N)=O(N)\mathcal{O}(N) + \mathcal{O}(N) = \mathcal{O}(N)O(*N*)+O(*N*)=O(*N*).
  - Again, we did not take into account the space needed to hold the results. Otherwise, the total space complexity would be O(N+M)\mathcal{O}(N + M)O(*N*+*M*).

  ## MST

  Kruskal's alg: can be applied to disconncted graph (better than prim's in sparse graph): 

  1. sort edges in non-decreasing order by weight
  2. take the current min edge in MST if this not form cycle with previous taken edge
  3. repeat 2 until all nodes visited (V-1 edges if connected, otherwise use Unionfind to count parts or track which node has been visited).

  

  Proof of Kruskal: 

  Notes: 1.**n nodes if no cycle at most n - 1 edges**. So since Kruskal stops on n - 1 edges added, it must be a spanning tree. Let's prove by contradiction, if Kruskal's spanning tree is not minimum. See here: https://leetcode.com/explore/learn/card/graph/621/algorithms-to-construct-minimum-spanning-tree/3856/

  

  Prim's Alg: can only be applied to connected graph (better than Kruskal's in dense graph)

  ***\*Step 1:\**** *Determine an arbitrary vertex as the starting vertex of the MST.*
  ***\*Step 2:\**** *Follow steps 3 to 5 till there are vertices that are not included in the MST (known as fringe vertex).*
  ***\*Step 3:\**** *Find edges connecting any tree vertex with the fringe vertices.*
  ***\*Step 4:\**** *Find the minimum among these edges.*
  ***\*Step 5:\**** *Add the chosen edge to the MST if it does not form any cycle.*
  ***\*Step 6:\**** *Return the MST and exit*

  

  ### Cut

  Cut is a partition of vertices into two disjoint subsets. And Crossing Edges are the edges that connect vertices from one subset to another subset.

  "Cut Property": For any cut `C` of the graph, if the weight of an edge `E` in the cut-set of `C` is strictly smaller than the weights of all other edges of the cut-set of `C`, then this edge belongs to all MSTs of the graph. (the cut-set here refers to the set of crossing edges)

  ## DFS

  1. Iterate through all nodes.
  2. For a directed acyclic graph, find all path from one node to another. (since acyclic, path nums must be finite)
  3. Find the Eulerian path (a path that visit all the edges): DFS + recorded visited path + put no where to go in stack + pop stack to a vector as result (reverse order of pushing in).
  4. Find undirected graph if is acyclic: cyclic if dfs find visited node but not direct parent (since two node at most be connected by 1 edge, so impossible count as cycle for two nodes).
  5. Find directed graph if is acyclic: cyclic if dfs find node in the parent visited branch (the current branch that is visiting) (this include two-node situation)
  6. In DG, has cycle from source means source to some node might have infinite paths.

  ## BFS

In Graph theory, the primary use cases of the “breadth-first search” (“BFS”) algorithm are:

1. Traversing all vertices in the “graph”;
2. Finding the shortest path between two vertices in a graph where **all edges have equal and positive weights**. Since DFS has to iterate through all nodes to evaluate all paths, while bfs once found source to target, guarantee to be shortest.

For a DAG, if find paths from one to another, if find all same as DFS, but if found one might be slower than DFS. For example if destination is very deep in graph, BFS has to go through almost all nodes to find, while DFS might discover not iterating all nodes.

For a directed acyclic graph (DAG) with *V* vertices, there could be at most $2^{v-2}$ possible paths to go from the starting vertex to the target vertex.  (each subset containing start and end is a path, so count subset number of $v - 2$ nodes, which is $s^{v-2}$)

TODO: what is binary heap and what is fibonnaci heaphttps://www.geeksforgeeks.org/fibonacci-heap-set-1-introduction/



## Single source shortest path(shortest path in weighted graph)

Edge relaxation: For example a->c is 3, but a->b is 1 and b->c is 1 so a->c can be relaxed like a rubber band by tighten a->b->c. In a simple manner, it's just update shortest path between two nodes by finding alternative paths.

### Dijkstra's algorithm

Can only be used to solve single source shortest path problem with non-negative weights.

1. Init all vertex with dist to source be infinity, and prev node be null. 
2. Choose the source vertex as currrent vertex, and set dist to 0, prev be null. push to pq.
3. select all adjacent but not visited vertex to the current vertex (pop from pq with min dist), update the old to source dist if (this adj vertex to current vertex + current vertex to source dist) is smaller than the adj vertex's dist to source node, if update successfully, write current vertex as the prev vertex of that adj vertex and push new dist node pair into pq. Mark current node as visited.
4. repeat 3 until no unvisited node.
5. To find shortest path from source to x vertex, the path min weight is x's dist to source and the path is the reverse order of x + track back prev node from x to source.

We can see there at most V(V-1) node in pq, each edge will be iterate twice when two side check their connected nodes, so at most 2Elog(V(V-1)) on the update step and we need to keep track of a vector of min dist of each node to source and init it need V, so in total if used a binary heap, we need O(V + ElogV) time.



### Bellman-Ford algorithm

Can be solve single source shortest path problem with any weights (including negative weights).

Theorem 1: a graph with no negative weighted edges with V vertex, the shortest path between two vertex has at most V - 1 edges.

Theorem 2: a graph with negative weight cycles, there is no shortest path.

**positive weight cycles**: sum of edges on cycle has a total weight that is positive.

**negative weight cycles**: sum of edges on cycle has a total weight hat is negative.

source to V vertex, 0 - V-1 of edges, construct a dp table.

TODO: SPFA in explore



## Topological sorting

**Algorithm:** Steps involved in finding the topological ordering of a DAG: 
**Step-1:** Compute in-degree (number of incoming edges) for each of the vertex present in the DAG and initialize the count of visited nodes as 0.
**Step-2:** Pick all the vertices with in-degree as 0 and add them into a queue (Enqueue operation)
**Step-3:** Remove a vertex from the queue (Dequeue operation) and then. 

1. Increment the count of visited nodes by 1.
2. Decrease in-degree by 1 for all its neighbouring nodes.
3. If the in-degree of neighbouring nodes is reduced to zero, then add it to the queue.

**Step 4:** Repeat Step 3 until the queue is empty.
**Step 5:** If the count of visited nodes is **not** equal to the number of nodes in the graph then the topological sort is not possible for the given graph. (Important, for cycle checking, disconnected does not effect topological sort)

Important fact: The number of minimal height tree for a tree is at most 2. For any chain formed, there can be 2.

Important fact: Find the minimal height tree is basically find the centroid of the tree (can be multiple), use topological sort to find the last in-deg to be 0

