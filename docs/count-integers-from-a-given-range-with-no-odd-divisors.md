# 计算给定范围内没有奇数除数的整数

> 原文:[https://www . geeksforgeeks . org/count-整数-从给定范围-不带奇数除数/](https://www.geeksforgeeks.org/count-integers-from-a-given-range-with-no-odd-divisors/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算不包含任何[个奇数因子](https://www.geeksforgeeks.org/find-sum-odd-factors-number/)的**【1，arr[I]】**范围内的整数个数。

**示例:**

> **输入:** arr[] = {15，16，20，35}
> **输出:** 3 4 4 5
> **解释:**
> 从 **1** 到 **arr[0] ( = 15)** 的无奇数除数，是 2，4，8。因此，计数为 3。
> 同样，对于 arr[1] (= 16)、arr[2] (= 20)、arr[3] (= 35)，计数分别为 4、4 和 5。
> 
> **输入:**arr[]= { 24 }
> T3】输出: 4

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素 **arr[i]** ，检查一个数在**【1，arr[I]】**范围内是否有奇数除数。如果它没有任何奇数除数，则递增计数。否则，继续下一个整数。最后，打印每个数组元素**arr【I】**获得的计数。
***时间复杂度:**O(N * max(arr[I])*
***辅助空间:** O(1)*

**高效方法:**最优思想基于以下观察:

**观察:**

> 任何数字都可以用 p<sub>1</sub><sup>x</sup><sub>T5】1</sub>* p<sub>2</sub><sup>x</sup><sub><sup>2</sup>T15】*---* p<sub>N</sub><sup>x</sup><sub>T21】N</sub>的形式表示，其中 p <sub>i</sub> 是一个[质数](https://www.geeksforgeeks.org/prime-numbers/)如果这个数没有任何奇数除数，那么**就不应该包含任何奇数质因数**。</sub>

因此，问题简化为寻找范围 **1** 到 **N** 内的整数的计数，使得这些数是两个的[次幂，这可以通过重复检查两个](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)的[次幂使得 **2 <sup>i</sup> ≤ N** 并在每一步中增加计数来以对数(N)时间复杂度完成。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

按照以下步骤解决问题:

*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并执行以下操作:
    *   初始化两个变量，比如说 **powerOfTwo** ，检查小于**arr【I】**的 **2** 的最大功率，另一个变量，比如说 **count** ，存储没有奇数除数的**【1，arr【I】】**范围内的整数个数。
    *   对于每个数组元素，求两个和**的**幂的值，计算**。**
    *   打印它们作为每个数组元素的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count integers in the
// range 1 to N having no odd divisors
void oddDivisors(int arr[], int N)
{
    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores the nearest power
        // of two less than arr[i]
        int powerOfTwo = 2;

        // Stores the count of integers
        // with no odd divisor for each query
        int count = 0;

        // Iterate until powerOfTwo is
        // less then or equal to arr[i]
        while (powerOfTwo <= arr[i]) {

            count++;
            powerOfTwo = 2 * powerOfTwo;
        }

        // Print the answer for
        // the current element
        cout << count << " ";
    }

    return;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 15, 16, 20, 35 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    oddDivisors(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count integers in the
// range 1 to N having no odd divisors
static void oddDivisors(int arr[], int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Stores the nearest power
        // of two less than arr[i]
        int powerOfTwo = 2;

        // Stores the count of integers
        // with no odd divisor for each query
        int count = 0;

        // Iterate until powerOfTwo is
        // less then or equal to arr[i]
        while (powerOfTwo <= arr[i])
        {
            count++;
            powerOfTwo = 2 * powerOfTwo;
        }

        // Print the answer for
        // the current element
        System.out.print(count + " ");
    }
    return;
}

// Driver Code
public static void main(String args[])
{
    // Given array
    int arr[] = { 15, 16, 20, 35 };

    // Size of the array
    int N = arr.length;
    oddDivisors(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count integers in the
# range 1 to N having no odd divisors
def oddDivisors(arr, N) :

    # Traverse the array
    for i in range(N) :

        # Stores the nearest power
        # of two less than arr[i]
        powerOfTwo = 2;

        # Stores the count of integers
        # with no odd divisor for each query
        count = 0;

        # Iterate until powerOfTwo is
        # less then or equal to arr[i]
        while (powerOfTwo <= arr[i]) :

            count += 1;
            powerOfTwo = 2 * powerOfTwo;

        # Print the answer for
        # the current element
        print(count, end = " ");

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 15, 16, 20, 35 ];

    # Size of the array
    N = len(arr);

    oddDivisors(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to count integers in the
// range 1 to N having no odd divisors
static void oddDivisors(int[] arr, int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Stores the nearest power
        // of two less than arr[i]
        int powerOfTwo = 2;

        // Stores the count of integers
        // with no odd divisor for each query
        int count = 0;

        // Iterate until powerOfTwo is
        // less then or equal to arr[i]
        while (powerOfTwo <= arr[i])
        {
            count++;
            powerOfTwo = 2 * powerOfTwo;
        }

        // Print the answer for
        // the current element
        Console.Write(count + " ");
    }
    return;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int[] arr = { 15, 16, 20, 35 };

    // Size of the array
    int N = arr.Length;
    oddDivisors(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Function to count integers in the
    // range 1 to N having no odd divisors
    function oddDivisors(arr , N) {

        // Traverse the array
        for (i = 0; i < N; i++) {

            // Stores the nearest power
            // of two less than arr[i]
            var powerOfTwo = 2;

            // Stores the count of integers
            // with no odd divisor for each query
            var count = 0;

            // Iterate until powerOfTwo is
            // less then or equal to arr[i]
            while (powerOfTwo <= arr[i]) {
                count++;
                powerOfTwo = 2 * powerOfTwo;
            }

            // Print the answer for
            // the current element
            document.write(count + " ");
        }
        return;
    }

    // Driver Code

        // Given array
        var arr = [ 15, 16, 20, 35 ];

        // Size of the array
        var N = arr.length;
        oddDivisors(arr, N);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
3 4 4 5
```

***时间复杂度:**O(N * log(max(arr[I])*
***辅助空间:** O(1)*