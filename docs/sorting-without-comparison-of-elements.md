# 无要素对比排序

> 原文:[https://www . geeksforgeeks . org/无元素比较排序/](https://www.geeksforgeeks.org/sorting-without-comparison-of-elements/)

给定一个包含小范围整数元素的数组，对该数组进行排序。我们需要编写一个基于非比较的排序算法，并对输入做以下假设。

1.  数组中的所有条目都是整数。
2.  数组中最大值和最小值之间的差值小于或等于 10^6.

```
Input : arr[] = {10, 30, 20, 4}
Output : 4 10 20 30

Input : arr[] = {10, 30, 1, 20, 4}
Output : 1 4 10 20 30
```

我们不允许使用类似[快速排序](https://www.geeksforgeeks.org/quick-sort/)、[合并排序](https://www.geeksforgeeks.org/merge-sort/)等基于比较的排序算法。
由于元素很小，我们使用数组元素作为索引。我们在计数数组中存储元素计数。一旦我们有了计数数组，我们遍历计数数组并打印每个当前元素的计数次数。

## C++

```
// C++ program to sort an array without comparison
// operator.
#include <bits/stdc++.h>
using namespace std;

int sortArr(int arr[], int n, int min, int max)
{
    // Count of elements in given range
    int m = max - min + 1;

    // Count frequencies of all elements
    vector<int> c(m, 0);
    for (int i=0; i<n; i++)
       c[arr[i] - min]++;

    // Traverse through range. For every
    // element, print it its count times.
    for (int i=0; i<m; i++)
        for  (int j=0; j < c[i]; j++)
          cout << (i + min) << " ";
}

// Driver Code
int main()
{
    int arr[] =  {10, 10, 1, 4, 4, 100, 0};
    int min = 0, max = 100;
    int n = sizeof(arr)/sizeof(arr[0]);
    sortArr(arr, n, min, max);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array without comparison
// operator.
import java.util.*;

// Represents node of a doubly linked list
class Node
{

    static void sortArr(int arr[], int n, int min, int max)
    {
        // Count of elements in given range
        int m = max - min + 1;

        // Count frequencies of all elements
        int[] c = new int[m];
        for (int i = 0; i < n; i++)
        {
            c[arr[i] - min]++;
        }

        // Traverse through range. For every
        // element, print it its count times.
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < c[i]; j++)
            {
                System.out.print((i + min) + " ");
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {10, 10, 1, 4, 4, 100, 0};
        int min = 0, max = 100;
        int n = arr.length;
        sortArr(arr, n, min, max);
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to sort an array without comparison
# operator.

def sortArr(arr, n, min_no, max_no):
    # Count of elements in given range
    m = max_no - min_no + 1

    # Count frequencies of all elements
    c = [0] * m
    for i in range(n):
        c[arr[i] - min_no] += 1

    # Traverse through range. For every
    # element, print it its count times.
    for i in range(m):
        for j in range((c[i])):
            print((i + min_no), end=" ")

# Driver Code
arr = [10, 10, 1, 4, 4, 100, 0]
min_no,max_no = 0,100
n = len(arr)
sortArr(arr, n, min_no, max_no)

# This code is contributed by Rajput-Ji
# Improved by Rutvik J
```

## C#

```
// C# program to sort an array
// without comparison operator.
using System;

class GFG
{

    // Represents node of a doubly linked list
    static void sortArr(int []arr, int n,
                        int min, int max)
    {
        // Count of elements in given range
        int m = max - min + 1;

        // Count frequencies of all elements
        int[] c = new int[m];
        for (int i = 0; i < n; i++)
        {
            c[arr[i] - min]++;
        }

        // Traverse through range. For every
        // element, print it its count times.
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < c[i]; j++)
            {
                Console.Write((i + min) + " ");
            }
        }
    }

    // Driver Code
    static public void Main ()
    {
        int []arr = {10, 10, 1, 4, 4, 100, 0};
        int min = 0, max = 100;
        int n = arr.Length;
        sortArr(arr, n, min, max);
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

    // Javascript program to sort an array
    // without comparison operator.

    // Represents node of a doubly linked list
    function sortArr(arr, n, min, max)
    {
        // Count of elements in given range
        let m = max - min + 1;

        // Count frequencies of all elements
        let c = new Array(m);
        c.fill(0);
        for (let i = 0; i < n; i++)
        {
            c[arr[i] - min]++;
        }

        // Traverse through range. For every
        // element, print it its count times.
        for (let i = 0; i < m; i++)
        {
            for (let j = 0; j < c[i]; j++)
            {
                document.write((i + min) + " ");
            }
        }
    }

    let arr = [10, 10, 1, 4, 4, 100, 0];
    let min = 0, max = 100;
    let n = arr.length;
    sortArr(arr, n, min, max);

</script>
```

**Output**

```
0 1 4 4 10 10 100
```

**什么是时间复杂度？**
上述算法的时间复杂度为 O(n + (max-min))

**是以上算法** [**稳定**](https://www.geeksforgeeks.org/stable-selection-sort/) **吗？**
上面的实现并不稳定，因为我们在排序的时候并不关心相同元素的顺序。

**如何让以上算法稳定？**
上述算法的稳定版本叫做[计数排序](https://www.geeksforgeeks.org/counting-sort/)。在计数排序中，我们将所有较小或相等值的和存储在 c[i]中，以便 c[i]存储 I 在排序数组中的实际位置。填充 c[]后，我们再次遍历输入数组，将每个元素放在它的位置，并减少计数。

**什么是非基于比较的标准算法？**
[计数排序](https://www.geeksforgeeks.org/counting-sort/)[基数排序](https://www.geeksforgeeks.org/radix-sort/)和[桶排序](https://www.geeksforgeeks.org/bucket-sort-2/)。