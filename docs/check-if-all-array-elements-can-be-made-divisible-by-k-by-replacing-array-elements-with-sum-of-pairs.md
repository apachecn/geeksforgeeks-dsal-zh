# 通过将数组元素替换为对的和来检查所有数组元素是否可以被 K 整除

> 原文:[https://www . geesforgeks . org/check-if-all-array-elements-通过用对和替换数组元素可以被 k 整除/](https://www.geeksforgeeks.org/check-if-all-array-elements-can-be-made-divisible-by-k-by-replacing-array-elements-with-sum-of-pairs/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和正整数 **K** ，任务是通过重复选择一对索引 **(i，j)** 并执行 **arr[i] = arr[i] + arr[j]** 来使数组的每个元素可被 **K** 整除。

**示例:**

> **输入:** arr[] = {3，6，3}，K = 6
> **输出:**真
> **解释:**
> 更新 arr[0] = arr[0] + arr[0]。
> 更新 arr[2] = arr[2] + arr[2]
> 
> **输入:** arr[] = {6，6，8，7，3}，K = 6
> T3】输出:假

**方法:**按照以下步骤解决问题:

*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】:
    *   检查 **arr[i]** 是否可以被 **K** 整除:
        *   初始化一个变量，比如说 **temp，**来存储每次迭代后**arr【I】**的值。
        *   重复将**arr【I】**乘以 **2** ，直到**arr【I】<K * temp**。
        *   检查**是否为[i] % K！= 0** 。如果发现是真的，打印**假的**返回。
*   完成以上步骤后，打印 **True** ，因为所有元素现在都可以被 **K** 整除。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Utility function to check if all array
// elements can be made divisible by K or not
bool makeArrayDivisibleByKUtil(
    int arr[], int N, int K)
{
    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Check whether arr[i] is
        // divisible by K or not
        if (arr[i] % K != 0) {

            // Stores value of arr[i]
            int temp = arr[i];

            while (arr[i] < K * temp) {

                // Multiply by 2 until it
                // is less than K * temp
                arr[i] = arr[i] * 2;
            }

            if (arr[i] % K != 0) {
                return false;
            }
        }
    }

    // Return true as all array
    // elements are divisible by K
    return true;
}

// Function to check whether all array
// elements can be made divisible by K or not
void makeArrayDivisibleByK(
    int arr[], int N, int K)
{
    if (makeArrayDivisibleByKUtil(arr, N, K)) {
        cout << "True" << endl;
    }
    else {
        cout << "False" << endl;
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 3, 6, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of K
    int K = 6;

    makeArrayDivisibleByK(arr, N, K);

    return 0;
}
```

## C

```
#include<stdio.h>

// Utility function to check if all array
// elements can be made divisible by K or not
int makeArrayDivisibleByKUtil(
    int arr[], int N, int K)
{

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Check whether arr[i] is
        // divisible by K or not
        if (arr[i] % K != 0)
        {

            // Stores value of arr[i]
            int temp = arr[i];
            while (arr[i] < K * temp)
            {

                // Multiply by 2 until it
                // is less than K * temp
                arr[i] = arr[i] * 2;
            }

            if (arr[i] % K != 0)
            {
                return 0;
            }
        }
    }

    // Return true as all array
    // elements are divisible by K
    return 1;
}

