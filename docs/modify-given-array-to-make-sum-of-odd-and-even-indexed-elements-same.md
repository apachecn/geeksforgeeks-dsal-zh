# 修改给定数组，使奇数和偶数索引元素的和相同

> 原文:[https://www . geesforgeks . org/modify-给定数组对奇数和偶数索引元素求和-相同/](https://www.geeksforgeeks.org/modify-given-array-to-make-sum-of-odd-and-even-indexed-elements-same/)

给定大小为 **N** 的二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，从数组中最多移除 **N/2** 个元素，使得奇数和偶数索引处的元素之和相等。任务是打印修改后的数组。
***注:** N 永远是偶数。可以有多个可能的结果，打印其中任何一个。*

**示例:**

> **输入:** arr[] = {1，1，1，0}
> **输出:** 1 1
> **解释:**
> 对于给定数组 arr[] = {1，1，1，0}
> 奇数位置元素之和，**Odd _ Sum**= arr[1]+arr[3]= 1+1 = 2。
> 偶位置元素之和，**偶 _ 和** = arr[2] + arr[4] = 1 + 0 = 1。
> 由于**奇数 _ 和** & **偶数 _ 和**不相等，去掉一些元素使其相等。
> 在移除 arr[3]和 arr[4]之后，数组变为 arr[] = {1，1}，使得奇数索引和偶数索引处的元素之和相等。
> 
> **输入:** arr[] = {1，0}
> **输出:** 0
> **解释:**
> 对于给定的数组 arr[] = {1，0}
> 奇数位置的元素之和， **Odd_Sum** = arr[1] = 0 = 0。
> 偶位置元素之和，**偶 _ 和** = 1 = 1。
> 由于**奇数 _ 和** & **偶数 _ 和**不相等，去掉一些元素使其相等。
> 移除 arr[0]后，数组变为 arr[] = {0}，使得奇数索引和偶数索引处的元素之和相等。

**方法:**思路是[统计给定数组中 **1s**](https://www.geeksforgeeks.org/count-1s-sorted-binary-array/) 和 **0s** 的个数，然后通过以下步骤使结果和相等:

1.  计算给定数组**arr【】**中 **0s** 和 **1s** 的数量，并将它们分别存储在变量 count_0 和 count_1 中。
2.  如果奇数和偶数索引处的元素之和相等，则无需移除任何数组元素。打印原始数组作为答案。
3.  如果 **count_0 ≥ N/2** ，则去掉所有的 **1** s，打印所有的零 **count_0** 次。
4.  否则，如果 **count_0 < N/2** ，通过去掉所有的 **0** s，可以使偶数和奇数指数之和按照以下条件相同:
    *   如果 **count_1 为奇数**，则打印 **1** 作为新数组**的元素(count _ 1–1)**次。
    *   否则，打印 **1** 作为新数组**的元素计数 _1** 的次数。
5.  根据上述条件打印结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to modify array to make
// sum of odd and even indexed
// elements equal
void makeArraySumEqual(int a[], int N)
{

    // Stores the count of 0s, 1s
    int count_0 = 0, count_1 = 0;

    // Stores sum of odd and even
    // indexed elements respectively
    int odd_sum = 0, even_sum = 0;

    for (int i = 0; i < N; i++) {

        // Count 0s
        if (a[i] == 0)
            count_0++;

        // Count 1s
        else
            count_1++;

        // Calculate odd_sum and even_sum
        if ((i + 1) % 2 == 0)
            even_sum += a[i];

        else if ((i + 1) % 2 > 0)
            odd_sum += a[i];
    }

    // If both are equal
    if (odd_sum == even_sum) {

        // Print the original array
        for (int i = 0; i < N; i++)
            cout <<" "<< a[i];
    }

    // Otherwise
    else {

        if (count_0 >= N / 2) {

            // Print all the 0s
            for (int i = 0; i < count_0; i++)
                cout <<"0 ";
        }
        else {

            // For checking even or odd
            int is_Odd = count_1 % 2;

            // Update total count of 1s
            count_1 -= is_Odd;

            // Print all 1s
            for (int i = 0; i < count_1; i++)
                cout <<"1 ";
        }
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 1, 1, 0 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    makeArraySumEqual(arr, N);

    return 0;
}

// This code is contributed by shivanisinghss2110.
```

## C

```
// C++ program for the above approach

#include <stdio.h>

// Function to modify array to make
// sum of odd and even indexed
// elements equal
void makeArraySumEqual(int a[], int N)
{
    // Stores the count of 0s, 1s
    int count_0 = 0, count_1 = 0;

    // Stores sum of odd and even
    // indexed elements respectively
    int odd_sum = 0, even_sum = 0;

    for (int i = 0; i < N; i++) {

        // Count 0s
        if (a[i] == 0)
            count_0++;

        // Count 1s
        else
            count_1++;

        // Calculate odd_sum and even_sum
        if ((i + 1) % 2 == 0)
            even_sum += a[i];

        else if ((i + 1) % 2 > 0)
            odd_sum += a[i];
    }

    // If both are equal
    if (odd_sum == even_sum) {

        // Print the original array
        for (int i = 0; i < N; i++)
            printf("%d ", a[i]);
    }

    // Otherwise
    else {

        if (count_0 >= N / 2) {

            // Print all the 0s
            for (int i = 0; i < count_0; i++)
                printf("0 ");
        }
        else {

            // For checking even or odd
            int is_Odd = count_1 % 2;

            // Update total count of 1s
            count_1 -= is_Odd;

            // Print all 1s
            for (int i = 0; i < count_1; i++)
                printf("1 ");
        }
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 1, 1, 0 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    makeArraySumEqual(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to modify array to make
    // sum of odd and even indexed
    // elements equal
    static void makeArraySumEqual(int a[], int N)
    {
        // Stores the count of 0s, 1s
        int count_0 = 0, count_1 = 0;

        // Stores sum of odd and even
        // indexed elements respectively
        int odd_sum = 0, even_sum = 0;

        for (int i = 0; i < N; i++) {

            // Count 0s
            if (a[i] == 0)
                count_0++;

            // Count 1s
            else
                count_1++;

            // Calculate odd_sum and even_sum
            if ((i + 1) % 2 == 0)
                even_sum += a[i];

            else if ((i + 1) % 2 > 0)
                odd_sum += a[i];
        }

        // If both are equal
        if (odd_sum == even_sum) {

            // Print the original array
            for (int i = 0; i < N; i++)
                System.out.print(a[i] + " ");
        }

        else
        {
            if (count_0 >= N / 2) {

                // Print all the 0s
                for (int i = 0; i < count_0; i++)
                    System.out.print("0 ");
            }
            else {

                // For checking even or odd
                int is_Odd = count_1 % 2;

                // Update total count of 1s
                count_1 -= is_Odd;

                // Print all 1s
                for (int i = 0; i < count_1; i++)
                    System.out.print("1 ");
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array arr[]
        int arr[] = { 1, 1, 1, 0 };

        int N = arr.length;

        // Function Call
        makeArraySumEqual(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to modify array to make
# sum of odd and even indexed
# elements equal
def makeArraySumEqual(a, N):

    # Stores the count of 0s, 1s
    count_0 = 0
    count_1 = 0

    # Stores sum of odd and even
    # indexed elements respectively
    odd_sum = 0
    even_sum = 0

    for i in range(N):

        # Count 0s
        if (a[i] == 0):
            count_0 += 1

        # Count 1s
        else:
            count_1 += 1

        # Calculate odd_sum and even_sum
        if ((i + 1) % 2 == 0):
            even_sum += a[i]

        elif ((i + 1) % 2 > 0):
            odd_sum += a[i]

    # If both are equal
    if (odd_sum == even_sum):

        # Print the original array
        for i in range(N):
            print(a[i], end = " ")

    # Otherwise
    else:
        if (count_0 >= N / 2):

            # Print all the 0s
            for i in range(count_0):
                print("0", end = " ")

        else:

            # For checking even or odd
            is_Odd = count_1 % 2

            # Update total count of 1s
            count_1 -= is_Odd

            # Print all 1s
            for i in range(count_1):
                print("1", end = " ")

# Driver Code

# Given array arr[]
arr = [ 1, 1, 1, 0 ]

N = len(arr)

# Function call
makeArraySumEqual(arr, N)

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to modify array to make
// sum of odd and even indexed
// elements equal
static void makeArraySumEqual(int []a,
                              int N)
{
  // Stores the count of 0s, 1s
  int count_0 = 0, count_1 = 0;

  // Stores sum of odd and even
  // indexed elements respectively
  int odd_sum = 0, even_sum = 0;

  for (int i = 0; i < N; i++)
  {
    // Count 0s
    if (a[i] == 0)
      count_0++;

    // Count 1s
    else
      count_1++;

    // Calculate odd_sum and even_sum
    if ((i + 1) % 2 == 0)
      even_sum += a[i];

    else if ((i + 1) % 2 > 0)
      odd_sum += a[i];
  }

  // If both are equal
  if (odd_sum == even_sum)
  {
    // Print the original array
    for (int i = 0; i < N; i++)
      Console.Write(a[i] + " ");
  }
  else
  {
    if (count_0 >= N / 2)
    {
      // Print all the 0s
      for (int i = 0; i < count_0; i++)
        Console.Write("0 ");
    }
    else
    {
      // For checking even or odd
      int is_Odd = count_1 % 2;

      // Update total count of 1s
      count_1 -= is_Odd;

      // Print all 1s
      for (int i = 0; i < count_1; i++)
        Console.Write("1 ");
    }
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 1, 1, 0};

  int N = arr.Length;

  // Function Call
  makeArraySumEqual(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to modify array to make
    // sum of odd and even indexed
    // elements equal
    function makeArraySumEqual(a, N)
    {
        // Stores the count of 0s, 1s
        let count_0 = 0, count_1 = 0;

        // Stores sum of odd and even
        // indexed elements respectively
        let odd_sum = 0, even_sum = 0;

        for (let i = 0; i < N; i++) {

            // Count 0s
            if (a[i] == 0)
                count_0++;

            // Count 1s
            else
                count_1++;

            // Calculate odd_sum and even_sum
            if ((i + 1) % 2 == 0)
                even_sum += a[i];

            else if ((i + 1) % 2 > 0)
                odd_sum += a[i];
        }

        // If both are equal
        if (odd_sum == even_sum) {

            // Print the original array
            for (let i = 0; i < N; i++)
                document.write(a[i] + " ");
        }

        else
        {
            if (count_0 >= N / 2) {

                // Print all the 0s
                for (let i = 0; i < count_0; i++)
                    document.write("0 ");
            }
            else {

                // For checking even or odd
                let is_Odd = count_1 % 2;

                // Update total count of 1s
                count_1 -= is_Odd;

                // Print all 1s
                for (let i = 0; i < count_1; i++)
                    document.write("1 ");
            }
        }
    }

// Driver Code

    // Given array arr[]
        let arr = [ 1, 1, 1, 0 ];

        let N = arr.length;

        // Function Call
        makeArraySumEqual(arr, N);

</script>
```

**Output:** 

```
1 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)