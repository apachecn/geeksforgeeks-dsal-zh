# 由 O(n)中数组的数字组成的两个数的最小和

> 原文:[https://www . geeksforgeeks . org/二进制数的最小和-由数组中的数字组成/](https://www.geeksforgeeks.org/minimum-sum-of-two-numbers-formed-from-digits-of-an-array-in-on/)

给定一个数字数组(值从 0 到 9)，求由数组的数字组成的两个数字的最小可能和。给定数组的所有数字都必须用来构成这两个数字。
**例:**

> **输入:** arr[] = {6，8，4，5，2，3}
> **输出:** 604
> 246 + 358 = 604
> **输入:** arr[] = {5，3，0，7，4}
> **输出:** 82

**方法:**当最小的数字出现在最高有效位置，次小的数字出现在次高有效位置，以此类推时，将从数字集合中形成一个最小的数字……
想法是通过交替从数组中挑选数字来构建两个数字(假设按升序排序)。因此，第一个数字由数组中奇数位置的数字组成，第二个数字由数组中偶数位置的数字组成。最后，我们返回第一个和第二个数的和。为了降低时间复杂度，可以使用数字的频率数组将数组排序为 0(n)，因为原始数组的每个元素都是一个数字，即最多可以有 10 个不同的元素。
以下是上述办法的实施:

## C++

```
// C++ implementation of above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the required minimum sum
int minSum(vector<int> arr, int n)
{

    // Array to store the
    // frequency of each digit
    int MAX = 10;
    int *freq = new int[MAX];
    for (int i = 0; i < n; i++) {

        // Store count of every digit
        freq[arr[i]]++;
    }

    // Update arr[] such that it is
    // sorted in ascending
    int k = 0;
    for (int i = 0; i < MAX; i++) {

        // Adding elements in arr[]
        // in sorted order
        for (int j = 0; j < freq[i]; j++) {
            arr[k++] = i;
        }
    }

    int num1 = 0;
    int num2 = 0;

    // Generating numbers alternatively
    for (int i = 0; i < n; i++) {

        if (i % 2 == 0)
            num1 = num1 * MAX + arr[i];
        else
            num2 = num2 * MAX + arr[i];
    }

    // Return the minimum possible sum
    return num1 + num2;
}

// Driver code
int main(void)
{
    vector<int>arr = { 6, 8, 4, 5, 2, 3 };
    int n = arr.size();
    cout << minSum(arr, n);
}
// This code is contributed by ankush_953
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
public class GFG {

    public static final int MAX = 10;

    // Function to return the required minimum sum
    static int minSum(int arr[], int n)
    {

        // Array to store the
        // frequency of each digit
        int freq[] = new int[MAX];
        for (int i = 0; i < n; i++) {

            // Store count of every digit
            freq[arr[i]]++;
        }

        // Update arr[] such that it is
        // sorted in ascending
        int k = 0;
        for (int i = 0; i < MAX; i++) {

            // Adding elements in arr[]
            // in sorted order
            for (int j = 0; j < freq[i]; j++) {
                arr[k++] = i;
            }
        }

        int num1 = 0;
        int num2 = 0;

        // Generating numbers alternatively
        for (int i = 0; i < n; i++) {

            if (i % 2 == 0)
                num1 = num1 * MAX + arr[i];
            else
                num2 = num2 * MAX + arr[i];
        }

        // Return the minimum possible sum
        return num1 + num2;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 6, 8, 4, 5, 2, 3 };
        int n = arr.length;
        System.out.print(minSum(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python implementation of above approach
# Function to return the required minimum sum
def minSum(arr, n):
    # Array to store the
    # frequency of each digit
    MAX = 10
    freq = [0]*MAX

    for i in range(n):
        # Store count of every digit
        freq[arr[i]] += 1

    # Update arr[] such that it is
    # sorted in ascending
    k = 0
    for i in range(MAX):
        # Adding elements in arr[]
        # in sorted order
        for j in range(0,freq[i]):
            arr[k] = i
            k += 1

    num1 = 0
    num2 = 0

    # Generating numbers alternatively
    for i in range(n):
        if i % 2 == 0:
            num1 = num1 * MAX + arr[i]
        else:
            num2 = num2 * MAX + arr[i]

    # Return the minimum possible sum
    return num1 + num2

# Driver code
arr = [ 6, 8, 4, 5, 2, 3 ]
n = len(arr);
print(minSum(arr, n))

#This code is contributed by ankush_953
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    public static int MAX = 10;
    // Function to return the required minimum sum
    static int minSum(int[] arr, int n)
    {

        // Array to store the
        // frequency of each digit
        int[] freq = new int[MAX];
        for (int i = 0; i < n; i++) {

            // Store count of every digit
            freq[arr[i]]++;
        }

        // Update arr[] such that it is
        // sorted in ascending
        int k = 0;
        for (int i = 0; i < MAX; i++) {

            // Adding elements in arr[]
            // in sorted order
            for (int j = 0; j < freq[i]; j++) {
                arr[k++] = i;
            }
        }

        int num1 = 0;
        int num2 = 0;

        // Generating numbers alternatively
        for (int i = 0; i < n; i++) {

            if (i % 2 == 0)
                num1 = num1 * MAX + arr[i];
            else
                num2 = num2 * MAX + arr[i];
        }

        // Return the minimum possible sum
        return num1 + num2;
    }

    // Driver code
    static public void Main()
    {
        int[] arr = { 6, 8, 4, 5, 2, 3 };
        int n = arr.Length;
        Console.WriteLine(minSum(arr, n));
    }
}

// This code is contributed by jit_t.
```

## java 描述语言

```
<script>   
    // Javascript implementation of above approach

    let MAX = 10;

    // Function to return the required minimum sum
    function minSum(arr, n)
    {

        // Array to store the
        // frequency of each digit
        let freq = new Array(MAX);
        freq.fill(0);
        for (let i = 0; i < n; i++) {

            // Store count of every digit
            freq[arr[i]]++;
        }

        // Update arr[] such that it is
        // sorted in ascending
        let k = 0;
        for (let i = 0; i < MAX; i++) {

            // Adding elements in arr[]
            // in sorted order
            for (let j = 0; j < freq[i]; j++) {
                arr[k++] = i;
            }
        }

        let num1 = 0;
        let num2 = 0;

        // Generating numbers alternatively
        for (let i = 0; i < n; i++) {

            if (i % 2 == 0)
                num1 = num1 * MAX + arr[i];
            else
                num2 = num2 * MAX + arr[i];
        }

        // Return the minimum possible sum
        return num1 + num2;
    }

    let arr = [ 6, 8, 4, 5, 2, 3 ];
    let n = arr.length;
    document.write(minSum(arr, n));

</script>
```

**Output:** 

```
604
```

**时间复杂度:** O(n)