// Function to check whether all array
// elements can be made divisible by K or not
void makeArrayDivisibleByK(
    int arr[], int N, int K)
{
    if (makeArrayDivisibleByKUtil(arr, N, K))
    {
        printf("True\n");
    }
    else
    {
        printf("False\n");
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 3,6,3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of K
    int K = 6;
    makeArrayDivisibleByK(arr, N, K);
    return 0;
}

// This code is contributed by santoshcharan.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
class GFG
{
    public static boolean makeArrayDivisibleBykUtil(int arr[],
                                                    int n,int k)
    {

        // Traverse the array
        for(int i = 0; i < n; i++)
        {

            // Check whether arr[i] is
            // divisible by k or not
            if(arr[i] % k != 0)
            {

                // Stores value of arr[i]
                int temp = arr[i];
                while(arr[i] < k * arr[i])
                {

                    // Multiply by 2 until it
                    // is less than k*temp
                    arr[i] = arr[i] * 2;
                }
                if(arr[i] % k != 0)
                {
                    return false;
                }
            }
        }

        // Return true as all array
        // elements are divisible by k
        return true;
    }
    public static void makeArrayDivisibleByk(int arr[],
                                             int n,int k)
    {
        if(makeArrayDivisibleBykUtil(arr, n, k))
        {
            System.out.println("True");
        }
        else
        {
            System.out.println("False");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array   
        int[] arr = { 3 , 6 , 3};

        // Size of the array
        int n = 3;
        int k = 6;

        // Calling the function
        makeArrayDivisibleByk(arr, n, k);
    }
}

// This code is contributed by santoshcharan.
```

## 蟒蛇 3

```
# Python 3 Program for the above approach

# Utility function to check if all array
# elements can be made divisible by K or not
def makeArrayDivisibleByKUtil(arr, N, K):

  # Traverse the array
  for i in range(N):

    # Check whether arr[i] is
    # divisible by K or not
    if (arr[i] % K != 0):

      # Stores value of arr[i]
      temp = arr[i]
      while (arr[i] < K * temp):

        # Multiply by 2 until it
        # is less than K * temp
        arr[i] = arr[i] * 2
      if (arr[i] % K != 0):
        return False

  # Return true as all array
  # elements are divisible by K
  return True

# Function to check whether all array
# elements can be made divisible by K or not
def makeArrayDivisibleByK(arr, N, K):
  if (makeArrayDivisibleByKUtil(arr, N, K)):
    print("True")
  else:
    print("False")

# Driver Code
if __name__ == '__main__':

  # Given array
  arr =  [3, 6, 3]

  # Size of the array
  N =  len(arr)

  # Given value of K
  K = 6
  makeArrayDivisibleByK(arr, N, K)

  # This code is contributed by bgangwar59.
```

## C#

```
using System;

class GFG
{
  public static bool makeArrayDivisibleBykUtil(int [] arr,
                                               int n,int k)
  {

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

      // Check whether arr[i] is
      // divisible by k or not
      if(arr[i] % k != 0)
      {

        // Stores value of arr[i]
        //int temp = arr[i];
        while(arr[i] < k * arr[i])
        {

          // Multiply by 2 until it
          // is less than k*temp
          arr[i] = arr[i] * 2;
        }
        if(arr[i] % k != 0)
        {
          return false;
        }
      }
    }

    // Return true as all array
    // elements are divisible by k
    return true;
  }
  public static void makeArrayDivisibleByk(int []arr,
                                           int n,int k)
  {
    if(makeArrayDivisibleBykUtil(arr, n, k))
    {
      Console.WriteLine("True");
    }
    else
    {
      Console.WriteLine("False");
    }
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Given array   
    int[] arr = { 3 , 6 , 3};

    // Size of the array
    int n = 3;
    int k = 6;

    // Calling the function
    makeArrayDivisibleByk(arr, n, k);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// Javascript Program for the above approach

// Utility function to check if all array
// elements can be made divisible by K or not
function makeArrayDivisibleByKUtil(arr, N, K)
{

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Check whether arr[i] is
        // divisible by K or not
        if (arr[i] % K != 0)
        {

            // Stores value of arr[i]
            let temp = arr[i];

            while (arr[i] < K * temp)
            {

                // Multiply by 2 until it
                // is less than K * temp
                arr[i] = arr[i] * 2;
            }

            if (arr[i] % K != 0)
            {
                return false;
            }
        }
    }

    // Return true as all array
    // elements are divisible by K
    return true;
}

// Function to check whether all array
// elements can be made divisible by K or not
function makeArrayDivisibleByK(arr, N, K)
{
    if (makeArrayDivisibleByKUtil(arr, N, K))
    {
        document.write("True<br>");
    }
    else
    {
        document.write("False<br>");
    }
}

// Driver Code

// Given array
let arr = [ 3, 6, 3 ];

// Size of the array
let N = arr.length;

// Given value of K
let K = 6;

makeArrayDivisibleByK(arr, N, K);

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
True
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(1)*