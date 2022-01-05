# 修改给定的数组，根据给定的条件用数字的和或积替换每个元素

> 原文:[https://www . geeksforgeeks . org/通过基于给定条件将每个元素替换为其数字的和或积来修改给定数组/](https://www.geeksforgeeks.org/modify-a-given-array-by-replacing-each-element-with-the-sum-or-product-of-their-digits-based-on-a-given-condition/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在对每个数组元素执行以下操作之一后修改数组元素:

*   如果数组元素中偶数数字的[计数](https://www.geeksforgeeks.org/count-even-odd-digits-integer/)大于奇数数字的[计数](https://www.geeksforgeeks.org/count-even-odd-digits-integer/)，那么将该元素更新为该元素所有数字的总和[。](https://www.geeksforgeeks.org/python-program-for-sum-the-digits-of-a-given-number/)
*   否则，将该元素更新为该元素所有数字的乘积。

**示例:**

> **输入:** arr[] = {113，141，214，3186}
> **输出:** 3 4 7 3186
> **解释:**
> 以下是对每个数组元素执行的操作:
> 
> 1.  **对于元素 arr[0](= 113):** 偶数和奇数的计数为 **0** 和 **3** 。作为偶数的计数<奇数的计数，因此将 arr[0](= 113)更新为数字 113 的每个数字的乘积，即 1 * 1 * 3 = 3。
> 2.  **对于元素 arr[1](= 141):** 偶数和奇数的计数为 **1** 和 **2** 。作为偶数的计数<奇数的计数，因此将 arr[1](= 141)更新为数字 141 的每个数字的乘积，即 1 * 4 * 1 = 4。
> 3.  **对于元素 arr[2]:(= 214)** 偶数和奇数位数为 **2** 和 **1** 。作为偶数的计数>奇数的计数，因此将 arr[2](= 214)更新为数字 214 的每个数字的总和，即 2 + 1 + 4 = 7。
> 4.  **对于元素 arr[3](= 3186):** 偶数和奇数的计数为 **2** 和 **2** 。由于偶数的计数与奇数的计数相同，因此不执行任何操作。因此，arr[3](= 3186)保持不变。
> 
> 完成上述操作后，数组将修改为{3，4，7，3186}。
> 
> **输入:** arr[] = {2，7，12，22，110 }
> T3】输出: 2 7 12 4 0

**方法:**给定的问题可以通过对每个数组元素执行给定的操作并相应地打印结果来解决。按照以下步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   [求数组当前元素的偶数和奇数个数](https://www.geeksforgeeks.org/count-even-odd-digits-integer/)。
    *   如果偶数和奇数的计数相同，则不需要执行任何操作。
    *   如果数组元素中偶数数字的[计数](https://www.geeksforgeeks.org/count-even-odd-digits-integer/)大于奇数数字的[计数](https://www.geeksforgeeks.org/count-even-odd-digits-integer/)，那么将该元素更新为该元素所有数字的总和[。](https://www.geeksforgeeks.org/python-program-for-sum-the-digits-of-a-given-number/)
    *   否则，将该元素更新为该元素所有数字的乘积。
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 作为修改后的数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify the given array
// as per the given conditions
void evenOdd(int arr[], int N)
{
    // Traverse the given array arr[]
    for (int i = 0; i < N; i++) {

        // Initialize the count of even
        // and odd digits
        int even_digits = 0;
        int odd_digits = 0;

        // Initialize temp with the
        // current array element
        int temp = arr[i];

        // For count the number of
        // even digits
        while (temp) {

            // Increment the odd count
            if ((temp % 10) & 1)
                odd_digits++;

            // Otherwise
            else
                even_digits++;

            // Divide temp by 10
            temp /= 10;
        }

        // Performe addition
        if (even_digits > odd_digits) {

            int res = 0;
            while (arr[i]) {

                res += arr[i] % 10;
                arr[i] /= 10;
            }
            cout << res << " ";
        }

        // Performe multiplication
        else if (odd_digits > even_digits) {

            int res = 1;
            while (arr[i]) {

                res *= arr[i] % 10;
                arr[i] /= 10;
            }
            cout << res << " ";
        }

        // Otherwise
        else
            cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 113, 141, 214, 3186 };
    int N = sizeof(arr) / sizeof(arr[0]);
    evenOdd(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to modify the given array
    // as per the given conditions
    static void evenOdd(int[] arr, int N)
    {
        // Traverse the given array arr[]
        for (int i = 0; i < N; i++) {

            // Initialize the count of even
            // and odd digits
            int even_digits = 0;
            int odd_digits = 0;

            // Initialize temp with the
            // current array element
            int temp = arr[i];

            // For count the number of
            // even digits
            while (temp > 0) {

                // Increment the odd count
                if ((temp % 10) % 2 != 0)
                    odd_digits++;

                // Otherwise
                else
                    even_digits++;

                // Divide temp by 10
                temp /= 10;
            }

            // Performe addition
            if (even_digits > odd_digits) {

                int res = 0;
                while (arr[i] > 0) {

                    res += arr[i] % 10;
                    arr[i] /= 10;
                }
                System.out.print(res + " ");
            }

            // Performe multiplication
            else if (odd_digits > even_digits) {

                int res = 1;
                while (arr[i] > 0) {

                    res *= arr[i] % 10;
                    arr[i] /= 10;
                }
                System.out.print(res + " ");
            }

            // Otherwise
            else
                System.out.print(arr[i] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 113, 141, 214, 3186 };
        int N = arr.length;
        evenOdd(arr, N);
    }
}

// This code is contributed by rishavmahato348.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to modify the given array
# as per the given conditions
def evenOdd(arr,N):

    # Traverse the given array arr[]
    for i in range(N):

        # Initialize the count of even
        # and odd digits
        even_digits = 0;
        odd_digits = 0;

        # Initialize temp with the
        # current array element
        temp = arr[i];

        # For count the number of
        # even digits
        while (temp):

            # Increment the odd count
            if ((temp % 10) & 1):
                odd_digits += 1;

            # Otherwise
            else:
                even_digits += 1;

            # Divide temp by 10
            temp = temp//10

        # Performe addition
        if (even_digits > odd_digits):

            res = 0;
            while (arr[i]):

                res += arr[i] % 10;
                arr[i] = arr[i]//10;

            print(res, end=" ");

        # Performe multiplication
        elif (odd_digits > even_digits):

            res = 1;
            while (arr[i]):

                res *= arr[i] % 10;
                arr[i] = arr[i]//10

            print(res, end=" ");

        # Otherwise
        else:
            print(arr[i], end=" ");

# Driver Code
arr = [113, 141, 214, 3186 ];
N = len(arr);
evenOdd(arr, N);

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach

using System;

class GFG {

    // Function to modify the given array
    // as per the given conditions
    static void evenOdd(int[] arr, int N)
    {
        // Traverse the given array arr[]
        for (int i = 0; i < N; i++) {

            // Initialize the count of even
            // and odd digits
            int even_digits = 0;
            int odd_digits = 0;

            // Initialize temp with the
            // current array element
            int temp = arr[i];

            // For count the number of
            // even digits
            while (temp > 0) {

                // Increment the odd count
                if ((temp % 10) % 2 != 0)
                    odd_digits++;

                // Otherwise
                else
                    even_digits++;

                // Divide temp by 10
                temp /= 10;
            }

            // Performe addition
            if (even_digits > odd_digits) {

                int res = 0;
                while (arr[i] > 0) {

                    res += arr[i] % 10;
                    arr[i] /= 10;
                }
                Console.Write(res + " ");
            }

            // Performe multiplication
            else if (odd_digits > even_digits) {

                int res = 1;
                while (arr[i] > 0) {

                    res *= arr[i] % 10;
                    arr[i] /= 10;
                }
                Console.Write(res + " ");
            }

            // Otherwise
            else
                Console.Write(arr[i] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 113, 141, 214, 3186 };
        int N = arr.Length;
        evenOdd(arr, N);
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>

 // JavaScript program for the above approach

// Function to modify the given array
// as per the given conditions
function evenOdd(arr,N)
{
    // Traverse the given array arr[]
    for (let i = 0; i < N; i++) {

        // Initialize the count of even
        // and odd digits
        let even_digits = 0;
        let odd_digits = 0;

        // Initialize temp with the
        // current array element
        let temp = arr[i];

        // For count the number of
        // even digits
        while (temp) {

            // Increment the odd count
            if ((temp % 10) & 1)
                odd_digits++;

            // Otherwise
            else
                even_digits++;

            // Divide temp by 10
            temp = parseInt(temp/10)
        }

        // Performe addition
        if (even_digits > odd_digits) {

            let res = 0;
            while (arr[i]) {

                res += arr[i] % 10;
                arr[i] = parseInt(arr[i]/10);
            }
            document.write(res+" ");
        }

        // Performe multiplication
        else if (odd_digits > even_digits) {

            let res = 1;
            while (arr[i]) {

                res *= arr[i] % 10;
                arr[i] = parseInt(arr[i]/10)
            }
            document.write(res+" ");
        }

        // Otherwise
        else
        document.write(arr[i]+" ");
    }
}

// Driver Code

    let  arr = [113, 141, 214, 3186 ];
    let N = arr.length;
    evenOdd(arr, N);

    // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
3 4 7 3186
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)