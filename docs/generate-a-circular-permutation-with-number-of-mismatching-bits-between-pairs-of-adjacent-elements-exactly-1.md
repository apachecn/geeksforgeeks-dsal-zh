# 生成一个循环置换，相邻元素对之间的不匹配位数正好为 1

> 原文:[https://www . geeksforgeeks . org/generate-a-循环置换-相邻元素对之间的错配位数-恰好-1/](https://www.geeksforgeeks.org/generate-a-circular-permutation-with-number-of-mismatching-bits-between-pairs-of-adjacent-elements-exactly-1/)

给定两个整数 **N** 和 **S** ，任务是从范围**【0，2】<sup>(N–1)</sup>**中找到数字的循环[排列](https://www.geeksforgeeks.org/permutation-and-combination/)，从 **S** 开始，使得任意一对相邻数字之间的不匹配位的[计数为**1**。](https://www.geeksforgeeks.org/number-of-mismatching-bits-in-the-binary-representation-of-two-integers/)

**示例:**

> **输入:** N = 2，S = 3
> **输出:**【3，2，0，1】
> **说明:**
> 数字 3、2、0、1 的二进制表示分别为“11”、“10”、“01”、“00”。
> 因此，以[3，2，0，1]的顺序排列它们确保了每对相邻元素(圆形)之间的比特差数为 1。
> 
> **输入:** N = 3，S = 2
> **输出:**【2，6，7，5，4，0，1，3】

**方法:**给定的问题可以基于以下观察来解决:

> *   A simple observation is that the numbers in the range of **[2] T3i, 2 <sup>I+1</sup> –1]** can be obtained by placing **' 1' [before each number in the range of **[0,2 <sup>I</sup> –1]****
> *   Therefore, the problem can be solved recursively by adding **' 1'** in front of each digit in the index of **2 <sup>I</sup> –1** <sup>, and the new digit can be inverted before being added to their arrangement.</sup>

按照以下步骤解决问题:

*   初始化一个列表，比如 **res** ，以存储所需的排列。
*   初始化一个整数，比如说**索引**，来存储从 **0** 开始的排列中 **S** 的位置。
*   以相反的顺序遍历范围**【0，N–1】**和[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **res[]** ，检查**当前编号**和 **2 <sup>i</sup>** 的和是否为 **S** 。如果发现为真，则用 **res** 的当前索引更新**索引**，并将**当前编号+2<sup>I</sup>T21 追加到列表 **res** 中。**
*   [通过**索引**位置旋转列表 res[]](https://www.geeksforgeeks.org/array-rotation/) 。
*   完成以上步骤后，打印列表 **res[]** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the permutation of
// integers from a given range such that
// number of mismatching bits between
// pairs of adjacent elements is 1
vector<int> circularPermutation(int n, int start)
{

    // Initialize an arrayList to
    // store the resultant permutation
    vector<int> res = {0};
    vector<int> ret;

    // Store the index of rotation
    int index = -1;

    // Iterate over the range [0, N - 1]
    for(int k = 0, add = 1 << k; k < n;
            k++, add = 1 << k)
    {

        // Traverse all the array elements
        // up to (2 ^ k)-th index in reverse
        for (int i = res.size() - 1;
                 i >= 0; i--)
        {

            // If current element is S
            if (res[i] + add == start)
                index = res.size();

            res.push_back(res[i] + add);
        }
    }

    // Check if S is zero
    if (start == 0)
        return res;

    // Rotate the array by index
    // value to the left
    while (ret.size() < res.size())
    {
        ret.push_back(res[index]);
        index = (index + 1) % res.size();
    }
    return ret;
}

// Driver Code
int main()
{
    int N = 2, S = 3;
    vector<int> print = circularPermutation(N, S);
    cout << "[";
    for(int i = 0; i < print.size() - 1; i++ )
    {
        cout << print[i] << ", ";
    }
    cout << print[print.size() - 1] << "]";

    return 0;
}

// This code is contributed by susmitakundugoaldanga
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the permutation of
    // integers from a given range such that
    // number of mismatching bits between
    // pairs of adjacent elements is 1
    public static List<Integer> circularPermutation(
        int n, int start)
    {
        // Initialize an arrayList to
        // store the resultant permutation
        List<Integer> res = new ArrayList<>(List.of(0)),
                      ret = new ArrayList<>();

        // Store the index of rotation
        int index = -1;

        // Iterate over the range [0, N - 1]
        for (int k = 0, add = 1 << k; k < n;
             k++, add = 1 << k) {

            // Traverse all the array elements
            // up to (2 ^ k)-th index in reverse
            for (int i = res.size() - 1;
                 i >= 0; i--) {

                // If current element is S
                if (res.get(i) + add == start)
                    index = res.size();

                res.add(res.get(i) + add);
            }
        }

        // Check if S is zero
        if (start == 0)
            return res;

        // Rotate the array by index
        // value to the left
        while (ret.size() < res.size()) {
            ret.add(res.get(index));
            index = (index + 1) % res.size();
        }

        return ret;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2, S = 3;

        System.out.println(
            circularPermutation(N, S));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the permutation of
# integers from a given range such that
# number of mismatching bits between
# pairs of adjacent elements is 1
def circularPermutation(n, start):

    # Initialize an arrayList to
    # store the resultant permutation
    res = [0]
    ret = []

    # Store the index of rotation
    index, add = -1, 1

    # Iterate over the range [0, N - 1]
    for k in range(n):
        add = 1<<k

        # Traverse all the array elements
        # up to (2 ^ k)-th index in reverse
        for i in range(len(res) - 1, -1, -1):

            # If current element is S
            if (res[i] + add == start):
                index = len(res)
            res.append(res[i] + add)
        add  = 1 << k

    # Check if S is zero
    if (start == 0):
        return res

    # Rotate the array by index
    # value to the left
    while (len(ret) < len(res)):
        ret.append(res[index])
        index = (index + 1) % len(res)
    return ret

# Driver Code
if __name__ == '__main__':
    N,S = 2, 3

    print (circularPermutation(N, S))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to find the permutation of
  // integers from a given range such that
  // number of mismatching bits between
  // pairs of adjacent elements is 1
  public static List<int> circularPermutation(
    int n, int start)
  {

    // Initialize an arrayList to
    // store the resultant permutation
    List<int> res = new List<int>(){0};
    List<int> ret = new List<int>();

    // Store the index of rotation
    int index = -1;

    // Iterate over the range [0, N - 1]
    for (int k = 0, add = 1 << k; k < n;
         k++, add = 1 << k)
    {

      // Traverse all the array elements
      // up to (2 ^ k)-th index in reverse
      for (int i = res.Count - 1;
           i >= 0; i--)
      {

        // If current element is S
        if (res[i] + add == start)
          index = res.Count;
        res.Add(res[i] + add);
      }
    }

    // Check if S is zero
    if (start == 0)
      return res;

    // Rotate the array by index
    // value to the left
    while (ret.Count < res.Count)
    {
      ret.Add(res[index]);
      index = (index + 1) % res.Count;
    }
    return ret;
  }

  // Driver Code
  static public void Main ()
  {
    int N = 2, S = 3;
    List<int> print = circularPermutation(N, S);
    Console.Write("[");
    for(int i = 0; i < print.Count - 1; i++ )
    {
      Console.Write(print[i] + ", ");
    }
    Console.Write(print[print.Count-1] + "]");
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the permutation of
// integers from a given range such that
// number of mismatching bits between
// pairs of adjacent elements is 1
function circularPermutation(n, start)
{

    // Initialize an arrayList to
    // store the resultant permutation
    var res = [0];
    var ret = [];

    // Store the index of rotation
    var index = -1;

    // Iterate over the range [0, N - 1]
    for(var k = 0, add = 1 << k; k < n;
            k++, add = 1 << k)
    {

        // Traverse all the array elements
        // up to (2 ^ k)-th index in reverse
        for (var i = res.length - 1;
                 i >= 0; i--)
        {

            // If current element is S
            if (res[i] + add == start)
                index = res.length;

            res.push(res[i] + add);
        }
    }

    // Check if S is zero
    if (start == 0)
        return res;

    // Rotate the array by index
    // value to the left
    while (ret.length < res.length)
    {
        ret.push(res[index]);
        index = (index + 1) % res.length;
    }
    return ret;
}

// Driver Code
var N = 2, S = 3;
var print = circularPermutation(N, S);
document.write( "[");
for(var i = 0; i < print.length - 1; i++ )
{
    document.write( print[i] + ", ");
}
document.write( print[print.length - 1] + "]");

</script>
```

**Output:** 

```
[3, 2, 0, 1]
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*