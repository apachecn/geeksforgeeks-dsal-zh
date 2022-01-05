# 将二进制字符串转换为另一个字符串所需的最小前缀数

> 原文:[https://www . geesforgeks . org/最小前缀-要求将二进制字符串翻转转换为另一个/](https://www.geeksforgeeks.org/minimum-prefixes-required-to-be-flipped-to-convert-a-binary-string-to-another/)

给定两个[长度为](https://www.geeksforgeeks.org/tag/binary-string/) **N、**的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **A** 和 **B** ，任务是通过重复翻转 **A** 的前缀的所有位，将字符串从 **A** 转换为字符串 **B** ，即将前缀中的所有 **0** 转换为 **1** s，反之亦然并打印

**示例:**

> **输入:**A =“001”，B =“000”
> **输出:**
> 2
> 3 2
> **解释:**
> 翻转前缀“001”将字符串修改为“110”。
> 翻转前缀“11”将字符串修改为“000”。
> 
> **输入:**A =“1000”，B =“1011”
> **输出:**
> 2
> 4 2
> **解释:**
> 翻转前缀“1000”将字符串修改为“0111”。
> 翻转前缀“01”将字符串修改为“1011”。

**简单方法:**最简单的方法是[反向遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **A** ，对于获得的每个 **i** <sup>第</sup>个字符，使得**A【I】**不等于**B【I】**，从索引**【0，I】**翻转 **A** 中存在的字符，并将操作数增加 **1** 在完成字符串遍历后，打印操作计数和每个操作中选择的前缀长度。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**想法是通过反向遍历字符串 **A** 一次固定一位。维护一个布尔变量，比如**反转**，初始设置为**假**，表示 **A** 中的当前位是否翻转。遍历时，执行以下操作:

*   如果 **A** 中的 **iᵗʰ** 位不等于 **B** 和**反相**中的 **iᵗʰ** 位为**假**，则增加操作次数并将**反相**设置为**真**。
*   否则，如果 **A** 中的 **iᵗʰ** 位等于 **B** 中的 **iᵗʰ** 位，并且**反相**为**真**，则增加操作计数并将**反相**设置为**假**。

按照以下步骤解决问题:

*   初始化一个布尔变量，说**将**反相为**假，**表示 **A** 中的位是否翻转。
*   初始化一个空的[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如 **res，**来存储每个操作中的前缀长度。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N–1，0】**中迭代，并执行以下步骤:
    *   如果 **A[i]！= B[I]****反相**为**假**，则需要翻转当前位。因此。将 **(i + 1)** 插入数组 **res** 并将**反转**更新为 **true** 。
    *   否则，检查**A[I]= = B[I]****反相**是否为**真**，然后插入 **(i + 1)** 至 **res** ，更新**反相**至**假**。
*   将数组 **res** 的[大小打印为使两个字符串相等所需的操作数。](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)
*   然后，打印存储在 **res** 中的值，以表示每个操作中的前缀长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count flips required
// to make strings A and B equal
void findOperations(string A,
                    string B, int N)
{
    // Stores the count of the
    // number of operations
    int operations = 0;

    // Stores the length of
    // the chosen prefixes
    vector<int> ops;

    // Stores if operations are
    // performed even or odd times
    bool invert = false;

    // Traverse the given string
    for (int i = N - 1; i >= 0; i--) {

        // If current characters in
        // the two strings are unequal
        if (A[i] != B[i]) {

            // If A[i] is not flipped
            if (!invert) {

                // Increment count
                // of operations
                operations++;

                // Insert the length of
                // the chosen prefix
                ops.push_back(i + 1);

                // Update invert to true
                invert = true;
            }
        }

        else {

            // If A[i] is flipped
            if (invert) {

                // Increment count
                // of operations
                operations++;

                // Insert length of
                // the chosen prefix
                ops.push_back(i + 1);

                // Update invert to false
                invert = false;
            }
        }
    }

    // Print the number of
    // operations required
    cout << operations << endl;

    // Print the chosen prefix
    // length in each operation
    if (operations != 0) {
        for (auto x : ops)
            cout << x << " ";
    }
}

// Driver Code
int main()
{
    // Given binary strings
    string A = "001", B = "000";
    int N = A.size();

    findOperations(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

// Function to count flips required
// to make Strings A and B equal
static void findOperations(String A,
                    String B, int N)
{
    // Stores the count of the
    // number of operations
    int operations = 0;

    // Stores the length of
    // the chosen prefixes
    Vector<Integer> ops =  new Vector<>();

    // Stores if operations are
    // performed even or odd times
    boolean invert = false;

    // Traverse the given String
    for (int i = N - 1; i >= 0; i--) {

        // If current characters in
        // the two Strings are unequal
        if (A.charAt(i) != B.charAt(i)) {

            // If A[i] is not flipped
            if (!invert) {

                // Increment count
                // of operations
                operations++;

                // Insert the length of
                // the chosen prefix
                ops.add(i + 1);

                // Update invert to true
                invert = true;
            }
        }

        else {

            // If A[i] is flipped
            if (invert) {

                // Increment count
                // of operations
                operations++;

                // Insert length of
                // the chosen prefix
                ops.add(i + 1);

                // Update invert to false
                invert = false;
            }
        }
    }

    // Print the number of
    // operations required
    System.out.print(operations +"\n");

    // Print the chosen prefix
    // length in each operation
    if (operations != 0) {
        for (int x : ops)
            System.out.print(x+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given binary Strings
    String A = "001", B = "000";
    int N = A.length();

    findOperations(A, B, N);

}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count flips required
# to make strings A and B equal
def findOperations(A, B, N):

    # Stores the count of the
    # number of operations
    operations = 0

    # Stores the length of
    # the chosen prefixes
    ops = []

    # Stores if operations are
    # performed even or odd times
    invert = False

    # Traverse the given string
    for i in range(N - 1, -1, -1):

        # If current characters in
        # the two strings are unequal
        if (A[i] != B[i]):

            # If A[i] is not flipped
            if (not invert):

                # Increment count
                # of operations
                operations += 1

                # Insert the length of
                # the chosen prefix
                ops.append(i + 1)

                # Update invert to true
                invert = True
        else:

            # If A[i] is flipped
            if (invert):

                # Increment count
                # of operations
                operations += 1

                # Insert length of
                # the chosen prefix
                ops.append(i + 1)

                # Update invert to false
                invert = False

    # Print the number of
    # operations required
    print (operations)

    # Print the chosen prefix
    # length in each operation
    if (operations != 0):
        for x in ops:
            print(x, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given binary strings
    A, B = "001", "000"
    N = len(A)

    findOperations(A, B, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count flips required
// to make Strings A and B equal
static void findOperations(String A,
                           String B, int N)
{

    // Stores the count of the
    // number of operations
    int operations = 0;

    // Stores the length of
    // the chosen prefixes
    List<int> ops =  new List<int>();

    // Stores if operations are
    // performed even or odd times
    bool invert = false;

    // Traverse the given String
    for(int i = N - 1; i >= 0; i--)
    {

        // If current characters in
        // the two Strings are unequal
        if (A[i] != B[i])
        {

            // If A[i] is not flipped
            if (!invert)
            {

                // Increment count
                // of operations
                operations++;

                // Insert the length of
                // the chosen prefix
                ops.Add(i + 1);

                // Update invert to true
                invert = true;
            }
        }

        else
        {

            // If A[i] is flipped
            if (invert)
            {

                // Increment count
                // of operations
                operations++;

                // Insert length of
                // the chosen prefix
                ops.Add(i + 1);

                // Update invert to false
                invert = false;
            }
        }
    }

    // Print the number of
    // operations required
    Console.Write(operations + "\n");

    // Print the chosen prefix
    // length in each operation
    if (operations != 0)
    {
        foreach(int x in ops)
            Console.Write(x + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given binary Strings
    String A = "001", B = "000";
    int N = A.Length;

    findOperations(A, B, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to count flips required
      // to make Strings A and B equal
      function findOperations(A, B, N) {
        // Stores the count of the
        // number of operations
        var operations = 0;

        // Stores the length of
        // the chosen prefixes
        var ops = [];

        // Stores if operations are
        // performed even or odd times
        var invert = false;

        // Traverse the given String
        for (var i = N - 1; i >= 0; i--) {
          // If current characters in
          // the two Strings are unequal
          if (A[i] !== B[i]) {
            // If A[i] is not flipped
            if (!invert) {
              // Increment count
              // of operations
              operations++;

              // Insert the length of
              // the chosen prefix
              ops.push(i + 1);

              // Update invert to true
              invert = true;
            }
          } else {
            // If A[i] is flipped
            if (invert) {
              // Increment count
              // of operations
              operations++;

              // Insert length of
              // the chosen prefix
              ops.push(i + 1);

              // Update invert to false
              invert = false;
            }
          }
        }

        // Print the number of
        // operations required
        document.write(operations + "<br>");

        // Print the chosen prefix
        // length in each operation
        if (operations !== 0) {
          for (const x of ops) {
            document.write(x + " ");
          }
        }
      }

      // Driver Code
      // Given binary Strings
      var A = "001",
        B = "000";
      var N = A.length;

      findOperations(A, B, N);
    </script>
```

**Output:** 

```
2
3 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)