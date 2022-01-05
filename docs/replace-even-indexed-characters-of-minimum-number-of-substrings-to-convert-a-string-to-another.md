# 替换最小数量子字符串的偶数索引字符，将一个字符串转换为另一个

> 原文:[https://www . geesforgeks . org/replace-even-indexed-字符-最小数量的子字符串-将字符串转换为另一个/](https://www.geeksforgeeks.org/replace-even-indexed-characters-of-minimum-number-of-substrings-to-convert-a-string-to-another/)

给定两个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)、 **str1** 和 **str2** ，任务是通过选择一个[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)并将出现在子串偶数索引处的所有字符替换为任意可能的字符，偶数次，将字符串 **str1** 转换为字符串 **str2** 。

**示例:**

> **输入:**str1 =“abcdef”，str 2 =“ffffff”
> T3】输出: 2
> **解释:**
> 选择子串{str1[0]，…，str[4]}并用‘f’替换子串的所有偶数索引将 str 1 修改为“fbfdff”。
> 选择子串{str1[1]，…，str[3]}并用‘f’替换子串的所有偶数索引，将 str1 修改为“ffffff”，与 str2 相同。
> 因此，要求输出为 2。
> 
> **输入:**str 1 =“rtrtyy”，str2 =“wtzy”
> T3】输出: 1
> **解释:**
> 选择子串{str1[0]，…，str[4]}并将 str1[0]替换为‘w’，将 str1[[2]替换为‘w’，将 str[4]修改为‘t’，与 str 2 相同。因此，所需的输出为 1。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntOp** ，以存储将字符串 **str1** 转换为 **str2** 所需的给定操作的最小计数。
*   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。对于每个 i <sup>第</sup>指数，检查**str 1【I】**和**str 2【I】**是否相同。如果发现不同，则找到最长的[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，该子串可能在两个串的偶数索引处包含不同的字符。替换 **str1** 子串的偶数索引字符，并将 **cntOp** 的值增加 **1** 。
*   最后，打印 **cntOp** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number of
// substrings of str1 such that replacing
// even-indexed characters of those substrings
// converts the string str1 to str2
int minOperationsReq(string str1, string str2)
{
    // Stores length of str1
    int N = str1.length();

    // Stores minimum count of operations
    // to convert str1 to str2
    int cntOp = 0;

    // Traverse both the given string
    for (int i = 0; i < N; i++) {

        // If current character in
        // both the strings are equal
        if (str1[i] == str2[i]) {
            continue;
        }

        // Stores current index
        // of the string
        int ptr = i;

        // If current character in both
        // the strings are not equal
        while (ptr < N && str1[ptr] != str2[ptr]) {

            // Replace str1[ptr]
            // by str2[ptr]
            str1[ptr] = str2[ptr];

            // Update ptr
            ptr += 2;
        }

        // Update cntOp
        cntOp++;
    }

    return cntOp;
}

// Driver Code
int main()
{
    string str1 = "abcdef";
    string str2 = "ffffff";

    cout << minOperationsReq(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;

class GFG {

    // Function to count the minimum number of
    // substrings of str1 such that replacing
    // even-indexed characters of those substrings
    // converts the string str1 to str2
    static int min_Operations(String str1,
                              String str2)
    {
        // Stores length of str1
        int N = str1.length();

        // Convert str1 to character array
        char[] str = str1.toCharArray();

        // Stores minimum count of operations
        // to convert str1 to str2
        int cntOp = 0;

        // Traverse both the given string
        for (int i = 0; i < N; i++) {

            // If current character in both
            // the strings are equal
            if (str[i] == str2.charAt(i)) {
                continue;
            }

            // Stores current index
            // of the string
            int ptr = i;

            // If current character in both the
            // string are not equal
            while (ptr < N && str[ptr] != str2.charAt(ptr)) {

                // Replace str1[ptr]
                // by str2[ptr]
                str[ptr] = str2.charAt(ptr);

                // Update ptr
                ptr += 2;
            }

            // Update cntOp
            cntOp++;
        }

        return cntOp;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str1 = "abcdef";
        String str2 = "ffffff";
        System.out.println(
            min_Operations(str1, str2));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the minimum number of
# substrings of str1 such that replacing
# even-indexed characters of those substrings
# converts the str1 to str2
def minOperationsReq(str11, str22):

    str1 = list(str11)
    str2 = list(str22)

    # Stores length of str1
    N = len(str1)

    # Stores minimum count of operations
    # to convert str1 to str2
    cntOp = 0

    # Traverse both the given string
    for i in range(N):

        # If current character in
        # both the strings are equal
        if (str1[i] == str2[i]):
            continue

        # Stores current index
        # of the string
        ptr = i

        # If current character in both
        # the strings are not equal
        while (ptr < N and str1[ptr] != str2[ptr]):

            # Replace str1[ptr]
            # by str2[ptr]
            str1[ptr] = str2[ptr]

            # Update ptr
            ptr += 2

        # Update cntOp
        cntOp += 1

    return cntOp

# Driver Code
str1 = "abcdef"
str2 = "ffffff"

print(minOperationsReq(str1, str2))

# This code is contributed by code_hunt
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

    // Function to count the minimum number of
    // substrings of str1 such that replacing
    // even-indexed characters of those substrings
    // converts the string str1 to str2
    static int min_Operations(String str1,
                              String str2)
    {

        // Stores length of str1
        int N = str1.Length;

        // Convert str1 to character array
        char[] str = str1.ToCharArray();

        // Stores minimum count of operations
        // to convert str1 to str2
        int cntOp = 0;

        // Traverse both the given string
        for (int i = 0; i < N; i++)
        {

            // If current character in both
            // the strings are equal
            if (str[i] == str2[i])
            {
                continue;
            }

            // Stores current index
            // of the string
            int ptr = i;

            // If current character in both the
            // string are not equal
            while (ptr < N && str[ptr] != str2[ptr])
            {

                // Replace str1[ptr]
                // by str2[ptr]
                str[ptr] = str2[ptr];

                // Update ptr
                ptr += 2;
            }

            // Update cntOp
            cntOp++;
        }

        return cntOp;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str1 = "abcdef";
        String str2 = "ffffff";
        Console.WriteLine(
            min_Operations(str1, str2));
    }
}

// This code contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the minimum number of
    // substrings of str1 such that replacing
    // even-indexed characters of those substrings
    // converts the string str1 to str2
    function min_Operations( str1,  str2)
    {
        // Stores length of str1
    var N = str1.length;

    // Stores minimum count of operations
    // to convert str1 to str2
    var cntOp = 0;

    // Traverse both the given string
    for (var i = 0; i < N; i++) {

        // If current character in
        // both the strings are equal
        if (str1.charCodeAt(i)== str2.charCodeAt(i))
        {

            continue;
        }

        // Stores current index
        // of the string
        var ptr = i;

        // If current character in both
        // the strings are not equal
        while (ptr < N && str1[ptr] != str2[ptr]) {

            // Replace str1[ptr]
            // by str2[ptr]

            str1 = str1.substring(0, ptr) + str2[ptr]
            + str1.substring(ptr + 1);
            // Update ptr
            ptr += 2;
        }

        // Update cntOp
        cntOp++;
    }

    return cntOp;
    }

    // Driver Code

         str1 = "abcdef";
         str2 = "ffffff";
        document.write(min_Operations(str1, str2));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)