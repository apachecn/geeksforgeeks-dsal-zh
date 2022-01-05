# 数组中频率与值相同的最大数字

> 原文:[https://www . geeksforgeeks . org/阵列中最大数量频率与值相同/](https://www.geeksforgeeks.org/largest-number-in-the-array-having-frequency-same-as-value/)

给定一个包含 **N** 个整数的数组 **arr** ，任务是找到数组中频率与其值相等的最大数。如果不存在这样的号码，则打印-1。
**例:**

> **输入:** arr = [3，2，5，2，4，5]
> **输出:** 2
> **解释:**
> 在这个给定的数组中，2 的频率是 2，而其余数字的频率与其本身不匹配。所以答案是 2。
> **输入:** arr = [3，3，3，4，4，4，4]
> **输出:** 4
> **解释:**
> 在这个给定的数组中，3 的频率是 3，4 是 4，但最大的数字是 4。所以答案是 4。
> **输入:** arr = [1，1，1，2，3，3]
> **输出:** -1
> **解释:**
> 给定数组中没有频率等于自身的数字。因此输出为-1。

**简单方法:**

1.  创建一个新数组来记录给定数组中出现的次数。
2.  以相反的顺序遍历新数组。
3.  返回第一个计数等于自身的数字。

下面是上述方法的实现:

## C++

```
// C++ solution to the above problem

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest number
// whose frequency is equal to itself.
int findLargestNumber(vector<int>& arr)
{

    // Find the maximum element in the array
    int k = *max_element(arr.begin(),
                         arr.end());
    int m[k] = {};

    for (auto n : arr)
        ++m[n];

    for (auto n = arr.size(); n > 0; --n) {
        if (n == m[n])
            return n;
    }
    return -1;
}

// Driver code
int main()
{
    vector<int> arr = { 3, 2, 5, 2, 4, 5 };

    cout << findLargestNumber(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java solution to the above problem
import java.util.*;

class GFG{

// Function to find the largest number
// whose frequency is equal to itself.
static int findLargestNumber(int[] arr)
{

    // Find the maximum element in the array
    int k = Arrays.stream(arr).max().getAsInt();
    int []m = new int[k + 1];

    for(int n : arr)
       ++m[n];

    for(int n = arr.length - 1; n > 0; --n)
    {
       if (n == m[n])
           return n;
    }
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 3, 2, 5, 2, 4, 5 };

    System.out.print(findLargestNumber(arr) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 solution to the above problem

# Function to find the largest number
# whose frequency is equal to itself.
def findLargestNumber(arr):

    # Find the maximum element in the array
    k = max(arr);
    m = [0] * (k + 1);

    for n in arr:
        m[n] += 1;

    for n in range(len(arr) - 1, 0, -1):
        if (n == m[n]):
            return n;

    return -1;

# Driver code
if __name__ == '__main__':

    arr = [ 3, 2, 5, 2, 4, 5 ];

    print(findLargestNumber(arr));

# This code is contributed by amal kumar choubey
```

## C#

```
// C# solution to the above problem
using System;
using System.Linq;

class GFG{

// Function to find the largest number
// whose frequency is equal to itself.
static int findLargestNumber(int[] arr)
{

    // Find the maximum element in the array
    int k = arr.Max();
    int []m = new int[k + 1];

    foreach(int n in arr)
        ++m[n];

    for(int n = arr.Length - 1; n > 0; --n)
    {
       if (n == m[n])
           return n;
    }
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 3, 2, 5, 2, 4, 5 };

    Console.Write(findLargestNumber(arr) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript solution to the above problem

// Function to find the largest number
// whose frequency is equal to itself.
function findLargestNumber(arr)
{

    // Find the maximum element in the array
    var k = arr.reduce((a,b)=> Math.max(a,b));
    var m = Array(k).fill(0);

    arr.forEach(n => {
        ++m[n];
    });

    for (var n = arr.length; n > 0; --n) {
        if (n == m[n])
            return n;
    }
    return -1;
}

// Driver code
var arr = [3, 2, 5, 2, 4, 5];
document.write( findLargestNumber(arr));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(N)*
**另一种方法:**
**注:**该方法仅在给定数组中的数字小于 65536 时有效，即 2 <sup>16</sup> 。

1.  这里，使用输入数组来存储计数。
2.  由于数值有限，只需使用整数的前半部分(前 16 位)通过相加 65536 来保持计数。
3.  使用[右移运算符](https://www.geeksforgeeks.org/bitwise-shift-operators-in-java/)(右移 16 位)[反向遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，返回第一个计数等于自身的数字。

以下是上述方法的实现:

## C++

```
// C++ code for the above problem

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest number
// whose frequency is equal to itself.
int findLargestNumber(vector<int>& arr)
{
    for (auto n : arr) {
        n &= 0xFFFF;
        if (n <= arr.size()) {
            // Adding 65536 to keep the
            // count of the current number
            arr[n - 1] += 0x10000;
        }
    }

    for (auto i = arr.size(); i > 0; --i) {
        // right shifting by 16 bits
        // to find the count of the
        // number i
        if ((arr[i - 1] >> 16) == i)
            return i;
    }
    return -1;
}

// Driver code
int main()
{
    vector<int> arr
        = { 3, 2, 5, 5, 2, 4, 5 };

    cout << findLargestNumber(arr)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above problem
class GFG{

// Function to find the largest number
// whose frequency is equal to itself.
static int findLargestNumber(int[] arr, int n)
{
    for(int i = 0; i < n; i++)
    {
        arr[i] &= 0xFFFF;
        if (arr[i] <= n)
        {

            // Adding 65536 to keep the
            // count of the current number
            arr[i] += 0x10000;
        }
    }

    for(int i = n - 1; i > 0; --i)
    {

        // Right shifting by 16 bits
        // to find the count of the
        // number i
        if ((arr[i] >> 16) == i)
            return i + 1;
    }
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 3, 2, 5, 5, 2, 4, 5 };
    int n = arr.length;

    System.out.print(findLargestNumber(arr, n) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 code for the above problem

# Function to find the largest number
# whose frequency is equal to itself.
def findLargestNumber(arr, n):
    for i in range(n):
        arr[i] &= 0xFFFF;
        if (arr[i] <= n):

            # Adding 65536 to keep the
            # count of the current number
            arr[i] += 0x10000;

    for i in range(n - 1, 0, -1):

        # Right shifting by 16 bits
        # to find the count of the
        # number i
        if ((arr[i] >> 16) == i):
            return i + 1;

    return -1;

# Driver code
if __name__ == '__main__':
    arr = [ 3, 2, 5, 5, 2, 4, 5 ];
    n = len(arr);

    print(findLargestNumber(arr, n));

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# code for the above problem
using System;

class GFG{

// Function to find the largest number
// whose frequency is equal to itself.
static int findLargestNumber(int[] arr, int n)
{
    for(int i = 0; i < n; i++)
    {
        arr[i] &= 0xFFFF;
        if (arr[i] <= n)
        {

            // Adding 65536 to keep the
            // count of the current number
            arr[i] += 0x10000;
        }
    }

    for(int i = n - 1; i > 0; --i)
    {

        // Right shifting by 16 bits
        // to find the count of the
        // number i
        if ((arr[i] >> 16) == i)
            return i + 1;
    }
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 5, 5, 2, 4, 5 };
    int n = arr.Length;

    Console.Write(findLargestNumber(arr, n) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript code for the above problem

// Function to find the largest number
// whose frequency is equal to itself.
function findLargestNumber(arr)
{
    arr.forEach(n => {

        n &= 0xFFFF;
        if (n <= arr.length) {
            // Adding 65536 to keep the
            // count of the current number
            arr[n - 1] += 0x10000;
        }
    });

    for(var i = arr.length; i > 0; --i) {
        // right shifting by 16 bits
        // to find the count of the
        // number i
        if ((arr[i - 1] >> 16) == i)
            return i;
    }
    return -1;
}

// Driver code
var arr
    = [3, 2, 5, 5, 2, 4, 5];
document.write( findLargestNumber(arr))

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(1)*