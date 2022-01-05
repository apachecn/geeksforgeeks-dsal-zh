# 生成排列的堆算法

> 原文:[https://www . geeksforgeeks . org/heaps-生成排列的算法/](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)

**堆的算法**用于生成 n 个对象的所有排列。其思想是通过选择一对要交换的元素从先前的排列生成每个排列，而不干扰其他 **n-2** 元素。
以下是生成 n 个给定数字的所有排列的图示。
**例:**

```
Input: 1 2 3
Output: 1 2 3
        2 1 3
        3 1 2
        1 3 2
        2 3 1
        3 2 1
```

**算法:**

1.  算法生成(n-1)！前 n-1 个元素的排列，将最后一个元素与每个元素相邻。这将生成以最后一个元素结束的所有排列。
2.  如果 n 是奇数，交换第一个和最后一个元素，如果 n 是偶数，交换第 i <sup>个</sup>元素(I 是从 0 开始的计数器)和最后一个元素，重复上述算法，直到 I 小于 n。
3.  在每次迭代中，算法将产生以当前最后一个元素结束的所有排列。

**实施:**

## C++

```
// C++ program to print all permutations using
// Heap's algorithm
#include <bits/stdc++.h>
using namespace std;

// Prints the array
void printArr(int a[], int n)
{
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    printf("\n");
}

// Generating permutation using Heap Algorithm
void heapPermutation(int a[], int size, int n)
{
    // if size becomes 1 then prints the obtained
    // permutation
    if (size == 1) {
        printArr(a, n);
        return;
    }

    for (int i = 0; i < size; i++) {
        heapPermutation(a, size - 1, n);

        // if size is odd, swap 0th i.e (first) and
        // (size-1)th i.e (last) element
        if (size % 2 == 1)
            swap(a[0], a[size - 1]);

        // If size is even, swap ith and
        // (size-1)th i.e (last) element
        else
            swap(a[i], a[size - 1]);
    }
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3 };
    int n = sizeof a / sizeof a[0];
    heapPermutation(a, n, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all permutations using
// Heap's algorithm
class HeapAlgo {
    // Prints the array
    void printArr(int a[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(a[i] + " ");
        System.out.println();
    }

    // Generating permutation using Heap Algorithm
    void heapPermutation(int a[], int size, int n)
    {
        // if size becomes 1 then prints the obtained
        // permutation
        if (size == 1)
            printArr(a, n);

        for (int i = 0; i < size; i++) {
            heapPermutation(a, size - 1, n);

            // if size is odd, swap 0th i.e (first) and
            // (size-1)th i.e (last) element
            if (size % 2 == 1) {
                int temp = a[0];
                a[0] = a[size - 1];
                a[size - 1] = temp;
            }

            // If size is even, swap ith
            // and (size-1)th i.e last element
            else {
                int temp = a[i];
                a[i] = a[size - 1];
                a[size - 1] = temp;
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        HeapAlgo obj = new HeapAlgo();
        int a[] = { 1, 2, 3 };
        obj.heapPermutation(a, a.length, a.length);
    }
}

// This code has been contributed by Amit Khandelwal.
```

## 蟒蛇 3

```
# Python program to print all permutations using
# Heap's algorithm

# Generating permutation using Heap Algorithm
def heapPermutation(a, size):

    # if size becomes 1 then prints the obtained
    # permutation
    if size == 1:
        print(a)
        return

    for i in range(size):
        heapPermutation(a, size-1)

        # if size is odd, swap 0th i.e (first)
        # and (size-1)th i.e (last) element
        # else If size is even, swap ith
        # and (size-1)th i.e (last) element
        if size & 1:
            a[0], a[size-1] = a[size-1], a[0]
        else:
            a[i], a[size-1] = a[size-1], a[i]

# Driver code
a = [1, 2, 3]
n = len(a)
heapPermutation(a, n)

# This code is contributed by ankush_953
# This code was cleaned up to by more pythonic by glubs9
```

## C#

```
// C# program to print all permutations using
// Heap's algorithm
using System;

public class GFG {
    // Prints the array
    static void printArr(int[] a, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(a[i] + " ");
        Console.WriteLine();
    }

    // Generating permutation using Heap Algorithm
    static void heapPermutation(int[] a, int size, int n)
    {
        // if size becomes 1 then prints the obtained
        // permutation
        if (size == 1)
            printArr(a, n);

        for (int i = 0; i < size; i++) {
            heapPermutation(a, size - 1, n);

            // if size is odd, swap 0th i.e (first) and
            // (size-1)th i.e (last) element
            if (size % 2 == 1) {
                int temp = a[0];
                a[0] = a[size - 1];
                a[size - 1] = temp;
            }

            // If size is even, swap ith and
            // (size-1)th i.e (last) element
            else {
                int temp = a[i];
                a[i] = a[size - 1];
                a[size - 1] = temp;
            }
        }
    }

    // Driver code
    public static void Main()
    {

        int[] a = { 1, 2, 3 };
        heapPermutation(a, a.Length, a.Length);
    }
}

/* This Java code is contributed by 29AjayKumar*/
```

## java 描述语言

```
<script>

// JavaScript program to print all permutations using
// Heap's algorithm

// Prints the array
function printArr(a,n)
{
    document.write(a.join(" ")+"<br>");

}

// Generating permutation using Heap Algorithm
function heapPermutation(a,size,n)
{
        // if size becomes 1 then prints the obtained
        // permutation
        if (size == 1)
            printArr(a, n);

        for (let i = 0; i < size; i++) {
            heapPermutation(a, size - 1, n);

            // if size is odd, swap 0th i.e (first) and
            // (size-1)th i.e (last) element
            if (size % 2 == 1) {
                let temp = a[0];
                a[0] = a[size - 1];
                a[size - 1] = temp;
            }

            // If size is even, swap ith
            // and (size-1)th i.e last element
            else {
                let temp = a[i];
                a[i] = a[size - 1];
                a[size - 1] = temp;
            }
        }
}

// Driver code
let a=[1, 2, 3];
heapPermutation(a, a.length, a.length);

// This code is contributed by rag2127

</script>
```

**输出:**

```
1 2 3
2 1 3
3 1 2
1 3 2
2 3 1
3 2 1
```

**参考文献:**
1。[【https://en . Wikipedia . org/wiki/Heap % 27s _ algorithm # cite _ note-3](https://en.wikipedia.org/wiki/Heap%27s_algorithm#cite_note-3)
本文由 **Rahul Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。