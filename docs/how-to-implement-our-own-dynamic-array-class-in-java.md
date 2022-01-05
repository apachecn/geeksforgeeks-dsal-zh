# 如何在 Java 中实现我们自己的动态数组类？

> 原文:[https://www . geesforgeks . org/如何在 java 中实现我们自己的动态数组类/](https://www.geeksforgeeks.org/how-to-implement-our-own-dynamic-array-class-in-java/)

给定的任务是在 Java 中实现一个[类](https://www.geeksforgeeks.org/classes-objects-java/)，它的行为类似于使用[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)的[动态数组](https://www.geeksforgeeks.org/how-do-dynamic-arrays-work/)。

**数组列表**与**动态数组**相同，能够在插入或删除元素时**自动调整**本身的大小，它们的存储由容器自动处理。

*   数组列表元素被放置在连续的存储中，这样它们就可以使用 [**迭代器**](https://www.geeksforgeeks.org/iterators-in-java/) 来访问和遍历。
*   在数组列表中，数据被插入到末尾。
*   在末尾插入需要不同的时间，因为有时可能需要扩展数组。
*   移除最后一个元素只需要恒定的时间，因为不会发生调整大小的情况。
*   在开始或中间插入和擦除在时间上是线性的。

### 要在动态数组类中实现的函数:

我们将实现的与数组列表相关联的某些函数有:

1.  **void push(int data)** :这个函数取一个元素，插入到最后一个。摊销时间复杂度为 **O(1)** 。
2.  **void push(int data，int index):** 它在指定的索引处插入数据。时间复杂度是 **O(1)** 。
3.  **int get(int index):** 用于获取指定索引处的元素。时间复杂度是 **O(1)** 。
4.  **void pop():** 删除最后一个元素。时间复杂度是 **O(1)** 。
5.  **int size():** 返回数组列表的大小，即数组列表中的元素个数。时间复杂度是 **O(1)** 。
6.  **int getcapacity():** 返回数组列表的容量。时间复杂度是 **O(1)** 。
7.  **void print():** 用于打印数组元素。时间复杂度是 **O(N)** ，其中 N 是数组列表的大小。

### 动态数组类的实现:

下面是我们自己的 ArrayList 类的实现。

```
// Java program to implement
// our own Dynamic Array class

import java.util.*;

// Self implementation of
// the ArrayList Class in Java
class ArrayListClass {

    // arr is the array which stores
    // our ArrayList elements
    private int arr[];

    // capacity is the total storage
    // capacity of the ArrayList
    private int capacity;

    // current is the number of elements
    // currently present in the ArrayList
    private int current;

    // Default constructor to initialise
    // an initial capacity of 1 element and
    // allocating storage using dynamic allocation
    public ArrayListClass()
    {
        arr = new int[1];
        capacity = 1;
        current = 0;
    }

    // Function to add an element at the last
    public void push(int data)
    {

        // if the number of elements
        // is equal to the capacity,
        // that means we don't have space
        // to accommodate more elements.
        // We need to double the capacity
        if (current == capacity) {
            int temp[] = new int[2 * capacity];

            // copying old array elements
            // to new array
            for (int i = 0; i < capacity; i++)
                temp[i] = arr[i];

            capacity *= 2;
            arr = temp;
        }

        // Inserting data
        arr[current] = data;
        current++;
    }

    // function to add element at any index
    void push(int data, int index)
    {

        // if index is equal to capacity
        // then this function is same
        // as push defined above
        if (index == capacity)
            push(data);
        else
            arr[index] = data;
    }

    // Function to extract
    // element at any index
    int get(int index)
    {

        // if index is within the range
        if (index < current)
            return arr[index];

        // if index is outside the range
        return -1;
    }

    // function to delete last element
    void pop()
    {
        current--;
    }

    // function to get size
    // of the ArrayList
    int size()
    {
        return current;
    }

    // function to get capacity
    // of the ArrayList
    int getcapacity()
    {
        return capacity;
    }

    // function to print ArrayList elements
    void print()
    {
        for (int i = 0; i < current; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }

    // Driver program to check ArrayListClass
    public static void main(String args[])
    {
        ArrayListClass v
            = new ArrayListClass();
        v.push(10);
        v.push(20);
        v.push(30);
        v.push(40);
        v.push(50);

        System.out.println("ArrayList size: "
                           + v.size());
        System.out.println(
            "ArrayList capacity: "
            + v.getcapacity());
        System.out.println(
            "ArrayList elements: ");
        v.print();

        v.push(100, 1);

        System.out.println(
            "\nAfter updating 1st index");

        System.out.println(
            "ArrayList elements: ");
        v.print();
        System.out.println(
            "Element at 1st index: "
            + v.get(1));

        v.pop();

        System.out.println(
            "\nAfter deleting the"
            + " last element");

        System.out.println(
            "ArrayList size: "
            + v.size());
        System.out.println(
            "ArrayList capacity: "
            + v.getcapacity());

        System.out.println(
            "ArrayList elements: ");
        v.print();
    }
}
```

**Output:**

```
ArrayList size: 5
ArrayList capacity: 8
ArrayList elements: 
10 20 30 40 50 

After updating 1st index
ArrayList elements: 
10 100 30 40 50 
Element at 1st index: 100

After deleting the last element
ArrayList size: 4
ArrayList capacity: 8
ArrayList elements: 
10 100 30 40

```