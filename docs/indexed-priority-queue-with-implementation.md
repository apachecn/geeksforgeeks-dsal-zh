# 带实现的索引优先级队列

> 原文:[https://www . geesforgeks . org/indexed-priority-queue-with-implementation/](https://www.geeksforgeeks.org/indexed-priority-queue-with-implementation/)

[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)是一种[数据结构](https://www.geeksforgeeks.org/data-structures/)，其中数据根据其优先级进行存储。在**索引优先级队列**中，数据就像标准优先级队列一样被存储，同时，数据的值可以使用它的关键字来更新。之所以称为“**索引**，是因为[哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)可以使用输入的键值对的键作为哈希映射的键来存储容器中的索引。这在使用最小堆实现[迪克斯特拉算法时非常方便。它也可以用在任何其他程序中，在这些程序中，需要将键值对放入优先级队列中，同时需要使用推送或弹出功能来更新键值。](https://www.geeksforgeeks.org/dijkstras-algorithm-for-adjacency-list-representation-greedy-algo-8/)

**<u>索引优先级队列中的操作:</u>** 索引优先级队列中可以执行的操作有:

1.  **<u>push</u>: ** Adding key-value pair in Indexed Priority Queue according to its priority.

    *实现:*为此，在容器中添加键值对，然后根据键值对中的值进行堆积。

    *时间复杂度:* O( log(n))

2.  **<u>pop:</u>**  Removing the highest priority key-value pair.

    *实现:*移除堆的顶部，然后堆容器的其余部分。

    *时间复杂度:* O( log(n))

3.  **<u>top</u>**: Return Key-Value pair to user.

    *实现:*返回堆顶部的键值对。

    *时间复杂度:* O(1)

4.  **<u>size</u>**: Return the number of key-value pairs in the Indexed Priority Queue.

    *实现:*跟踪类中队列中的元素数量，并在调用 size()函数时返回变量。

    *时间复杂度:* O(1)

5.  **<u>empty</u>**: Return true when Indexed Priority Queue is empty.

    *实现:*当元素变量个数等于零时返回 true。

    *时间复杂度:* O(1)

6.  **<u>changeAtKey</u>**: This function differentiate Indexed Priority Queue from standard priority queue. It takes two arguments from user, first is key and second is new value, and it update old value associated with the key to new value provided and update its position according to priority of new value.

    *实现:*保留一个哈希映射，它的键是键值对中的键，它指向容器中键的索引。调用该函数时，根据当前元素的优先级更新所需索引处的值并定位当前元素，最后更改哈希映射中的索引值。

    *时间复杂度:* O( log(n))

**索引优先级队列的实现:**

索引优先级队列是使用[二进制堆](https://www.geeksforgeeks.org/binary-heap/)实现的，但是也可以使用[斐波那契堆](https://www.geeksforgeeks.org/fibonacci-heap-set-1-introduction/)或 [K 进制堆实现。](https://www.geeksforgeeks.org/k-ary-heap/)

定义索引优先级队列实例时，需要传递四个参数(两个命令和两个可选参数)，它们是:

1.  **键**的数据类型:这是定义中的第一个参数，应该是可以在哈希映射中哈希的数据类型，或者用户已经将自己的哈希函数作为第四个参数传递。要了解哈希映射中哈希函数的更多信息，请参阅本文。
2.  **数值的数据类型**:这是定义中的第二个参数。
3.  **比较器**:这是第三个可选参数。默认情况下，索引优先级队列将使用最大堆来实现，以改变用户必须传递不同的比较器，其参数(即比较器的参数)作为值的数据类型。
4.  **哈希函数**:这是第四个参数，只有当用户为 key 传递自定义数据类型(比如类)时才需要，那么用户必须传递自己的哈希函数。

下面是索引优先级队列的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

template <class T1, class T2,
          class Comparator = less<T2>,
          class Hash = hash<T1> >

class indexed_priority_queue {

    // Storing indices of values using key
    unordered_map<T1, long long int, Hash> m;

    // Container
    vector<pair<T1, T2> > v;

    // Size
    long long numberOfElement;

    // Creating a instance of Comparator class
    Comparator comp;

    // Max Capacity
    long long capacity = LLONG_MAX;

    // Obtaing the index value from hash map
    long long int getValueIndex(T1 key)
    {
        if (m[key] == 0) {
            cout << "No Such Key Exist";
            return -1;
        }
        return v[m[key] - 1];
    }

    // heapify the container
    void heapify(vector<pair<T1, T2> >& v,
                 long long int heap_size,
                 long long index)
    {
        long long leftChild = 2 * index + 1,
                  rightChild = 2 * index + 2,
                  suitableNode = index;

        if (leftChild < heap_size
            && comp(v[suitableNode].second,
                    v[leftChild].second)) {
            suitableNode = leftChild;
        }

        if (rightChild < heap_size
            && comp(v[suitableNode].second,
                    v[rightChild].second)) {
            suitableNode = rightChild;
        }

        if (suitableNode != index) {

            // swap the value
            pair<T1, T2> temp = v[index];
            v[index] = v[suitableNode];
            v[suitableNode] = temp;

            // updating the map
            m[v[index].first] = index + 1;
            m[v[suitableNode].first]
                = suitableNode + 1;

            // heapify other affected nodes
            heapify(v, numberOfElement,
                    suitableNode);
        }
    }

public:
    indexed_priority_queue()
    {
        numberOfElement = 0;
        m.clear();
        v.clear();
    }

    void push(T1 key, T2 value)
    {
        if (numberOfElement == capacity) {
            cout << "Overflow";
            return;
        }
        if (m[key] != 0) {
            cout << "Element Already Exists";
            return;
        }

        // Adding element
        v.push_back(make_pair(key, value));
        numberOfElement++;
        m[key] = numberOfElement;

        long long index = numberOfElement - 1;

        // Comparing to parent node
        while (index != 0
               && comp(v[(index - 1) / 2].second,
                       v[index].second)) {

            // swap the value
            pair<T1, T2> temp = v[index];
            v[index] = v[(index - 1) / 2];
            v[(index - 1) / 2] = temp;

            // updating the map
            m[v[index].first] = index + 1;
            m[v[(index - 1) / 2].first]
                = (index - 1) / 2 + 1;

            // updating index in map
            index = (index - 1) / 2;
        }
    }

    void pop()
    {
        if (numberOfElement == 0) {
            cout << "UnderFlow";
            return;
        }

        // Removing element
        v.erase(v.begin());
        numberOfElement--;
        heapify(v, numberOfElement, 0);
    }

    pair<T1, T2> top() { return v[0]; }

    long long int size() { return numberOfElement; }

    bool empty() { return numberOfElement == 0; }

    void changeAtKey(T1 key, T2 value)
    {
        if (m[key] == 0) {
            cout << "No Such Key Exist";
            return;
        }
        long long index = m[key] - 1;
        v[index].second = value;

        // Comparing to child nodes
        heapify(v, numberOfElement, index);

        // Comparing to Parent Node
        while (index != 0
               && comp(v[(index - 1) / 2].second,
                       v[index].second)) {

            // swap the value
            pair<T1, T2> temp = v[index];
            v[index] = v[(index - 1) / 2];
            v[(index - 1) / 2] = temp;

            // updating the map
            m[v[index].first] = index + 1;
            m[v[(index - 1) / 2].first]
                = (index - 1) / 2 + 1;

            // updating index in map
            index = (index - 1) / 2;
        }
    }
};

void display(indexed_priority_queue<int, int> IPQ)
{
    indexed_priority_queue<int, int> temp = IPQ;
    while (!IPQ.empty()) {
        pair<int, int> tmp;
        tmp = IPQ.top();
        IPQ.pop();
        cout << "( " << tmp.first << ", "
             << tmp.second << " ) ";
    }
    cout << '\n';
}

// Driver Code
int main()
{

    // First parameter is key datatype
    // and it should be hashable
    // Second parameter is value datatype comparator
    // function (by default it implements maxheap)
    indexed_priority_queue<int, int> IPQ;

    // Check if empty
    cout << "Checking if initially the IPQ is empty\n";
    if (IPQ.empty())
        cout << "IPQ is empty\n";
    else
        cout << "IPQ is not empty\n";

    // Insertion
    cout << "Inserting pairs (2, 1), (3, 7), "
         << " (1, 0) and (4, 5)\n";
    IPQ.push(2, 1);
    IPQ.push(3, 7);
    IPQ.push(1, 0);
    IPQ.push(4, 5);

    // Printing the contents of IPQ
    cout << "IPQ: ";
    display(IPQ);
    cout << '\n';

    // Checking size and top after pushing
    cout << "Size: " << IPQ.size() << endl;
    cout << "Top: " << IPQ.top().first
         << ", " << IPQ.top().second
         << "\n\n";

    // Replace operation
    cout << "Changing value associated with"
         << " key 3 to 2 and 1 to 9\n";
    IPQ.changeAtKey(3, 2);
    IPQ.changeAtKey(1, 9);

    // Checking size and top after replacement
    cout << "Size: " << IPQ.size() << endl;
    cout << "Top: " << IPQ.top().first
         << ", " << IPQ.top().second
         << "\n\n";

    // Deleting 2 elements from IPQ
    cout << "Poping an element from IPQ: ";
    IPQ.pop();
    cout << "\nPoping an element from IPQ: ";
    IPQ.pop();
    cout << '\n\n';

    // Printing the contents of IPQ after deletion
    cout << "IPQ: ";
    display(IPQ);
    cout << '\n';

    // Checking size and top after pushing
    cout << "Size: " << IPQ.size() << endl;
    cout << "Top: " << IPQ.top().first
         << ", " << IPQ.top().second
         << "\n\n";

    return 0;
}
```

**Output:**

> 检查最初 IPQ 是否是空的
> IPQ 是空的
> 
> 插入对(2，1)、(3，7)、(1，0)和(4，5)
> IPQ: ( 3，7 ) ( 4，5 ) ( 2，1 ) ( 1，0)
> 
> 尺寸:4
> 顶部:3、7
> 
> 更改与键 3 至 2 和 1 至 9 相关的值
> 尺寸:4
> 顶部:1，9
> 
> 从 IPQ 大力推广元素:
> 从 IPQ 大力推广元素:
> 
> IPQ: ( 3，2 ) ( 2，1)
> 
> 尺寸:2
> 顶部:3、2