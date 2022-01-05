# c++中对的优先级队列(先排序)

> 原文:[https://www . geesforgeks . org/priority-c 对队列-按优先顺序排列/](https://www.geeksforgeeks.org/priority-queue-of-pairs-in-c-ordered-by-first/)

在 C++中， [priority_queue](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) 实现[堆](https://www.geeksforgeeks.org/heap-data-structure/)。以下是创建[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)类型的优先级队列的一些示例。

按第一个元素排序的最大优先级队列(或最大堆)

```
// C++ program to create a priority queue of pairs.
// By default a max heap is created ordered
// by first element of pair.
#include <bits/stdc++.h>

using namespace std;

// Driver program to test methods of graph class
int main()
{
    // By default a max heap is created ordered
    // by first element of pair.
    priority_queue<pair<int, int> > pq;

    pq.push(make_pair(10, 200));
    pq.push(make_pair(20, 100));
    pq.push(make_pair(15, 400));

    pair<int, int> top = pq.top();
    cout << top.first << " " << top.second;
    return 0;
}
```

输出:

```
20 100
```

 **按第一个元素**排序的最小优先级队列(或最小堆)

```
// C++ program to create a priority queue of pairs.
// We can create a min heap by passing adding two 
// parameters, vector and greater().
#include <bits/stdc++.h>

using namespace std;

typedef pair<int, int> pi;

// Driver program to test methods of graph class
int main()
{
    // By default a min heap is created ordered
    // by first element of pair.
    priority_queue<pi, vector<pi>, greater<pi> > pq;

    pq.push(make_pair(10, 200));
    pq.push(make_pair(20, 100));
    pq.push(make_pair(15, 400));

    pair<int, int> top = pq.top();
    cout << top.first << " " << top.second;
    return 0;
}
```

输出:

```
10 200
```