# c++ STL 中向量的优先级队列，示例

> 原文:[https://www . geesforgeks . org/priority-queue-of-vectors-in-c-STL-with-examples/](https://www.geeksforgeeks.org/priority-queue-of-vectors-in-c-stl-with-examples/)

**[STL 中的 Priority Queue](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)**Priority Queue 是容器适配器的一种类型，专门设计为队列的第一个元素是队列中所有元素中最大的，并且元素的顺序是非递增的(因此我们可以看到队列的每个元素都有一个优先级{固定顺序})

**[STL 中的向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)** 向量与动态数组相同，能够在插入或删除元素时自动调整自身大小，其存储由容器自动处理。向量元素被放在连续的存储中，这样就可以使用迭代器访问和遍历它们。

**STL 中向量的优先级队列:**向量的优先级队列在设计复杂的数据结构时非常有效。

**语法:**

```
priority_queue<vector<datatype>> pq;

```

**例如**:考虑一个简单的问题，我们必须打印队列中的最大向量。

```
// C++ program to demonstrate
// use of priority queue for vectors

#include <bits/stdc++.h>
using namespace std;

priority_queue<vector<int> > pq;

// Prints maximum vector
void Print_Maximum_Vector(vector<int> Vec)
{
    for (int i = 0; i < Vec.size(); i++) {
        cout << Vec[i] << " ";
    }
    cout << endl;
    return;
}

// Driver code
int main()
{
    // Initializing some vectors
    vector<int> data_1{ 10, 20, 30, 40 };
    vector<int> data_2{ 10, 20, 35, 40 };
    vector<int> data_3{ 30, 25, 10, 50 };
    vector<int> data_4{ 20, 10, 30, 40 };
    vector<int> data_5{ 5, 10, 30, 40 };

    // Inserting vectors into priority queue
    pq.push(data_1);
    pq.push(data_2);

    // printing the maximum vector till now
    Print_Maximum_Vector(pq.top());

    // Inserting vectors into priority queue
    pq.push(data_3);

    // printing the maximum vector till now
    Print_Maximum_Vector(pq.top());

    // Inserting vectors into priority queue
    pq.push(data_4);
    pq.push(data_5);

    // printing the maximum vector till now
    Print_Maximum_Vector(pq.top());

    return 0;
}
```

**Output:**

```
10 20 35 40 
30 25 10 50 
30 25 10 50

```