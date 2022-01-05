# 非重复数组元素的最近完美平方的最近 2 次幂

> 原文:[https://www . geeksforgeeks . org/非重复数组元素的最近二次方/](https://www.geeksforgeeks.org/nearest-power-of-2-of-nearest-perfect-squares-of-non-repeating-array-elements/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到[唯一数组元素](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)的最近[完美方块](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)的最近[完美 2 次方](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)。如果数组不包含任何唯一元素，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {4，11，4，3，4}
> **输出:** 4 8
> **解释:**
> 给定数组中唯一的元素是 11 和 3。
> 最近的 11 和 3 的完美平方分别是 9 和 4。
> 9 和 4 的 2 的最近幂分别是 8 和 4。
> 
> **输入:** arr[] = {1，1，2，2，3，3}
> **输出:** -1

**天真法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于单个出现的每个数组元素，打印数组元素最近的[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)的最近的[完美 2 次方](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)。否则，如果数组中没有唯一的元素，则打印 **-1** 。

***时间复杂度:**O(N<sup>2</sup>* log N)*
***辅助空间:** O(1)*

**高效方法:**以上可以通过 [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) 进行优化。按照以下步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将每个数组元素的[频率存储在](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)中，比如 **M** 。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，执行以下步骤:
    *   如果当前元素的频率为 **1** ，则打印当前元素的[最近完美平方](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)的[最近 2](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/) 次幂。
    *   否则[继续下一次迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   完成上述步骤后，如果上述步骤中不存在任何唯一元素，则打印“**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find nearest
// perfect square of num
int perfectSquare(int num)
{
    // Calculate square root of num
    int sr = sqrt(num);

    // Calculate perfect square
    int a = sr * sr;
    int b = (sr + 1) * (sr + 1);

    // Find the nearest perfect square
    if ((num - a) < (b - num)) {
        return a;
    }
    else {
        return b;
    }
}

// Function to find the power of 2
// nearest to the number num
int powerOfTwo(int num)
{
    // Calculate log base 2 of num
    int lg = log2(num);

    // Highest power of 2 which is <= num
    int p = pow(2, lg);

    return p;
}

// Function to find the nearest perfect
// square and the nearest power of 2 of
// every array element whose occurrence is 1
void uniqueElement(int arr[], int N)
{
    bool ans = true;

    // Stores frequency of array elements
    unordered_map<int, int> freq;

    // Traverse the array and update
    // frequency of current array element
    for (int i = 0; i < N; i++) {
        freq[arr[i]]++;
    }

    // Traverse the map freq
    for (auto el : freq) {

        // If the frequency is 1
        if (el.second == 1) {

            ans = false;

            // Find nearest perfect square
            int ps = perfectSquare(el.first);

            // Print the nearest power of 2
            cout << powerOfTwo(ps) << ' ';
        }
    }

    // If the any does not contain
    // any non-repeating elements
    if (ans)
        cout << "-1";
}

// Driver Code
int main()
{
    int arr[] = { 4, 11, 4, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    uniqueElement(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

  // Function to find nearest
  // perfect square of num
  static int perfectSquare(int num)
  {

    // Calculate square root of num
    int sr = (int)(Math.sqrt(num));

    // Calculate perfect square
    int a = sr * sr;
    int b = (sr + 1) * (sr + 1);

    // Find the nearest perfect square
    if ((num - a) < (b - num)) {
      return a;
    }
    else {
      return b;
    }
  }

  // Function to find the power of 2
  // nearest to the number num
  static int powerOfTwo(int num)
  {

    // Calculate log base 2 of num
    int lg = (int)(Math.log(num) / Math.log(2));

    // Highest power of 2 which is <= num
    int p = (int)(Math.pow(2, lg));

    return p;
  }

  // Function to find the nearest perfect
  // square and the nearest power of 2 of
  // every array element whose occurrence is 1
  static void uniqueElement(int arr[], int N)
  {
    boolean ans = true;

    // Stores frequency of array elements
    HashMap<Integer, Integer> freq
      = new HashMap<Integer, Integer>();

    // Traverse the array and update
    // frequency of current array element
    for (int i = 0; i < N; i++) {
      if (freq.containsKey(arr[i])) {
        freq.put(arr[i], freq.get(arr[i]) + 1);
      }
      else {
        freq.put(arr[i], 1);
      }
    }

    // Traverse the map freq
    for (Map.Entry<Integer, Integer> el :
         freq.entrySet()) {

      // If the frequency is 1
      if (el.getValue() == 1) {

        ans = false;

        // Find nearest perfect square

        int ps = perfectSquare(el.getKey());

        // Print the nearest power of 2
        System.out.print(powerOfTwo(ps) + " ");
      }
    }

    // If the any does not contain
    // any non-repeating elements
    if (ans)
      System.out.print("-1");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 4, 11, 4, 3, 4 };
    int N = arr.length;

    uniqueElement(arr, N);
  }
}

// This code is contributed by subhammahato348.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt, log2, pow

# Function to find nearest
# perfect square of num
def perfectSquare(num):

    # Calculate square root of num
    sr = int(sqrt(num))

    # Calculate perfect square
    a = sr * sr
    b = (sr + 1) * (sr + 1)

    # Find the nearest perfect square
    if ((num - a) < (b - num)):
        return a
    else:
        return b

# Function to find the power of 2
# nearest to the number num
def powerOfTwo(num):

    # Calculate log base 2 of num
    lg = int(log2(num))

    # Highest power of 2 which is <= num
    p = int(pow(2, lg))

    return p

# Function to find the nearest perfect
# square and the nearest power of 2 of
# every array element whose occurrence is 1
def uniqueElement(arr, N):

    ans = True

    # Stores frequency of array elements
    freq = {}

    # Traverse the array and update
    # frequency of current array element
    for i in range(N):
        if (arr[i] in freq):
            freq[arr[i]] += 1
        else:
            freq[arr[i]] = 1

    # Traverse the map freq
    res = []
    for key,value in freq.items():

        # If the frequency is 1
        if (value == 1):
            ans = False

            # Find nearest perfect square
            ps = perfectSquare(key)

            # Print the nearest power of 2
            res.append(powerOfTwo(ps))

    res.sort(reverse = False)
    for x in res:
      print(x, end = " ")

    # If the any does not contain
    # any non-repeating elements
    if (ans):
        print("-1")

# Driver Code
if __name__ == '__main__':

    arr =  [4, 11, 4, 3, 4]
    N =  len(arr)

    uniqueElement(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to find nearest
// perfect square of num
static int perfectSquare(int num)
{

    // Calculate square root of num
    int sr = (int)(Math.Sqrt(num));

    // Calculate perfect square
    int a = sr * sr;
    int b = (sr + 1) * (sr + 1);

    // Find the nearest perfect square
    if ((num - a) < (b - num))
    {
        return a;
    }
    else
    {
        return b;
    }
}

// Function to find the power of 2
// nearest to the number num
static int powerOfTwo(int num)
{

    // Calculate log base 2 of num
    int lg = (int)(Math.Log(num) / Math.Log(2));

    // Highest power of 2 which is <= num
    int p = (int)(Math.Pow(2, lg));

    return p;
}

// Function to find the nearest perfect
// square and the nearest power of 2 of
// every array element whose occurrence is 1
static void uniqueElement(int[] arr, int N)
{
    bool ans = true;

    // Stores frequency of array elements
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    // Traverse the array and update
    // frequency of current array element
    for(int i = 0; i < N; i++)
    {
        if (freq.ContainsKey(arr[i]))
        {
            freq[arr[i]] = freq[arr[i]] + 1;
        }
        else
        {
            freq[arr[i]] = 1;
        }
    }

    // Traverse the map freq
    foreach(var el in freq.OrderBy(el => el.Key))
    {

        // If the frequency is 1
        if (el.Value == 1)
        {
            ans = false;

            // Find nearest perfect square
            int ps = perfectSquare(el.Key);

            // Print the nearest power of 2
            Console.Write(powerOfTwo(ps) + " ");
        }
    }

    // If the any does not contain
    // any non-repeating elements
    if (ans)
        Console.Write("-1");
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 4, 11, 4, 3, 4 };
    int N = arr.Length;

    uniqueElement(arr, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find nearest
// perfect square of num
function perfectSquare(num)
{

    // Calculate square root of num
    let sr = Math.floor(Math.sqrt(num));

    // Calculate perfect square
    let a = sr * sr;
    let b = (sr + 1) * (sr + 1);

    // Find the nearest perfect square
    if ((num - a) < (b - num))
    {
        return a;
    }
    else
    {
        return b;
    }
}

// Function to find the power of 2
// nearest to the number num
function powerOfTwo(num)
{

    // Calculate log base 2 of num
    let lg = Math.floor(Math.log2(num));

    // Highest power of 2 which is <= num
    let p = Math.pow(2, lg);

    return p;
}

// Function to find the nearest perfect
// square and the nearest power of 2 of
// every array element whose occurrence is 1
function uniqueElement(arr, N)
{
    let ans = true;
    arr.reverse();

    // Stores frequency of array elements
    let freq = new Map();

    // Traverse the array and update
    // frequency of current array element
    for(let i = 0; i < N; i++)
    {
        freq[arr[i]]++;
        if (freq.has(arr[i]))
        {
            freq.set(arr[i],
            freq.get(arr[i]) + 1)
        }
        else[
            freq.set(arr[i], 1)
        ]
    }

    // Traverse the map freq
    for(let el of freq)
    {

        // If the frequency is 1
        if (el[1] == 1)
        {
            ans = false;

            // Find nearest perfect square
            let ps = perfectSquare(el[0]);

            // Print the nearest power of 2
            document.write(powerOfTwo(ps) + ' ');
        }
    }

    // If the any does not contain
    // any non-repeating elements
    if (ans)
        document.write("-1");
}

// Driver Code
let arr = [ 4, 11, 4, 3, 4 ];
let N = arr.length;

uniqueElement(arr, N);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
4 8
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*