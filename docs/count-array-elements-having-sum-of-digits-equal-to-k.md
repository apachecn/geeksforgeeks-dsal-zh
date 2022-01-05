# 计数位数总和等于 K 的数组元素

> 原文:[https://www . geesforgeks . org/count-array-elements-having-sum-of-digits-equal-k/](https://www.geeksforgeeks.org/count-array-elements-having-sum-of-digits-equal-to-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算其[位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)等于 **K** 的数组元素的数量。

**示例:**

> ***输入:** arr[] = {23，54，87，29，92，62}，K = 11*
> ***输出:** 2*
> ***解释:***
> *29 = 2+9 = 11*
> *92 = 9+2 = 11*
> 
> ***输入:** arr[]= {11，04，57，99，98，32}，K = 18*
> ***输出:** 1*

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **N** ，来存储数组的大小。
*   初始化一个变量，比如说**计数**，来存储具有等于 **K** 的[数字总和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)的元素。
*   声明一个函数， **sumOfDigits()** 到[计算一个数字的位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素，检查位数之和是否等于 **K** 。如果发现为真，则将**计数**增加 **1** 。
*   打印**的值，将**计为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// sum of digits of the number N
int sumOfDigits(int N)
{
    // Stores the sum of digits
    int sum = 0;
    while (N != 0) {
        sum += N % 10;
        N /= 10;
    }

    // Return the sum
    return sum;
}

// Function to count array elements
int elementsHavingDigitSumK(int arr[], int N, int K)
{
    // Store the count of array
    // elements having sum of digits K
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N; ++i) {

        // If sum of digits is equal to K
        if (sumOfDigits(arr[i]) == K) {

            // Increment the count
            count++;
        }
    }

    // Print the count
    cout << count;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 23, 54, 87, 29, 92, 62 };

    // Given value of K
    int K = 11;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to count array elements
    // having sum of digits equal to K
    elementsHavingDigitSumK(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

    // Function to calculate the
    // sum of digits of the number N
    static int sumOfDigits(int N)
    {

        // Stores the sum of digits
        int sum = 0;
        while (N != 0) {
            sum += N % 10;
            N /= 10;
        }

        // Return the sum
        return sum;
    }

    // Function to count array elements
    static void elementsHavingDigitSumK(int[] arr, int N, int K)
    {

        // Store the count of array
        // elements having sum of digits K
        int count = 0;

        // Traverse the array
        for (int i = 0; i < N; ++i)
        {

            // If sum of digits is equal to K
            if (sumOfDigits(arr[i]) == K)
            {

                // Increment the count
                count++;
            }
        }

        // Print the count
        System.out.println(count);
    } 

  // Driver code
  public static void main(String args[])
  {

    // Given array
    int[] arr = { 23, 54, 87, 29, 92, 62 };

    // Given value of K
    int K = 11;

    // Size of the array
    int N = arr.length;

    // Function call to count array elements
    // having sum of digits equal to K
    elementsHavingDigitSumK(arr, N, K);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the
# sum of digits of the number N
def sumOfDigits(N) :

    # Stores the sum of digits
    sum = 0
    while (N != 0) :
        sum += N % 10
        N //= 10

    # Return the sum
    return sum

# Function to count array elements
def elementsHavingDigitSumK(arr, N, K) :

    # Store the count of array
    # elements having sum of digits K
    count = 0

    # Traverse the array
    for i in range(N):

        # If sum of digits is equal to K
        if (sumOfDigits(arr[i]) == K) :

            # Increment the count
            count += 1

    # Prthe count
    print(count)

# Driver Code

# Given array
arr = [ 23, 54, 87, 29, 92, 62 ]

# Given value of K
K = 11

# Size of the array
N = len(arr)

# Function call to count array elements
# having sum of digits equal to K
elementsHavingDigitSumK(arr, N, K)

# This code is contributed by souravghosh0416.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to calculate the
    // sum of digits of the number N
    static int sumOfDigits(int N)
    {

        // Stores the sum of digits
        int sum = 0;
        while (N != 0) {
            sum += N % 10;
            N /= 10;
        }

        // Return the sum
        return sum;
    }

    // Function to count array elements
    static void elementsHavingDigitSumK(int[] arr, int N, int K)
    {
        // Store the count of array
        // elements having sum of digits K
        int count = 0;

        // Traverse the array
        for (int i = 0; i < N; ++i) {

            // If sum of digits is equal to K
            if (sumOfDigits(arr[i]) == K) {

                // Increment the count
                count++;
            }
        }

        // Print the count
        Console.WriteLine(count);
    } 

  // Driver code
  static void Main()
  {

    // Given array
    int[] arr = { 23, 54, 87, 29, 92, 62 };

    // Given value of K
    int K = 11;

    // Size of the array
    int N = arr.Length;

    // Function call to count array elements
    // having sum of digits equal to K
    elementsHavingDigitSumK(arr, N, K);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to calculate the
    // sum of digits of the number N
    function sumOfDigits(N)
    {

        // Stores the sum of digits
        let sum = 0;
        while (N != 0) {
            sum += N % 10;
            N = parseInt(N / 10, 10);
        }

        // Return the sum
        return sum;
    }

    // Function to count array elements
    function elementsHavingDigitSumK(arr, N, K)
    {
        // Store the count of array
        // elements having sum of digits K
        let count = 0;

        // Traverse the array
        for (let i = 0; i < N; ++i) {

            // If sum of digits is equal to K
            if (sumOfDigits(arr[i]) == K) {

                // Increment the count
                count++;
            }
        }

        // Print the count
        document.write(count);
    }

    // Given array
    let arr = [ 23, 54, 87, 29, 92, 62 ];

    // Given value of K
    let K = 11;

    // Size of the array
    let N = arr.length;

    // Function call to count array elements
    // having sum of digits equal to K
    elementsHavingDigitSumK(arr, N, K);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(1)*