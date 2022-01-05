# 一个阵列的所有非重复子阵列的乘积

> 原文:[https://www . geeksforgeeks . org/全非重复阵列子阵列产品/](https://www.geeksforgeeks.org/product-of-all-non-repeating-subarrays-of-an-array/)

给定一个包含大小为 **N** 的不同整数 **arr[]** 的数组，任务是打印数组中所有非重复子数组的乘积。
**例:**

> **输入:** arr[] = {2，4}
> **输出:** 64
> **解释:**
> 给定数组的可能子阵分别为{2}、{2，4}、{4}
> 乘积分别为 2、8、4。因此，所有子阵列的总积= 64
> **输入:** arr[] = {10，3，7}
> **输出:** 1944810000
> **说明:**
> 给定阵列的可能子阵列为{10}、{10，3}、{0，7}、{10，3，7}、{3}、{7}、{3 }、{ 3 }、{ 3，7}。
> 产品分别为 10、30、70、210、3、7、21。因此，所有子阵列的总乘积= 1944810000

**天真方法:**这个问题的天真方法是[生成给定数组的所有子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并计算它们的乘积。这种方法的时间复杂度是指数级的。
**高效进场:**思路是做一个观察。如果我们观察不重复的子阵列，我们可以观察到子阵列中单个元素的*出现*遵循与阵列长度的关系。

*   例如，让数组 arr[] = {10，3，7}。
*   上述数组中所有不重复的可能子数组是:{{10}、{10，3}、{10，7}、{10，3，7}、{3}、{7}、{3，7}}。
*   在上述子阵列中，每个元素的[频率可以观察为:](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) 

```
Frequency of 10 in subarrays = 4
Frequency of 3 in subarrays = 4
Frequency of 7 in subarrays = 4
```

*   这里，以下等式适用于任何长度的数组:

```
Frequency of element = 2(arr.length-1)
```

*   因此，为了得到最终产品，我们可以简单地执行:

```
product = 10 * (freq_of_10) * 3 * (freq_of_3) * 7 * (freq_of_7)
```

*   所以思路就是简单的[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对每个元素及其对应的频率进行乘法运算。

以下是上述方法的实现:

## C++

```
// C++ program to find the product of
// all non-repeating Subarrays of an Array
#include <bits/stdc++.h>
using namespace std;

// Function to find the product of
// all non-repeating Subarrays of an Array
long product(int arr[], int n)
{

    // Finding the occurrence of every element
    double occurrence = pow(2, n - 1);

    double product = 1;

    // Iterating through the array and
    // finding the product
    for(int i = 0; i < n; i++)
    {

        // We are taking the power of each
        // element in array with the occurrence
        // and then taking product of those.
        product *= pow(arr[i], occurrence);
    }
    return (long)product;
}

// Driver code
int main()
{
    int arr[] = { 10, 3, 7 };

    int len = sizeof(arr) / sizeof(arr[0]);

    cout << product(arr, len);
    return 0;
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product of
// all non-repeating Subarrays of an Array

public class GFG {

    // Function to find the product of
    // all non-repeating Subarrays of an Array
    private static long product(int[] arr)
    {
        // Finding the occurrence of every element
        double occurrence = Math.pow(2, arr.length - 1);

        double product = 1;

        // Iterating through the array and
        // finding the product
        for (int i = 0; i < arr.length; i++) {

            // We are taking the power of each
            // element in array with the occurrence
            // and then taking product of those.
            product *= Math.pow(arr[i], occurrence);
        }

        return (long)product;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 10, 3, 7 };

        System.out.println(product(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the product of
# all non-repeating Subarrays of an Array

# Function to find the product of
# all non-repeating Subarrays of an Array
def product(arr):

    # Finding the occurrence of every element
    occurrence = pow(2, len(arr) - 1);

    product = 1;

    # Iterating through the array and
    # finding the product
    for i in range(0, len(arr)):

        # We are taking the power of each
        # element in array with the occurrence
        # and then taking product of those.
        product *= pow(arr[i], occurrence);

    return product;

# Driver code
arr = [ 10, 3, 7 ];
print(product(arr));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to find the product of
// all non-repeating Subarrays of an Array
using System;
class GFG{

// Function to find the product of
// all non-repeating Subarrays of an Array
private static long product(int[] arr)
{
    // Finding the occurrence of every element
    double occurrence = Math.Pow(2, arr.Length - 1);

    double product = 1;

    // Iterating through the array and
    // finding the product
    for (int i = 0; i < arr.Length; i++)
    {

        // We are taking the power of each
        // element in array with the occurrence
        // and then taking product of those.
        product *= Math.Pow(arr[i], occurrence);
    }
    return (long)product;
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 10, 3, 7 };

    Console.WriteLine(product(arr));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to find the product of
// all non-repeating Subarrays of an Array

    // Function to find the product of
    // all non-repeating Subarrays of an Array
    function product(arr)
    {
        // Finding the occurrence of every element
        let occurrence = Math.pow(2, arr.length - 1);

        let product = 1;

        // Iterating through the array and
        // finding the product
        for (let i = 0; i < arr.length; i++) {

            // We are taking the power of each
            // element in array with the occurrence
            // and then taking product of those.
            product *= Math.pow(arr[i], occurrence);
        }

        return product;
    }

// Driver Code

    let arr = [ 10, 3, 7 ];

    document.write(product(arr));

</script>
```

**Output:** 

```
1944810000
```

**时间复杂度:** *O(N)* ，其中 N 为阵的大小
T5】辅助空间: O(1)