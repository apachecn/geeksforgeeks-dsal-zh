# 给定数组中具有复合和的最大子集

> 原文:[https://www . geesforgeks . org/最大子集组合给定数组中的和/](https://www.geeksforgeeks.org/largest-subset-with-composite-sum-in-given-array/)

给定一个由 **n** 个不同正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 。找出给定数组中最大的[子集](https://www.geeksforgeeks.org/power-set/)的长度，其和为一个[组合数](https://www.geeksforgeeks.org/composite-number/)，并打印所需的数组(顺序或打印元素无关紧要)。

> **注意:**如果复合和有多个大小最大的子集，输出其中任意一个。

**示例:**

> **输入:** arr[] = {8，1，4}，n=3
> **输出:** 2、【8，4】
> **说明:**所需子集可以是【8，1】=>8+1 = 9(复合数)。也可以考虑，[8，4](总和= 12 的复合数)。注意[8，1，4]不能考虑，因为它的和不是一个复合数。Sum = 8 + 1 + 4 = 13(不是复合数)。
> 
> **输入:** arr[] = {6，4，2，3}，n=4
> **输出:** 4、【6，2，4，3】
> **说明:**所有元素之和，= 6 + 4 + 2 + 3 = 15(合成数)，是最大的子集。

**方法:**给定的问题可以很容易地解决，方法是考虑所有偶数加起来是一个偶数(除了 2 之外，它总是一个复合数)，然后在这个和上加一个奇数，并检查这个和是否是复合的。按照以下步骤解决问题:

*   [创建一个 **temp[]** 向量](https://www.geeksforgeeks.org/how-to-implement-our-own-vector-class-in-c/)，首先存储所有偶数，然后存储给定数组中的奇数。
*   创建一个变量 **cursum，**初始化为零，存储 temp 数组的当前和，变量 **maxlen = 0** ，存储合成和的最大长度。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n)** ，并执行以下任务:
    *   将值**温度【I】**添加到变量**电流**中。
    *   如果数值**currsum**是一个复合数， **currsum** 大于 **maxlen** ，则将 **maxlen** 的值设置为 **i+1。**
*   执行上述步骤后，打印 **maxlen** 的值作为答案，首先打印数组**temp【】**中的 **maxlen** 元素作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the current
// sum is composite or not
bool checkComposite(int n)
{

    // 1 and 2 are not composite
    // number
    if (n == 1 || n == 2) {
        return false;
    }

    // If the number is divisible
    // by any digit except 2 and itself
    // then it's composite
    for (int i = 2; i < n; i++) {

        // If composite
        if (n % i == 0 && i != n) {
            return true;
        }
    }

    return false;
}

// Utility Function to find largest composite
// subset sum
void largestCompositeSum(int arr[], int n)
{

    // Vector to store the elements of
    // arr in order of first even then
    // odd numbers
    vector<int> temp;

    // Even numbers pushed first in
    // temp array
    for (int i = 0; i < n; i++) {

        // Even check
        if (arr[i] % 2 == 0) {
            temp.push_back(arr[i]);
        }
    }

    // Odd numbers pushed
    for (int i = 0; i < n; i++) {
        // Odd check
        if (arr[i] % 2 == 1) {
            temp.push_back(arr[i]);
        }
    }

    // To store current sum
    int cursum = 0;

    // To store maximum length composite
    // sum
    int maxlen = 0;

    for (int i = 0; i < n; i++) {
        cursum += temp[i];

        // If composite then update
        // cursum
        if (checkComposite(cursum)
            && cursum > maxlen) {
            maxlen = i + 1;
        }
    }

    cout << maxlen << endl;

    // Printing the required array
    for (int i = 0; i < maxlen; i++) {
        cout << temp[i] << " ";
    }

    return;
}

// Driver Code
int main()
{

    int n = 3;
    int arr[3] = { 8, 1, 4 };

    // Function called
    largestCompositeSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to check if the current
  // sum is composite or not
  static boolean checkComposite(int n)
  {

    // 1 and 2 are not composite
    // number
    if (n == 1 || n == 2) {
      return false;
    }

    // If the number is divisible
    // by any digit except 2 and itself
    // then it's composite
    for (int i = 2; i < n; i++) {

      // If composite
      if (n % i == 0 && i != n) {
        return true;
      }
    }

    return false;
  }

  // Utility Function to find largest composite
  // subset sum
  static void largestCompositeSum(int arr[], int n)
  {

    // Vector to store the elements of
    // arr in order of first even then
    // odd numbers
    Vector<Integer> temp = new Vector<Integer>();

    // Even numbers pushed first in
    // temp array
    for (int i = 0; i < n; i++) {

      // Even check
      if (arr[i] % 2 == 0) {
        temp.add(arr[i]);
      }
    }

    // Odd numbers pushed
    for (int i = 0; i < n; i++) {
      // Odd check
      if (arr[i] % 2 == 1) {
        temp.add(arr[i]);
      }
    }

    // To store current sum
    int cursum = 0;

    // To store maximum length composite
    // sum
    int maxlen = 0;

    for (int i = 0; i < n; i++) {
      cursum += temp.get(i);

      // If composite then update
      // cursum
      if (checkComposite(cursum)
          && cursum > maxlen) {
        maxlen = i + 1;
      }
    }

    System.out.print(maxlen +"\n");

    // Printing the required array
    for (int i = 0; i < maxlen; i++) {
      System.out.print(temp.get(i)+ " ");
    }

    return;
  }

  // Driver Code
  public static void main(String[] args)
  {

    int n = 3;
    int arr[] = { 8, 1, 4 };

    // Function called
    largestCompositeSum(arr, n);

  }
}

// This code is contributed by shikhasingrajput
```

## 计算机编程语言

```
# Python program for the above approach

# Function to check if the current
# sum is composite or not
def checkComposite(n):

    # 1 and 2 are not composite
    # number
    if (n == 1 or n == 2):
        return false

    # If the number is divisible
    # by any digit except 2 and itself
    # then it's composite
    for i in range(2, n):

        # If composite
        if (n % i == 0 and i != n):
            return True

    return False

# Utility Function to find largest composite
# subset sum
def largestCompositeSum(arr, n):

    # Vector to store the elements of
    # arr in order of first even then
    # odd numbers
    temp = []

    # Even numbers pushed first in
    # temp array
    for i in range(n):

        # Even check
        if (arr[i] % 2 == 0):
            temp.append(arr[i])

    # Odd numbers pushed
    for i in range(n):
        # Odd check
        if (arr[i] % 2 == 1):
            temp.append(arr[i])

    # To store current sum
    cursum = 0;

    # To store maximum length composite
    # sum
    maxlen = 0;

    for i in range(n):
        cursum += temp[i]

        # If composite then update
        # cursum
        if (checkComposite(cursum)
            and cursum > maxlen):
            maxlen = i + 1

    print(maxlen)

    l = len(temp) - maxlen
    for i in range(l):
        temp.remove(temp[i + maxlen])

    # Printing the required array
    print(*temp)

    return

# Driver code
n = 3
arr = [8, 1, 4]

# Function called
largestCompositeSum(arr, n);

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to check if the current
    // sum is composite or not
    static bool checkComposite(int n)
    {

        // 1 and 2 are not composite
        // number
        if (n == 1 || n == 2) {
            return false;
        }

        // If the number is divisible
        // by any digit except 2 and itself
        // then it's composite
        for (int i = 2; i < n; i++) {

            // If composite
            if (n % i == 0 && i != n) {
                return true;
            }
        }

        return false;
    }

    // Utility Function to find largest composite
    // subset sum
    static void largestCompositeSum(int[] arr, int n)
    {

        // Vector to store the elements of
        // arr in order of first even then
        // odd numbers
        List<int> temp = new List<int>();

        // Even numbers pushed first in
        // temp array
        for (int i = 0; i < n; i++) {

            // Even check
            if (arr[i] % 2 == 0) {
                temp.Add(arr[i]);
            }
        }

        // Odd numbers pushed
        for (int i = 0; i < n; i++) {
            // Odd check
            if (arr[i] % 2 == 1) {
                temp.Add(arr[i]);
            }
        }

        // To store current sum
        int cursum = 0;

        // To store maximum length composite
        // sum
        int maxlen = 0;

        for (int i = 0; i < n; i++) {
            cursum += temp[i];

            // If composite then update
            // cursum
            if (checkComposite(cursum) && cursum > maxlen) {
                maxlen = i + 1;
            }
        }

        Console.WriteLine(maxlen);

        // Printing the required array
        for (int i = 0; i < maxlen; i++) {
            Console.Write(temp[i] + " ");
        }

        return;
    }

    // Driver Code
    public static void Main()
    {

        int n = 3;
        int[] arr = { 8, 1, 4 };

        // Function called
        largestCompositeSum(arr, n);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to check if the current
       // sum is composite or not
       function checkComposite(n) {

           // 1 and 2 are not composite
           // number
           if (n == 1 || n == 2) {
               return false;
           }

           // If the number is divisible
           // by any digit except 2 and itself
           // then it's composite
           for (let i = 2; i < n; i++) {

               // If composite
               if (n % i == 0 && i != n) {
                   return true;
               }
           }

           return false;
       }

       // Utility Function to find largest composite
       // subset sum
       function largestCompositeSum(arr, n) {

           // Vector to store the elements of
           // arr in order of first even then
           // odd numbers
           let temp = [];

           // Even numbers pushed first in
           // temp array
           for (let i = 0; i < n; i++) {

               // Even check
               if (arr[i] % 2 == 0) {
                   temp.push(arr[i]);
               }
           }

           // Odd numbers pushed
           for (let i = 0; i < n; i++) {
               // Odd check
               if (arr[i] % 2 == 1) {
                   temp.push(arr[i]);
               }
           }

           // To store current sum
           let cursum = 0;

           // To store maximum length composite
           // sum
           let maxlen = 0;

           for (let i = 0; i < n; i++) {
               cursum += temp[i];

               // If composite then update
               // cursum
               if (checkComposite(cursum)
                   && cursum > maxlen) {
                   maxlen = i + 1;
               }
           }

           document.write(maxlen + '<br>');

           // Printing the required array
           for (let i = 0; i < maxlen; i++) {
               document.write(temp[i] + " ");
           }

           return;
       }

       // Driver Code
       let n = 3;
       let arr = [8, 1, 4];

       // Function called
       largestCompositeSum(arr, n);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
2
8 4
```

***时间复杂度:**O(n<sup>2</sup>)*
***辅助空间:** O(n)，临时数组需要。*