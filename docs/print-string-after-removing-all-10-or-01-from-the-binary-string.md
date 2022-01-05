# 从二进制字符串中删除所有(“10”或“01”)后打印字符串

> 原文:[https://www . geesforgeks . org/从二进制字符串中删除所有 10 或 01 后打印字符串/](https://www.geeksforgeeks.org/print-string-after-removing-all-10-or-01-from-the-binary-string/)

给定一个仅由 0 和 1 组成的二进制字符串 **str** ，任务是在从字符串中逐个删除“10”和“01”后打印该字符串。如果字符串为空，则打印-1。

**示例:**

> **输入:** str = "101100"
> **输出:** -1
> **解释:**
> 第一步，从字符串中移除索引 0 和 1 处的“10”。
> 101100 - > 1100
> 在第二步中，从字符串中删除索引 1 和 2 处的“10”。
> 1100 - > 10
> 最后去掉“10”，串变成空的。
> 10 - >空
> 
> **输入:** str = "010110100"
> **输出:** 0
> **解释:**
> 在第一步中，从字符串中删除索引 0 和 1 处的“01”。
> 010110100 - > 0110100
> 在第二步中，从字符串中删除索引 0 和 1 处的“01”。
> 0110100 - > 10100
> 在第三步中，从字符串中删除索引 0 和 1 处的“10”。
> 10100 - > 100
> 最后去掉“10”，字符串变为“0”。
> 100 - > 0

**观察:**仔细观察，由于给定的字符串是二进制字符串，除了字符串中存在的不能与其补语配对的额外 0 和 1 之外，所有字符串都可以被清除。例如:

> Let str = "010110100 "。
> 对于这个字符串，0 的个数是 5，1 的个数是 4。
> 现在，让我们开始一个接一个地移除替换子字符串:
> 
> 1.  **01** 0110100 - > 0110100
> 2.  **01** 10100 - > 10100
> 3.  **10** 100 - > 100
> 4.  **10** 0 - > 0
> 
> 此时，字符串不能进一步减少。

因此，从上面的例子可以看出，只要字符串中有 1 和 0，字符串就可以减少。
我们已经在上一篇文章中讨论了查找 0 和 1 的[删除计数的方法。在这里，我们对前面的方法做了一点修改，在所有可能的删除之后生成剩余的字符串。](https://www.geeksforgeeks.org/deletions-of-01-or-10-in-binary-string-to-make-it-free-from-01-or-10/)

**方法:**从上面的观察可以得出结论，最终的字符串只包含**额外的 1 或 0**，它们不能与字符串中的任何数字配对。因此，解决这个问题的思路是对字符串中 0 和 1 的**数**进行计数，找出两个计数之间的**差**。该计数表示基于较高值的**剩余 1 或 0**的数量。

可以按照以下步骤计算答案:

1.  获取字符串中存在的 0 的**计数**，并将其存储在变量中**。**
2.  **获取字符串中存在的 1 的**计数，并将其存储在另一个变量中。****
3.  **如果 1 的**计数等于 0 的**，则可以减少整个字符串。因此，返回 **-1** 。**
4.  **如果 **1 的计数大于 0**的计数，那么最后剩下许多 1，进一步减少是不可能的。因此，将许多 **1 的**追加到一个空字符串中并返回该字符串。**
5.  **类似地，如果 **0 的计数大于 1 的计数**，则找出差异，并将那些许多 **0 的**附加到空字符串中并返回。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to print the final string
// after removing all the occurrences of
// "10" and "01" from the given binary string
#include <bits/stdc++.h>
using namespace std;

// Function to print the final string
// after removing all the occurrences of
// "10" and "01" from the given binary string
void finalString(string str)
{

    // Variables to store the
    // count of 1's and 0's
    int x = 0, y = 0;

    // Variable left will store
    // whether 0's or 1's is left
    // in the final string
    int left;

    // Length of the string
    int n = str.length();

    // For loop to count the occurrences
    // of 1's and 0's in the string
    for (int i = 0; i < n; i++) {
        if (str[i] == '1')
            x++;
        else
            y++;
    }

    // To check if the count of 1's is
    // greater than the count of 0's or not.
    // If x is greater, then those many 1's
    // are printed.
    if (x > y)
        left = 1;
    else
        left = 0;

    // Length of the final remaining string
    // after removing all the occurrences
    int length = n - 2 * min(x, y);

    // Printing the final string
    for (int i = 0; i < length; i++) {
        cout << left;
    }
}

// Driver Code
int main()
{
    string str = "010110100100000";
    finalString(str);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to print the final String
// after removing all the occurrences of
// "10" and "01" from the given binary String
import java.util.*;

class GFG{

// Function to print the final String
// after removing all the occurrences of
// "10" and "01" from the given binary String
static void finalString(String str)
{

    // Variables to store the
    // count of 1's and 0's
    int x = 0, y = 0;

    // Variable left will store
    // whether 0's or 1's is left
    // in the final String
    int left;

    // Length of the String
    int n = str.length();

    // For loop to count the occurrences
    // of 1's and 0's in the String
    for (int i = 0; i < n; i++) {
        if (str.charAt(i) == '1')
            x++;
        else
            y++;
    }

    // To check if the count of 1's is
    // greater than the count of 0's or not.
    // If x is greater, then those many 1's
    // are printed.
    if (x > y)
        left = 1;
    else
        left = 0;

    // Length of the final remaining String
    // after removing all the occurrences
    int length = n - 2 * Math.min(x, y);

    // Printing the final String
    for (int i = 0; i < length; i++) {
        System.out.print(left);
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "010110100100000";
    finalString(str);
}
}

// This code is contributed by sapnasingh4991
```

## **蟒蛇 3**

```
# Python 3 program to print the final string
# after removing all the occurrences of
# "10" and "01" from the given binary string

# Function to print the final string
# after removing all the occurrences of
# "10" and "01" from the given binary string
def finalString(st):

    # Variables to store the
    # count of 1's and 0's
    x , y = 0 , 0

    # Length of the string
    n = len(st)

    # For loop to count the occurrences
    # of 1's and 0's in the string
    for i in range( n):
        if (st[i] == '1'):
            x += 1
        else:
            y += 1

    # To check if the count of 1's is
    # greater than the count of 0's or not.
    # If x is greater, then those many 1's
    # are printed.
    if (x > y):
        left = 1
    else:
        left = 0

    # Length of the final remaining string
    # after removing all the occurrences
    length = n - 2 * min(x, y);

    # Printing the final string
    for i in range(length):
        print(left, end="")

# Driver Code
if __name__ == "__main__":
    st = "010110100100000"
    finalString(st)

# This code is contributed by chitranayal

```

## **C#**

```
// C# program to print the readonly String
// after removing all the occurrences of
// "10" and "01" from the given binary String
using System;

class GFG{

// Function to print the readonly String
// after removing all the occurrences of
// "10" and "01" from the given binary String
static void finalString(String str)
{

    // Variables to store the
    // count of 1's and 0's
    int x = 0, y = 0;

    // Variable left will store
    // whether 0's or 1's is left
    // in the readonly String
    int left;

    // Length of the String
    int n = str.Length;

    // For loop to count the occurrences
    // of 1's and 0's in the String
    for (int i = 0; i < n; i++) {
        if (str[i] == '1')
            x++;
        else
            y++;
    }

    // To check if the count of 1's is
    // greater than the count of 0's or not.
    // If x is greater, then those many 1's
    // are printed.
    if (x > y)
        left = 1;
    else
        left = 0;

    // Length of the readonly remaining String
    // after removing all the occurrences
    int length = n - 2 * Math.Min(x, y);

    // Printing the readonly String
    for (int i = 0; i < length; i++) {
        Console.Write(left);
    }
}

// Driver Code
public static void Main(String[] args)
{
    String str = "010110100100000";
    finalString(str);
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript program to print the final String
// after removing all the occurrences of
// "10" and "01" from the given binary String

// Function to print the final String
// after removing all the occurrences of
// "10" and "01" from the given binary String
function finalString(str)
{

    // Variables to store the
    // count of 1's and 0's
    let x = 0, y = 0;

    // Variable left will store
    // whether 0's or 1's is left
    // in the final String
    let left;

    // Length of the String
    let n = str.length;

    // For loop to count the occurrences
    // of 1's and 0's in the String
    for (let i = 0; i < n; i++) {
        if (str[i] == '1')
            x++;
        else
            y++;
    }

    // To check if the count of 1's is
    // greater than the count of 0's or not.
    // If x is greater, then those many 1's
    // are printed.
    if (x > y)
        left = 1;
    else
        left = 0;

    // Length of the final remaining String
    // after removing all the occurrences
    let length = n - 2 * Math.min(x, y);

    // Printing the final String
    for (let i = 0; i < length; i++) {
        document.write(left);
    }
}

// Driver Code

    let  str = "010110100100000";
    finalString(str);

</script>
```

****Output:** 

```
00000
```** 

****时间复杂度分析:****

*   **计算 1 和 0 出现次数的 for 循环需要 **O(N)** 时间，其中 N 是字符串的长度。**
*   **if 语句需要恒定的时间。所以 if 语句的时间复杂度是 **O(1)** 。**
*   **当整个字符串只有 0 或 1 时，打印最终字符串的循环在最坏的情况下需要 **O(N)****
*   **因此，整体时间复杂度为 **O(N)** 。**