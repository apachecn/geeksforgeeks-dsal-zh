# c++中对的优先级队列，按第一和第二元素排序

> 原文:[https://www . geesforgeks . org/priority-按第一和第二元素排序的 c 对队列/](https://www.geeksforgeeks.org/priority-queue-of-pairs-in-c-with-ordering-by-first-and-second-element/)

[优先级队列:](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)优先级队列是[队列](https://www.geeksforgeeks.org/queue-data-structure/)的扩展，优先弹出与优先级相关联的元素和优先级较高的元素。

优先级队列可以包含具有各种数据类型的元素，例如整数、整数对、自定义数据类型。但是有一点很常见，那就是有一个元素定义了元素的优先级。
因此，优先级队列对可以有两种排序方式–

*   按对的第一个元素排序
*   按对的第二个元素排序

### 按第一个元素排序的优先级队列

在 C++中，如果元素是成对的形式，那么默认情况下，元素的优先级取决于第一个元素。因此，我们只需要使用成对的优先级队列。

## C++

```
// C++ implementation of the
// priority queue of pairs
// ordered by the first element

#include <iostream>
#include <queue>
using namespace std;

// Function to print the data of
// the priority queue ordered by first
void showpq(
    priority_queue<pair<int, int> > g)
{
    // Loop to print the elements
    // until the priority queue
    // is not empty
    while (!g.empty()) {
        cout << g.top().first
             << " " << g.top().second
             << endl;
        g.pop();
    }
    cout << endl;
}

// Driver Code
int main()
{
    priority_queue<pair<int, int> > p1;

    // Insertion of elements
    p1.push(make_pair(4, 5));
    p1.push(make_pair(5, 4));
    p1.push(make_pair(1, 6));
    p1.push(make_pair(7, 3));
    p1.push(make_pair(9, 4));
    showpq(p1);
    return 0;
}
```

**Output:**

```
9 4
7 3
5 4
4 5
1 6

```