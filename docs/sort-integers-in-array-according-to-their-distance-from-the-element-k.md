# 根据整数与元素 K 的距离对数组中的整数进行排序

> 原文:[https://www . geesforgeks . org/sort-integers-in-array-根据它们与元素的距离-k/](https://www.geeksforgeeks.org/sort-integers-in-array-according-to-their-distance-from-the-element-k/)

给定一个由 N 个整数组成的**数组 arr[]** 和一个**整数 K** ，任务是根据这些整数与给定整数 **K** 的距离对它们进行排序。如果超过 **1** 元素处于相同距离，则按递增顺序打印。
**注**:数组中两个元素之间的距离是以它们的指数之差来度量的。
***注:**整数 K 始终出现在数组 **arr[]** 中，并且是**唯一的**。*

**示例:**

> **输入:** arr[] = {12，10，102，31，15}，K = 102
> **输出:** 102 10 31 12 15
> **解释:**
> 元素在它们各自与 K 的距离为，距离为 0: 102 的
> 距离为 1: 10 的
> ，31 以排序形式出现。
> 距离 2: 12，15 以排序形式。
> 因此，我们得到的数组是[ 102，10，31，12，15 ]
> 
> **输入:** arr[] = {14，1101，10，35，0}，K = 35
> **输出:** 35 0 10 1101 14
> **解释:**
> 元素与 K 的距离分别为，
> 距离为 0: 35
> 距离为 1: 10，0，在排序形式中我们有 0，10。
> 在距离 2: 1101 处
> 在距离 3: 14 处
> 因此，我们得到的数组是【35，0，10，1101，14】

**方法:**
为了解决上述问题，我们创建了一个辅助向量来存储距离 K 任意距离的元素，然后找到数组 arr[]中给定整数 K 的位置，并将元素 K 插入辅助向量中的位置 0。从 K 开始沿左侧方向遍历数组，并在距离 K 的向量中插入这些元素。对 K 的右侧元素重复上述过程。最后，按排序顺序打印距离 0 的数组元素。

下面是上述方法的实现:

## C++

```
// C++ implementation to Sort the integers in
// array according to their distance from given
// element K present in the array
#include <bits/stdc++.h>
using namespace std;

// Function to get sorted array based on
// their distance from given integer K
void distanceSort(int arr[], int K, int n)
{
    // Vector to store respective elements
    // with their distance from integer K
    vector<int> vd[n];

    // Find the position of integer K
    int pos;

    for (int i = 0; i < n; i++) {
        if (arr[i] == K) {
            pos = i;
            break;
        }
    }

    // Insert the elements with their
    // distance from K in vector

    int i = pos - 1, j = pos + 1;

    // Element at distance 0
    vd[0].push_back(arr[pos]);

    // Elements at left side of K
    while (i >= 0) {
        vd[pos - i].push_back(arr[i]);
        --i;
    }

    // Elements at right side of K
    while (j < n) {
        vd[j - pos].push_back(arr[j]);
        ++j;
    }

    // Print the vector content in sorted order
    for (int i = 0; i <= max(pos, n - pos - 1); ++i) {

        // Sort elements at same distance
        sort(begin(vd[i]), end(vd[i]));

        // Print elements at distance i from K
        for (auto element : vd[i])
            cout << element << " ";
    }
}

// Driver code
int main()
{
    int arr[] = {14, 1101, 10, 35, 0 }, K = 35;

    int n = sizeof(arr) / sizeof(arr[0]);

    distanceSort(arr, K, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Sort the integers in
// array according to their distance from given
// element K present in the array
import java.util.*;

class GFG{

// Function to get sorted array based on
// their distance from given integer K
@SuppressWarnings("unchecked")
static void distanceSort(int arr[], int K, int n)
{

    // Vector to store respective elements
    // with their distance from integer K
    Vector vd[] = new Vector[n];

    for(int i = 0; i < n; i++)
    {
        vd[i] = new Vector();
    }

    // Find the position of integer K
    int pos = 0;

    for(int i = 0; i < n; i++)
    {
        if (arr[i] == K)
        {
            pos = i;
            break;
        }
    }

    // Insert the elements with their
    // distance from K in vector
    int i = pos - 1, j = pos + 1;

    // Element at distance 0
    vd[0].add(arr[pos]);

    // Elements at left side of K
    while (i >= 0)
    {
        vd[pos - i].add(arr[i]);
        --i;
    }

    // Elements at right side of K
    while (j < n)
    {
        vd[j - pos].add(arr[j]);
        ++j;
    }

    // Print the vector content in sorted order
    for(i = 0; i <= Math.max(pos, n - pos - 1); ++i)
    {

        // Sort elements at same distance
        Collections.sort(vd[i]);

        // Print elements at distance i from K
        for (j = 0; j < vd[i].size(); j++)
        {
            int element = (int)vd[i].get(j);
            System.out.print(element + " ");
        }
    }
}

// Driver Code
public static void main(String s[])
{
    int arr[] = {14, 1101, 10, 35, 0 };
    int K = 35;

    int n = arr.length;

    distanceSort(arr, K, n);
}   
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation to Sort the integers in
# array according to their distance from given
# element K present in the array

# Function to get sorted array based on
# their distance from given integer K
def distanceSort(arr,K,n):
    # Vector to store respective elements
    # with their distance from integer K
    vd = [[] for i in range(n)]

    # Find the position of integer K

    for i in range(n):
        if (arr[i] == K):
            pos = i
            break

    # Insert the elements with their
    # distance from K in vector

    i = pos - 1
    j = pos + 1

    # Element at distance 0
    vd[0].append(arr[pos])

    # Elements at left side of K
    while (i >= 0):
        vd[pos - i].append(arr[i])
        i -= 1

    # Elements at right side of K
    while (j < n):
        vd[j - pos].append(arr[j])
        j += 1

    # Print the vector content in sorted order
    for i in range(max(pos, n - pos - 1) + 1):

        # Sort elements at same distance
        vd[i].sort(reverse=False)

        # Print elements at distance i from K
        for element in vd[i]:
            print(element,end = " ")

# Driver code
if __name__ == '__main__':
    arr =  [14, 1101, 10, 35, 0]
    K = 35

    n = len(arr)

    distanceSort(arr, K, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to Sort the integers in
// array according to their distance from given
// element K present in the array
using System;
using System.Collections.Generic;
class GFG{

// Function to get sorted array based on
// their distance from given integer K
static void distanceSort(int []arr,
                         int K, int n)
{   
    // List to store respective elements
    // with their distance from integer K
    List<int> []vd = new List<int>[n];
    int i ;
    for(i = 0; i < n; i++)
    {
        vd[i] = new List<int>();
    }

    // Find the position of integer K
    int pos = 0;

    for(i = 0; i < n; i++)
    {
        if (arr[i] == K)
        {
            pos = i;
            break;
        }
    }

    // Insert the elements with their
    // distance from K in vector
    int j = pos + 1;
     i = pos - 1;

    // Element at distance 0
    vd[0].Add(arr[pos]);

    // Elements at left side of K
    while (i >= 0)
    {
        vd[pos - i].Add(arr[i]);
        --i;
    }

    // Elements at right side of K
    while (j < n)
    {
        vd[j - pos].Add(arr[j]);
        ++j;
    }

    // Print the vector content in sorted order
    for(i = 0; i <= Math.Max(pos,
                             n - pos - 1); ++i)
    {       
        // Sort elements at same distance
        vd[i].Sort();

        // Print elements at distance i from K
        for (j = 0; j < vd[i].Count; j++)
        {
            int element = (int)vd[i][j];
            Console.Write(element + " ");
        }
    }
}

// Driver Code
public static void Main(String []args)
{
    int []arr = {14, 1101, 10, 35, 0};
    int K = 35;
    int n = arr.Length;
    distanceSort(arr, K, n);
}   
}

// This code is contributed by shikhasingrajput
```

**Output:** 

```
35 0 10 1101 14
```

**时间复杂度:** O(N)

**辅助空间:** O(N)