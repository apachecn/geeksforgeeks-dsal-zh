# 最小可能整数 K，使得每个数组元素除以 K 的上限最多为 M

> 原文:[https://www . geeksforgeeks . org/最小可能整数-k 这样每个数组元素的上限除以 k 最多为-m/](https://www.geeksforgeeks.org/smallest-possible-integer-k-such-that-ceil-of-each-array-element-when-divided-by-k-is-at-most-m/)

给定一个由 **N** 个正整数和一个正整数 **M** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到最小可能的整数 **K** ，使得**ceil(arr[0]/K)+ceil(arr[1]/K)+…。+ceil(arr[N–1]/K)**最多为**M**。

**示例:**

> **输入:** arr[] = {4，3，2，7}，M = 5
> **输出:** 4
> **说明:**
> 对于 K = 4，ceil(4/4)+ceil(3/4)+ceil(2/4)+ceil(7/4)= 1+1+1+2 = 5 的值。因此，打印 5。
> 
> **输入:** arr[] = {1，2，3}，M = 4
> T3】输出: 2

**进场:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。从数组**arr【】**中设置**低**值为 **1** 和**高**值为最大值，应用二分搜索法求小于等于 **M** 的 **K** 值。按照以下步骤解决问题:

*   初始化变量，说**低= 1** 和**高**作为[最大阵元](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。
*   [重复一段时间循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到**高–低> 1** 并执行以下任务:
    *   通过 **mid =(低+高)/2** 更新 mid 的值。
    *   [遍历数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，通过假设**中间**为 **K** 求 **ceil(arr[i]/K)** 之和。
    *   如果**之和**大于 **M** ，则将**高**的值更新为**高=中**。否则，将**低**的值更新为**低=中+ 1** 。
*   完成以上步骤后，如果**和**最多为**M**，打印**低值**。否则，打印**高值**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the sum of ceil
// values of the arr[] for the K value
// is at most M or not
bool isvalid(int arr[], int K, int N, int M)
{

    // Stores the sum of ceil values
    int sum = 0;

    for (int i = 0; i < N; i++) {

        // Update the sum
        sum += (int)ceil(arr[i] * 1.0 / K);
    }

    // Return true if sum is less than
    // or equal to M, false otherwise
    return sum <= M;
}

// Function to find the smallest possible
// integer K  such that ceil(arr[0]/K) +
// ceil(arr[1]/K) +....+ ceil(arr[N-1]/K)
// is less than or equal to M
int smallestValueForK(int arr[], int N, int M)
{

    // Stores the low value
    int low = 1;

    // Stores the high value
    int high = *max_element(arr, arr + N);

    // Stores the middle value
    int mid;

    while (high - low > 1) {

        // Update the mid value
        mid = (high + low) / 2;

        // Check if the mid value is K
        if (!isvalid(arr, mid, N, M))

            // Update the low value
            low = mid + 1;
        else

            // Update the high value
            high = mid;
    }

    // Check if low is K or high is K
    // and return it
    return isvalid(arr, low, N, M) ? low : high;
}

// Driver Code
int main()
{

    int arr[] = { 4, 3, 2, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 5;

    cout << smallestValueForK(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to check if the sum of ceil
    // values of the arr[] for the K value
    // is at most M or not
    static boolean isvalid(int[] arr, int K, int N, int M)
    {

        // Stores the sum of ceil values
        int sum = 0;

        for (int i = 0; i < N; i++) {

            // Update the sum
            sum += Math.ceil(arr[i] * 1.0 / K);
        }

        // Return true if sum is less than
        // or equal to M, false otherwise
        return sum <= M;
    }

    // Function to find the smallest possible
    // integer K  such that ceil(arr[0]/K) +
    // ceil(arr[1]/K) +....+ ceil(arr[N-1]/K)
    // is less than or equal to M
    static int smallestValueForK(int[] arr, int N, int M)
    {

        // Stores the low value
        int low = 1;

        // Stores the high value
        int high = arr[0]; 
        //Loop through the array 
        for (int i = 0; i < arr.length; i++) { 
            //Compare elements of array with max 
           if(arr[i] > high) 
               high = arr[i]; 
        } 
        // Stores the middle value
        int mid;

        while (high - low > 1) {

            // Update the mid value
            mid = (high + low) / 2;

            // Check if the mid value is K
            if (isvalid(arr, mid, N, M)==false)

                // Update the low value
                low = mid + 1;
            else

                // Update the high value
                high = mid;
        }

        // Check if low is K or high is K
        // and return it
        return isvalid(arr, low, N, M) ? low : high;
    }

    // Driver Code
    public static void main(String args[])
    {

        int arr[] = { 4, 3, 2, 7 };
        int N = arr.length;
        int M = 5;

        System.out.print(smallestValueForK(arr, N, M));
    }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# python program for the above approach
import math
# Function to check if the sum of ceil
# values of the arr[] for the K value
# is at most M or not

def isvalid(arr, K, N, M):

    # Stores the sum of ceil values
    sum = 0

    for i in range(0, N):

        # Update the sum
        sum += math.ceil(arr[i] * 1.0 / K)

    # Return true if sum is less than
    # or equal to M, false otherwise
    return sum <= M

# Function to find the smallest possible
# integer K such that ceil(arr[0]/K) +
# ceil(arr[1]/K) +....+ ceil(arr[N-1]/K)
# is less than or equal to M
def smallestValueForK(arr, N, M):

    # Stores the low value
    low = 1

    # Stores the high value
    high = arr[0]
    for i in range(1, len(arr)):
        high = max(high, arr[i])

        # Stores the middle value
    mid = 0

    while (high - low > 1):

        # Update the mid value
        mid = (high + low) // 2

        # Check if the mid value is K
        if (not isvalid(arr, mid, N, M)):

                        # Update the low value
            low = mid + 1
        else:

                        # Update the high value
            high = mid

        # Check if low is K or high is K
        # and return it
    if(isvalid(arr, low, N, M)):
        return low
    else:
        return high

# Driver Code
if __name__ == "__main__":

    arr = [4, 3, 2, 7]
    N = len(arr)
    M = 5

    print(smallestValueForK(arr, N, M))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
class GFG {

    // Function to check if the sum of ceil
    // values of the arr[] for the K value
    // is at most M or not
    static bool isvalid(int[] arr, int K, int N, int M)
    {

        // Stores the sum of ceil values
        int sum = 0;

        for (int i = 0; i < N; i++) {

            // Update the sum
            sum += (int)Math.Ceiling(arr[i] * 1.0 / K);
        }

        // Return true if sum is less than
        // or equal to M, false otherwise
        return sum <= M;
    }

    // Function to find the smallest possible
    // integer K  such that ceil(arr[0]/K) +
    // ceil(arr[1]/K) +....+ ceil(arr[N-1]/K)
    // is less than or equal to M
    static int smallestValueForK(int[] arr, int N, int M)
    {

        // Stores the low value
        int low = 1;

        // Stores the high value
        int high = arr.Max();

        // Stores the middle value
        int mid;

        while (high - low > 1) {

            // Update the mid value
            mid = (high + low) / 2;

            // Check if the mid value is K
            if (!isvalid(arr, mid, N, M))

                // Update the low value
                low = mid + 1;
            else

                // Update the high value
                high = mid;
        }

        // Check if low is K or high is K
        // and return it
        return isvalid(arr, low, N, M) ? low : high;
    }

    // Driver Code
    public static void Main()
    {

        int[] arr = { 4, 3, 2, 7 };
        int N = arr.Length;
        int M = 5;

        Console.WriteLine(smallestValueForK(arr, N, M));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to check if the sum of ceil
        // values of the arr[] for the K value
        // is at most M or not
        function isvalid(arr, K, N, M)
        {

            // Stores the sum of ceil values
            let sum = 0;

            for (let i = 0; i < N; i++) {

                // Update the sum
                sum += Math.ceil(arr[i] * 1.0 / K);
            }

            // Return true if sum is less than
            // or equal to M, false otherwise
            return sum <= M;
        }

        // Function to find the smallest possible
        // integer K  such that ceil(arr[0]/K) +
        // ceil(arr[1]/K) +....+ ceil(arr[N-1]/K)
        // is less than or equal to M
        function smallestValueForK(arr, N, M) {

            // Stores the low value
            let low = 1;

            // Stores the high value
            let high = Number.MIN_VALUE;

            for (let i = 0; i < N; i++) {
                high = Math.max(high, arr[i]);
            }

            // Stores the middle value
            let mid;

            while (high - low > 1) {

                // Update the mid value
                mid = (high + low) / 2;

                // Check if the mid value is K
                if (!isvalid(arr, mid, N, M))

                    // Update the low value
                    low = mid + 1;
                else

                    // Update the high value
                    high = mid;
            }

            // Check if low is K or high is K
            // and return it
            return isvalid(arr, low, N, M) ? low : high;
        }

        // Driver Code
        let arr = [4, 3, 2, 7];
        let N = arr.length;
        let M = 5;

        document.write(smallestValueForK(arr, N, M));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*