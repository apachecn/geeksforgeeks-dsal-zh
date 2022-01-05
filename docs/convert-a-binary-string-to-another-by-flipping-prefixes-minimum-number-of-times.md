# 通过翻转前缀最少次数将二进制字符串转换为另一个

> 原文:[https://www . geesforgeks . org/convert-a-binary-string-to-other-by-flip-前缀-最小次数/](https://www.geeksforgeeks.org/convert-a-binary-string-to-another-by-flipping-prefixes-minimum-number-of-times/)

给定两个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **A** 和 **B** ，任务是通过重复翻转 **A** 的前缀，即反转所选前缀中位的出现顺序，将字符串 **A** 转换为 **B** 。打印所需的翻转次数和所有前缀的长度。

**示例:**

> **输入:** A = "01 "，B = "10"
> **输出:**
> 3
> 1 2 1
> **解释:**
> 操作 1:从字符串 A 中选择长度为 1 的前缀(= "01 ")。翻转前缀“0”会将字符串修改为“11”。
> 操作 2:从字符串 A 中选择长度为 2 的前缀(=“11”)。翻转前缀“11”会将字符串修改为“00”。
> 操作 3:从字符串 A 中选择长度为 1 的前缀(=“00”)。将前缀“0”翻转为“1”会将字符串修改为“10”，这与字符串 b 相同。
> 因此，所需的操作总数为 3。
> 
> **输入:** A = "0 "，B = " 1 "
> T3】输出:T5】1
> 1

**方法:**给定的问题可以通过逐个固定位来解决。要固定 **i <sup>第</sup>位**，当**A【I】**和**B【I】**不相等时，翻转长度前缀 **i** ，然后翻转长度前缀 **1** 。现在，翻转长度的前缀 **i** 。这三个操作不会改变 **A** 中的任何其他位。在 **A[i]** 不相等 **B[i]** 的所有指数上执行这些操作。由于每一位使用 3 次操作，总体来说将使用 **3 * N** 次操作。

为了最小化操作的数量，可以通过以相反的顺序逐个固定比特来修改上述方法。要固定 **i <sup>第</sup>位**，要么需要翻转长度为 **i** 的前缀，要么需要翻转第一位，然后需要翻转长度为 **i** 的前缀。但是按照相反的顺序，先前固定的位不会通过该过程再次翻转，并且每个位最多需要 **2** 次操作。因此，所需的最小操作次数为 **2*N** 。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number
// of operations required to convert
// string a to another string b
void minOperations(string a, string b, int n)
{
    // Store the lengths of each
    // prefixes selected
    vector<int> ops;

    // Traverse the string
    for (int i = n - 1; i >= 0; i--) {
        if (a[i] != b[i]) {

            // If first character
            // is same as b[i]
            if (a[0] == b[i]) {

                // Insert 1 to ops[]
                ops.push_back(1);

                // And, flip the bit
                a[0] = '0' + !(a[0] - '0');
            }

            // Reverse the prefix
            // string of length i + 1
            reverse(a.begin(), a.begin() + i + 1);

            // Flip the characters
            // in this prefix length
            for (int j = 0; j <= i; j++) {
                a[j] = '0' + !(a[j] - '0');
            }

            // Push (i + 1) to array ops[]
            ops.push_back(i + 1);
        }
    }

    // Print the number of operations
    cout << ops.size() << "\n";

    // Print the length of
    // each prefixes stored
    for (int x : ops) {
        cout << x << ' ';
    }
}

// Driver Code
int main()
{
    string a = "10", b = "01";
    int N = a.size();

    minOperations(a, b, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG
{

  // Function to count minimum number
  // of operations required to convert
  // string a to another string b
  static void minOperations(String s1, String s2, int n)
  {

    char a[] = s1.toCharArray();
    char b[] = s2.toCharArray();

    // Store the lengths of each
    // prefixes selected
    ArrayList<Integer> ops = new ArrayList<>();

    // Traverse the string
    for (int i = n - 1; i >= 0; i--) {
      if (a[i] != b[i]) {

        // If first character
        // is same as b[i]
        if (a[0] == b[i]) {

          // Insert 1 to ops[]
          ops.add(1);

          // And, flip the bit
          a[0] = (a[0] == '0' ? '1' : '0');
        }

        // Reverse the prefix
        // string of length i + 1
        reverse(a, 0, i);

        // Flip the characters
        // in this prefix length
        for (int j = 0; j <= i; j++) {
          a[j] = (a[j] == '0' ? '1' : '0');
        }

        // Push (i + 1) to array ops[]
        ops.add(i + 1);
      }
    }

    // Print the number of operations
    System.out.println(ops.size());

    // Print the length of
    // each prefixes stored
    for (int x : ops) {
      System.out.print(x + " ");
    }
  }

  // Function to reverse a[]
  // from start to end
  static void reverse(char a[], int start, int end)
  {

    while (start < end) {
      char temp = a[start];
      a[start] = a[end];
      a[end] = temp;
      start++;
      end--;
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    String a = "10", b = "01";
    int N = a.length();

    minOperations(a, b, N);
  }
}

// This code is contributed by Kingash.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to count minimum number
  // of operations required to convert
  // string a to another string b
  static void minOperations(string s1, string s2, int n)
  {

    char[] a = s1.ToCharArray();
    char[] b = s2.ToCharArray();

    // Store the lengths of each
    // prefixes selected
    List<int> ops = new List<int>();

    // Traverse the string
    for (int i = n - 1; i >= 0; i--) {
      if (a[i] != b[i]) {

        // If first character
        // is same as b[i]
        if (a[0] == b[i]) {

          // Insert 1 to ops[]
          ops.Add(1);

          // And, flip the bit
          a[0] = (a[0] == '0' ? '1' : '0');
        }

        // Reverse the prefix
        // string of length i + 1
        reverse(a, 0, i);

        // Flip the characters
        // in this prefix length
        for (int j = 0; j <= i; j++) {
          a[j] = (a[j] == '0' ? '1' : '0');
        }

        // Push (i + 1) to array ops[]
        ops.Add(i + 1);
      }
    }

    // Print the number of operations
    Console.WriteLine(ops.Count);

    // Print the length of
    // each prefixes stored
    foreach (int x in ops) {
      Console.Write(x + " ");
    }
  }

  // Function to reverse a[]
  // from start to end
  static void reverse(char[] a, int start, int end)
  {

    while (start < end) {
      char temp = a[start];
      a[start] = a[end];
      a[end] = temp;
      start++;
      end--;
    }
  }

  // Driver Code
  public static void Main()
  {
    string a = "10", b = "01";
    int N = a.Length;

    minOperations(a, b, N);
  }
}

// This code is contributed by souravghosh0416.
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach
      // Function to count minimum number
      // of operations required to convert
      // string a to another string b
      function minOperations(s1, s2, n) {
        var a = s1.split("");
        var b = s2.split("");

        // Store the lengths of each
        // prefixes selected
        var ops = [];

        // Traverse the string
        for (var i = n - 1; i >= 0; i--) {
          if (a[i] !== b[i]) {
            // If first character
            // is same as b[i]
            if (a[0] === b[i]) {
              // Insert 1 to ops[]
              ops.push(1);

              // And, flip the bit
              a[0] = a[0] === "0" ? "1" : "0";
            }

            // Reverse the prefix
            // string of length i + 1
            reverse(a, 0, i);

            // Flip the characters
            // in this prefix length
            for (var j = 0; j <= i; j++) {
              a[j] = a[j] === "0" ? "1" : "0";
            }

            // Push (i + 1) to array ops[]
            ops.push(i + 1);
          }
        }

        // Print the number of operations
        document.write(ops.length + "<br>");

        // Print the length of
        // each prefixes stored
        for (const x of ops) {
          document.write(x + " ");
        }
      }

      // Function to reverse a[]
      // from start to end
      function reverse(a, start, end) {
        while (start < end) {
          var temp = a[start];
          a[start] = a[end];
          a[end] = temp;
          start++;
          end--;
        }
      }

      // Driver Code
      var a = "10", b = "01";
      var N = a.length;

      minOperations(a, b, N);
</script>
```

**Output:** 

```
3
1 2 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*