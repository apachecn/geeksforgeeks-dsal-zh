# 通过对数组元素的最接近的完美正方形进行排序来修改数组，数组元素的数字按降序排序

> 原文:[https://www . geeksforgeeks . org/modify-array-by-sorting-最近的完美数组元素平方-按降序排列其数字/](https://www.geeksforgeeks.org/modify-array-by-sorting-nearest-perfect-squares-of-array-elements-having-their-digits-sorted-in-decreasing-order/)

给定一个大小为**N**(*1≤N≤10<sup>5</sup>*)的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是将每个数组元素的数字按降序排序，并用[最近的完美正方形](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)替换每个数组元素，然后按升序打印该数组。

**示例:**

> **输入** : arr[ ] = {29，43，28，12}
> **输出** : 25 49 81 100
> **解释:**
> 按降序对每个数组元素的数字进行排序将 arr[ ]修改为{92，43，82，21}。
> 用最近的完美正方形替换元素将 arr[]修改为{100，49，81，25}。
> 按升序对数组排序将 arr[]修改为{25，49，81，100}。
> 
> **输入** : arr[ ] = {517，142，905}
> 输出 : 441 729 961

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对每个数组元素执行以下操作。
    *   [将其转换为等效的字符串表示形式](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)。
    *   [按降序排列字符串](https://www.geeksforgeeks.org/sort-string-characters/)。
    *   [将字符串转换回其等效整数](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)。
    *   找到当前阵元的 [**最近的完美方块**](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/) 。
*   现在，[按照升序对数组](https://www.geeksforgeeks.org/how-to-sort-an-array-using-stl-in-c/)进行排序。
*   [打印排序后的数组](https://www.geeksforgeeks.org/java-program-to-print-the-elements-of-an-array/)。

下面是上述方法的实现。

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort array in ascending order
// after replacing array elements by nearest
// perfect square of decreasing order of digits
void sortArr(int arr[], int N)
{

    // Traverse the array of strings
    for (int i = 0; i < N; i++) {

        // Convert the current array
        // element to a string
        string s = to_string(arr[i]);

        // Sort each string in descending order
        sort(s.begin(), s.end(), greater<char>());

        // Convert the string to
        // equivalent integer
        arr[i] = stoi(s);

        // Calculate square root of
        // current array element
        int sr = sqrt(arr[i]);

        // Calculate perfect square
        int a = sr * sr;
        int b = (sr + 1) * (sr + 1);

        // Find the nearest perfect square
        if ((arr[i] - a) < (b - arr[i]))
            arr[i] = a;
        else
            arr[i] = b;
    }

    // Sort the array in ascending order
    sort(arr, arr + N);

    // Print the array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 29, 43, 28, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);
    sortArr(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
  static void reverse(char[] a) 
  {
    int i, n = a.length;
    char t;
    for (i = 0; i < n / 2; i++) 
    {
      t = a[i];
      a[i] = a[n - i - 1];
      a[n - i - 1] = t;
    }
  }

  // Function to sort array in ascending order
  // after replacing array elements by nearest
  // perfect square of decreasing order of digits
  static void sortArr(int arr[], int N)
  {

    // Traverse the array of strings
    for (int i = 0; i < N; i++) {

      // Convert the current array
      // element to a string
      String s = Integer.toString(arr[i]);
      char[] str = s.toCharArray();

      // Sort each string in descending order
      Arrays.sort(str);
      reverse(str);

      String string = new String(str);

      // Convert the string to
      // equivalent integer
      arr[i] = Integer.parseInt(string);

      // Calculate square root of
      // current array element
      int sr = (int)Math.sqrt(arr[i]);

      // Calculate perfect square
      int a = sr * sr;
      int b = (sr + 1) * (sr + 1);

      // Find the nearest perfect square
      if ((arr[i] - a) < (b - arr[i]))
        arr[i] = a;
      else
        arr[i] = b;
    }

    // Sort the array in ascending order
    Arrays.sort(arr);

    // Print the array
    for (int i = 0; i < N; i++) {
      System.out.print(arr[i] + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 29, 43, 28, 12 };
    int N = arr.length;
    sortArr(arr, N);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python 3 program of the above approach
import math

# Function to sort array in ascending order
# after replacing array elements by nearest
# perfect square of decreasing order of digits
def sortArr(arr, N):

    # Traverse the array of strings
    for i in range(N):

        # Convert the current array
        # element to a string
        s = str(arr[i])

        # Sort each string in descending order
        list1 = list(s)
        list1.sort(reverse = True)
        s = ''.join(list1)

        # Convert the string to
        # equivalent integer
        arr[i] = int(s)

        # Calculate square root of
        # current array element
        sr = int(math.sqrt(arr[i]))

        # Calculate perfect square
        a = sr * sr
        b = (sr + 1) * (sr + 1)

        # Find the nearest perfect square
        if ((arr[i] - a) < (b - arr[i])):
            arr[i] = a
        else:
            arr[i] = b

    # Sort the array in ascending order
    arr.sort()

    # Print the array
    for i in range(N):
        print(arr[i], end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [29, 43, 28, 12]
    N = len(arr)
    sortArr(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program of the above approach

using System;
using System.Collections.Generic;

class GFG{

  // Function to sort array in ascending order
  // after replacing array elements by nearest
  // perfect square of decreasing order of digits
  static void sortArr(int []arr, int N)
  {

    // Traverse the array of strings
    for (int i = 0; i < N; i++) {

      // Convert the current array
      // element to a string
      int num = arr[i];
      string s = num.ToString();

      // Sort each string in descending order
      char []temp = s.ToCharArray();
      Array.Sort(temp);
      int st = 0;
      int ed = temp.Length-1;
      while(st<ed){
        char ch = temp[st];
        temp[st] = temp[ed];
        temp[ed] = ch;
        st++;
        ed--;
      }
      string charsStr = new string(temp);
      // sort(s.begin(), s.end(), greater<char>());

      // Convert the string to
      // equivalent integer
      arr[i] = Int32.Parse(charsStr);

      // Calculate square root of
      // current array element
      int sr = (int)Math.Sqrt(arr[i]);

      // Calculate perfect square
      int a = sr * sr;
      int b = (sr + 1) * (sr + 1);

      // Find the nearest perfect square
      if ((arr[i] - a) < (b - arr[i]))
        arr[i] = a;
      else
        arr[i] = b;
    }

    // Sort the array in ascending order
    Array.Sort(arr);

    // Print the array
    for (int i = 0; i < N; i++) {
      Console.Write(arr[i]+" ");
    }
  }

  // Driver Code
  public static void Main()
  {
    int []arr = { 29, 43, 28, 12 };
    int N = arr.Length;
    sortArr(arr, N);

  }
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

      // JavaScript program of the above approach
      // Function to sort array in ascending order
      // after replacing array elements by nearest
      // perfect square of decreasing order of digits

      function sortArr(arr, N) {
        // Traverse the array of strings
        for (var i = 0; i < N; i++) {
          // Convert the current array
          // element to a string
          var num = arr[i];
          var s = num.toString();

          // Sort each string in descending order
          var temp = s.split("");
          temp.sort((a, b) => b - a);
          s = temp.join("");

          // Convert the string to
          // equivalent integer
          arr[i] = parseInt(s);

          // Calculate square root of
          // current array element
          var sr = parseInt(Math.sqrt(arr[i]));

          // Calculate perfect square
          var a = sr * sr;
          var b = (sr + 1) * (sr + 1);

          // Find the nearest perfect square
          if (arr[i] - a < b - arr[i]) arr[i] = a;
          else arr[i] = b;
        }

        // Sort the array in ascending order
        arr.sort((a, b) => a - b);

        // Print the array
        for (var i = 0; i < N; i++) {
          document.write(arr[i] + " ");
        }
      }

      // Driver Code
      var arr = [29, 43, 28, 12];
      var N = arr.length;
      sortArr(arr, N);

</script>
```

**Output:** 

```
25 49 81 100
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*