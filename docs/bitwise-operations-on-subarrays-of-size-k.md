# 大小为 K 的子阵列上的逐位运算

> 原文:[https://www . geeksforgeeks . org/k 尺寸子阵列的逐位运算/](https://www.geeksforgeeks.org/bitwise-operations-on-subarrays-of-size-k/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个数字 **K** ，任务是找到大小为 **K** 的子阵列元素的**最小值**和**最大值**值。

**示例:**

> **输入:** arr[]={2，5，3，6，11，13}，k = 3
> **输出:**
> 最大 AND = 2
> 最小 AND = 0
> 最大 OR = 15
> 最小 OR = 7
> **说明:**
> 最大 AND 由子阵列 3、6 和 11 生成，3 & 6 & 11 = 2
> 最小 AND 由子阵列 2、3 生成 2 & 3 & 5 = 0
> 最大或由子阵列 2、6 和 13 产生，2 | 6 | 13 = 15
> 最小或由子阵列 2、3 和 5 产生，2 | 3 | 5 = 7
> 
> **输入:** arr[]={5，9，7，19}，k = 2
> **输出:**
> 最大 AND = 3
> 最小 AND = 1
> 最大 OR = 23
> 最小 OR = 13

**天真方法:**天真方法是[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)大小为 **K** 并检查上面形成的子阵列中哪一个会给出最小和最大的按位“或”和“与”。
**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(K)*

**高效方法:**思路是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决这个问题。以下是步骤:

1.  遍历大小为 **K** 的前缀数组，对于每个数组，元素遍历它的每个位，并且如果设置了位数组，则将位数组(通过保持大小为 32 的整数数组位)增加 1。
2.  将该位数组转换为十进制数，比如说*和*，并将滑动窗口移动到下一个索引。
3.  对于大小为 **K** 的下一个子阵列的新添加元素，遍历新添加元素的每个位，如果设置了位数组，则将位数组增加 **1** 。
4.  要从前一个窗口中删除第一个元素，如果设置了位数组，则将它减少 1。
5.  用位数组生成的新十进制数的最小值或最大值更新*和*。

*   下面是寻找 **<u>最大位“或”子阵</u>** 的程序:

## C++

```
// C++ program for maximum values of
// each bitwise OR operation on
// element of subarray of size K
#include <iostream>
using namespace std;

// Function to convert bit array to
// decimal number
int build_num(int bit[])
{
    int ans = 0;

    for (int i = 0; i < 32; i++)
        if (bit[i])
            ans += (1 << i);

    return ans;
}

// Function to find  maximum values of
// each bitwise OR operation on
// element of subarray of size K
int maximumOR(int arr[], int n, int k)
{
    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[32] = { 0 };

    // Create a sliding window of size k
    for (int i = 0; i < k; i++) {
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }
    }

    // Function call
    int max_or = build_num(bit);

    for (int i = k; i < n; i++) {

        // Perform operation for
        // removed element
        for (int j = 0; j < 32; j++) {
            if (arr[i - k] & (1 << j))
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }

        // Taking maximum value
        max_or = max(build_num(bit), max_or);
    }

    // Return the result
    return max_or;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    cout << maximumOR(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for maximum values of
// each bitwise OR operation on
// element of subarray of size K
import java.util.*;
class GFG{

// Function to convert bit array to
// decimal number
static int build_num(int bit[])
{
    int ans = 0;

    for (int i = 0; i < 32; i++)
        if (bit[i] > 0)
            ans += (1 << i);

    return ans;
}

// Function to find  maximum values of
// each bitwise OR operation on
// element of subarray of size K
static int maximumOR(int arr[], int n, int k)
{
    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[] = new int[32];

    // Create a sliding window of size k
    for (int i = 0; i < k; i++)
    {
        for (int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    // Function call
    int max_or = build_num(bit);

    for (int i = k; i < n; i++)
    {

        // Perform operation for
        // removed element
        for (int j = 0; j < 32; j++)
        {
            if ((arr[i - k] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for (int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking maximum value
        max_or = Math.max(build_num(bit), max_or);
    }

    // Return the result
    return max_or;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = arr.length;

    // Function Call
    System.out.print(maximumOR(arr, n, k));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for maximum values of
# each bitwise OR operation on
# element of subarray of size K

# Function to convert bit array to
# decimal number
def build_num(bit):

    ans = 0;

    for i in range(32):
        if (bit[i] > 0):
            ans += (1 << i);

    return ans;

# Function to find maximum values of
# each bitwise OR operation on
# element of subarray of size K
def maximumOR(arr, n, k):

    # Maintain an integer array bit
    # of size 32 all initialized to 0
    bit = [0] * 32;

    # Create a sliding window of size k
    for i in range(k):
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

    # Function call
    max_or = build_num(bit);

    for i in range(k, n):

        # Perform operation for
        # removed element
        for j in range(32):
            if ((arr[i - k] & (1 << j)) > 0):
                bit[j] -= 1;

        # Perform operation for
        # added_element
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

        # Taking maximum value
        max_or = max(build_num(bit), max_or);

    # Return the result
    return max_or;

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 2, 5, 3, 6, 11, 13 ];

    # Given subarray size K
    k = 3;
    n = len(arr);

    # Function call
    print(maximumOR(arr, n, k));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for maximum values of
// each bitwise OR operation on
// element of subarray of size K
using System;
class GFG{

    // Function to convert bit
    // array to decimal number
    static int build_num(int[] bit)
    {
        int ans = 0;
          for (int i = 0; i < 32; i++)
            if (bit[i] > 0)
                ans += (1 << i);
        return ans;
    }

    // Function to find  maximum values of
    // each bitwise OR operation on
    // element of subarray of size K
    static int maximumOR(int[] arr, int n, int k)
    {
        // Maintain an integer array bit[]
        // of size 32 all initialized to 0
        int[] bit = new int[32];

        // Create a sliding window of size k
        for (int i = 0; i < k; i++)
        {
            for (int j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }
        }

        // Function call
        int max_or = build_num(bit);

        for (int i = k; i < n; i++)
        {

            // Perform operation for
            // removed element
            for (int j = 0; j < 32; j++)
            {
                if ((arr[i - k] & (1 << j)) > 0)
                    bit[j]--;
            }

            // Perform operation for
            // added_element
            for (int j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }

            // Taking maximum value
            max_or = Math.Max(build_num(bit), max_or);
        }

        // Return the result
        return max_or;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given array []arr
        int[] arr = {2, 5, 3, 6, 11, 13};

        // Given subarray size K
        int k = 3;
        int n = arr.Length;

        // Function Call
        Console.Write(maximumOR(arr, n, k));
    }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
    // Javascript program for maximum values of
    // each bitwise OR operation on
    // element of subarray of size K

    // Function to convert bit array to
    // decimal number
    function build_num(bit)
    {
        let ans = 0;

        for (let i = 0; i < 32; i++)
            if (bit[i] > 0)
                ans += (1 << i);

        return ans;
    }

       // Function to find  maximum values of
    // each bitwise OR operation on
    // element of subarray of size K
    function maximumOR(arr, n, k)
    {
        // Maintain an integer array bit[]
        // of size 32 all initialized to 0
        let bit = new Array(32);
        bit.fill(0);

        // Create a sliding window of size k
        for (let i = 0; i < k; i++)
        {
            for (let j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }
        }

        // Function call
        let max_or = build_num(bit);

        for (let i = k; i < n; i++)
        {

            // Perform operation for
            // removed element
            for (let j = 0; j < 32; j++)
            {
                if ((arr[i - k] & (1 << j)) > 0)
                    bit[j]--;
            }

            // Perform operation for
            // added_element
            for (let j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }

            // Taking maximum value
            max_or = Math.max(build_num(bit), max_or);
        }

        // Return the result
        return max_or;
    }

    // Given array []arr
    let arr = [2, 5, 3, 6, 11, 13];

    // Given subarray size K
    let k = 3;
    let n = arr.length;

    // Function Call
    document.write(maximumOR(arr, n, k));

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
15
```

**时间复杂度:** *O(n * B)* 其中 n 是数组的大小，B 是大小为 32 的整数数组位。
T5【辅助空间: *O(n)*

*   下面是寻找 **<u>最小位或子阵</u>** 的程序:

## C++

```
// C++ program for minimum values of
// each bitwise OR operation on
// element of subarray of size K
#include <iostream>
using namespace std;

// Function to convert bit array
// to decimal number
int build_num(int bit[])
{
    int ans = 0;

    for (int i = 0; i < 32; i++)
        if (bit[i])
            ans += (1 << i);

    return ans;
}

// Function to find  minimum values of
// each bitwise OR operation on
// element of subarray of size K
int minimumOR(int arr[], int n, int k)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[32] = { 0 };

    // Create a sliding window of size k
    for (int i = 0; i < k; i++) {
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }
    }

    // Function call
    int min_or = build_num(bit);

    for (int i = k; i < n; i++) {

        // Perform operation for
        // removed element
        for (int j = 0; j < 32; j++) {
            if (arr[i - k] & (1 << j))
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }

        // Taking minimum value
        min_or = min(build_num(bit),
                     min_or);
    }

    // Return the result
    return min_or;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    cout << minimumOR(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for minimum values of
// each bitwise OR operation on
// element of subarray of size K
import java.util.*;

class GFG{

// Function to convert bit array
// to decimal number
static int build_num(int bit[])
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
        if (bit[i] > 0)
            ans += (1 << i);

    return ans;
}

// Function to find minimum values of
// each bitwise OR operation on
// element of subarray of size K
static int minimumOR(int arr[], int n, int k)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[] = new int[32];

    // Create a sliding window of size k
    for(int i = 0; i < k; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    // Function call
    int min_or = build_num(bit);

    for(int i = k; i < n; i++)
    {

        // Perform operation for
        // removed element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i - k] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking minimum value
        min_or = Math.min(build_num(bit),
                          min_or);
    }

    // Return the result
    return min_or;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = arr.length;

    // Function call
    System.out.print(minimumOR(arr, n, k));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for minimum values
# of each bitwise OR operation on
# element of subarray of size K

# Function to convert bit array
# to decimal number
def build_num(bit):

    ans = 0;

    for i in range(32):
        if (bit[i] > 0):
            ans += (1 << i);

    return ans;

# Function to find minimum values of
# each bitwise OR operation on
# element of subarray of size K
def minimumOR(arr, n, k):

    # Maintain an integer array bit
    # of size 32 all initialized to 0
    bit = [0] * 32;

    # Create a sliding window of size k
    for i in range(k):
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

    # Function call
    min_or = build_num(bit);

    for i in range(k, n):

        # Perform operation for
        # removed element
        for j in range(32):
            if ((arr[i - k] & (1 << j)) > 0):
                bit[j] -= 1;

        # Perform operation for
        # added_element
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

        # Taking minimum value
        min_or = min(build_num(bit), min_or);

    # Return the result
    return min_or;

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 2, 5, 3, 6, 11, 13 ];

    # Given subarray size K
    k = 3;
    n = len(arr);

    # Function call
    print(minimumOR(arr, n, k));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for minimum values of
// each bitwise OR operation on
// element of subarray of size K
using System;

class GFG{

// Function to convert bit array
// to decimal number
static int build_num(int []bit)
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
        if (bit[i] > 0)
            ans += (1 << i);

    return ans;
}

// Function to find minimum values of
// each bitwise OR operation on
// element of subarray of size K
static int minimumOR(int []arr, int n, int k)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int []bit = new int[32];

    // Create a sliding window of size k
    for(int i = 0; i < k; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    // Function call
    int min_or = build_num(bit);

    for(int i = k; i < n; i++)
    {

        // Perform operation for
        // removed element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i - k] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking minimum value
        min_or = Math.Min(build_num(bit),
                          min_or);
    }

    // Return the result
    return min_or;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = arr.Length;

    // Function call
    Console.Write(minimumOR(arr, n, k));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for minimum values of
// each bitwise OR operation on
// element of subarray of size K

// Function to convert bit array
// to decimal number
function build_num(bit)
{
    let ans = 0;

    for(let i = 0; i < 32; i++)
        if (bit[i] > 0)
            ans += (1 << i);

    return ans;
}

// Function to find  minimum values of
// each bitwise OR operation on
// element of subarray of size K
function minimumOR(arr, n, k)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    let bit = new Array(32);
    bit.fill(0);

    // Create a sliding window of size k
    for(let i = 0; i < k; i++)
    {
        for(let j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    // Function call
    let min_or = build_num(bit);

    for(let i = k; i < n; i++)
    {

        // Perform operation for
        // removed element
        for(let j = 0; j < 32; j++)
        {
            if ((arr[i - k] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for(let j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking minimum value
        min_or = Math.min(build_num(bit), min_or);
    }

    // Return the result
    return min_or;
}

// Driver code

// Given array arr[]
let arr = [ 2, 5, 3, 6, 11, 13 ];

// Given subarray size K
let k = 3;
let n = arr.length;

// Function Call
document.write(minimumOR(arr, n, k));

// This code is contributed by rameshtravel07  

</script>
```

**Output:** 

```
7
```

**时间复杂度:** *O(n * B)* 其中 n 是数组的大小，B 是大小为 32 的整数数组位。
**辅助空间:** *O(n)*

*   下面是寻找 **<u>最大位与子阵</u>** 的程序:

## C++

```
// C++ program for maximum values of
// each bitwise AND operation on
// element of subarray of size K
#include <iostream>
using namespace std;

// Function to convert bit array
// to decimal number
int build_num(int bit[], int k)
{
    int ans = 0;

    for (int i = 0; i < 32; i++)

        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find maximum values of
// each bitwise AND operation on
// element of subarray of size K
int maximumAND(int arr[], int n, int k)
{
    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[32] = { 0 };

    // Create a sliding window of size k
    for (int i = 0; i < k; i++) {
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }
    }

    // Function call
    int max_and = build_num(bit, k);

    for (int i = k; i < n; i++) {

        // Perform operation for
        // removed element
        for (int j = 0; j < 32; j++) {
            if (arr[i - k] & (1 << j))
                bit[j]--;
        }

        // Perform operation for
        // added element
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }

        // Taking maximum value
        max_and = max(build_num(bit, k),
                      max_and);
    }

    // Return the result
    return max_and;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    cout << maximumAND(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for maximum values of
// each bitwise AND operation on
// element of subarray of size K
class GFG{

// Function to convert bit array
// to decimal number
static int build_num(int bit[], int k)
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find maximum values of
// each bitwise AND operation on
// element of subarray of size K
static int maximumAND(int arr[],
                      int n, int k)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[] = new int[32];

    // Create a sliding window of size k
    for(int i = 0; i < k; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    // Function call
    int max_and = build_num(bit, k);

    for(int i = k; i < n; i++)
    {

        // Perform operation for
        // removed element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i - k] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation for
        // added element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking maximum value
        max_and = Math.max(build_num(bit, k),
                           max_and);
    }

    // Return the result
    return max_and;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = arr.length;

    // Function call
    System.out.print(maximumAND(arr, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for maximum values of
# each bitwise AND operation on
# element of subarray of size K

# Function to convert bit array
# to decimal number
def build_num(bit, k):

    ans = 0;

    for i in range(32):
        if (bit[i] == k):
            ans += (1 << i);

    return ans;

# Function to find maximum values of
# each bitwise AND operation on
# element of subarray of size K
def maximumAND(arr, n, k):

    # Maintain an integer array bit
    # of size 32 all initialized to 0
    bit = [0] * 32;

    # Create a sliding window of size k
    for i in range(k):
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

    # Function call
    max_and = build_num(bit, k);

    for i in range(k, n):

        # Perform operation for
        # removed element
        for j in range(32):
            if ((arr[i - k] & (1 << j)) > 0):
                bit[j] -= 1;

        # Perform operation for
        # added element
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

        # Taking maximum value
        max_and = max(build_num(bit, k),
                      max_and);

    # Return the result
    return max_and;

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 2, 5, 3, 6, 11, 13 ];

    # Given subarray size K
    k = 3;
    n = len(arr);

    # Function call
    print(maximumAND(arr, n, k));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for maximum values of
// each bitwise AND operation on
// element of subarray of size K
using System;
class GFG{

    // Function to convert bit
    // array to decimal number
    static int build_num(int[] bit, int k)
    {
        int ans = 0;
          for (int i = 0; i < 32; i++)
            if (bit[i] == k)
                ans += (1 << i);
        return ans;
    }

    // Function to find maximum values of
    // each bitwise AND operation on
    // element of subarray of size K
    static int maximumAND(int[] arr, int n, int k)
    {

        // Maintain an integer array bit[]
        // of size 32 all initialized to 0
        int[] bit = new int[32];

        // Create a sliding window of size k
        for (int i = 0; i < k; i++)
        {
            for (int j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }
        }

        // Function call
        int max_and = build_num(bit, k);

        for (int i = k; i < n; i++)
        {

            // Perform operation for
            // removed element
            for (int j = 0; j < 32; j++)
            {
                if ((arr[i - k] & (1 << j)) > 0)
                    bit[j]--;
            }

            // Perform operation for
            // added element
            for (int j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }

            // Taking maximum value
            max_and = Math.Max(build_num(bit, k),
                               max_and);
        }

        // Return the result
        return max_and;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given array []arr
        int[] arr = {2, 5, 3, 6, 11, 13};

        // Given subarray size K
        int k = 3;
        int n = arr.Length;

        // Function call
        Console.Write(maximumAND(arr, n, k));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // Javascript program for maximum values of
    // each bitwise AND operation on
    // element of subarray of size K

    // Function to convert bit
    // array to decimal number
    function build_num(bit, k)
    {
        let ans = 0;
        for (let i = 0; i < 32; i++)
          if (bit[i] == k)
            ans += (1 << i);
        return ans;
    }

    // Function to find maximum values of
    // each bitwise AND operation on
    // element of subarray of size K
    function maximumAND(arr, n, k)
    {

        // Maintain an integer array bit[]
        // of size 32 all initialized to 0
        let bit = new Array(32);
        bit.fill(0);

        // Create a sliding window of size k
        for (let i = 0; i < k; i++)
        {
            for (let j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }
        }

        // Function call
        let max_and = build_num(bit, k);

        for (let i = k; i < n; i++)
        {

            // Perform operation for
            // removed element
            for (let j = 0; j < 32; j++)
            {
                if ((arr[i - k] & (1 << j)) > 0)
                    bit[j]--;
            }

            // Perform operation for
            // added element
            for (let j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }

            // Taking maximum value
            max_and = Math.max(build_num(bit, k),
                               max_and);
        }

        // Return the result
        return max_and;
    }

    // Given array []arr
    let arr = [2, 5, 3, 6, 11, 13];

    // Given subarray size K
    let k = 3;
    let n = arr.length;

    // Function call
    document.write(maximumAND(arr, n, k));

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** *O(n * B)* 其中 n 是数组的大小，B 是大小为 32 的整数数组位。
T5【辅助空间: *O(n)*

*   下面是寻找 [**<u>最小位与子阵</u>**](https://www.geeksforgeeks.org/bitwise-and-of-sub-array-closest-to-k/) 的程序:

## C++

```
// C++ program for minimum values of
// each bitwise AND operation on
// elements of subarray of size K
#include <iostream>
using namespace std;

// Function to convert bit array
// to decimal number
int build_num(int bit[], int k)
{
    int ans = 0;

    for (int i = 0; i < 32; i++)
        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find minimum values of
// each bitwise AND operation on
// element of subarray of size K
int minimumAND(int arr[], int n, int k)
{
    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[32] = { 0 };

    // Create a sliding window of size k
    for (int i = 0; i < k; i++) {
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }
    }

    // Function call
    int min_and = build_num(bit, k);

    for (int i = k; i < n; i++) {

        // Perform operation to removed
        // element
        for (int j = 0; j < 32; j++) {
            if (arr[i - k] & (1 << j))
                bit[j]--;
        }

        // Perform operation to add
        // element
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }

        // Taking minimum value
        min_and = min(build_num(bit, k),
                      min_and);
    }

    // Return the result
    return min_and;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    cout << minimumAND(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for minimum values of
// each bitwise AND operation on
// elements of subarray of size K
class GFG{

// Function to convert bit array
// to decimal number
static int build_num(int bit[], int k)
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find minimum values of
// each bitwise AND operation on
// element of subarray of size K
static int minimumAND(int arr[], int n, int k)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[] = new int[32];

    // Create a sliding window of size k
    for(int i = 0; i < k; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    // Function call
    int min_and = build_num(bit, k);

    for(int i = k; i < n; i++)
    {

        // Perform operation to removed
        // element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i - k] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation to add
        // element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking minimum value
        min_and = Math.min(build_num(bit, k),
                           min_and);
    }

    // Return the result
    return min_and;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = arr.length;

    // Function call
    System.out.print(minimumAND(arr, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for minimum values of
# each bitwise AND operation on
# elements of subarray of size K

# Function to convert bit array
# to decimal number
def build_num(bit, k):
    ans = 0;

    for i in range(32):
        if (bit[i] == k):
            ans += (1 << i);

    return ans;

# Function to find minimum values of
# each bitwise AND operation on
# element of subarray of size K
def minimumAND(arr, n, k):
    # Maintain an integer array bit
    # of size 32 all initialized to 0
    bit = [0] * 32;

    # Create a sliding window of size k
    for i in range(k):
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

    # Function call
    min_and = build_num(bit, k);

    for i in range(k, n):

        # Perform operation to removed
        # element
        for j in range(32):
            if ((arr[i - k] & (1 << j)) > 0):
                bit[j] -=1;

        # Perform operation to add
        # element
        for j in range(32):
            if ((arr[i] & (1 << j)) > 0):
                bit[j] += 1;

        # Taking minimum value
        min_and = min(build_num(bit, k), min_and);

    # Return the result
    return min_and;

# Driver Code
if __name__ == '__main__':
    # Given array arr
    arr = [2, 5, 3, 6, 11, 13];

    # Given subarray size K
    k = 3;
    n = len(arr);

    # Function call
    print(minimumAND(arr, n, k));

    # This code contributed by Rajput-Ji
```

## C#

```
// C# program for minimum values of
// each bitwise AND operation on
// elements of subarray of size K
using System;

class GFG{

// Function to convert bit array
// to decimal number
static int build_num(int []bit, int k)
{    
    int ans = 0;

    for(int i = 0; i < 32; i++)
        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find minimum values of
// each bitwise AND operation on
// element of subarray of size K
static int minimumAND(int []arr, int n, int k)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int []bit = new int[32];

    // Create a sliding window of size k
    for(int i = 0; i < k; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    // Function call
    int min_and = build_num(bit, k);

    for(int i = k; i < n; i++)
    {

        // Perform operation to removed
        // element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i - k] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation to add
        // element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking minimum value
        min_and = Math.Min(build_num(bit, k),
                           min_and);
    }

    // Return the result
    return min_and;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 2, 5, 3, 6, 11, 13 };

    // Given subarray size K
    int k = 3;
    int n = arr.Length;

    // Function call
    Console.Write(minimumAND(arr, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript program for minimum values of
    // each bitwise AND operation on
    // elements of subarray of size K

    // Function to convert bit array
    // to decimal number
    function build_num(bit, k)
    {   
        let ans = 0;

        for(let i = 0; i < 32; i++)
            if (bit[i] == k)
                ans += (1 << i);

        return ans;
    }

    // Function to find minimum values of
    // each bitwise AND operation on
    // element of subarray of size K
    function minimumAND(arr, n, k)
    {

        // Maintain an integer array bit[]
        // of size 32 all initialized to 0
        let bit = new Array(32);
        bit.fill(0);

        // Create a sliding window of size k
        for(let i = 0; i < k; i++)
        {
            for(let j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }
        }

        // Function call
        let min_and = build_num(bit, k);

        for(let i = k; i < n; i++)
        {

            // Perform operation to removed
            // element
            for(let j = 0; j < 32; j++)
            {
                if ((arr[i - k] & (1 << j)) > 0)
                    bit[j]--;
            }

            // Perform operation to add
            // element
            for(let j = 0; j < 32; j++)
            {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }

            // Taking minimum value
            min_and = Math.min(build_num(bit, k), min_and);
        }

        // Return the result
        return min_and;
    }

    // Given array []arr
    let arr = [ 2, 5, 3, 6, 11, 13 ];

    // Given subarray size K
    let k = 3;
    let n = arr.length;

    // Function call
    document.write(minimumAND(arr, n, k));

</script>
```

**Output:** 

```
0
```

**时间复杂度:** *O(n * B)* 其中 n 是数组的大小，B 是大小为 32 的整数数组位。
T5【辅助空间: *O(n)*

*   下面是寻找 [**<u>最小逐位异或子阵列</u>**T5】的程序:](https://www.geeksforgeeks.org/find-the-subarray-of-size-k-with-minimum-xor/)

## C++

```
// C++ program to find the subarray
/// with minimum XOR
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum XOR
// of the subarray of size K
void findMinXORSubarray(int arr[],
                        int n, int k)
{
    // K must be smaller than
    // or equal to n
    if (n < k)
        return;

    // Initialize the beginning
    // index of result
    int res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    int curr_xor = 0;
    for (int i = 0; i < k; i++)
        curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    int min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for (int i = k; i < n; i++) {

        // XOR with current item
        // and first item of
        // previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k]);

        // Update result if needed
        if (curr_xor < min_xor) {
            min_xor = curr_xor;
            res_index = (i - k + 1);
        }
    }

    // Print the minimum XOR
    cout << min_xor << "\n";
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 7, 90, 20, 10, 50, 40 };

    // Given subarray size K
    int k = 3;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findMinXORSubarray(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the subarray
// with minimum XOR
class GFG{

// Function to find the minimum XOR
// of the subarray of size K
static void findMinXORSubarray(int arr[],
                               int n, int k)
{

    // K must be smaller than
    // or equal to n
    if (n < k)
        return;

    // Initialize the beginning
    // index of result
    int res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    int curr_xor = 0;
    for(int i = 0; i < k; i++)
        curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    int min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for(int i = k; i < n; i++)
    {

        // XOR with current item
        // and first item of
        // previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k]);

        // Update result if needed
        if (curr_xor < min_xor)
        {
            min_xor = curr_xor;
            res_index = (i - k + 1);
        }
    }

    // Print the minimum XOR
    System.out.println(min_xor);
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 3, 7, 90, 20, 10, 50, 40 };

    // Given subarray size K
    int k = 3;
    int n = arr.length;

    // Function call
    findMinXORSubarray(arr, n, k);
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to find the subarray
# with minimum XOR

# Function to find the minimum XOR
# of the subarray of size K
def findMinXORSubarray(arr, n, k):

    # K must be smaller than
    # or equal to n
    if (n < k):
        return;

    # Initialize the beginning
    # index of result
    res_index = 0;

    # Compute XOR sum of first
    # subarray of size K
    curr_xor = 0;
    for i in range(k):
        curr_xor ^= arr[i];

    # Initialize minimum XOR
    # sum as current xor
    min_xor = curr_xor;

    # Traverse from (k+1)'th
    # element to n'th element
    for i in range(k, n):

        # XOR with current item
        # and first item of
        # previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k]);

        # Update result if needed
        if (curr_xor < min_xor):
            min_xor = curr_xor;
            res_index = (i - k + 1);

    # Print the minimum XOR
    print(min_xor);

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [ 3, 7, 90, 20, 10, 50, 40 ];

    # Given subarray size K
    k = 3;
    n = len(arr);

    # Function call
    findMinXORSubarray(arr, n, k);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to find the subarray
// with minimum XOR
using System;
class GFG{

// Function to find the minimum XOR
// of the subarray of size K
static void findMinXORSubarray(int []arr,
                               int n, int k)
{

    // K must be smaller than
    // or equal to n
    if (n < k)
        return;

    // Initialize the beginning
    // index of result
    int res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    int curr_xor = 0;
    for(int i = 0; i < k; i++)
        curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    int min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for(int i = k; i < n; i++)
    {

        // XOR with current item
        // and first item of
        // previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k]);

        // Update result if needed
        if (curr_xor < min_xor)
        {
            min_xor = curr_xor;
            res_index = (i - k + 1);
        }
    }

    // Print the minimum XOR
    Console.WriteLine(min_xor);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 3, 7, 90, 20, 10, 50, 40 };

    // Given subarray size K
    int k = 3;
    int n = arr.Length;

    // Function call
    findMinXORSubarray(arr, n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the subarray
// with minimum XOR

// Function to find the minimum XOR
// of the subarray of size K
function findMinXORSubarray(arr, n, k)
{

    // K must be smaller than
    // or equal to n
    if (n < k)
        return;

    // Initialize the beginning
    // index of result
    let res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    let curr_xor = 0;
    for(let i = 0; i < k; i++)
        curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    let min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for(let i = k; i < n; i++)
    {

        // XOR with current item
        // and first item of
        // previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k]);

        // Update result if needed
        if (curr_xor < min_xor)
        {
            min_xor = curr_xor;
            res_index = (i - k + 1);
        }
    }

    // Print the minimum XOR
    document.write(min_xor);
}

// Driver code

// Given array arr[]
let arr = [ 3, 7, 90, 20, 10, 50, 40 ];

// Given subarray size K
let k = 3;
let n = arr.length;

// Function Call
findMinXORSubarray(arr, n, k);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
16
```

**时间复杂度:** *O(n * B)* 其中 n 是数组的大小，B 是大小为 32 的整数数组位。
T5【辅助空间: *O(n)*