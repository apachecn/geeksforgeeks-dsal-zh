# 集合位等于 K 的数组所有元素的异或

> 原文:[https://www . geesforgeks . org/数组中所有元素的异或位等于 k/](https://www.geeksforgeeks.org/xor-of-all-elements-of-array-with-set-bits-equal-to-k/)

给定一个整数数组和一个数字 k，任务是只求数组中总集合位等于 k 的那些元素的异或。
**示例** :

```
Input : arr[] = {1, 22, 3, 10}, K=1
Output : 1
Elements with set bits equal to 1 is 1.
So, XOR is also 1.

Input : arr[] = {3, 4, 10, 5, 8}, K=2
Output : 12
```

**进场:**

1.  初始化一个空向量。
2.  从左到右遍历数组形式，检查每个元素的设置位。
3.  使用，C++内置函数 __builtin_popcount()对设置位进行计数。
4.  将带有 K 个集合位的元素推入向量。
5.  最后求向量所有元素的异或。

以下是上述方法的实现:

## C++

```
// C++ program to find Xor
// of all elements with set bits
// equal to K
#include <bits/stdc++.h>
using namespace std;

// Function to find Xor
// of desired elements
int xorGivenSetBits(int arr[], int n, int k)
{
    // Initialize vector
    vector<int> v;

    for (int i = 0; i < n; i++) {
        if (__builtin_popcount(arr[i]) == k) {
            // push required elements
            v.push_back(arr[i]);
        }
    }

    // Initialize result with first element of vector
    int result = v[0];

    for (int i = 1; i < v.size(); i++)
        result = result ^ v[i];

    return result;
}

// Driver code
int main()
{
    int arr[] = { 2, 13, 1, 19, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    cout << xorGivenSetBits(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Xor
// of all elements with set bits
// equal to K
import java.util.*;

class GFG
{

    // Function to find Xor
    // of desired elements
    static int xorGivenSetBits(int arr[],
                                int n, int k)
    {
        // Initialize vector
        Vector<Integer> v = new Vector<>();

        for (int i = 0; i < n; i++)
        {
            if (Integer.bitCount(arr[i]) == k)
            {
                // push required elements
                v.add(arr[i]);
            }
        }

        // Initialize result with first element of vector
        int result = v.get(0);

        for (int i = 1; i < v.size(); i++)
        {
            result = result ^ v.get(i);
        }

        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {2, 13, 1, 19, 7};
        int n = arr.length;
        int k = 3;
        System.out.println(xorGivenSetBits(arr, n, k));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find Xor of all
# elements with set bits equal to K

# Function to find Xor of desired elements
def xorGivenSetBits(arr, n, k):

    # Initialize vector
    v = []
    for i in range(0, n, 1):
        if (bin(arr[i]).count('1') == k):

            # push required elements
            v.append(arr[i])

    # Initialize result with first
    # element of vector
    result = v[0]

    for i in range(1, len(v), 1):
        result = result ^ v[i]

    return result

# Driver code
if __name__ == '__main__':
    arr = [2, 13, 1, 19, 7]
    n = len(arr)
    k = 3

    print(xorGivenSetBits(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find Xor
// of all elements with set bits
// equal to K
using System;
using System.Collections;
using System.Linq;

class GFG
{

// Function to find Xor
// of desired elements
static int xorGivenSetBits(int []arr, int n, int k)
{
    // Initialize vector
    ArrayList v=new ArrayList();

    for (int i = 0; i < n; i++)
    {
        if (Convert.ToString(arr[i], 2).Count(c => c == '1') == k)
        {
            // push required elements
            v.Add(arr[i]);
        }
    }

    // Initialize result with first element of vector
    int result = (int)v[0];

    for (int i = 1; i < v.Count; i++)
        result = result ^ (int)v[i];

    return result;
}

// Driver code
static void Main()
{
    int []arr = { 2, 13, 1, 19, 7 };
    int n = arr.Length;
    int k = 3;

    Console.WriteLine(xorGivenSetBits(arr, n, k));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript program to find Xor
// of all elements with set bits
// equal to K

// Function to find Xor
// of desired elements
function xorGivenSetBits(arr, n, k)
{
    // Initialize vector
    let v = [];

    for (let i = 0; i < n; i++) {
        if (bitcount(arr[i]) == k) {
            // push required elements
            v.push(arr[i]);
        }
    }

    // Initialize result with first
    // element of vector
    let result = v[0];

    for (let i = 1; i < v.length; i++)
        result = result ^ v[i];

    return result;
}

function bitcount(n)
{
  var count = 0;
  while (n)
  {
    count += n & 1;
    n >>= 1;
  }
  return count;
}

// Driver code
    let arr = [ 2, 13, 1, 19, 7 ];
    let n = arr.length;
    let k = 3;

    document.write(xorGivenSetBits(arr, n, k));

</script>
```

**Output:** 

```
25
```