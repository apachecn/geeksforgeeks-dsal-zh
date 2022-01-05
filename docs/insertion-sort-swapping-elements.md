# 通过交换元素进行插入排序

> 原文:[https://www . geesforgeks . org/insert-sort-swapping-elements/](https://www.geeksforgeeks.org/insertion-sort-swapping-elements/)

[插入排序](https://www.geeksforgeeks.org/insertion-sort/)适用于小尺寸的数组。如果数组已经排序，它还实现了 O(n)的最佳复杂度。我们已经讨论了[迭代插入排序](https://www.geeksforgeeks.org/insertion-sort/)和[递归插入排序](https://www.geeksforgeeks.org/recursive-insertion-sort/)。在本文中，讨论了迭代版本和递归版本的稍微不同的实现。

**迭代插入排序**

让我们看看迭代插入排序的算法

```
function insertionSort(V)
    i, j, k
    for i from  1..length(V)
        k = V[i]
        j = i-1
        while j > 0 and  k < V[j]
            V[j+1] = V[j]
            j -= 1
        V[j] = k
    return V
```

在 while 循环中，我们将所有大于 k 的值移动一个位置，然后将 k 插入到第一个位置，其中 k 大于数组值。如果我们交换连续的数组元素，也会得到同样的效果。通过反复交换，k 将移动到正确的位置。
我们举个例子来说明一下

```
Insert 3 in A = {1, 2, 4, 5, 6}
Put 3 at the end of list. 
A = {1, 2, 4, 5, 6, 3}
3 < 6, swap 3 and 6
A = {1, 2, 4, 5, 3, 6}
3 < 5 swap 3 and 5
A = {1, 2, 4, 3, 5, 6}
3 < 4 swap 3 and 4
A = {1, 2, 3, 4, 5, 6}
3 > 2 so stop

By repeatedly swapping 3 travels to its proper position in the list
```

因此上述算法可以修改为

```
function insertionSort(V)
    for i in 1...length(V)
        j = i
        while ( j > 0 and V[j] < V[j-1])
            Swap V[j] and V[j-1]
            j -= 1
    return V
```

该算法的 CPP 代码如下

## C++

```
// Iterative CPP program to sort
// an array by swapping elements
#include <iostream>
#include <vector>
using namespace std;
using Vector = vector<int>;

// Utility function to print a Vector
void printVector(const Vector& V)
{
    for (auto e : V) {
        cout << e << " ";
    }
    cout << endl;
}

// Function performs insertion sort on
// vector V
void insertionSort(Vector& V)
{
    int N = V.size();
    int i, j, key;

    for (i = 1; i < N; i++) {
        j = i;

        // Insert V[i] into list 0..i-1
        while (j > 0 and V[j] < V[j - 1]) {

            // Swap V[j] and V[j-1]
            swap(V[j], V[j - 1]);

            // Decrement j by 1
            j -= 1;
        }
    }
}

// Driver Code
int main()
{
    Vector A = { 9, 8, 7, 5, 2, 1, 2, 3 };

    cout << "Array: " << endl;
    printVector(A);

    cout << "After Sorting :" << endl;
    insertionSort(A);
    printVector(A);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to sort
// an array by swapping elements
import java.io.*;
import java.util.*;

class GFG
{
    // Utility function to print a Vector
    static void printVector( Vector<Integer> V)
    {
    for (int i = 0; i < V.size(); i++) {
            System.out.print(V.get(i)+" ");

            }
            System.out.println();
    }

    // Function performs insertion sort on
    // vector V
    static void insertionSort(Vector<Integer> V)
    {
        int N = V.size();
        int i, j, key;

        for (i = 1; i < N; i++) {
            j = i;

            // Insert V[i] into list 0..i-1
            while (j > 0 && V.get(j) < V.get(j - 1)) {

                // Swap V[j] and V[j-1]
                int temp= V.get(j);
                V.set(j, V.get(j - 1));
                V.set(j - 1, temp);

                // Decrement j by 1
                j -= 1;
            }
        }
    }

    public static void main (String[] args)
    {
        Vector<Integer> A = new Vector<Integer> ();
        A.add(0, 9);
        A.add(1, 8);
        A.add(2, 7);
        A.add(3, 5);
        A.add(4, 2);
        A.add(5, 1);
        A.add(6, 2);
        A.add(7, 3);
        System.out.print("Array: ");
        printVector(A);
        System.out.print("After Sorting :");
        insertionSort(A);
        printVector(A);
    }
}

//This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Iterative python program to sort
# an array by swapping elements
import math

# Utility function to print a Vector
def printVector( V):

    for i in V:
        print(i ,end= " ")
    print (" ")

def insertionSort( V):

    N = len(V)

    for i in range(1,N):
    j = i

        # Insert V[i] into list 0..i-1
    while (j > 0 and V[j] < V[j - 1]) :

        # Swap V[j] and V[j-1]
        temp = V[j];
        V[j] = V[j - 1];
        V[j-1] = temp;

        # Decrement j
        j -= 1

# Driver method
A = [ 9, 8, 7, 5, 2, 1, 2, 3 ]
n = len(A)
print("Array")
printVector(A)
print( "After Sorting :")
insertionSort(A)
printVector(A)

# This code is contributed by Gitanjali.
```

## C#

```
// Iterative C# program to sort
// an array by swapping elements
using System;
using System.Collections.Generic;

class GFG
{
    // Utility function to print a Vector
    static void printVector(List<int> V)
    {
        for (int i = 0; i < V.Count; i++)
        {
            Console.Write(V[i] + " ");
        }
        Console.WriteLine();
    }

    // Function performs insertion sort on
    // vector V
    static void insertionSort(List<int> V)
    {
        int N = V.Count;
        int i, j;

        for (i = 1; i < N; i++)
        {
            j = i;

            // Insert V[i] into list 0..i-1
            while (j > 0 && V[j] < V[j - 1])
            {

                // Swap V[j] and V[j-1]
                int temp= V[j];
                V[j] = V[j - 1];
                V[j - 1] = temp;

                // Decrement j by 1
                j -= 1;
            }
        }
    }

    // Driver Code
    public static void Main (String[] args)
    {
        List<int> A = new List<int> ();
        A.Insert(0, 9);
        A.Insert(1, 8);
        A.Insert(2, 7);
        A.Insert(3, 5);
        A.Insert(4, 2);
        A.Insert(5, 1);
        A.Insert(6, 2);
        A.Insert(7, 3);
        Console.Write("Array: \n");
        printVector(A);
        Console.Write("After Sorting :\n");
        insertionSort(A);
        printVector(A);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Iterative Javascript program to sort
// an array by swapping elements

// Utility function to print a Vector
function printVector(V) {
    for (let e of V) {
        document.write(e + " ");
    }
    document.write("<br>");
}

// Function performs insertion sort on
// vector V
function insertionSort(V) {
    let N = V.length;
    let i, j, key;

    for (i = 1; i < N; i++) {
        j = i;

        // Insert V[i] into list 0..i-1
        while (j > 0 && V[j] < V[j - 1]) {

            // Swap V[j] and V[j-1]
            let temp = V[j];
            V[j] = V[j - 1];
            V[j - 1] = temp;
            // Decrement j by 1
            j -= 1;
        }
    }
}

// Driver Code
let A = [9, 8, 7, 5, 2, 1, 2, 3];

document.write("Array: " + "<br>");
printVector(A);

document.write("After Sorting :" + "<br>");
insertionSort(A);
printVector(A);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
Array: 
9 8 7 5 2 1 2 3 
After Sorting :
1 2 2 3 5 7 8 9 
```

**递归插入排序**

考虑大小为 N 的数组 A

*   首先递归排序大小为 N-1 的子列表
*   将 A 的最后一个元素插入到排序的子列表中。

要执行插入步骤，请使用如上所述的重复交换。
算法

```
function insertionSortRecursive(A, N)
    if N >= 1 
        insertionSortRecursive(A, N-1)
        j = N-1
        while j > 0 and A[j] < A[j-1]
            Swap A[j] and A[j-1]
            j = j-1
        [end of while]
    [end of if]
```

以下是上述方法的实施:

## C++

```
// Recursive CPP program to sort an array
// by swapping elements
#include <iostream>
#include <vector>

using namespace std;
using Vector = vector<int>;

// Utility function to print a Vector
void printVector(const Vector& V)
{
    for (auto e : V) {
        cout << e << " ";
    }
    cout << endl;
}

// Function to perform Insertion Sort recursively
void insertionSortRecursive(Vector& V, int N)
{
    if (N <= 1)
        return;

    // General Case
    // Sort V till second last element and
    // then insert last element into V
    insertionSortRecursive(V, N - 1);

    // Insertion step
    int j = N - 1;
    while (j > 0 and V[j] < V[j - 1]) {

        // Swap V[j] and V[j-1]
        swap(V[j], V[j - 1]);

        // Decrement j
        j -= 1;
    }
}

// Driver Code
int main()
{

    // Declare a vector of size 10
    Vector A = { 9, 8, 7, 5, 2, 1, 2, 3 };

    cout << "Array: " << endl;
    printVector(A);

    cout << "After Sorting :" << endl;
    insertionSortRecursive(A, A.size());
    printVector(A);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to sort
// an array by swapping elements
import java.io.*;
import java.util.*;

class GFG
{
    // Utility function to print a Vector
    static void printVector( Vector<Integer> V)
    {
    for (int i = 0; i < V.size(); i++) {
            System.out.print(V.get(i) + " ");

            }
            System.out.println();
    }

    // Function performs insertion sort on
    // vector V
    static void insertionSortRecursive(Vector<Integer> V,int N)
    {
        if (N <= 1)
            return;

        // General Case
        // Sort V till second last element and
        // then insert last element into V
        insertionSortRecursive(V, N - 1);

        // Insertion step
        int j = N - 1;

            // Insert V[i] into list 0..i-1
            while (j > 0 && V.get(j) < V.get(j - 1))
            {

                // Swap V[j] and V[j-1]
                int temp= V.get(j);
                V.set(j, V.get(j - 1));
                V.set(j - 1, temp);

                // Decrement j by 1
                j -= 1;
            }

    }

    // Driver code
    public static void main (String[] args)
    {
        Vector<Integer> A = new Vector<Integer> ();
        A.add(0, 9);
        A.add(1, 8);
        A.add(2, 7);
        A.add(3, 5);
        A.add(4, 2);
        A.add(5, 1);
        A.add(6, 2);
        A.add(7, 3);
        System.out.print("Array: ");
        printVector(A);
        System.out.print("After Sorting :");
        insertionSortRecursive(A,A.size());
        printVector(A);
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Recursive python program
# to sort an array
# by swapping elements
import math

# Utility function to print
# a Vector
def printVector( V):

    for i in V:
        print(i, end = " ")
    print (" ")

# Function to perform Insertion
# Sort recursively
def insertionSortRecursive(V, N):

    if (N <= 1):
        return 0

    # General Case
    # Sort V till second
    # last element and
    # then insert last element
    # into V
    insertionSortRecursive(V, N - 1)

    # Insertion step
    j = N - 1
    while (j > 0 and V[j] < V[j - 1]) :

        # Swap V[j] and V[j-1]
        temp = V[j];
        V[j] = V[j - 1];
        V[j-1] = temp;

        # Decrement j
        j -= 1

# Driver method
A = [ 9, 8, 7, 5, 2, 1, 2, 3 ]
n=len(A)
print("Array")
printVector(A)
print( "After Sorting :")

insertionSortRecursive(A,n)
printVector(A)

# This code is contributed
# by Gitanjali.
```

## C#

```
// Recursive C# program to sort
// an array by swapping elements
using System;
using System.Collections.Generic;

class GFG
{
    // Utility function to print a Vector
    static void printVector(List<int> V)
    {
        for (int i = 0; i < V.Count; i++)
        {
            Console.Write(V[i] + " ");
        }
        Console.WriteLine();
    }

    // Function performs insertion sort on
    // vector V
    static void insertionSortRecursive(List<int> V,
                                            int N)
    {
        if (N <= 1)
            return;

        // General Case
        // Sort V till second last element and
        // then insert last element into V
        insertionSortRecursive(V, N - 1);

        // Insertion step
        int j = N - 1;

        // Insert V[i] into list 0..i-1
        while (j > 0 && V[j] < V[j - 1])
        {

            // Swap V[j] and V[j-1]
            int temp = V[j];
            V[j] = V[j - 1];
            V[j - 1] = temp;

            // Decrement j by 1
            j -= 1;
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        List<int> A = new List<int> ();
        A.Insert(0, 9);
        A.Insert(1, 8);
        A.Insert(2, 7);
        A.Insert(3, 5);
        A.Insert(4, 2);
        A.Insert(5, 1);
        A.Insert(6, 2);
        A.Insert(7, 3);
        Console.Write("Array: ");
        printVector(A);
        Console.Write("After Sorting :");
        insertionSortRecursive(A, A.Count);
        printVector(A);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Recursive Javascript program to sort an array
// by swapping elements

// Utility function to print a Vector
function printVector(V) {
    for (let e of V) {
        document.write(e + " ");
    }
    document.write("<br>");
}

// Function to perform Insertion Sort recursively
function insertionSortRecursive(V, N) {
    if (N <= 1)
        return;

    // General Case
    // Sort V till second last element and
    // then insert last element into V
    insertionSortRecursive(V, N - 1);

    // Insertion step
    let j = N - 1;
    while (j > 0 && V[j] < V[j - 1]) {

        // Swap V[j] and V[j-1]
        let temp = V[j];
        V[j] = V[j - 1];
        V[j - 1] = temp;

        // Decrement j
        j -= 1;
    }
}

// Driver Code

// Declare a vector of size 10
let A = [9, 8, 7, 5, 2, 1, 2, 3];

document.write("Array: <br>");
printVector(A);

document.write("After Sorting :<br>");
insertionSortRecursive(A, A.length);
printVector(A);

// This code is contributed by gfgking.
</script>
```

**输出:**

```
Array: 
9 8 7 5 2 1 2 3 
After Sorting :
1 2 2 3 5 7 8 9 
```

**注**
算法的时间复杂度仍然是 O(N^2)最差的情况。此外，这些版本可能会更慢，因为重复交换需要更多的操作。然而，讨论这些版本是因为它们的实现简单且易于理解。
**参考**
[堆栈溢出–通过交换进行插入排序](https://stackoverflow.com/questions/40051083/insertion-sort-by-swapping)