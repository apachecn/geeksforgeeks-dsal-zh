# 在数组所有可能排序对的有序列表中找到第 k 对

> 原文:[https://www . geesforgeks . org/find-the-kth-pair-in-ordered-list-of-all-seven-pair-of-the-array/](https://www.geeksforgeeks.org/find-the-kth-pair-in-ordered-list-of-all-possible-sorted-pairs-of-the-array/)

给定一个包含 **N** 整数和一个数字 **K** 的数组 **arr[]** ，任务是在数组 **arr[]** 的所有可能的 N <sup>2</sup> 排序对的有序列表中找到第 K 对。

> 仅当 **p1 ≤ p2** 和 **q1 < q2** 时，一对(p1，q1)在词典上小于另一对(p2，q2)。

**示例:**

> **输入:** arr[] = {2，1}，K = 4
> **输出:** {2，2}
> **解释:**
> 给定数组的排序顺序为{1，1}、{1，2}、{2，1}、{2，2}。所以第四对是 **{2，2}** 。
> **输入:** arr[] = {3，1，5}，K = 2
> **输出:** {1，3}

**方法:**自然，来自所有可能的对集合的第 K 个排序对将是 **{arr[K/N]，arr[K%N]}** 。但是，只有当数组中的所有元素都是唯一的时，此方法才有效。因此，遵循以下步骤来使数组表现得像一个唯一的数组:

*   让数组 arr[]为{X，X，X，… D <sub>1</sub> ，D <sub>2</sub> ，D<sub>3</sub>…D<sub>N–T</sub>}。
*   这里，让我们假设数组中重复元素的数量为 T，被重复的元素为 x。因此，数组中不同元素的数量为(N–T)。
*   现在，从 N <sup>2</sup> 对元素中的第一个 N * T 对开始，第一个 T <sup>2</sup> 元素将始终为{X，X}。
*   下一个 T 元素是{X，D <sub>2</sub> }，下一个 T 元素是{X，D <sub>2</sub> 等等。
*   所以，如果我们需要找到第 K 个元素，从 K 中减去 N * T，跳过前 T 个相同的元素。
*   重复上述过程，直到 K 变得小于 N * T
*   在这一步，对中的第一个元素将是计数器变量“I”。第二个元素是剩余元素中的第 K 个元素，也就是 K / T。所以，需要的答案是{arr[i]，arr[K/T]}。

下面是上述方法的实现:

## C++

```
// C++ program to find the K-th pair
// in a lexicographically sorted array

#include <bits/stdc++.h>
using namespace std;

// Function to find the k-th pair
void kthpair(int n, int k, int arr[])
{
    int i, t;

    // Sorting the array
    sort(arr, arr + n);

    --k;

    // Iterating through the array
    for (i = 0; i < n; i += t) {

        // Finding the number of same elements
        for (t = 1; arr[i] == arr[i + t]; ++t)
            ;

        // Checking if N*T is less than the
        // remaining K. If it is, then arr[i]
        // is the first element in the required
        // pair
        if (t * n > k)
            break;

        k = k - t * n;
    }

    // Printing the K-th pair
    cout << arr[i] << ' ' << arr[k / t];
}

// Driver code
int main()
{

    int n = 3, k = 2;
    int arr[n] = { 3, 1, 5 };
    kthpair(n, k, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the K-th pair
// in a lexicographically sorted array
import java.util.*;
class GFG{

// Function to find the k-th pair
static void kthpair(int n, int k,
                    int arr[])
{
    int i, t = 0;

    // Sorting the array
    Arrays.sort(arr);

    --k;

    // Iterating through the array
    for (i = 0; i < n; i += t)
    {

        // Finding the number of same elements
        for (t = 1; arr[i] == arr[i + t]; ++t)
            ;

        // Checking if N*T is less than the
        // remaining K. If it is, then arr[i]
        // is the first element in the required
        // pair
        if (t * n > k)
            break;

        k = k - t * n;
    }

    // Printing the K-th pair
    System.out.print(arr[i] + " " +    
                     arr[k / t]);
}

// Driver code
public static void main(String[] args)
{
    int n = 3, k = 2;
    int arr[] = { 3, 1, 5 };
    kthpair(n, k, arr);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the K-th pair
# in a lexicographically sorted array

# Function to find the k-th pair
def kthpair(n, k, arr):

    # Sorting the array
    arr.sort()
    k -= 1

    # Iterating through the array
    i = 0
    while (i < n):

        # Finding the number of same elements
        t = 1
        while (arr[i] == arr[i + t]):
            t += 1

        # Checking if N*T is less than the
        # remaining K. If it is, then arr[i]
        # is the first element in the required
        # pair
        if (t * n > k):
            break
        k = k - t * n

        i += t

    # Printing the K-th pair
    print(arr[i], " ", arr[k // t])

# Driver code
if __name__ == "__main__":

    n, k = 3, 2
    arr = [ 3, 1, 5 ]

    kthpair(n, k, arr)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the K-th pair
// in a lexicographically sorted array
using System;

class GFG{

// Function to find the k-th pair
static void kthpair(int n, int k,
                    int[] arr)
{
    int i, t = 0;

    // Sorting the array
    Array.Sort(arr);

    --k;

    // Iterating through the array
    for(i = 0; i < n; i += t)
    {

       // Finding the number of same elements
       for(t = 1; arr[i] == arr[i + t]; ++t);

          // Checking if N*T is less than the
          // remaining K. If it is, then arr[i]
          // is the first element in the required
          // pair
          if (t * n > k)
              break;
          k = k - t * n;
    }

    // Printing the K-th pair
    Console.Write(arr[i] + " " + arr[k / t]);
}

// Driver code
static public void Main ()
{
    int n = 3, k = 2;
    int[] arr = { 3, 1, 5 };

    kthpair(n, k, arr);
}
}

// This code is contributed by ShubhamCoder
```

## java 描述语言

```
<script>

// Java program to find the K-th pair
// in a lexicographically sorted array

// Function to find the k-th pair
function kthpair(n,k,arr)
{
    let i, t = 0;

    // Sorting the array
    arr.sort();

    --k;

    // Iterating through the array
    for (i = 0; i < n; i += t)
    {

        // Finding the number of same elements
        for (t = 1; arr[i] == arr[i + t]; ++t)
            ;

        // Checking if N*T is less than the
        // remaining K. If it is, then arr[i]
        // is the first element in the required
        // pair
        if (t * n > k)
            break;

        k = k - t * n;
    }

    // Printing the K-th pair
    document.write(arr[i] + " " +    
                     arr[k / t]);
}

// Driver code

    let n = 3, k = 2;
   let arr =[ 3, 1, 5 ];
    kthpair(n, k, arr);

//contributed by 171fa07058
</script>
```

**Output:** 

```
1 3
```

**时间复杂度:** *O(N * log(N))* ，其中 N 是数组的大小。

**辅助空间:** O(1)