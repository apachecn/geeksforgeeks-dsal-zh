# 将阵列分割成最小数量的子集，每对之间的差异大于 1

> 原文:[https://www . geesforgeks . org/split-array-in-min-每对差异大于 1 的子集数/](https://www.geeksforgeeks.org/split-array-into-min-number-of-subsets-with-difference-between-each-pair-greater-than-1/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是将该数组拆分为**最小**数量的子集，使得每个子集中的每对元素的差值严格大于 1。
***注意:**数组中所有元素都是截然不同的。*

**示例:**

> **输入:** arr = {5，10，6，50}
> **输出:** 2
> **解释:**
> 可能的分区有:{5，10，50}，{6}
> 
> **输入:** arr = {2，4，6}
> **输出:** 1
> **解释:**
> 可能的分区有:{2，4，6}

**方法:**思路是观察如果没有这样的对 **i** 、 **j** 使得**| arr[I]–arr[j]| = 1**，那么就有可能把所有的元素放在同一个分区，否则就把它们分成两个分区。所以要求的最小分区数始终是 **1** 或 **2** 。

1.  [给定数组排序](https://www.geeksforgeeks.org/sorting-algorithms/)。
2.  比较相邻的元素。如果在任何一点上它们的差等于 1，那么打印**“2”**，因为所需的子集划分数将总是 2，因为我们可以将上述对中的一个元素放入另一个子集。
3.  如果我们遍历了所有数组，没有发现任何相邻的差异小于 2 的对，那么打印**“1”**而不将数组分成子集，我们可以使所有可能的对的差异至少为 2。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Split the array into
// minimum number of subsets with
// difference strictly > 1
void split(int arr[], int n)
{
    // Sort the array
    sort(arr, arr + n);
    int count = 1;

    // Traverse through the sorted array
    for (int i = 1; i < n; i++) {

        // Check the pairs of elements
        // with difference 1
        if (arr[i] - arr[i - 1] == 1) {

            // If we find even a single
            // pair with difference equal
            // to 1, then 2 partitions
            // else only 1 partition
            count = 2;
            break;
        }
    }

    // Print the count of partitions
    cout << count << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 4, 6 };

    // Size of the array
    int n = sizeof(arr) / sizeof(int);

    // Function Call
    split(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to split the array into
// minimum number of subsets with
// difference strictly > 1
static void split(int arr[], int n)
{

    // Sort the array
    Arrays.sort(arr);
    int count = 1;

    // Traverse through the sorted array
    for(int i = 1; i < n; i++)
    {

        // Check the pairs of elements
        // with difference 1
        if (arr[i] - arr[i - 1] == 1)
        {

            // If we find even a single
            // pair with difference equal
            // to 1, then 2 partitions
            // else only 1 partition
            count = 2;
            break;
        }
    }

    // Print the count of partitions
    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 4, 6 };

    // Size of the array
    int n = arr.length;

    // Function call
    split(arr, n);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to Split the array into
# minimum number of subsets with
# difference strictly > 1
def split(arr, n):

    # Sort the array
    arr.sort()
    count = 1

    # Traverse through the sorted array
    for i in range(1, n):

        # Check the pairs of elements
        # with difference 1
        if(arr[i] - arr[i - 1] == 1):

            # If we find even a single
            # pair with difference equal
            # to 1, then 2 partitions
            # else only 1 partition
            count = 2
            break

    # Print the count of partitions
    print(count)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 4, 6 ]

    # Size of the array
    n = len(arr)

    # Function call
    split(arr, n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to split the array into
// minimum number of subsets with
// difference strictly > 1
static void split(int []arr, int n)
{
    // Sort the array
    Array.Sort(arr);
    int count = 1;

    // Traverse through the sorted array
    for(int i = 1; i < n; i++)
    {

        // Check the pairs of elements
        // with difference 1
        if (arr[i] - arr[i - 1] == 1)
        {
            // If we find even a single
            // pair with difference equal
            // to 1, then 2 partitions
            // else only 1 partition
            count = 2;
            break;
        }
    }

    // Print the count of partitions
    Console.Write(count);
}

// Driver Code
public static void Main(string[] args)
{

    // Given array
    int[] arr = new int[]{ 2, 4, 6 };

    // Size of the array
    int n = arr.Length;

    // Function call
    split(arr, n);
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function to split the array into
// minimum number of subsets with
// difference strictly > 1
function split(arr, n)
{

    // Sort the array
    arr.sort();
    let count = 1;

    // Traverse through the sorted array
    for(let i = 1; i < n; i++)
    {

        // Check the pairs of elements
        // with difference 1
        if (arr[i] - arr[i - 1] == 1)
        {

            // If we find even a single
            // pair with difference equal
            // to 1, then 2 partitions
            // else only 1 partition
            count = 2;
            break;
        }
    }

    // Prlet the count of partitions
   document.write(count);
}

// Driver Code

   // Given array
    let arr = [ 2, 4, 6 ];

    // Size of the array
    let n = arr.length;

    // Function call
    split(arr, n);

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N log N)，其中 N 为数组长度。*
***辅助空间:** O(1)*