# 在给定的二进制串中把所有 1 组合在一起所需的 1 的子串的最小移位

> 原文:[https://www . geesforgeks . org/给定二进制字符串中所有 1 分组所需的 1 子字符串的最小移位数/](https://www.geeksforgeeks.org/minimum-shifts-of-substrings-of-1s-required-to-group-all-1s-together-in-a-given-binary-string/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/generate-all-binary-strings-from-given-pattern/) **S** ，任务是打印最小数量的索引，只由 **1s** 组成的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)需要被移位，使得字符串中存在的所有 **1** s 被组合在一起。

**示例:**

> **输入:** S = "00110111011"
> **输出:** 2
> **解释:**
> **操作 1:** 将子串{S[2]，S[3]} ( *基于 0 的索引*)向右移动并放置在 S[4]和 S[5]之间。现在，S 修改为“00011111011”。
> **操作 2:** 将子串{S[10]，S[11]}向左移动，放在 S[7]和 S[8]之间。现在，S 修改为“00011111110”。
> 因此需要移位 2 个子串。
> 
> **输入:** S = "1001001"
> **输出:** 4
> **解释:**
> **操作 1:** 将 S[0]处的‘1’向右移动两个索引，放在 S[2]和 S[3]之间。现在，S 修改为“0011001”。
> **操作 2:** 将 S[6]处的“1”向左移动两个索引，放在 S[3]和 S[4]之间。现在，S 修改为“0011100”。
> 因此需要移位 4 个子串。

**方法:**通过观察所需的最小操作数等于任意一对连续的 **1** 之间存在的 **0** 的数量，可以解决问题。按照以下步骤解决问题:

1.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符，搜索字符**‘1’**的第一次和最后一次出现，并将其存储在变量中，例如分别为**第一个**和**最后一个**。
2.  遍历范围**【第一个，最后一个】**，统计子串 **{S【第一个】中出现的**【0】**的数量，..，S[lastOne]}** 并将其打印为所需输出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count indices substrings
// of 1s need to be shifted such that
// all 1s in the string are grouped together
void countShifts(string str)
{
    // Stores first occurrence of '1'
    int firstOne = -1;

    // Stores last occurrence of '1'
    int lastOne = -1;

    // Count of 0s between firstOne and lastOne
    int count = 0;

    // Traverse the string to find the
    // first and last occurrences of '1'
    for (int i = 0; i < str.length(); i++) {
        if (str[i] == '1') {

            if (firstOne == -1)
                firstOne = i;

            lastOne = i;
        }
    }

    if ((firstOne == -1) || (firstOne == lastOne)) {
        cout << 0;
        return;
    }

    // Count number of 0s present between
    // firstOne and lastOne
    for (int i = firstOne; i <= lastOne; i++) {

        if (str[i] == '0') {

            count++;
        }
    }

    // Print minimum operations
    cout << count << endl;
}

// Driver Code
int main()
{

    // Given string
    string str = "00110111011";

    countShifts(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count indices substrings
// of 1s need to be shifted such that
// all 1s in the string are grouped together
static void countShifts(String str)
{

    // Stores first occurrence of '1'
    int firstOne = -1;

    // Stores last occurrence of '1'
    int lastOne = -1;

    // Count of 0s between firstOne and lastOne
    int count = 0;

    // Traverse the string to find the
    // first and last occurrences of '1'
    for(int i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) == '1')
        {
            if (firstOne == -1)
                firstOne = i;

            lastOne = i;
        }
    }

    if ((firstOne == -1) || (firstOne == lastOne))
    {
        System.out.print(0);
        return;
    }

    // Count number of 0s present between
    // firstOne and lastOne
    for(int i = firstOne; i <= lastOne; i++)
    {
        if (str.charAt(i) == '0')
        {      
            count++;
        }
    }

    // Print minimum operations
    System.out.println(count);
}

// Driver code
public static void main (String[] args)
{

    // Given string
    String str = "00110111011";

    countShifts(str); 
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count indices substrings
# of 1s need to be shifted such that
# all 1s in the string are grouped
# together
def countShifts(str):

    # Stores first occurrence of '1'
    firstOne = -1

    # Stores last occurrence of '1'
    lastOne = -1

    # Count of 0s between firstOne
    # and lastOne
    count = 0

    # Traverse the string to find the
    # first and last occurrences of '1'
    for i in range(len(str)):
        if (str[i] == '1'):

            if (firstOne == -1):
                firstOne = i

            lastOne = i

    if ((firstOne == -1) or
        (firstOne == lastOne)):
        print(0)
        return

    # Count number of 0s present between
    # firstOne and lastOne
    for i in range(firstOne, lastOne + 1, 1):
        if (str[i] == '0'):
            count += 1

    # Print minimum operations
    print(count)

# Driver Code

# Given string
str = "00110111011"

countShifts(str)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to count indices substrings
    // of 1s need to be shifted such that
    // all 1s in the string are grouped together
    static void countShifts(string str)
    {
        // Stores first occurrence of '1'
        int firstOne = -1;

        // Stores last occurrence of '1'
        int lastOne = -1;

        // Count of 0s between firstOne and lastOne
        int count = 0;

        // Traverse the string to find the
        // first and last occurrences of '1'
        for (int i = 0; i < str.Length; i++)
        {
            if (str[i] == '1')
            {

                if (firstOne == -1)
                    firstOne = i;

                lastOne = i;
            }
        }

        if ((firstOne == -1) || (firstOne == lastOne))
        {
            Console.Write(0);
            return;
        }

        // Count number of 0s present between
        // firstOne and lastOne
        for (int i = firstOne; i <= lastOne; i++)
        {

            if (str[i] == '0')
            {      
                count++;
            }
        }

        // Print minimum operations
        Console.WriteLine(count);
    }

  // Driver code
  static void Main()
  {

        // Given string
        string str = "00110111011";

        countShifts(str); 
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to count indices substrings
    // of 1s need to be shifted such that
    // all 1s in the string are grouped together
    function countShifts(str)
    {

        // Stores first occurrence of '1'
        let firstOne = -1;

        // Stores last occurrence of '1'
        let lastOne = -1;

        // Count of 0s between firstOne and lastOne
        let count = 0;

        // Traverse the string to find the
        // first and last occurrences of '1'
        for (let i = 0; i < str.length; i++)
        {
            if (str[i] == '1')
            {

                if (firstOne == -1)
                    firstOne = i;

                lastOne = i;
            }
        }

        if ((firstOne == -1) || (firstOne == lastOne))
        {
            Console.Write(0);
            return;
        }

        // Count number of 0s present between
        // firstOne and lastOne
        for (let i = firstOne; i <= lastOne; i++)
        {

            if (str[i] == '0')
            {     
                count++;
            }
        }

        // Print minimum operations
        document.write(count);
    }

// Driver code

      // Given string
        let str = "00110111011";

        countShifts(str);

  // This code is contributed by splevel62.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)