# 通过将数组元素的数字右移至超过 K 的值来修改数组

> 原文:[https://www . geesforgeks . org/通过右移将数组元素的数字修改为超过-k 的值/](https://www.geeksforgeeks.org/modify-array-by-right-shifting-digits-of-array-elements-to-values-exceeding-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K** ，任务是通过对数组元素执行右移位操作来使所有数组元素 **> K** 。
**注:**如果无法制作所有数组元素 **> K** ，则打印 **-1** 。

**示例:**

> **输入:** arr[] = { 21，22，23，19 }，K = 24
> **输出:** { 26，26，27，25 }
> **解释:**
> arr[0] = 10101。执行 1 次右移-→ 11010 → 26
> arr[1] = 10110。执行 3 次右移→ 11010 → 26
> arr[2] = 10111。执行 1 次右移→ 11011 → 27
> arr[3] = 10011。执行 2 次右移→ 11001 → 25
> 
> **输入:** arr[] = { 45，37，54，46，62 }，K = 48
> **输出:** { 54，50，54，53，62 }

**方法:**按照以下步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
2.  对每个数组元素**arr【I】**的数字执行[右移操作](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)。
3.  如果**arr【I】>k**，更新**arr【I】**[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
4.  如果任何数组元素 **arr[i] ≤ K，**则打印 **-1**
5.  否则，[打印数组](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/) **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find
// MSB of a number
int setBitNumber(int n)
{

    // Stores the position of the
    // most significant set bit
    int k = log2(n);

    // Return the position of the
    // most significant set bit
    return k;
}

// Function to check if all array
// elements are exceeding k or not
bool check(int arr[], int k, int n)
{

    // Traverse the array arr
    for (int i = 0; i < n; i++) {

        // If current element
        // does not exceed k
        if (arr[i] <= k)
            return false;
    }

    return true;
}

// Function to modify array by
// right shifting digits such that
// all array elements are exceeding k
void modifyArray(int arr[], int k, int n)
{

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If current element
        // exceeds k
        if (arr[i] > k)
            continue;

        else {

            // Count bits in the binary
            // representation of arr[i]

            // MSB of arr[i]
            int bits = setBitNumber(arr[i]);

            int el = arr[i];

            // Perform right shift operations
            for (int j = 0; j < bits; j++) {

                // If the current element is odd
                if (el & 1) {

                    // Right shift the element
                    el >>= 1;

                    // Perform OR with the bitmask
                    el |= (1 << bits);
                }

                // If the current element is even
                else {

                    // Right shift the element
                    el >>= 1;
                }

                // If current element exceeds k
                if (el > k) {
                    arr[i] = el;
                    break;
                }
            }
        }
    }

    // Check if all array elements
    // are greater than k or not
    if (check(arr, k, n)) {
        for (int i = 0; i < n; i++)
            cout << arr[i] << " ";
    }
    else
        cout << -1;
}

// Driver Code
int main()
{
    int arr[] = { 21, 22, 23, 19 };

    // Size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 24;

    modifyArray(arr, k, n);
    return 0;
}

// This code is contributed by subhammahato348.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
public class GFG
{

  // Function to find
  // MSB of a number
  static int setBitNumber(int n)
  {

    // Stores the position of the
    // most significant set bit
    int k = (int)(Math.log(n) / Math.log(2));

    // Return the position of the
    // most significant set bit
    return k;
  }

  // Function to check if all array
  // elements are exceeding k or not
  static boolean check(int[] arr, int k, int n)
  {

    // Traverse the array arr
    for (int i = 0; i < n; i++)
    {

      // If current element
      // does not exceed k
      if (arr[i] <= k)
        return false;
    }

    return true;
  }

  // Function to modify array by
  // right shifting digits such that
  // all array elements are exceeding k
  static void modifyArray(int[] arr, int k, int n)
  {

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // If current element
      // exceeds k
      if (arr[i] > k)
        continue;
      else
      {

        // Count bits in the binary
        // representation of arr[i]

        // MSB of arr[i]
        int bits = setBitNumber(arr[i]);
        int el = arr[i];

        // Perform right shift operations
        for (int j = 0; j < bits; j++)
        {

          // If the current element is odd
          if ((el & 1) != 0)
          {

            // Right shift the element
            el >>= 1;

            // Perform OR with the bitmask
            el |= (1 << bits);
          }

          // If the current element is even
          else
          {

            // Right shift the element
            el >>= 1;
          }

          // If current element exceeds k
          if (el > k)
          {
            arr[i] = el;
            break;
          }
        }
      }
    }

    // Check if all array elements
    // are greater than k or not
    if (check(arr, k, n)) {
      for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
    }
    else
      System.out.print("-1");
  }

  // Driver code
  public static void main(String[] args) {
    int[] arr = { 21, 22, 23, 19 };

    // Size of array
    int n = arr.length;
    int k = 24;
    modifyArray(arr, k, n);
  }
}

