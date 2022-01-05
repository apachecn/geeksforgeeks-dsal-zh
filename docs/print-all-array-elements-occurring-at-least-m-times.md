# 打印所有出现至少 M 次的数组元素

> 原文:[https://www . geesforgeks . org/print-all-array-elements-occurrent-至少-m-times/](https://www.geeksforgeeks.org/print-all-array-elements-occurring-at-least-m-times/)

给定一个由 **N** 个整数和一个正整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出出现**至少 M** 次的数组元素的数量。

**示例:**

> **输入:** arr[] = {2，3，2，2，3，5，6，3}，M = 2
> **输出:** 2 3
> **说明:**
> 在给定数组 arr[]，出现次数至少为 M 次的元素为{2，3}。
> 
> **输入:** arr[] = { *1，32，2，1，33，5，1，5* }，M = 2
> T5】输出: 1 5

**天真方法:**解决问题最简单的方法如下:

*   从左到右遍历数组
*   检查一个元素是否已经出现在前面的遍历中。如果出现，检查下一个元素。否则再次从第**个**位置到第**(n–1)个**位置遍历数组。
*   如果频率是 **> = M** 。打印元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of array
// elements with frequency at least M
void printElements(int arr[], int N, int M)
{

    // Traverse the array
    for (int i = 0; i < N; i++) {

        int j;
        for (j = i - 1; j >= 0; j--) {
            if (arr[i] == arr[j])
                break;
        }

        // If the element appeared before
        if (j >= 0)
            continue;

        // Count frequency of the element
        int freq = 0;
        for (j = i; j < N; j++) {
            if (arr[j] == arr[i])
                freq++;
        }

        if (freq >= M)
            cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 2, 2, 3, 5, 6, 3 };
    int M = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    printElements(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the number of array
// elements with frequency at least M
static void printElements(int[] arr, int N, int M)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        int j;
        for(j = i - 1; j >= 0; j--)
        {
            if (arr[i] == arr[j])
                break;
        }

        // If the element appeared before
        if (j >= 0)
            continue;

        // Count frequency of the element
        int freq = 0;
        for(j = i; j < N; j++)
        {
            if (arr[j] == arr[i])
                freq++;
        }

        if (freq >= M)
            System.out.print(arr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 3, 2, 2, 3, 5, 6, 3 };
    int M = 2;
    int N = arr.length;

    printElements(arr, N, M);
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of array
# elements with frequency at least M
def printElements(arr, N, M):

    # Traverse the array
    for  i in range(N):
        j = i - 1

        while j >= 0:
            if (arr[i] == arr[j]):
                break

            j -= 1

        # If the element appeared before
        if (j >= 0):
            continue

        # Count frequency of the element
        freq = 0

        for j in range(i, N):
            if (arr[j] == arr[i]):
                freq += 1

        if (freq >= M):
            print(arr[i], end = " ")

# Driver Code
arr = [ 2, 3, 2, 2, 3, 5, 6, 3 ]
M = 2
N = len(arr)

printElements(arr, N, M)

# This code is contributed by rohitsingh07052
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number of array
// elements with frequency at least M
static void printElements(int[] arr, int N, int M)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        int j;
        for(j = i - 1; j >= 0; j--)
        {
            if (arr[i] == arr[j])
                break;
        }

        // If the element appeared before
        if (j >= 0)
            continue;

        // Count frequency of the element
        int freq = 0;
        for(j = i; j < N; j++)
        {
            if (arr[j] == arr[i])
                freq++;
        }

        if (freq >= M)
            Console.Write(arr[i] + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 3, 2, 2, 3, 5, 6, 3 };
    int M = 2;
    int N = arr.Length;

    printElements(arr, N, M);
}
}

// This code is contributed by subham348
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of array
// elements with frequency at least M
function printElements(arr, N, M)
{

    // Traverse the array
    for (let i = 0; i < N; i++) {

        let j;
        for (j = i - 1; j >= 0; j--) {
            if (arr[i] == arr[j])
                break;
        }

        // If the element appeared before
        if (j >= 0)
            continue;

        // Count frequency of the element
        let freq = 0;
        for (j = i; j < N; j++) {
            if (arr[j] == arr[i])
                freq++;
        }

        if (freq >= M)
            document.write(arr[i] + " ");
    }
}

// Driver Code
    let arr = [ 2, 3, 2, 2, 3, 5, 6, 3 ];
    let M = 2;
    let N = arr.length;

    printElements(arr, N, M);

 // This code is contributed by subham348.
</script>
```

**Output**

```
2 3 
```

**方法:**给定的问题可以通过[将数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率存储在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中，比如说 **M** ，将频率为**的地图中所有元素至少打印 M** 来解决。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of array
// elements with frequency at least M
void printElements(int arr[], int N, int M)
{
    // Stores the frequency of each
    // array elements
    unordered_map<int, int> freq;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of
        // current array element
        freq[arr[i]]++;
    }

    // Traverse the map and print array
    // elements occurring at least M times
    for (auto it : freq) {

        if (it.second >= M) {
            cout << it.first << " ";
        }
    }

    return;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 2, 2,
                  3, 5, 6, 3 };
    int M = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    printElements(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG
{

  // Function to find the number of array
  // elements with frequency at least M
  static void printElements(int arr[], int N, int M)
  {

    // Stores the frequency of each
    // array elements
    HashMap<Integer, Integer> freq = new HashMap<>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Update frequency of
      // current array element
      freq.put(arr[i],
               freq.getOrDefault(arr[i], 0) + 1);
    }

    // Traverse the map and print array
    // elements occurring at least M times
    for (int key : freq.keySet())
    {

      if (freq.get(key) >= M) {
        System.out.print(key + " ");
      }
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 2, 3, 2, 2, 3, 5, 6, 3 };
    int M = 2;
    int N = arr.length;

    printElements(arr, N, M);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of array
# elements with frequency at least M
def printElements(arr, N, M):

    # Stores the frequency of each
    # array elements
    freq = {}

    # Traverse the array
    for i in arr:

        # Update frequency of
        # current array element
        freq[i] = freq.get(i, 0) + 1

    # Traverse the map and prarray
    # elements occurring at least M times
    for it in freq:

        if (freq[it] >= M):
            print(it, end = " ")

    return

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 2, 2, 3, 5, 6, 3]
    M = 2
    N = len(arr)

    printElements(arr, N, M)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the number of array
// elements with frequency at least M
static void printElements(int []arr, int N, int M)
{

    // Stores the frequency of each
    // array elements
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency of
        // current array element
        if (freq.ContainsKey(arr[i]))
            freq[arr[i]] += 1;
        else
            freq[arr[i]] = 1;
    }

    // Traverse the map and print array
    // elements occurring at least M times
    foreach(var item in freq)
    {
        if (item.Value >= M)
        {
            Console.Write(item.Key + " ");
        }
    }

    return;
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 3, 2, 2,
                  3, 5, 6, 3 };
    int M = 2;
    int N = arr.Length;

    printElements(arr, N, M);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of array
// elements with frequency at least M
function printElements(arr, N, M) {
    // Stores the frequency of each
    // array elements
    let freq = new Map();

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // Update frequency of
        // current array element
        freq[arr[i]]++;
        if (freq.has(arr[i])) {
            freq.set(arr[i], freq.get(arr[i]) + 1)
        } else {
            freq.set(arr[i], 1)
        }
    }

    // Traverse the map and print array
    // elements occurring at least M times
    for (let it of freq) {

        if (it[1] >= M) {
            document.write(it[0] + " ");
        }
    }

    return;
}

// Driver Code

let arr = [2, 3, 2, 2,
    3, 5, 6, 3];
let M = 2;
let N = arr.length;

printElements(arr, N, M);

// This code is contributed by gfgking.
</script>
```

**Output**

```
2 3 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

#### 方法 2:使用内置的 python 函数:

*   使用 [**【计数器()**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能计算每个元素的频率
*   遍历频率数组并打印至少出现 m 次的所有元素。

下面是实现:

## 蟒蛇 3

```
# Python3 implementation
from collections import Counter

# Function to find the number of array
# elements with frequency at least M
def printElements(arr, M):

    # Counting frequency of every element using Counter
    mp = Counter(arr)

    # Traverse the map and print all
    # the elements with occurrence atleast m times
    for it in mp:
        if mp[it] >= M:
            print(it, end=" ")

# Driver code
arr = [2, 3, 2, 2, 3, 5, 6, 3]
M = 2

printElements(arr, M)

# This code is contributed by vikkycirus
```

**Output**

```
2 3 
```

**时间复杂度:** O(N)

**辅助空间:** O(N)