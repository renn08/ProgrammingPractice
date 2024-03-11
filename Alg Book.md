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



Follows the order on this one:

https://github.com/youngyangyang04/leetcode-master

## Array

|       Data Type        | Size (in bytes) |              Range              |
| :--------------------: | :-------------: | :-----------------------------: |
|       short int        |        2        |        -32,768 to 32,767        |
|   unsigned short int   |        2        |           0 to 65,535           |
|      unsigned int      |        4        |       0 to 4,294,967,295        |
|          int           |        4        | -2,147,483,648 to 2,147,483,647 |
|        long int        |        4        | -2,147,483,648 to 2,147,483,647 |
|   unsigned long int    |        4        |       0 to 4,294,967,295        |
|     long long int      |        8        |       -(2^63) to (2^63)-1       |
| unsigned long long int |        8        | 0 to 18,446,744,073,709,551,615 |
|      signed char       |        1        |           -128 to 127           |
|     unsigned char      |        1        |            0 to 255             |
|         float          |        4        |     -3.4×10^38 to 3.4×10^38     |
|         double         |        8        |    -1.7×10^308 to1.7×10^308     |
|      long double       |       12        |   -1.1×10^4932 to1.1×10^4932    |
|        wchar_t         |     2 or 4      |        1 wide character         |

How to define the struct:

struct Node{

};

```
// Create a string of size n and fill
// the string with character x.
string s(size_t n, char x);
```

Set uses red-black tree(one kind of balanced tree) while unordered_set uses hash table, so the latter one has a faster performance on insert, access and delete.

In C++, the `std::set` container provides a built-in iterator that allows you to iterate through the elements in a sorted order. Here's an example of how you can iterate through a `std::set` in ascending order:

```
cppCopy code
#include <iostream>
#include <set>

int main() {
    std::set<int> mySet = {5, 3, 1, 4, 2};

    // Iterate through the set in ascending order
    for (const auto& element : mySet) {
        std::cout << element << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the `for` loop uses a range-based loop and `const auto&` to iterate through each element of the set. The elements are accessed in ascending order due to the nature of the `std::set` container.

If you want to iterate in descending order, you can use reverse iterators as shown in the following example:

```
cppCopy code
#include <iostream>
#include <set>