// This code is conntrributed by divyesh072019.
```

## 蟒蛇 3

```
# Python program to implement
# the above approach
import math

# Function to find
# MSB of a number
def setBitNumber(n):

    # Stores the position of the
    # most significant set bit
    k = int(math.log(n, 2))

    # Return the position of the
    # most significant set bit
    return k

# Function to check if all array
# elements are exceeding k or not
def check(arr, k):

    # Traverse the array arr
    for el in arr:

        # If current element
        # does not exceed k
        if el <= k:
            return False
    return True

# Function to modify array by
# right shifting digits such that
# all array elements are exceeding k
def modifyArray(arr, k):

    # Traverse the array
    for i in range(len(arr)):

        # If current element
        # exceeds k
        if arr[i] > k:
            continue
        else:

            # Count bits in the binary
            # representation of arr[i]

            # MSB of arr[i]
            bits = setBitNumber(arr[i])
            el = arr[i]

            # Perform right shift operations
            for j in range(bits):

                # If the current element is odd
                if el & 1:

                    # Right shift the element
                    el >>= 1

                    # Perform OR with the bitmask
                    el |= (1 << bits)

                # If the current element is even
                else:

                    # Right shift the element
                    el >>= 1

                # If current element exceeds k
                if el > k:
                    arr[i] = el
                    break

    # Check if all array elements
    # are greater than k or not
    if check(arr, k):
        return arr
    else:
        return -1

# Driver Code

arr = [21, 22, 23, 19]
k = 24

print(modifyArray(arr, k))
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find
  // MSB of a number
  static int setBitNumber(int n)
  {

    // Stores the position of the
    // most significant set bit
    int k = (int)(Math.Log(n, 2));

    // Return the position of the
    // most significant set bit
    return k;
  }

  // Function to check if all array
  // elements are exceeding k or not
  static bool check(int[] arr, int k, int n)
  {

    // Traverse the array arr
    for (int i = 0; i < n; i++)
    {

      // If current element
      // does not exceed k
      if (arr[i] <= k)
        return false;
    }

    return true;
  }

  // Function to modify array by
  // right shifting digits such that
  // all array elements are exceeding k
  static void modifyArray(int[] arr, int k, int n)
  {

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // If current element
      // exceeds k
      if (arr[i] > k)
        continue;
      else
      {

        // Count bits in the binary
        // representation of arr[i]

        // MSB of arr[i]
        int bits = setBitNumber(arr[i]);
        int el = arr[i];

        // Perform right shift operations
        for (int j = 0; j < bits; j++)
        {

          // If the current element is odd
          if ((el & 1) != 0)
          {

            // Right shift the element
            el >>= 1;

            // Perform OR with the bitmask
            el |= (1 << bits);
          }

          // If the current element is even
          else
          {

            // Right shift the element
            el >>= 1;
          }

          // If current element exceeds k
          if (el > k)
          {
            arr[i] = el;
            break;
          }
        }
      }
    }

    // Check if all array elements
    // are greater than k or not
    if (check(arr, k, n)) {
      for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
    }
    else
      Console.Write("-1");
  }

  // Driver Code
  public static void Main()
  {
    int[] arr = { 21, 22, 23, 19 };

    // Size of array
    int n = arr.Length;
    int k = 24;
    modifyArray(arr, k, n);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find
// MSB of a number
function setBitNumber(n)
{

    // Stores the position of the
    // most significant set bit
    let k = Math.log2(n);

    // Return the position of the
    // most significant set bit
    return k;
}

// Function to check if all array
// elements are exceeding k or not
function check(arr, k, n)
{

    // Traverse the array arr
    for (let i = 0; i < n; i++)
    {

        // If current element
        // does not exceed k
        if (arr[i] <= k)
            return false;
    }
    return true;
}

// Function to modify array by
// right shifting digits such that
// all array elements are exceeding k
function modifyArray(arr, k, n)
{

    // Traverse the array
    for (let i = 0; i < n; i++)
    {

        // If current element
        // exceeds k
        if (arr[i] > k)
            continue;

        else
        {

            // Count bits in the binary
            // representation of arr[i]

            // MSB of arr[i]
            let bits = setBitNumber(arr[i]);
            let el = arr[i];

            // Perform right shift operations
            for (let j = 0; j < bits; j++)
            {

                // If the current element is odd
                if (el & 1)
                {

                    // Right shift the element
                    el >>= 1;

                    // Perform OR with the bitmask
                    el |= (1 << bits);
                }

                // If the current element is even
                else
                {

                    // Right shift the element
                    el >>= 1;
                }

                // If current element exceeds k
                if (el > k)
                {
                    arr[i] = el;
                    break;
                }
            }
        }
    }

    // Check if all array elements
    // are greater than k or not
    if (check(arr, k, n))
    {
        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }
    else
        document.write(-1);
}

// Driver Code
let arr = [ 21, 22, 23, 19 ];

// Size of array
let n = arr.length;
let k = 24;
modifyArray(arr, k, n);

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
[26, 26, 27, 25]
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)