# 递增子阵的最大值和最小值之间的所有差值之和

> 原文:[https://www . geeksforgeeks . org/递增子阵的最大和最小差之和/](https://www.geeksforgeeks.org/sum-of-all-differences-between-maximum-and-minimum-of-increasing-subarrays/)

给定一个由 **N** 个整数组成的数组**arr【】**，任务是找出给定数组中所有严格递增子数组的**最大**和**最小**元素之间的差的和。所有的子阵列都需要处于其最长可能的形式，即如果一个子阵列**【I，j】**形成一个严格递增的子阵列，那么它应该被视为一个整体而不是**【I，k】**和**【k+1，j】**对于某些 **i < = k < = j.**

> 如果对于子阵列中的每一个 i <sup>第</sup>个索引，除了最后一个索引，**arr【I+1】>arr【I】**
> 之外，子阵列被认为是严格递增的

**示例:**

> **输入:** arr[ ] = {7，1，5，3，6，4}
> **输出:** 7
> **解释:**
> 所有可能增加的子阵为{7}、{1，5}、{3，6}和{4}
> 因此，sum =(7–7)+(5–1)+(6–3)+(4–4)= 7
> 
> **输入:** arr[ ] = {1，2，3，4，5，2}
> **输出:** 4
> **解释:**
> 所有可能增加的子阵都是{1，2，3，4，5}和{2}
> 因此，sum =(5–1)+(2–2)= 4

**方法:**
按照以下步骤解决问题:

*   遍历数组，对于每次迭代，找到当前子数组严格增加到的最右边的元素。
*   设 **i** 为当前子阵的起始元素， **j** 为当前子阵严格递增的指标。该子阵列的最大值和最小值分别为**arr【j】**和**arr【I】**。因此，将**(arr[j]–arr[I])**加到**和**中。
*   从 **(j+1) <sup>第</sup>个索引**继续迭代下一个子阵列。
*   完成数组遍历后，打印**和**的最终值。

下面是上述方法的实现:

## C++

```
// C++ Program to find the sum of
// differences of maximum and minimum
// of strictly increasing subarrays

#include <bits/stdc++.h>
using namespace std;

// Function to calculate and return the
// sum of differences of maximum and
// minimum of strictly increasing subarrays
int sum_of_differences(int arr[], int N)
{

    // Stores the sum
    int sum = 0;

    int i, j, flag;

    // Traverse the array
    for (i = 0; i < N - 1; i++) {

        if (arr[i] < arr[i + 1]) {
            flag = 0;

            for (j = i + 1; j < N - 1; j++) {

                // If last element of the
                // increasing sub-array is found
                if (arr[j] >= arr[j + 1]) {

                    // Update sum
                    sum += (arr[j] - arr[i]);

                    i = j;

                    flag = 1;

                    break;
                }
            }

            // If the last element of the array
            // is reached
            if (flag == 0 && arr[i] < arr[N - 1]) {

                // Update sum
                sum += (arr[N - 1] - arr[i]);

                break;
            }
        }
    }

    // Return the sum
    return sum;
}

// Driver Code
int main()
{

    int arr[] = { 6, 1, 2, 5, 3, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << sum_of_differences(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// differences of maximum and minimum
// of strictly increasing subarrays
class GFG{

// Function to calculate and return the
// sum of differences of maximum and
// minimum of strictly increasing subarrays
static int sum_of_differences(int arr[], int N)
{

    // Stores the sum
    int sum = 0;

    int i, j, flag;

    // Traverse the array
    for(i = 0; i < N - 1; i++)
    {
        if (arr[i] < arr[i + 1])
        {
            flag = 0;

            for(j = i + 1; j < N - 1; j++)
            {

                // If last element of the
                // increasing sub-array is found
                if (arr[j] >= arr[j + 1])
                {

                    // Update sum
                    sum += (arr[j] - arr[i]);
                    i = j;
                    flag = 1;

                    break;
                }
            }

            // If the last element of the array
            // is reached
            if (flag == 0 && arr[i] < arr[N - 1])
            {

                // Update sum
                sum += (arr[N - 1] - arr[i]);

                break;
            }
        }
    }

    // Return the sum
    return sum;
}

// Driver Code
public static void main (String []args)
{
    int arr[] = { 6, 1, 2, 5, 3, 4 };

    int N = arr.length;

    System.out.print(sum_of_differences(arr, N));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# differences of maximum and minimum
# of strictly increasing subarrays

# Function to calculate and return the
# sum of differences of maximum and
# minimum of strictly increasing subarrays
def sum_of_differences(arr, N):

    # Stores the sum
    sum = 0

    # Traverse the array
    i = 0
    while(i < N - 1):

        if arr[i] < arr[i + 1]:
            flag = 0

            for j in range(i + 1, N - 1):

                # If last element of the
                # increasing sub-array is found
                if arr[j] >= arr[j + 1]:

                    # Update sum
                    sum += (arr[j] - arr[i])
                    i = j
                    flag = 1

                    break

            # If the last element of the array
            # is reached
            if flag == 0 and arr[i] < arr[N - 1]:

                # Update sum
                sum += (arr[N - 1] - arr[i])
                break

        i += 1

    # Return the sum
    return sum

# Driver Code
arr = [ 6, 1, 2, 5, 3, 4 ]

N = len(arr)

print(sum_of_differences(arr, N))

# This code is contributed by yatinagg
```

## C#

```
// C# program to find the sum of
// differences of maximum and minimum
// of strictly increasing subarrays
using System;
class GFG{

// Function to calculate and return the
// sum of differences of maximum and
// minimum of strictly increasing subarrays
static int sum_of_differences(int []arr, int N)
{

    // Stores the sum
    int sum = 0;

    int i, j, flag;

    // Traverse the array
    for(i = 0; i < N - 1; i++)
    {
        if (arr[i] < arr[i + 1])
        {
            flag = 0;

            for(j = i + 1; j < N - 1; j++)
            {

                // If last element of the
                // increasing sub-array is found
                if (arr[j] >= arr[j + 1])
                {

                    // Update sum
                    sum += (arr[j] - arr[i]);
                    i = j;
                    flag = 1;

                    break;
                }
            }

            // If the last element of the array
            // is reached
            if (flag == 0 && arr[i] < arr[N - 1])
            {

                // Update sum
                sum += (arr[N - 1] - arr[i]);

                break;
            }
        }
    }

    // Return the sum
    return sum;
}

// Driver Code
public static void Main (string []args)
{
    int []arr = { 6, 1, 2, 5, 3, 4 };

    int N = arr.Length;

    Console.Write(sum_of_differences(arr, N));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program to find the sum of
// differences of maximum and minimum
// of strictly increasing subarrays

// Function to calculate and return the
// sum of differences of maximum and
// minimum of strictly increasing subarrays
function sum_of_differences(arr, N)
{

    // Stores the sum
    let sum = 0;

    let i, j, flag;

    // Traverse the array
    for(i = 0; i < N - 1; i++)
    {
        if (arr[i] < arr[i + 1])
        {
            flag = 0;

            for(j = i + 1; j < N - 1; j++)
            {

                // If last element of the
                // increasing sub-array is found
                if (arr[j] >= arr[j + 1])
                {

                    // Update sum
                    sum += (arr[j] - arr[i]);
                    i = j;
                    flag = 1;
                    break;
                }
            }

            // If the last element of the array
            // is reached
            if (flag == 0 && arr[i] < arr[N - 1])
            {

                // Update sum
                sum += (arr[N - 1] - arr[i]);

                break;
            }
        }
    }

    // Return the sum
    return sum;
}

// Driver code
let arr = [ 6, 1, 2, 5, 3, 4 ];

let N = arr.length;

document.write(sum_of_differences(arr, N));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*