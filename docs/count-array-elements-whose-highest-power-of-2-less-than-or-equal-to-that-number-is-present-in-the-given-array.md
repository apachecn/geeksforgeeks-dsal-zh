# 对给定数组中最高 2 次幂小于或等于该数的数组元素进行计数

> 原文:[https://www . geesforgeks . org/count-array-elements-其最高 2 次方小于或等于给定数组中存在的数字/](https://www.geeksforgeeks.org/count-array-elements-whose-highest-power-of-2-less-than-or-equal-to-that-number-is-present-in-the-given-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出数组元素的数量，其[的最高 2 次幂小于或等于数组](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)中存在的数量。

**示例:**

> **输入:** arr[] = {3，4，6，9}
> **输出:** 2
> **说明:**
> 数组中存在 2 个数组元素(4 和 6)，其 2 的最高幂小于它(即 4)。
> 
> **输入:** arr[] = {3，9，10，8，1 }
> T3】输出: 3

**天真方法:**给定的问题可以通过计算给定数组中[的最高幂为 2](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/) 的元素来解决，并且可以通过[再次遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)来找到这些元素。检查所有元素后，打印获得的总计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)来保持访问元素的计数并相应地更新结果元素的计数来优化。按照以下步骤解决给定的问题:

*   初始化一个变量，比如**计数**，它存储数组中最高[次幂 2](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 小于或等于[次幂的元素的计数。](https://www.geeksforgeeks.org/check-if-a-value-is-present-in-an-array-in-java/)
*   初始化一张[图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **M** ，存储数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，如果地图中存在不超过该元素的**arr【I】**的 2 的最高[次幂的频率，则将**计数**的值增加 **1。**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)
*   完成上述步骤后，打印**计数**的值作为元素的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count array elements
// whose highest power of 2 is less
// than or equal to that number is
// present in the given array
int countElement(int arr[], int N)
{
    // Stores the resultant count
    // of array elements
    int count = 0;

    // Stores frequency of
    // visited array elements
    unordered_map<int, int> m;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        m[arr[i]]++;
    }

    for (int i = 0; i < N; i++) {

        // Calculate log base 2
        // of the element arr[i]
        int lg = log2(arr[i]);

        // Highest power of 2 whose
        // value is at most arr[i]
        int p = pow(2, lg);

        // Increment the count by 1
        if (m[p]) {
            count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 3, 4, 6, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countElement(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;
import java.io.*;

class GFG{

static int log2(int N)
{

    // Calculate log2 N indirectly
    // using log() method
    int result = (int)(Math.log(N) /
                       Math.log(2));

    return result;
}

// Function to count array elements
// whose highest power of 2 is less
// than or equal to that number is
// present in the given array
static int countElement(int arr[], int N)
{

    // Stores the resultant count
    // of array elements
    int count = 0;

    // Stores frequency of
    // visited array elements
   HashMap<Integer, Integer> m = new HashMap<>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        if (m.containsKey(arr[i]))
        {
            m.put(arr[i], m.get(arr[i]) + 1);
        }
        else
        {
            m.put(arr[i], 1);
        }
    }

    for(int i = 0; i < N; i++)
    {

        // Calculate log base 2
        // of the element arr[i]
        int lg = log2(arr[i]);

        // Highest power of 2 whose
        // value is at most arr[i]
        int p = (int)Math.pow(2, lg);

        // Increment the count by 1
        if (m.containsKey(p))
        {
            count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 3, 4, 6, 9 };
    int N = arr.length;

    System.out.println(countElement(arr, N));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach
from math import log2

# Function to count array elements
# whose highest power of 2 is less
# than or equal to that number is
# present in the given array
def countElement(arr, N):
    # Stores the resultant count
    # of array elements
    count = 0

    # Stores frequency of
    # visited array elements
    m = {}

    # Traverse the array
    for i in range(N):
        m[arr[i]] = m.get(arr[i], 0) + 1

    for i in range(N):
        # Calculate log base 2
        # of the element arr[i]
        lg = int(log2(arr[i]))

        # Highest power of 2 whose
        # value is at most arr[i]
        p = pow(2, lg)

        # Increment the count by 1
        if (p in m):
            count += 1

    # Return the resultant count
    return count

# Driver Code
if __name__ == '__main__':
    arr= [3, 4, 6, 9]
    N = len(arr)
    print (countElement(arr, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to count array elements
// whose highest power of 2 is less
// than or equal to that number is
// present in the given array
static int countElement(int []arr, int N)
{
    // Stores the resultant count
    // of array elements
    int count = 1;

    // Stores frequency of
    // visited array elements
    Dictionary<int,int> m = new Dictionary<int,int>();

    // Traverse the array
    for (int i = 0; i < N; i++) {
        if(m.ContainsKey(arr[i]))
         m[arr[i]]++;
        else
         m.Add(arr[i],1);
    }

    for(int i = 0; i < N; i++) {

        // Calculate log base 2
        // of the element arr[i]
        int lg = (int)Math.Log(arr[i]);

        // Highest power of 2 whose
        // value is at most arr[i]
        int p = (int)Math.Pow(2, lg);

        // Increment the count by 1
        if (m.ContainsKey(p)) {
            count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 4, 6, 9 };
    int N = arr.Length;
    Console.Write(countElement(arr, N));

}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count array elements
// whose highest power of 2 is less
// than or equal to that number is
// present in the given array
function countElement(arr, N) {
    // Stores the resultant count
    // of array elements
    let count = 0;

    // Stores frequency of
    // visited array elements
    let m = new Map();

    // Traverse the array
    for (let i = 0; i < N; i++) {
        if (m.has(arr[i])) {
            m.set(arr[i], m.get(arr[i]) + 1)
        } else {
            m.set(arr[i], 1)
        }
    }

    for (let i = 0; i < N; i++) {

        // Calculate log base 2
        // of the element arr[i]
        let lg = Math.floor(Math.log2(arr[i]));

        // Highest power of 2 whose
        // value is at most arr[i]
        let p = Math.pow(2, lg);

        // Increment the count by 1
        if (m.get(p)) {
            count++;
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code

let arr = [3, 4, 6, 9];
let N = arr.length
document.write(countElement(arr, N));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)