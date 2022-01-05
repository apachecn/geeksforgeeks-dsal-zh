# 达到给定分数所需的最短时间

> 原文:[https://www . geesforgeks . org/达到给定分数所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-reach-a-given-score/)

给定一个整数**目标**和一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **arr[i]** 表示为第 **i** <sup>第</sup>数组元素评分 **1** 点所需的时间，任务是找到从给定数组中获取评分**目标**所需的最短时间。

**示例:**

> **输入:** arr[] = {1，3，3，4}，目标= 10
> **输出:** 6
> **解释:**
> 在时间瞬间，t = 1:数组的得分:{1，0，0，0}
> 在时间瞬间，t = 2:数组的得分:{2，0，0，0}
> 在时间瞬间，t = 3:数组的得分:{3，1，1，0}
> 在时间 1}
> 在时间瞬间，t = 5:数组的得分:{5，1，1，1}
> 在时间瞬间，t = 6:数组的得分:{6，2，2，1 }
> t = 5 后的数组总得分= 6 + 2 + 2 + 1 = 11 ( > 10)。 因此
> 
> **输入:** arr[] = {2，4，3}，目标= 20
> T3】输出: 20

**方法:**思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来[存储数组元素的频率](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)和[迭代 Hashmap](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) 并不断更新分数，直到达到**目标**。一个重要的观察是，任何元素， **arr[i]在任何时刻都会将 t / arr[i]** 添加到分数中 **t** 。按照以下步骤解决问题:

*   初始化一个变量，说**时间**，存储所需的最小时间，**将**与 **0** 相加，存储任意时刻的得分 **t** 。
*   将数组元素的[频率存储在散列表](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) **M** 中。
*   迭代直到**和**小于**目标**，执行以下步骤:
    *   将**总和**设置为 **0** ，并将**时间**的值增加 **1** 。
    *   现在，[遍历 hashmap](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) **M** ，在每次迭代中按**频率*(时间/值)**递增**和**的值。
*   完成以上步骤后，打印**时间**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum time
// required to achieve given score target
void findMinimumTime(int* p, int n,
                     int target)
{
    // Store the frequency of elements
    unordered_map<int, int> um;

    // Traverse the array p[]
    for (int i = 0; i < n; i++) {

        // Update the frequency
        um[p[i]]++;
    }

    // Stores the minimum time required
    int time = 0;

    // Store the current score
    // at any time instant t
    int sum = 0;

    // Iterate until sum is at
    // least equal to target
    while (sum < target) {

        sum = 0;

        // Increment time with
        // every iteration
        time++;

        // Traverse the map
        for (auto& it : um) {

            // Increment the points
            sum += it.second
                   * (time / it.first);
        }
    }

    // Print the time required
    cout << time;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int target = 10;

    // Function Call
    findMinimumTime(arr, N, target);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to calculate minimum time
// required to achieve given score target
static void findMinimumTime(int [] p, int n,
                            int target)
{

    // Store the frequency of elements
    HashMap<Integer,
            Integer> um = new HashMap<>();

    // Traverse the array p[]
    for(int i = 0; i < n; i++)
    {

        // Update the frequency
        if (!um.containsKey(p[i]))
            um.put(p[i], 1);
        else
            um.put(p[i],
            um.get(p[i]) + 1);
    }

    // Stores the minimum time required
    int time = 0;

    // Store the current score
    // at any time instant t
    int sum = 0;

    while (sum < target)
    {
        sum = 0;

        // Increment time with
        // every iteration
        time++;

        // Traverse the map
        for(Map.Entry<Integer,
                 Integer> it : um.entrySet())
        {

            // Increment the points
            sum += it.getValue() * (time / it.getKey());
        }
    }

    // Print the time required
    System.out.println(time);
}

// Driver Code
public static void main(String args[])
{
    int[] arr = { 1, 3, 3, 4 };
    int N = arr.length;
    int target = 10;

    // Function Call
    findMinimumTime(arr, N, target);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate minimum time
# required to achieve given score target
def findMinimumTime(p, n, target):

    # Store the frequency of elements
    um = {}

    # Traverse the array p[]
    for i in range(n):

        # Update the frequency
        um[p[i]] = um.get(p[i], 0) + 1

    # Stores the minimum time required
    time = 0

    # Store the current score
    # at any time instant t
    sum = 0

    # Iterate until sum is at
    # least equal to target
    while (sum < target):

        sum = 0

        # Increment time with
        # every iteration
        time += 1

        # Traverse the map
        for it in um:

            # Increment the points
            sum += um[it] * (time // it)

    # Print time required
    print(time)

# Driver Code
if __name__ == '__main__':
    arr = [1, 3, 3, 4]
    N = len(arr)
    target = 10

    # Function Call
    findMinimumTime(arr, N, target)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System.Collections.Generic;
using System;
using System.Linq;

class GFG{

// Function to calculate minimum time
// required to achieve given score target
static void findMinimumTime(int [] p, int n,
                            int target)
{

    // Store the frequency of elements
    Dictionary<int,
               int> um = new Dictionary<int,
                                        int>();

    // Traverse the array p[]
    for(int i = 0; i < n; i++)
    {

        // Update the frequency
        if (um.ContainsKey(p[i]) == true)
            um[p[i]] += 1;
        else
            um[p[i]] = 1;
    }

    // Stores the minimum time required
    int time = 0;

    // Store the current score
    // at any time instant t
    int sum = 0;

    // Iterate until sum is at
    // least equal to target
    var val = um.Keys.ToList();

    while (sum < target)
    {
        sum = 0;

        // Increment time with
        // every iteration
        time++;

        // Traverse the map
        foreach(var key in val)
        {

            // Increment the points
            sum += um[key] * (time / key);
        }
    }

    // Print the time required
    Console.WriteLine(time);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 3, 3, 4 };
    int N = arr.Length;
    int target = 10;

    // Function Call
    findMinimumTime(arr, N, target);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// Js program for the above approach
// Function to calculate minimum time
// required to achieve given score target
function findMinimumTime( p,  n,
                      target)
{
    // Store the frequency of elements
    let um = new Map();

    // Traverse the array p[]
    for (let i = 0; i < n; i++) {

        // Update the frequency
        if(um[p[i]])
        um[p[i]]++;
        else
        um[p[i]] = 1
    }

    // Stores the minimum time required
    let time = 0;

    // Store the current score
    // at any time instant t
    let sum = 0;

    // Iterate until sum is at
    // least equal to target
    while (sum < target) {

        sum = 0;

        // Increment time with
        // every iteration
        time++;

        // Traverse the map
        for (let it in um) {

            // Increment the points
            sum += um[it]
                   * Math.floor(time / it);
        }
    }

    // Print the time required
    document.write(time);
}

// Driver Code
let arr =  [1, 3, 3, 4];
    let N = arr.length;
    let target = 10;

    // Function Call
    findMinimumTime(arr, N, target);

// This code is contributed by rohitsingh07052.
</script>
```

**Output**

```
6
```

***时间复杂度:** O(目标*N)*
***辅助空间:** O(N)*