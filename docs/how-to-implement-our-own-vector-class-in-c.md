# 如何在 C++中实现自己的 Vector 类？

> 原文:[https://www . geesforgeks . org/如何实现我们自己的矢量类 in-c/](https://www.geeksforgeeks.org/how-to-implement-our-own-vector-class-in-c/)

给定的任务是在 C++中实现一个行为类似于[向量类](https://www.geeksforgeeks.org/vector-in-cpp-stl/)的类。
向量与动态数组相同，能够在插入或删除元素时自动调整自身大小，其存储由容器自动处理。向量元素被放在连续的存储中，这样就可以使用迭代器访问和遍历它们。在向量中，数据被插入到末尾。在末尾插入需要不同的时间，因为有时可能需要扩展数组。移除最后一个元素只需要恒定的时间，因为不会发生调整大小的情况。在开始或中间插入和擦除在时间上是线性的。

我们也可以使用模板使向量类通用。
与我们将要实现的向量相关联的某些函数是:

*   **void push(int data)** :这个函数取一个元素，插入到最后一个。摊销时间复杂度为 O(1)。
*   **void push(int data，int index):** 它在指定的索引处插入数据。时间复杂度为 O(1)。
*   **int get(int index):** 用于获取指定索引处的元素。时间复杂度为 O(1)。
*   **void pop():** 删除最后一个元素。时间复杂度为 O(1)。
*   **int size():** 返回向量的大小，即向量中的元素个数。时间复杂度为 O(1)。
*   **int getcapacity():** 返回向量的容量。时间复杂度为 O(1)。
*   **void print():** 用于打印数组元素。时间复杂度为 O(N)，其中 N 是向量的大小。

下面是我们自己的 Vector 类的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Self implementation of
// the Vector Class in C++

#include <bits/stdc++.h>
using namespace std;
template <typename T> class vectorClass
{

    // arr is the integer pointer
    // which stores the address of our vector
    T* arr;

    // capacity is the total storage
    // capacity of the vector
    int capacity;

    // current is the number of elements
    // currently present in the vector
    int current;

public:
    // Default constructor to initialise
    // an initial capacity of 1 element and
    // allocating storage using dynamic allocation
    vectorClass()
    {
        arr = new T[1];
        capacity = 1;
        current = 0;
    }

    // Function to add an element at the last
    void push(T data)
    {

        // if the number of elements is equal to the
        // capacity, that means we don't have space to
        // accommodate more elements. We need to double the
        // capacity
        if (current == capacity) {
            T* temp = new T[2 * capacity];

            // copying old array elements to new array
            for (int i = 0; i < capacity; i++) {
                temp[i] = arr[i];
            }

            // deleting previous array
            delete[] arr;
            capacity *= 2;
            arr = temp;
        }

        // Inserting data
        arr[current] = data;
        current++;
    }

    // function to add element at any index
    void push(T data, int index)
    {

        // if index is equal to capacity then this
        // function is same as push defined above
        if (index == capacity)
            push(data);
        else
            arr[index] = data;
    }

    // function to extract element at any index
    T get(int index)
    {

        // if index is within the range
        if (index < current)
            return arr[index];
    }

    // function to delete last element
    void pop() { current--; }

    // function to get size of the vector
    int size() { return current; }

    // function to get capacity of the vector
    int getcapacity() { return capacity; }

    // function to print array elements
    void print()
    {
        for (int i = 0; i < current; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
};

// Driver code
int main()
{
    vectorClass<int> v;
    vectorClass<char> v1;
    v.push(10);
    v.push(20);
    v.push(30);
    v.push(40);
    v.push(50);
    v1.push(71);
    v1.push(72);
    v1.push(73);
    v1.push(74);

    cout << "Vector size : " << v.size() << endl;
    cout << "Vector capacity : " << v.getcapacity() << endl;

    cout << "Vector elements : ";
    v.print();

    v.push(100, 1);

    cout << "\nAfter updating 1st index" << endl;

    cout << "Vector elements of type int : " << endl;
    v.print();
    // This was possible because we used templates
    cout << "Vector elements of type char : " << endl;
    v1.print();
    cout << "Element at 1st index of type int: " << v.get(1)
         << endl;
    cout << "Element at 1st index of type char: "
         << v1.get(1) << endl;

    v.pop();
    v1.pop();

    cout << "\nAfter deleting last element" << endl;

    cout << "Vector size of type int: " << v.size() << endl;
    cout << "Vector size of type char: " << v1.size()
         << endl;
    cout << "Vector capacity of type int : "
         << v.getcapacity() << endl;
    cout << "Vector capacity of type char : "
         << v1.getcapacity() << endl;

    cout << "Vector elements of type int: ";
    v.print();
    cout << "Vector elements of type char: ";
    v1.print();

    return 0;
}
```

**Output**

```
Vector size : 5
Vector capacity : 8
Vector elements : 10 20 30 40 50 

After updating 1st index
Vector elements of type int : 
10 100 30 40 50 
Vector elements of type char : 
G H I J 
Element at 1st index of type int: 100
Element at 1st index of type char: H

After deleting last element
Vector size of type int: 4
Vector size of type char: 3
Vector capacity of type int : 8
Vector capacity of type char : 4
Vector elements of type int: 10 100 30 40 
Vector elements of type char: G H I 
```