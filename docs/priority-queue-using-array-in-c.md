# c++中使用数组的优先级队列

> 原文:[https://www . geesforgeks . org/priority-queue-use-array-in-c/](https://www.geeksforgeeks.org/priority-queue-using-array-in-c/)

[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)是[队列](https://www.geeksforgeeks.org/queue-data-structure/)数据结构的扩展，其中每个元素都有一个与之相关联的特定优先级。它基于优先级值，从队列中删除元素。

**对优先级队列的操作:**

*   **enqueue():** 该函数用于将新数据插入队列。
*   **出列():**该函数从队列中移除优先级最高的元素。
*   **peek()/top():** 此函数用于获取队列中优先级最高的元素，而不将其从队列中移除。

**方法:**想法是创建一个结构来存储元素的值和优先级，然后创建该结构的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)来存储元素。以下是将要实现的功能:

*   **enqueue():** 用于在队列末尾插入元素。
*   **peek():**
    *   遍历优先级队列，找到优先级最高的元素并返回其索引。
    *   在多个元素具有相同优先级的情况下，找到具有最高优先级的具有最高值的元素。
*   **出列():**
    *   使用 **peek()** 函数找到优先级最高的索引让我们将该位置称为 **ind** ，然后将位置 **ind** 之后的所有元素的位置向左移动一个位置。
    *   将尺寸减小一。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure for the elements in the
// priority queue
struct item {
    int value;
    int priority;
};

// Store the element of a priority queue
item pr[100000];

// Pointer to the last index
int size = -1;

// Function to insert a new element
// into priority queue
void enqueue(int value, int priority)
{
    // Increase the size
    size++;

    // Insert the element
    pr[size].value = value;
    pr[size].priority = priority;
}

// Function to check the top element
int peek()
{
    int highestPriority = INT_MIN;
    int ind = -1;

    // Check for the element with
    // highest priority
    for (int i = 0; i <= size; i++) {

        // If priority is same choose
        // the element with the
        // highest value
        if (highestPriority
                == pr[i].priority
            && ind > -1
            && pr[ind].value
                   < pr[i].value) {
            highestPriority = pr[i].priority;
            ind = i;
        }
        else if (highestPriority
                 < pr[i].priority) {
            highestPriority = pr[i].priority;
            ind = i;
        }
    }

    // Return position of the element
    return ind;
}

// Function to remove the element with
// the highest priority
void dequeue()
{
    // Find the position of the element
    // with highest priority
    int ind = peek();

    // Shift the element one index before
    // from the position of the element
    // with highest priortity is found
    for (int i = ind; i < size; i++) {
        pr[i] = pr[i + 1];
    }

    // Decrease the size of the
    // priority queue by one
    size--;
}

// Driver Code
int main()
{
    // Function Call to insert elements
    // as per the priority
    enqueue(10, 2);
    enqueue(14, 4);
    enqueue(16, 4);
    enqueue(12, 3);

    // Stores the top element
    // at the moment
    int ind = peek();

    cout << pr[ind].value << endl;

    // Dequeue the top element
    dequeue();

    // Check the top element
    ind = peek();
    cout << pr[ind].value << endl;

      // Dequeue the top element
    dequeue();

      // Check the top element
    ind = peek();
    cout << pr[ind].value << endl;

    return 0;
}
```

**Output:** 

```
16
12
```

***复杂度分析:***

*   *入队():O(1)*
*   *peek(): O(N)*
*   *出列:O(N)*

**<u>优先队列的应用</u> :**

*   对于[调度算法](https://www.geeksforgeeks.org/cpu-scheduling-in-operating-systems/)，中央处理器必须处理具有优先级的特定任务。具有较高优先级的进程首先被执行。
*   在分时计算机系统中，等待 CPU 时间的过程被加载到[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中。
*   排序优先级队列用于对[堆](https://www.geeksforgeeks.org/heap-sort/)进行排序。