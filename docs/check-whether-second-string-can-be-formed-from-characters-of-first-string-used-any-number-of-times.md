# 检查第二个字符串是否可以由第一个字符串的字符任意多次使用形成

> 原文:[https://www . geeksforgeeks . org/check-第二个字符串是否可以由第一个字符串使用任意次数的字符构成/](https://www.geeksforgeeks.org/check-whether-second-string-can-be-formed-from-characters-of-first-string-used-any-number-of-times/)

给定两根尺寸为 **N** 的线 **str1** 和尺寸为 **M** 的线 **str2** 。任务是找出是否有可能仅使用 **str1** 的字符来组成 **str2** ，使得 **str1** 的每个字符可以被使用任意次数。
**注:**小写字母和大写字母应视为不同。

**例:**

> **输入:** str1 =“快棕狐狸跳”，str2 =“狐狸比狗快”
> **输出:**无
> **说明:**
> 在 **str2** 中，有 **d** 字符，而 **str1** 中没有。所以，不可能从**串**到
> 串**串 2**
> 
> **输入:** str1 =“我们都喜欢极客”str2 =“我们都喜欢极客”
> T3】输出:是

**天真方法:**最简单的方法是搜索 **str1** 中 **str2** 的每个字符。如果找到所有字符，则打印“是”。否则打印“否”。

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*

**有效方法:**想法是在**计数【】**数组中标记 **str1** 所有角色的存在。然后遍历 **str2** ，检查 **str1** 中是否有 str2 的字符。

1.  制作一个大小为 256 的数组**计数[]** (总的 [ASCII](https://www.geeksforgeeks.org/program-print-ascii-value-character/) 字符数)并设置为零。
2.  然后迭代 **str1** 并使**计数[str[i]] = 1** 来标记每个字符的出现。
3.  迭代 **str2** 并检查该字符是否出现在 **str1** 中，或者是否使用 **count[]** 数组。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if
// str2 can be made by characters
// of str1 or not
void isPossible(string str1, string str2)
{
    // To store the
    // occurrence of every
    // character
    int arr[256] = { 0 };

    // Length of the two
    // strings
    int l1 = str1.size();
    int l2 = str2.size();

    int i, j;

    // Assume that it is
    // possible to compose the
    // string str2 from str1
    bool possible = true;

    // Iterate over str1
    for (i = 0; i < l1; i++) {
        // Store the presence of every
        // character
        arr[str1[i]] = 1;
    }

    // Iterate over str2
    for (i = 0; i < l2; i++) {

        // Ignore the spaces
        if (str2[i] != ' ') {

            // Check for the presence
            // of character in str1
            if (arr[str2[i]] == 1)
                continue;

            else {
                possible = false;
                break;
            }
        }
    }

    // If it is possible to make
    // str2 from str1
    if (possible) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}

// Driver Code
int main()
{
    // Given strings
    string str1 = "we all love geeksforgeeks";
    string str2 = "we all love geeks";

    // Function Call
    isPossible(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach

import java.util.Arrays;

class GFG {

    // Function to check if
    // str2 can be made by characters
    // of str1 or not
    public static void isPossible(String str1, String str2) {
        // To store the
        // occurrence of every
        // character
        int arr[] = new int[256];

        Arrays.fill(arr, 0);
        // Length of the two
        // strings
        int l1 = str1.length();
        int l2 = str2.length();

        int i, j;

        // Assume that it is
        // possible to compose the
        // string str2 from str1
        boolean possible = true;

        // Iterate over str1
        for (i = 0; i < l1; i++) {
            // Store the presence of every
            // character
            arr[str1.charAt(i)] = 1;
        }

        // Iterate over str2
        for (i = 0; i < l2; i++) {

            // Ignore the spaces
            if (str2.charAt(i) != ' ') {

                // Check for the presence
                // of character in str1
                if (arr[str2.charAt(i)] == 1)
                    continue;

                else {
                    possible = false;
                    break;
                }
            }
        }

        // If it is possible to make
        // str2 from str1
        if (possible) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given strings
        String str1 = "we all love geeksforgeeks";
        String str2 = "we all love geeks";

        // Function Call
        isPossible(str1, str2);

    }

}

// This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if
// str2 can be made by characters
// of str1 or not
static void isPossible(string str1, string str2)
{

    // To store the
    // occurrence of every
    // character
    int []arr = new int[256];
    Array.Clear(arr,0,256);

    // Length of the two
    // strings
    int l1 = str1.Length;
    int l2 = str2.Length;

    int i;

    // Assume that it is
    // possible to compose the
    // string str2 from str1
    bool possible = true;

    // Iterate over str1
    for (i = 0; i < l1; i++) {
        // Store the presence of every
        // character
        arr[str1[i]] = 1;
    }

    // Iterate over str2
    for (i = 0; i < l2; i++) {

        // Ignore the spaces
        if (str2[i] != ' ') {

            // Check for the presence
            // of character in str1
            if (arr[str2[i]] == 1)
                continue;

            else {
                possible = false;
                break;
            }
        }
    }

    // If it is possible to make
    // str2 from str1
    if (possible) {
        Console.Write("Yes");
    }
    else {
        Console.Write("No");
    }
}

// Driver Code
public static void Main()
{
    // Given strings
    string str1 = "we all love geeksforgeeks";
    string str2 = "we all love geeks";

    // Function Call
    isPossible(str1, str2);
}
}

// This code is contributed by ipg2016107.
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to check if
# str2 can be made by characters
# of str1 or not
def isPossible(str1, str2):

      # To store the
    # occurrence of every
    # character
    arr = {}

    # Length of the two
    # strings
    l1 = len(str1)
    l2 = len(str2)

        # Assume that it is
    # possible to compose the
    # string str2 from str1
    possible = True

        # Iterate over str1
    for i in range(l1):

      # Store the presence or every element
        arr[str1[i]] = 1

        # Iterate over str2
    for i in range(l2):

      # Ignore the spaces
        if str2[i] != ' ':

              # Check for the presence
           # of character in str1
            if arr[str2[i]] == 1:
                continue
            else:
                possible = False
                break

     # If it is possible to make
    # str2 from str1          
    if possible:
        print("Yes")
    else:
        print("No")

# Driver code
str1 = "we all love geeksforgeeks"
str2 = "we all love geeks"

# Function call.
isPossible(str1, str2)

# This code is contributed by Parth Manchanda
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

// Function to check if
// str2 can be made by characters
// of str1 or not
function isPossible(str1, str2) {
  // To store the
  // occurrence of every
  // character
  let arr = new Array(256).fill(0);

  // Length of the two
  // strings
  let l1 = str1.length;
  let l2 = str2.length;

  let i, j;

  // Assume that it is
  // possible to compose the
  // string str2 from str1
  let possible = true;

  // Iterate over str1
  for (i = 0; i < l1; i++) {
    // Store the presence of every
    // character
    arr[str1[i]] = 1;
  }

  // Iterate over str2
  for (i = 0; i < l2; i++) {
    // Ignore the spaces
    if (str2[i] != " ") {
      // Check for the presence
      // of character in str1
      if (arr[str2[i]] == 1) continue;
      else {
        possible = false;
        break;
      }
    }
  }

  // If it is possible to make
  // str2 from str1
  if (possible) {
    document.write("Yes<br>");
  } else {
    document.write("No<br>");
  }
}

// Driver Code

// Given strings
let str1 = "we all love geeksforgeeks";
let str2 = "we all love geeks";

// Function Call
isPossible(str1, str2);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N+M)*
***辅助空间:** O(1)*