# 检查一个二进制字符串是否可以被分割成不相交的子序列，这些子序列等于“010”

> 原文:[https://www . geesforgeks . org/check-if-a-binary-string-can-split-in-unjoint-subseries-哪些-等于-010/](https://www.geeksforgeeks.org/check-if-a-binary-string-can-be-split-into-disjoint-subsequences-which-are-equal-to-010/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/string-data-structure/)、 **S** ，任务是检查是否有可能将该字符串划分为不相交的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)等于**“010”**。

**示例:**

> **输入:** S = "010100"
> **输出:**是
> **解释:**按照 **01** 010 **0** 的方式分割字符串，生成两个等于“010”的子序列。
> 
> **输入:**S = " 010000 "
> T3】输出:否

**方法:**这个想法是基于这样的观察:如果下列任何一个条件成立，给定的二进制字符串将不满足要求的条件:

*   如果在任何时候**‘1’**s 的前缀计数大于**‘0’**s 的前缀计数
*   如果在任何时候**‘1’**s 的后缀计数大于**‘0’**s 的后缀计数
*   如果整个字符串中**‘0’**的计数不等于**‘1’**的计数的两倍。

按照以下步骤解决问题:

1.  初始化一个布尔变量，**将**设为**真**检查字符串， **S** 是否满足给定条件。
2.  创建两个变量， **count0** 和 **count1** 到[存储字符串](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/)、 **S** 中 0 和 1 的频率。
3.  [使用变量 **i** 在范围**【0，N–1】**内遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、 **S**
    1.  如果 **S[i]** 等于 **1** ，则将 **count1** 的值增加 **1** 。
    2.  否则，用 **1** 递增**的值，计数 0** 。
    3.  检查**计数 1 >计数 0** 的值，然后将 **res** 更新为 **false** 。
4.  检查**计数 0** 的值是否不等于 **2 *计数 1** ，然后将 **res** 更新为 **false** 。
5.  将**计数 0** 和**计数 1** 的值重置为 **0** 。
6.  [反方向穿过弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，重复步骤 **3.1** 至 **3.3** 。
7.  如果 **res** 的值仍为 **true** ，则打印**是**结果，否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given string
// can be partitioned into a number of
// subsequences all of which are equal to "010"
bool isPossible(string s)
{
    // Store the size
    // of the string
    int n = s.size();

    // Store the count of 0s and 1s
    int count_0 = 0, count_1 = 0;

    // Traverse the given string
    // in the forward direction
    for (int i = 0; i < n; i++) {

        // If the character is '0',
        // increment count_0 by 1
        if (s[i] == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1 by 1
        else
            ++count_1;

        // If at any point,
        // count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }

    // If count_0 is not equal
    // to twice count_1,
    // return false
    if (count_0 != (2 * count_1))
        return false;

    // Reset the value of count_0 and count_1
    count_0 = 0, count_1 = 0;

    // Traverse the string in
    // the reverse direction
    for (int i = n - 1; i >= 0; --i) {

        // If the character is '0'
        // increment count_0
        if (s[i] == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1
        else
            ++count_1;

        // If count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }

    return true;
}

// Driver Code
int main()
{
    // Given string
    string s = "010100";

    // Function Call
    if (isPossible(s))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class MyClass
{

// Function to check if the given string
// can be partitioned into a number of
// subsequences all of which are equal to "010"
static boolean isPossible(String s)
{

    // Store the size
    // of the string
    int n = s.length();

    // Store the count of 0s and 1s
    int count_0 = 0, count_1 = 0;

    // Traverse the given string
    // in the forward direction
    for (int i = 0; i < n; i++) {

        // If the character is '0',
        // increment count_0 by 1
        if (s.charAt(i) == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1 by 1
        else
            ++count_1;

        // If at any point,
        // count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }

    // If count_0 is not equal
    // to twice count_1,
    // return false
    if (count_0 != (2 * count_1))
        return false;

    // Reset the value of count_0 and count_1
    count_0 = 0; count_1 = 0;

    // Traverse the string in
    // the reverse direction
    for (int i = n - 1; i >= 0; --i) {

        // If the character is '0'
        // increment count_0
        if (s.charAt(i) == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1
        else
            ++count_1;

        // If count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }

    return true;
}

// Driver Code
public static void main(String args[])
{
    // Given string
    String s = "010100";

    // Function Call
    if (isPossible(s))
         System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the given string
# can be partitioned into a number of
# subsequences all of which are equal to "010"
def isPossible(s):

    # Store the size
    # of the string
    n = len(s)

    # Store the count of 0s and 1s
    count_0, count_1 = 0, 0

    # Traverse the given string
    # in the forward direction
    for i in range(n):

        # If the character is '0',
        # increment count_0 by 1
        if (s[i] == '0'):
            count_0 += 1

        # If the character is '1'
        # increment count_1 by 1
        else:
            count_1 += 1

        # If at any point,
        # count_1 > count_0,
        # return false
        if (count_1 > count_0):
            return False

    # If count_0 is not equal
    # to twice count_1,
    # return false
    if (count_0 != (2 * count_1)):
        return False

    # Reset the value of count_0 and count_1
    count_0, count_1 = 0, 0

    # Traverse the string in
    # the reverse direction
    for i in range(n - 1, -1, -1):

        # If the character is '0'
        # increment count_0
        if (s[i] == '0'):
            count_0 += 1

        # If the character is '1'
        # increment count_1
        else:
            count_1 += 1

        # If count_1 > count_0,
        # return false
        if (count_1 > count_0):
            return False

    return True

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "010100"

    # Function Call
    if (isPossible(s)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the given string
// can be partitioned into a number of
// subsequences all of which are equal to "010"
static bool isPossible(String s)
{

    // Store the size
    // of the string
    int n = s.Length;

    // Store the count of 0s and 1s
    int count_0 = 0, count_1 = 0;

    // Traverse the given string
    // in the forward direction
    for(int i = 0; i < n; i++)
    {

        // If the character is '0',
        // increment count_0 by 1
        if (s[i] == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1 by 1
        else
            ++count_1;

        // If at any point,
        // count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }

    // If count_0 is not equal
    // to twice count_1,
    // return false
    if (count_0 != (2 * count_1))
        return false;

    // Reset the value of count_0 and count_1
    count_0 = 0;
    count_1 = 0;

    // Traverse the string in
    // the reverse direction
    for(int i = n - 1; i >= 0; --i)
    {

        // If the character is '0'
        // increment count_0
        if (s[i] == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1
        else
            ++count_1;

        // If count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }
    return true;
}

// Driver code
static public void Main()
{

    // Given string
    String s = "010100";

    // Function Call
    if (isPossible(s))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if the given string
// can be partitioned into a number of
// subsequences all of which are equal to "010"
function isPossible(s)
{
    // Store the size
    // of the string
    let n = s.length;

    // Store the count of 0s and 1s
    let count_0 = 0, count_1 = 0;

    // Traverse the given string
    // in the forward direction
    for (let i = 0; i < n; i++) {

        // If the character is '0',
        // increment count_0 by 1
        if (s[i] == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1 by 1
        else
            ++count_1;

        // If at any point,
        // count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }

    // If count_0 is not equal
    // to twice count_1,
    // return false
    if (count_0 != (2 * count_1))
        return false;

    // Reset the value of count_0 and count_1
    count_0 = 0; count_1 = 0;

    // Traverse the string in
    // the reverse direction
    for (let i = n - 1; i >= 0; --i) {

        // If the character is '0'
        // increment count_0
        if (s[i] == '0')
            ++count_0;

        // If the character is '1'
        // increment count_1
        else
            ++count_1;

        // If count_1 > count_0,
        // return false
        if (count_1 > count_0)
            return false;
    }

    return true;
}

// Driver Code
// Given string
let s = "010100";

// Function Call
if (isPossible(s))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)