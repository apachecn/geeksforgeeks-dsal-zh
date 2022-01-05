# 将元素数组连接成单个元素

> 原文:[https://www . geeksforgeeks . org/将元素数组连接成单个元素/](https://www.geeksforgeeks.org/concatenate-the-array-of-elements-into-a-single-element/)

给定一个由 **N** 个整数组成的[数组，](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印通过连接数组元素获得的单个整数值。

**示例**:

> **输入:** arr[] = {1，23，345 }
> T3】输出: 12345
> 
> **输入:** arr[] = {123，45，6，78 }
> T3】输出: 12345678

**方法:**给定的问题可以基于以下观察来解决:

> 1.  Consider **x** and **y** as two integer values to be connected. And the length of the integer **y** is also considered as **l** .
> 2.  Then two integers **x** and **y** can be connected together as follows:
>     *   **X×10 <sup>l</sup> +Y**

按照以下步骤解决问题:

*   初始化一个变量，说 **ans** 为 **0，**存储结果值。
*   [使用变量 **i、**遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，然后在每次迭代中将 **ans** 乘以 **10** 乘以[的幂](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)整数 **arr[i]** 中的[位数，并将 **ans** 增加 **arr[i]。**](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)
*   最后，完成上述步骤后，打印在**和**中获得的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the integer value
// obtained by joining array elements
// together
int ConcatenateArr(int arr[], int N)
{
    // Stores the resulting integer value
    int ans = arr[0];

    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        // Stores the count of digits of
        // arr[i]
        int l = floor(log10(arr[i]) + 1);

        // Update ans
        ans = ans * pow(10, l);

        // Increment ans by arr[i]
        ans += arr[i];
    }
    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 23, 456 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << ConcatenateArr(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the integer value
// obtained by joining array elements
// together
static int ConcatenateArr(int[] arr, int N)
{

    // Stores the resulting integer value
    int ans = arr[0];

    // Traverse the array arr[]
    for(int i = 1; i < N; i++)
    {

        // Stores the count of digits of
        // arr[i]
        int l = (int)Math.floor(Math.log10(arr[i]) + 1);

        // Update ans
        ans = ans * (int)Math.pow(10, l);

        // Increment ans by arr[i]
        ans += arr[i];
    }

    // Return the ans
    return ans;
}

// Driver Code
public static void main(String args[])
{

    // Input
    int arr[] = { 1, 23, 456 };
    int N = arr.length;

    // Function call
    System.out.println(ConcatenateArr(arr, N));
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the integer value
# obtained by joining array elements
# together
def ConcatenateArr(arr,  N):

    # Stores the resulting integer value
    ans = arr[0]

    # Traverse the array arr[]
    for i in range(1,  N):

        # Stores the count of digits of
        # arr[i]
        l = math.floor(math.log10(arr[i]) + 1)

        # Update ans
        ans = ans * math.pow(10, l)

        # Increment ans by arr[i]
        ans += arr[i]

    # Return the ans
    return int( ans)

# Driver Code
if __name__ == "__main__":

    # Input
    arr = [1, 23, 456]
    N = len(arr)

    # Function call
    print(ConcatenateArr(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the integer value
// obtained by joining array elements
// together
static int ConcatenateArr(int[] arr, int N)
{

    // Stores the resulting integer value
    int ans = arr[0];

    // Traverse the array arr[]
    for(int i = 1; i < N; i++)
    {

        // Stores the count of digits of
        // arr[i]
        int l = (int)Math.Floor(Math.Log10(arr[i]) + 1);

        // Update ans
        ans = ans * (int)Math.Pow(10, l);

        // Increment ans by arr[i]
        ans += arr[i];
    }

    // Return the ans
    return ans;
}

// Driver Code
public static void Main()
{
    // Input
    int[] arr = { 1, 23, 456 };
    int N = arr.Length;

    // Function call
    Console.Write(ConcatenateArr(arr, N));

}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to find the integer value
       // obtained by joining array elements
       // together
       function ConcatenateArr(arr, N)
       {

           // Stores the resulting integer value
           let ans = arr[0];

           // Traverse the array arr[]
           for (let i = 1; i < N; i++) {

               // Stores the count of digits of
               // arr[i]
               let l = Math.floor(Math.log10(arr[i]) + 1);

               // Update ans
               ans = ans * Math.pow(10, l);

               // Increment ans by arr[i]
               ans += arr[i];
           }
           // Return the ans
           return ans;
       }

       // Driver Code

       // Input
       let arr = [1, 23, 456];
       let N = arr.length;

       // Function call
       document.write(ConcatenateArr(arr, N));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
123456
```

***时间复杂度:** O(N*log(M))，其中 M 是数组的最大元素。*
***辅助空间:** O(1)*