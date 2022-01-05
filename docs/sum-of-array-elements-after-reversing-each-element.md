# 每个元素反转后的数组元素之和

> 原文:[https://www . geeksforgeeks . org/每个元素反转后的数组元素总和/](https://www.geeksforgeeks.org/sum-of-array-elements-after-reversing-each-element/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在每个数组元素的[个反转数字后，找到所有数组元素](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)的[个和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {7，234，58100}
> **输出:** 18939
> **解释:**
> 每个数组元素反转后的修改数组= {7，432，18500}。
> 因此，修改后数组的和= 7 + 432 + 18500 = 18939。
> 
> **输入:** arr[] = {0，100，220}
> **输出:** 320
> **解释:**
> 将每个数组元素反转后的修改数组= {0，100，220}。
> 因此，修改后的数组之和= 0 + 100 + 220 = 320。

**逼近:**思路是[按照给定的条件对给定数组的每个数](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)进行反转，求反转后形成的所有数组元素的[和。以下是解决问题的步骤:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

1.  初始化一个变量，比如**和**，来存储需要的和。
2.  初始化变量**将**计数为 **0** 并将 **f** 计数为**假**以存储**arr【I】**的结束 **0** s 的计数并标记以避免所有非结束 **0** 。
3.  将 **rev** 初始化为 **0** 来存储每个数组元素的反转。
4.  [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对每个数组元素执行以下操作:
    *   递增**计数**并将**arr【I】**除以 10，直到遍历完末尾的所有零。
    *   将 **f** 重置为真，表示已经考虑了所有以 0 结尾的数字。
    *   现在，通过更新 **rev = rev*10 + arr[i] % 10** 和 **arr[i] = arr[i]/10** 来反转 **arr[i]** 。
    *   遍历 arr[i]的每个数字后，更新 **rev = rev * Math.pow(10，计数)**将所有以 0 结尾的数字加到反转数字的末尾。
5.  对于上述步骤中的每个反向数，将该值加到合成的**和**中。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of elements
// after reversing each element in arr[]
void totalSum(int arr[], int n)
{

    // Stores the final sum
    int sum = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // Stores count of ending 0s
        int count = 0;

        int rev = 0, num = arr[i];

        // Flag to avoid count of 0s
        // that doesn't ends with 0s
        bool f = false;

        while (num > 0)
        {

            // Count of ending 0s
            while (num > 0 && !f &&
                   num % 10 == 0)
            {
                count++;
                num = num / 10;
            }

            // Update flag with true
            f = true;

            // Reversing the num
            if (num > 0)
            {
                rev = rev * 10 +
                      num % 10;

                num = num / 10;
            }
        }

        // Add all ending 0s to
        // end of rev
        if (count > 0)
            rev = rev * pow(10, count);

        // Update sum
        sum = sum + rev;
    }

    // Print total sum
    cout << sum;
}

// Driver Code
int main()
{

    // Given arr[]
    int arr[] = { 7, 234, 58100 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    totalSum(arr, n);

    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the sum of elements
    // after reversing each element in arr[]
    static void totalSum(int[] arr)
    {
        // Stores the final sum
        int sum = 0;

        // Traverse the given array
        for (int i = 0;
            i < arr.length; i++) {

            // Stores count of ending 0s
            int count = 0;

            int rev = 0, num = arr[i];

            // Flag to avoid count of 0s
            // that doesn't ends with 0s
            boolean f = false;

            while (num > 0) {

                // Count of ending 0s
                while (num > 0 && !f
                    && num % 10 == 0) {
                    count++;
                    num = num / 10;
                }

                // Update flag with true
                f = true;

                // Reversing the num
                if (num > 0) {
                    rev = rev * 10
                        + num % 10;

                    num = num / 10;
                }
            }

            // Add all ending 0s to
            // end of rev
            if (count > 0)
                rev = rev
                    * (int)Math.pow(10,
                                    count);

            // Update sum
            sum = sum + rev;
        }

        // Print total sum
        System.out.print(sum);
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given arr[]
        int[] arr = { 7, 234, 58100 };

        // Function Call
        totalSum(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of elements
# after reversing each element in arr[]
def totalSum(arr, n):

    # Stores the final sum
    sums = 0

    # Traverse the given array
    for i in range(0, n):

        # Stores count of ending 0s
        count = 0

        rev = 0
        num = arr[i]

        # Flag to avoid count of 0s
        # that doesn't ends with 0s
        f = False

        while num > 0:

            # Count of ending 0s
            while (num > 0 and f == False and
                   num % 10 == 0):
                count = count + 1
                num = num // 10

            # Update flag with true
            f = True

            # Reversing the num
            if num > 0:
                rev = rev * 10 + num % 10
                num = num // 10

        # Add all ending 0s to
        # end of rev
        if (count > 0):
            rev = rev * pow(10, count)

            # Update sum
        sums = sums + rev

    # Print total sum
    print(sums)

# Driver Code
if __name__ == "__main__":

    # Given arr[]
    arr = [ 7, 234, 58100 ]

    n = len(arr)

    # Function call
    totalSum(arr, n)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the sum of elements
// after reversing each element in arr[]
static void totalSum(int[] arr)
{

    // Stores the final sum
    int sum = 0;

    // Traverse the given array
    for(int i = 0; i < arr.Length; i++)
    {

        // Stores count of ending 0s
        int count = 0;

        int rev = 0, num = arr[i];

        // Flag to avoid count of 0s
        // that doesn't ends with 0s
        bool f = false;

        while (num > 0)
        {

            // Count of ending 0s
            while (num > 0 && !f &&
                   num % 10 == 0)
            {
                count++;
                num = num / 10;
            }

            // Update flag with true
            f = true;

            // Reversing the num
            if (num > 0)
            {
                rev = rev * 10 +
                      num % 10;

                num = num / 10;
            }
        }

        // Add all ending 0s to
        // end of rev
        if (count > 0)
            rev = rev * (int)Math.Pow(10, count);

        // Update sum
        sum = sum + rev;
    }

    // Print total sum
    Console.Write(sum);
}

// Driver Code
static public void Main()
{

    // Given arr[]
    int[] arr = { 7, 234, 58100 };

    // Function call
    totalSum(arr);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the sum of elements
// after reversing each element in arr[]
function totalSum(arr, n)
{

    // Stores the final sum
    let sum = 0;

    // Traverse the given array
    for(let i = 0; i < n; i++)
    {

        // Stores count of ending 0s
        let count = 0;

        let rev = 0, num = arr[i];

        // Flag to avoid count of 0s
        // that doesn't ends with 0s
        let f = false;

        while (num > 0)
        {

            // Count of ending 0s
            while (num > 0 && !f &&
                num % 10 == 0)
            {
                count++;
                num = Math.floor(num / 10);
            }

            // Update flag with true
            f = true;

            // Reversing the num
            if (num > 0)
            {
                rev = rev * 10 +
                    num % 10;

                num = Math.floor(num / 10);
            }
        }

        // Add all ending 0s to
        // end of rev
        if (count > 0)
            rev = rev * Math.pow(10, count);

        // Update sum
        sum = sum + rev;
    }

    // Print total sum
    document.write(sum);
}

// Driver Code

    // Given arr[]
    let arr = [ 7, 234, 58100 ];

    let n = arr.length;

    // Function call
    totalSum(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
18939
```

***时间复杂度:** O(N*log <sub>10</sub> M，其中 N 表示数组长度，M 表示最大数组元素。*
***辅助空间:** O(1)*