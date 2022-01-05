# 按排序顺序打印给定数字中的所有重复数字

> 原文:[https://www . geesforgeks . org/print-all-repeating-digits-present-in-给定的数字-按排序顺序/](https://www.geeksforgeeks.org/print-all-repeating-digits-present-in-a-given-number-in-sorted-order/)

给定一个整数 **N** ，任务是按排序顺序打印所有出现在 **N** 中的重复数字。

**示例:**

> **输入:** N = 45244336543
> **输出:** 3 4 5
> **说明:**重复数字为 3 4 5
> 
> **输入:** N = 987065467809
> **输出:** 0 6 7 8 9

**方式:**思路是用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)存储 **N** 的数字的[频率，打印那些频率超过 **1 的数字。**](https://www.geeksforgeeks.org/find-the-frequency-of-a-digit-in-a-number/)

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，存储数字 **0-9** 的频率。
*   [将整数转换为其等价字符串](https://www.geeksforgeeks.org/different-ways-for-integer-to-string-conversions-in-java/)。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，对于每个字符，执行以下步骤:
    *   [使用](https://www.geeksforgeeks.org/convert-char-to-int-in-java-with-examples/)[打字](https://www.geeksforgeeks.org/type-conversion-in-c/)将当前字符转换为整数
    *   在[哈希表](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)中增加该数字的计数。
*   [遍历 HashMap](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) 打印计数超过 1 的数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print repeating
// digits present in the number N
void printDup(string N)
{
  // Stores the count of
  // unique digits
  int res = 0;

  // Map to store frequency
  // of each digit
  int cnt[10];

  // Set count of all digits to 0
  for (int i = 0; i < 10; i++)
    cnt[i] = 0;

  // Traversing the string
  for (int i = 0; i < N.size(); i++) {

    // Convert the character
    // to equivalent integer
    int digit = (N[i] - '0');

    // Increase the count of digit
    cnt[digit] += 1;
  }

  // Traverse the Map
  for (int i = 0; i < 10; i++) {

    // If frequency
    // of digit exceeds 1
    if (cnt[i] > 1)
      cout << i << " ";
  }

  cout << endl;
}

// Driver Code
int main()
{

  string N = "45244336543";

  // Function call to print
  // repeating digits in N
  printDup(N);

  return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

  // Function to print repeating
  // digits present in the number N
  static void printDup(String N)
  {
    // Stores the count of
    // unique digits
    int res = 0;

    // Map to store frequency
    // of each digit
    int cnt[] = new int[10];

    // Traversing the string
    for (int i = 0; i < N.length(); i++) {

      // Convert the character
      // to equivalent integer
      int digit = (N.charAt(i) - '0');

      // Increase the count of digit
      cnt[digit] += 1;
    }

    // Traverse the Map
    for (int i = 0; i < 10; i++) {

      // If frequency
      // of digit exceeds 1
      if (cnt[i] > 1)
        System.out.print(i + " ");
    }

    System.out.println();
  }

  // Driver Code
  public static void main(String[] args)
  {

    String N = "45244336543";

    // Function call to print
    // repeating digits in N
    printDup(N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python implementation
# of the above approach

# Function to print repeating
# digits present in the number N
def printDup(N):

    # Stores the count of
    # unique digits
    res = 0

    # Set count of all digits to 0
    cnt = [0] * 10

    # Convert integer to
    # equivalent string
    string = str(N)

    # Traversing the string
    for i in string:

        # Convert the character
        # to equivalent integer
        digit = int(i)

        # Increase the count of digit
        cnt[digit] += 1

    # Traverse the Map
    for i in range(10):

        # If frequency
        # of digit is 1
        if (cnt[i] > 1):

            # If count exceeds 1
            print(i, end=" ")

# Driver Code

N = 45244336543

# Function call to print
# repeating digits in N
printDup(N)
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

  // Function to print repeating
  // digits present in the number N
  static void printDup(string N)
  {

    // Stores the count of
    // unique digits
    int res = 0;

    // Map to store frequency
    // of each digit
    int[] cnt = new int[10];

    // Traversing the string
    for (int i = 0; i < N.Length; i++) {

      // Convert the character
      // to equivalent integer
      int digit = (N[i] - '0');

      // Increase the count of digit
      cnt[digit] += 1;
    }

    // Traverse the Map
    for (int i = 0; i < 10; i++) {

      // If frequency
      // of digit exceeds 1
      if (cnt[i] > 1)
        Console.Write(i + " ");
    }

    Console.WriteLine();
  }

  // Driver code
  public static void Main()
  {

    string N = "45244336543";

    // Function call to print
    // repeating digits in N
    printDup(N);
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print repeating
// digits present in the number N
function printDup(N)
{
  // Stores the count of
  // unique digits
  var res = 0;

  // Map to store frequency
  // of each digit
  var cnt = Array(10);

  // Set count of all digits to 0
  for (var i = 0; i < 10; i++)
    cnt[i] = 0;

  // Traversing the string
  for (var i = 0; i < N.length; i++) {

    // Convert the character
    // to equivalent integer
    var digit = (N[i] - '0');

    // Increase the count of digit
    cnt[digit] += 1;
  }

  // Traverse the Map
  for (var i = 0; i < 10; i++) {

    // If frequency
    // of digit exceeds 1
    if (cnt[i] > 1)
      document.write( i + " ");
  }

  document.write("<br>");
}

// Driver Code
var N = "45244336543";
// Function call to print
// repeating digits in N
printDup(N);

</script>
```

**Output:** 

```
3 4 5
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*