# 打印每个数组元素的数字，不分割该元素的任何数字

> 原文:[https://www . geeksforgeeks . org/print-digits-for-每个数组元素不除该元素的任何数字/](https://www.geeksforgeeks.org/print-digits-for-each-array-element-that-does-not-divide-any-digit-of-that-element/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，每个数组元素 **arr[i]** 的任务是从**【0，9】**中找到所有不除 **arr[i]** 中任何数字的数字。

**示例:**

> **输入:** arr[] = {4162，1152，99842}
> **输出:**
> 4162->5 7 8 9
> 1152->3 4 6 7 8 9
> 99842->5 6 7
> **解释:**
> **为 arr[0] ( = 4162):** 无位数
> **对于 arr[1]( = 1152):** 元素 1152 的所有数字都不能被 9、8、7、6、4、3 整除。
> **对于 arr[2]( = 99842):** 元素 99842 的所有数字都不能被 7、6、5 整除。
> 
> **输入:**arr[]= { 2021 }
> T3】输出:T5】2021->3 4 5 6 7 8 9

**方法:**按照以下步骤解决问题:

*   [遍历给定数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，并执行以下步骤:
    *   使用变量 **i** 迭代范围**【2，9】**，如果元素**arr【I】**中不存在任何可被 **i** 整除的数字，则打印数字 **i** 。
    *   否则，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)进行下一次迭代。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find digits for each array
// element that doesn't divide any digit
// of the that element
void indivisibleDigits(int arr[], int N)
{
    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        int num = 0;

        cout << arr[i] << ": ";

        // Iterate over the range [2, 9]
        for (int j = 2; j < 10; j++) {

            int temp = arr[i];

            // Stores if there exists any digit
            // in arr[i] which is divisible by j
            bool flag = true;

            while (temp > 0) {

                // If any digit of the number
                // is divisible by j
                if ((temp % 10) != 0
                    && (temp % 10) % j == 0) {

                    flag = false;
                    break;
                }

                temp /= 10;
            }

            // If the digit j doesn't
            // divide any digit of arr[i]
            if (flag) {
                cout << j << ' ';
            }
        }

        cout << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 4162, 1152, 99842 };
    int N = sizeof(arr) / sizeof(arr[0]);

    indivisibleDigits(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to find digits for each array
  // element that doesn't divide any digit
  // of the that element
  static void indivisibleDigits(int[] arr, int N)
  {

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {
      System.out.print(arr[i] + ": ");

      // Iterate over the range [2, 9]
      for (int j = 2; j < 10; j++)
      {
        int temp = arr[i];

        // Stores if there exists any digit
        // in arr[i] which is divisible by j
        boolean flag = true;
        while (temp > 0) {

          // If any digit of the number
          // is divisible by j
          if ((temp % 10) != 0
              && (temp % 10) % j == 0) {

            flag = false;
            break;
          }

          temp /= 10;
        }

        // If the digit j doesn't
        // divide any digit of arr[i]
        if (flag) {
          System.out.print(j + " ");
        }
      }

      System.out.println();
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 4162, 1152, 99842 };
    int N = arr.length;

    indivisibleDigits(arr, N);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find digits for each array
# element that doesn't divide any digit
# of the that element
def indivisibleDigits(arr, N) :

    # Traverse the array arr[]
    for i in range(N):

        num = 0

        print(arr[i], end = ' ')

        # Iterate over the range [2, 9]
        for j in range(2, 10):

            temp = arr[i]

            # Stores if there exists any digit
            # in arr[i] which is divisible by j
            flag = True

            while (temp > 0) :

                # If any digit of the number
                # is divisible by j
                if ((temp % 10) != 0
                    and (temp % 10) % j == 0) :

                    flag = False
                    break

                temp //= 10

            # If the digit j doesn't
            # divide any digit of arr[i]
            if (flag) :
                print(j, end = ' ')

        print()

# Driver Code

arr = [ 4162, 1152, 99842 ]
N = len(arr)

indivisibleDigits(arr, N)

# This code is contributed by susmitakundugoaldanga.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find digits for each array
  // element that doesn't divide any digit
  // of the that element
  static void indivisibleDigits(int[] arr, int N)
  {

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {
      Console.Write(arr[i] + ": ");

      // Iterate over the range [2, 9]
      for (int j = 2; j < 10; j++)
      {
        int temp = arr[i];

        // Stores if there exists any digit
        // in arr[i] which is divisible by j
        bool flag = true;
        while (temp > 0) {

          // If any digit of the number
          // is divisible by j
          if ((temp % 10) != 0
              && (temp % 10) % j == 0) {

            flag = false;
            break;
          }

          temp /= 10;
        }

        // If the digit j doesn't
        // divide any digit of arr[i]
        if (flag) {
          Console.Write(j + " ");
        }
      }

      Console.WriteLine();
    }
  }

  // Driver Code
  public static void Main()
  {
    int[] arr = { 4162, 1152, 99842 };
    int N = arr.Length;

    indivisibleDigits(arr, N);
  }
}

// This code is contributed by rishavmahato348.
```

## java 描述语言

```
<script>

// javascript program for the above approach
// Function to find digits for each array
    // element that doesn't divide any digit
    // of the that element
    function indivisibleDigits(arr , N) {

        // Traverse the array arr
        for (i = 0; i < N; i++) {
            document.write(arr[i] + ": ");

            // Iterate over the range [2, 9]
            for (j = 2; j < 10; j++) {
                var temp = arr[i];

                // Stores if there exists any digit
                // in arr[i] which is divisible by j
                var flag = true;
                while (temp > 0) {

                    // If any digit of the number
                    // is divisible by j
                    if ((temp % 10) != 0 && (temp % 10) % j == 0) {

                        flag = false;
                        break;
                    }

                    temp = parseInt(temp/10);
                }

                // If the digit j doesn't
                // divide any digit of arr[i]
                if (flag) {
                    document.write(j + " ");
                }
            }

            document.write("<br/>");
        }
    }

    // Driver Code

        var arr = [ 4162, 1152, 99842 ];
        var N = arr.length;

        indivisibleDigits(arr, N);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
4162: 5 7 8 9 
1152: 3 4 6 7 8 9 
99842: 5 6 7
```

***时间复杂度:**O(10 * N * log<sub>10</sub>N)*
*T8】辅助空间: O(1)*