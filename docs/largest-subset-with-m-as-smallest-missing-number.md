# 以 M 为最小缺失数的最大子集

> 原文:[https://www . geesforgeks . org/以 m 为最小缺失数的最大子集/](https://www.geeksforgeeks.org/largest-subset-with-m-as-smallest-missing-number/)

给定一个由 **N** 个正整数和一个正整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找出最长子集[的长度，其最小缺失整数](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)为 **M** 。如果不存在这样的子集，打印**-1”**。

**示例:**

> **输入:** arr[] = {1，2，4}，M = 3
> **输出:** 3
> **解释:**
> 给定数组的可能子集是{1}、{2}、{3}、{1，2}、{2，4}、{1，4}和{1，2，4}。
> 其中包含[1，M–1]范围内元素但不包含 M 的子集为{1，2}和{1，2，4}。
> 这些子集包含 3 作为最小缺失正整数。
> 因此，子集{1，2，4}是长度为 3 的最长必需子集。
> 
> **输入:** arr[] = {2，2，3}，M = 4
> **输出:** -1
> **解释:**
> 数组中最小的缺失正整数为 1。
> 因此，数组中所有可能的子集都将 1 作为最小的缺失正整数。
> 因此，不存在以 4 为最小缺失整数的子集。

**天真法:**最简单的方法是[生成给定数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，并在那些子集中存储最大长度，这些子集的 [**最小缺失整数**](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/) 为 m，最后打印最大长度作为答案。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**
要优化上述方法，请考虑以下观察结果。如果数组中没有小于 **M** 的元素缺失，则最大子集的大小为 1，由除 **M** 之外的所有数组元素组成。否则，不可能有最小缺失数 **M** 的子集。

请遵循以下步骤:

1.  将阵列中除 **M** 以外的所有元素插入到[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。
2.  [求数组**arr【】**中元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)(比如 **cnt** )的频率，不等于 **M** 。
3.  找到集合中**最小缺失数**，如果等于 **M** ，则打印 **cnt** 的值作为子集的最大尺寸。
4.  否则，打印**-1”**，因为最小缺失数为 **M** 的子集是不可能的。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find and return the
// length of the longest subset
// whose smallest missing value is M
ll findLengthOfMaxSubset(int arr[],
                        int n, int m)
{
    // Initialize a set
    set<int> s;

    int answer = 0;

    for (int i = 0; i < n; i++) {

        int tmp = arr[i];

        // If array element is not
        // equal to M
        if (tmp != m) {

            // Insert into set
            s.insert(tmp);

            // Increment frequency
            answer++;
        }
    }

    // Stores minimum missing
    // number
    int min = 1;

    // Iterate to find the
    // minimum missing
    // integer
    while (s.count(min)) {
        min++;
    }

    // If minimum obtained
    // is less than M
    if (min != m) {

        // Update answer
        answer = -1;
    }

    // Return answer
    return answer;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 3;

    cout << findLengthOfMaxSubset(
        arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find and return the
// length of the longest subset
// whose smallest missing value is M
static int findLengthOfMaxSubset(int arr[],
                                int n, int m)
{

    // Initialize a set
    Set<Integer> s = new HashSet<>();

    int answer = 0;

    for(int i = 0; i < n; i++)
    {
        int tmp = arr[i];

        // If array element is not
        // equal to M
        if (tmp != m)
        {

            // Insert into set
            s.add(tmp);

            // Increment frequency
            answer++;
        }
    }

    // Stores minimum missing
    // number
    int min = 1;

    // Iterate to find the
    // minimum missing
    // integer
    while (s.contains(min))
    {
        min++;
    }

    // If minimum obtained
    // is less than M
    if (min != m)
    {

        // Update answer
        answer = -1;
    }

    // Return answer
    return answer;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 4 };
    int N = arr.length;
    int M = 3;

    System.out.print(findLengthOfMaxSubset(
        arr, N, M));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find and return the
# length of the longest subset
# whose smallest missing value is M
def findLengthOfMaxSubset(arr, n, m):

    # Initialize a set
    s = [];

    answer = 0;

    for i in range(n):
        tmp = arr[i];

        # If array element is not
        # equal to M
        if (tmp != m):

            # Insert into set
            s.append(tmp);

            # Increment frequency
            answer += 1;

    # Stores minimum missing
    # number
    min = 1;

    # Iterate to find the
    # minimum missing
    # integer
    while (s.count(min)):
        min += 1;

    # If minimum obtained
    # is less than M
    if (min != m):

        # Update answer
        answer = -1;

    # Return answer
    return answer;

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 4 ];
    N = len(arr);
    M = 3;

    print(findLengthOfMaxSubset(arr, N, M));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find and return the
// length of the longest subset
// whose smallest missing value is M
static int findLengthOfMaxSubset(int []arr,
                                 int n, int m)
{

    // Initialize a set
    HashSet<int> s = new HashSet<int>();

    int answer = 0;

    for(int i = 0; i < n; i++)
    {
        int tmp = arr[i];

        // If array element is not
        // equal to M
        if (tmp != m)
        {

            // Insert into set
            s.Add(tmp);

            // Increment frequency
            answer++;
        }
    }

    // Stores minimum missing
    // number
    int min = 1;

    // Iterate to find the
    // minimum missing
    // integer
    while (s.Contains(min))
    {
        min++;
    }

    // If minimum obtained
    // is less than M
    if (min != m)
    {

        // Update answer
        answer = -1;
    }

    // Return answer
    return answer;
}

// Driver code
public static void Main (string[] args)
{
    int []arr = { 1, 2, 4 };
    int N = arr.Length;
    int M = 3;

    Console.Write(findLengthOfMaxSubset(arr, N, M));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find and return the
// length of the longest subset
// whose smallest missing value is M
function findLengthOfMaxSubset(arr, n, m)
{

    // Initialize a set
    let s = new Set();

    let answer = 0;

    for(let i = 0; i < n; i++)
    {
        let tmp = arr[i];

        // If array element is not
        // equal to M
        if (tmp != m)
        {

            // Insert into set
            s.add(tmp);

            // Increment frequency
            answer++;
        }
    }

    // Stores minimum missing
    // number
    let min = 1;

    // Iterate to find the
    // minimum missing
    // integer
    while (s.has(min))
    {
        min++;
    }

    // If minimum obtained
    // is less than M
    if (min != m)
    {

        // Update answer
        answer = -1;
    }

    // Return answer
    return answer;
}

// Driver code
let arr = [ 1, 2, 4 ];
let N = arr.length;
let M = 3;

document.write(findLengthOfMaxSubset(arr, N, M));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*