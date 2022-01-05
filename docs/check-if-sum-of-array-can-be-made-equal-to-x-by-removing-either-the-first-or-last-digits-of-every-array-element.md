# 通过删除每个数组元素的第一个或最后一个数字来检查数组的和是否等于 X

> 原文:[https://www . geesforgeks . org/check-if-sum-of-array-and-to-x-通过移除每个数组元素的第一个或最后一个数字/](https://www.geeksforgeeks.org/check-if-sum-of-array-can-be-made-equal-to-x-by-removing-either-the-first-or-last-digits-of-every-array-element/)

给定一个由 **N** 个正整数和一个正整数 **X** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是通过移除每个数组元素的第一个或最后一个数字[来检查给定数组](https://www.geeksforgeeks.org/find-first-last-digits-number/)的[和是否可以等于 **X** 。如果可以使数组元素之和等于 **X** ，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {545，433，654，23}，X = 134
> **输出:**是
> **说明:**
> 以下去掉数字使数组之和等于 **X** :
> 
> *   删除 arr[0]的第一个数字会将 arr[0]修改为 45。
> *   删除 arr[1]的第一个数字将修改为 33。
> *   删除 arr[2]的第一个数字会将 arr[2]修改为 54。
> *   删除 arr[3]的最后一位数字会将 arr[3]修改为 2。
> 
> 修改后的数组为{45，33，54，2}。因此，修改后的数组之和= 45 + 33 + 54 + 2 = 134(= X)。
> 
> **输入:** arr[] = {54，22，76，432}，X = 48
> **输出:**否

**方法:**给定的问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)通过生成所有可能的方法来移除每个数组元素的第一个或最后一个数字来解决。按照以下步骤解决给定的问题。

*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如说 **makeSumX(arr，S，I，X)** ，该函数以数组 **arr[]** 、当前和 **S** 、当前索引 **i** 、所需和 **X** 为参数，进行如下操作:
    *   如果当前索引等于数组的[长度，当前和 **S** 等于所需和 **X** ，则返回**真**。否则，返回**假**。](https://www.geeksforgeeks.org/how-to-determine-length-or-size-of-an-array-in-java/)
    *   [将整数**arr【I】**转换为字符串](https://www.geeksforgeeks.org/convert-a-string-to-integer-array-in-c-c/)。
    *   [删除整数](https://www.geeksforgeeks.org/program-to-delete-nth-digit-of-a-number/)**arr【I】**的最后一位数字，并将其存储在一个变量中，比如 **L** 。
    *   [删除整数](https://www.geeksforgeeks.org/program-to-delete-nth-digit-of-a-number/)**arr【I】**的第一位数字，并将其存储在一个变量中，比如 **R** 。
    *   将该函数的值作为 **makeSumX(arr，S + L，i + 1，X)和 makeSumX(arr，S + R，i + 1，X)** 的[位或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)返回。
*   如果函数 **makeSumX(arr，0，0，X)** 返回的值为真，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility Function to check if the sum
// of the array elements can be made
// equal to X by removing either the first
// or last digits of every array element
bool makeSumX(int arr[], int X, int S,
              int i, int N)
{

    // Base Case
    if (i == N)
    {
        return S == X;
    }

    // Convert arr[i] to string
    string a = to_string(arr[i]);

    // Remove last digit
    int l = stoi(a.substr(0, a.length() - 1));

    // Remove first digit
    int r = stoi(a.substr(1));

    // Recursive function call
    bool x = makeSumX(arr, X, S + l, i + 1, N);
    bool y = makeSumX(arr, X, S + r, i + 1, N);

    return (x || y);
}

// Function to check if sum of given
// array can be made equal to X or not
void Check(int arr[], int X, int N)
{

    if (makeSumX(arr, X, 0, 0, N))
    {
        cout << "Yes";
    }
    else
    {
        cout << "No";
    }
}

// Driver code
int main()
{
    int arr[] = { 545, 433, 654, 23 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int X = 134;

    // Function Call
    Check(arr, X, N);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Utility Function to check if the sum
// of the array elements can be made
// equal to X by removing either the first
// or last digits of every array element
static boolean makeSumX(int arr[], int X,
                        int S, int i)
{

    // Base Case
    if (i == arr.length)
    {
        return S == X;
    }

    // Convert arr[i] to string
    String a = Integer.toString(arr[i]);

    // Remove last digit
    int l = Integer.parseInt(
        a.substring(0, a.length() - 1));

    // Remove first digit
    int r = Integer.parseInt(a.substring(1));

    // Recursive function call
    boolean x = makeSumX(arr, X, S + l, i + 1);
    boolean y = makeSumX(arr, X, S + r, i + 1);

    return (x || y);
}

// Function to check if sum of given
// array can be made equal to X or not
static void Check(int arr[], int X)
{

    if (makeSumX(arr, X, 0, 0))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 545, 433, 654, 23 };
    int X = 134;

    // Function Call
    Check(arr, X);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Utility Function to check if the sum
# of the array elements can be made
# equal to X by removing either the first
# or last digits of every array element
def makeSumX(arr, X, S, i):

      # Base Case
    if i == len(arr):
        return S == X

    # Convert arr[i] to string
    a = str(arr[i])

    # Remove last digit
    l = int(a[:-1])

    # Remove first digit
    r = int(a[1:])

    # Recursive function call
    x = makeSumX(arr, X, S + l, i + 1)
    y = makeSumX(arr, X, S + r, i + 1)

    return x | y

# Function to check if sum of given
# array can be made equal to X or not
def Check(arr, X):

    if (makeSumX(arr, X, 0, 0)):
      print("Yes")
    else:
      print("No")

# Driver Code

arr = [545, 433, 654, 23]
X = 134

Check(arr, X)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic; 

class GFG{

// Utility Function to check if the sum
// of the array elements can be made
// equal to X by removing either the first
// or last digits of every array element
static bool makeSumX(int[] arr, int X,
                     int S, int i)
{

    // Base Case
    if (i == arr.Length)
    {
        return S == X;
    }

    // Convert arr[i] to string
    string a = Convert.ToString(arr[i]);

    // Remove last digit
    int l = Int32.Parse(
        a.Substring(0, a.Length - 1));

    // Remove first digit
    int r = Int32.Parse(a.Substring(1));

    // Recursive function call
    bool x = makeSumX(arr, X, S + l, i + 1);
    bool y = makeSumX(arr, X, S + r, i + 1);

    return (x || y);
}

// Function to check if sum of given
// array can be made equal to X or not
static void Check(int[] arr, int X)
{
    if (makeSumX(arr, X, 0, 0))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 545, 433, 654, 23 };
    int X = 134;

    // Function Call
    Check(arr, X);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
       // Javascript program for the above approach

       // Utility Function to check if the sum
       // of the array elements can be made
       // equal to X by removing either the first
       // or last digits of every array element
       function makeSumX(arr, X, S,
           i, N) {

           // Base Case
           if (i === N) {
               return S === X
           }

           // Convert arr[i] to string
           let a = (arr[i]).toString()

           // Remove last digit
           let l = parseInt((a.substr(0, a.length - 1)))

           // Remove first digit
           let r = parseInt((a.substr(1)))

           // Recursive function call
           let x = makeSumX(arr, X, S + l, i + 1, N);
           let y = makeSumX(arr, X, S + r, i + 1, N);

           return (x || y);
       }

       // Function to check if sum of given
       // array can be made equal to X or not
       function Check(arr, X, N) {

           if (makeSumX(arr, X, 0, 0, N)) {
               document.write("Yes")
           }
           else {
               document.write("No")
           }
       }

       // Driver code

       let arr = [545, 433, 654, 23];
       let N = arr.length;
       let X = 134;

       // Function Call
       Check(arr, X, N);

       // This code is contributed by Hritik
   </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*