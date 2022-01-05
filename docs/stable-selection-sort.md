# 稳定选择排序

> 原文:[https://www.geeksforgeeks.org/stable-selection-sort/](https://www.geeksforgeeks.org/stable-selection-sort/)

如果两个键相等或相同的对象在排序输出中出现的顺序与它们在要排序的输入数组中出现的顺序相同，则排序算法被称为[稳定](https://www.geeksforgeeks.org/stability-in-sorting-algorithms/)。
任何本质上不稳定的基于比较的排序算法都可以修改为稳定的，方法是更改键比较操作，以便两个键的比较将位置视为具有相同键的对象的一个因素，或者对其进行调整，使其含义不变并变得稳定。
**例:**

```
Note: Subscripts are only used for understanding the concept.

Input : 4A 5 3 2 4B 1
Output : 1 2 3 4B 4A 5

Stable Selection Sort would have produced
Output : 1 2 3 4A 4B 5
```

[选择排序](https://www.geeksforgeeks.org/selection-sort/)的工作原理是找到最小元素，然后通过与位于该最小元素位置的元素进行交换，将其插入到正确的位置。这就是它不稳定的原因。
交换可能会影响将一个键(比如说 A)推到一个比相等键(比如说 B)更大的位置。这使得它们不符合期望的顺序。
在上面的例子 4 中 <sub>A</sub> 在 4 <sub>B</sub> 之后被推动，并且在完成分类之后，该 4 <sub>A</sub> 保留在该 4 <sub>B</sub> 之后。因此导致不稳定。
如果不是交换，而是将最小元素放在它的位置而不交换，即通过将每个元素向前推一步将数字放在它的位置，选择排序可以变得稳定。
简单来说，使用类似[插入排序](https://www.geeksforgeeks.org/insertion-sort/)的技术，这意味着在正确的位置插入元素。
举例说明:

```
Example: 4<sub>A 5 3 2 4B 1</sub>
         First minimum element is 1, now instead
         of swapping. Insert 1 in its correct place 
         and pushing every element one step forward
         i.e forward pushing.
         1 4<sub>A 5 3 2 4B</sub>
         Next minimum is 2 :
         1 2 4<sub>A 5 3 4B</sub>
         Next minimum is 3 :
         1 2 3 4<sub>A 5 4B</sub>
         Repeat the steps until array is sorted.
         1 2 3 4<sub>A 4B 5</sub>
```

## C++

```
// C++ program for modifying Selection Sort
// so that it becomes stable.
#include <iostream>
using namespace std;

void stableSelectionSort(int a[], int n)
{
    // Iterate through array elements
    for (int i = 0; i < n - 1; i++)
    {

        // Loop invariant : Elements till a[i - 1]
        // are already sorted.

        // Find minimum element from
        // arr[i] to arr[n - 1].
        int min = i;
        for (int j = i + 1; j < n; j++)
            if (a[min] > a[j])
                min = j;

        // Move minimum element at current i.
        int key = a[min];
        while (min > i)
        {
            a[min] = a[min - 1];
            min--;
        }
        a[i] = key;
    }
}

void printArray(int a[], int n)
{
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;
}

// Driver code
int main()
{
    int a[] = { 4, 5, 3, 2, 4, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    stableSelectionSort(a, n);
    printArray(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for modifying Selection Sort
// so that it becomes stable.
class GFG
{
    static void stableSelectionSort(int[] a, int n)
    {
        // Iterate through array elements
        for (int i = 0; i < n - 1; i++)
        {

            // Loop invariant : Elements till
            // a[i - 1] are already sorted.

            // Find minimum element from
            // arr[i] to arr[n - 1].
            int min = i;
            for (int j = i + 1; j < n; j++)
                if (a[min] > a[j])
                    min = j;

            // Move minimum element at current i.
            int key = a[min];
            while (min > i)
            {
                a[min] = a[min - 1];
                min--;
            }

            a[i] = key;
        }
    }

    static void printArray(int[] a, int n)
    {
        for (int i = 0; i < n; i++)
        System.out.print(a[i]+ " ");

        System.out.println();
    }

    // Driver code
    public static void main (String[] args)
    {
        int[] a = { 4, 5, 3, 2, 4, 1 };
        int n = a.length;
        stableSelectionSort(a, n);
        printArray(a, n);
    }
}

// This code is contributed by Mr. Somesh Awasthi
```

## 蟒蛇 3

```
# Python3 program for modifying Selection Sort
# so that it becomes stable.
def stableSelectionSort(a, n):

    # Traverse through all array elements
    for i in range(n):

        # Find the minimum element in remaining
        # unsorted array
        min_idx = i
        for j in range(i + 1, n):
            if a[min_idx] > a[j]:
                min_idx = j

        # Move minimum element at current i
        key = a[min_idx]
        while min_idx > i:
            a[min_idx] = a[min_idx - 1]
            min_idx -= 1
        a[i] = key

def printArray(a, n):
    for i in range(n):
        print("%d" %a[i], end = " ")

# Driver Code
a = [4, 5, 3, 2, 4, 1]
n = len(a)
stableSelectionSort(a, n)
printArray(a, n)

# This code is contributed
# by Mr. Raju Pitta
```

## C#

```
// C# program for modifying Selection Sort
// so that it becomes stable.
using System;

class GFG
{
    static void stableSelectionSort(int[] a, int n)
    {
        // Iterate through array elements
        for (int i = 0; i < n - 1; i++)
        {

            // Loop invariant : Elements till
            // a[i - 1] are already sorted.

            // Find minimum element from
            // arr[i] to arr[n - 1].
            int min = i;
            for (int j = i + 1; j < n; j++)
                if (a[min] > a[j])
                    min = j;

            // Move minimum element at current i.
            int key = a[min];
            while (min > i)
            {
                a[min] = a[min - 1];
                min--;
            }

            a[i] = key;
        }
    }

    static void printArray(int[] a, int n)
    {
        for (int i = 0; i < n; i++)
        Console.Write(a[i] + " ");

        Console.WriteLine();
    }

    // Driver code
    public static void Main ()
    {
        int[] a = { 4, 5, 3, 2, 4, 1 };
        int n = a.Length;
        stableSelectionSort(a, n);
        printArray(a, n);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
// Javascript program for modifying Selection Sort
// so that it becomes stable.

   function stableSelectionSort(a, n)
    {
        // Iterate through array elements
        for (let i = 0; i < n - 1; i++)
        {

            // Loop invariant : Elements till
            // a[i - 1] are already sorted.

            // Find minimum element from
            // arr[i] to arr[n - 1].
            let min = i;
            for (let j = i + 1; j < n; j++)
                if (a[min] > a[j])
                    min = j;

            // Move minimum element at current i.
            let key = a[min];
            while (min > i)
            {
                a[min] = a[min - 1];
                min--;
            }

            a[i] = key;
        }
    }

    function prletArray(a, n)
    {
        for (let i = 0; i < n; i++)
        document.write(a[i]+ " ");

        document.write("<br/>");
    }

// driver function

        let a = [ 4, 5, 3, 2, 4, 1 ];
        let n = a.length;
        stableSelectionSort(a, n);
        prletArray(a, n);

</script>
```

输出:

```
1 2 3 4 4 5
```

本文由**舒巴姆拉纳**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。