int main() {
    std::set<int> mySet = {5, 3, 1, 4, 2};

    // Iterate through the set in descending order
    for (auto it = mySet.rbegin(); it != mySet.rend(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

Here, `mySet.rbegin()` returns a reverse iterator pointing to the last element, and `mySet.rend()` returns an iterator representing the position before the first element. By iterating from `rbegin()` to `rend()` and dereferencing the iterator `it`, you can access the elements in descending order.

It's important to note that the order of iteration in a `std::set` is based on the sorting criterion (usually less-than operator by default) applied to the elements, ensuring the elements are visited in a sorted order.

The default insert value of a unordered_map will be 0, 0.0, false.



INT_MAX = 2147483647 = 2.15*10^9

string.erase or vector.erase is O(N)

resize is the efficient way to modify front and end of a array's auxiliary elements.

When you call `vector.resize(new_size)`, the behavior depends on whether the new size is larger or smaller than the current size of the vector:

1. If `new_size` is larger than the current size, the function will append default-constructed elements to the vector until it reaches the new size. The additional elements are appended to the end of the vector. This means that existing elements in the vector will remain unchanged, and new elements will be added after the existing ones.
2. If `new_size` is smaller than the current size, the function will remove elements from the end of the vector until it reaches the new size. This effectively truncates the vector to the specified size. The removed elements are destroyed, and the memory they occupied is deallocated.



## KMP Alg

mainly aimed for string match alg.

前缀是包含首字母但不包含尾字母的所有子串。

后缀是包含尾字母但不包含首字母的所有子串。

求最长相等前后缀的长度：

aabaaf 

a 0

aa 1

aab 0

aaba 1

aabaa 2

aabaaf 0

if a mismatch happens, refers to the max equal prefix backfix length of the substring end right before the current mismatched char, the number is just the index which we should start to match again.

How to calculate the next table (前缀表)：

不减一写法：

```c++
// try to calculate next, next[i] represent the 当string end with idx i时候前后缀相同最大长度 （称为t）
void getNext(int* next, const string& s) {
        int j = 0;// 前缀末尾 （目的去求最长前缀，然后j+1就是最长长度 
        next[0] = 0;// string end with the first element has 0 t
        for(int i = 1; i < s.size(); i++) {// 0 is already defined in next, start with 1, i is the 后缀末尾
            while (j > 0 && s[i] != s[j]) { // j要保证大于0，因为下面有取j-1作为数组下标的操作
                j = next[j - 1]; // 尝试匹配最新一位，假若不相等，找到后退位置（这里开始重新尝试匹配，因为此位置之前的前缀可以和保留着和当前后缀（除去不匹配的那一位）的匹配重新从next位置尝试匹配，找还匹配部分的t所以j-1
            }
            if (s[i] == s[j]) { // 由于只看到idx i的后缀只需要比较一位
                j++;//保持前后缀相等
            }
            next[i] = j;//要的是t，j是idx在匹配子串末尾后一位刚好等于长度
        }
    }
```

kmp worst time is O(n +m) m text size, n pattern size 

Why?

I would say a pattern like

```
xx........x
| n times |
```

and a string like

```
xxx.........xyx...........xy....
| n-1 times | | n-1 times |
```

would be one of the worst cases, but it's still `O(m+n)`

each mismatch on y would need process the whole pattern, so N *times of y appears = N * M/ N = M

and also the first scan through pattern, so O(M+N)

while normal double ptr might has worst O(M(N - 1))





| Num                                                          | Title                                              | Solution in one sentence                                     |
| ------------------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------ |
| 344                                                          | reverse array                                      | reverse from idx start with a length l, replace idx start + i with start + l - 1 - i and i from 0 to (l - 1) / 2 |
| 剑指offer5(***)                                              | 替换空格                                           | 1.no copy, double ptr, resize space for string(str.resize(new_size)), start from behind filling using double ptr point to the end of the original array and resiezed array(on the same one). 2. copy and filling from beginning to end. |
| 155(***)                                                     | Reverse word in a string                           | 1. Stack. 2. (better) reverse whole and then reverse each word, double ptr for removing auxiliary space in between words, one for wirte correct string, one for the current element in original string. Use resize to move auxiliary space at the end of string. Then double ptr for reverse each word. |
| [剑指 Offer 58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/) |                                                    | reverse part and reverse whole, no extra space.              |
| 28(\*\*\*\*\*)                                               | Find the Index of the First Occurrence in a String | KMP alg or double ptr, seems on small cases the complexity no much difference |
| 459                                                          | Repeated Substring pattern                         | Cat two, remove head tail, should find original in it, using KMP |
|                                                              |                                                    |                                                              |

基础课1

Time comlexity 

O(x^x) > O(x!) > O(2^x) > O(x^2)

Best Complexity, worst complexity, average complexity

for example, fast sort, (last element pivot) worst O(n^2) worst O(nlogn)

Master's throem

T(n) = aT(n/b) + n^c 

if logba > c T(n) = n^(logba)

if = T(n) = n^c * logn

if < T(n) = n^c

Array representation:

Java: 

```java
int[] a = new int[5];
char[][] c = new char[3][];
c[0] = new char[4];// this three are can be at different space, but in c++ such as int a[3][5], all are stored consecutively
// java array has array header before the array stored, so the length can be directly accessed.
c[1] = new char[6];
c[2] = new char[5];
// a.length = 5, can do in java not in c++
ArrayList<Integer> a = new ArrayList<Integer>(5);
```

double ptr:

two sum, three sum, even odd sort, pivot sort, remove element, merge two sorted array

after sort, double ptr, one at begin, one at end, if > t, end-- if <t first++ else return





Lower_bound(a.begin(), a.end(), target) returns the iterator to the first elemnt taht is no less than target, if all smaller than target, return a.end()

Upper_bound(xxx) returns the first element greater than target, if all is no larger than ,return a.end()
