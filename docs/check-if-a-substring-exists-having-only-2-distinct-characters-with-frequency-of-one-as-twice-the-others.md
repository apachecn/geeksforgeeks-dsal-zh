# 检查是否存在只有两个不同字符的子串，频率是其他子串的两倍

> 原文:[https://www . geesforgeks . org/check-if-a-substring-exists-with-2-distinct-characters-with-frequency-of-one-two-others/](https://www.geeksforgeeks.org/check-if-a-substring-exists-having-only-2-distinct-characters-with-frequency-of-one-as-twice-the-others/)

给定一个 **N** 小写英文字母的[字符串](https://www.geeksforgeeks.org/string-data-structure/)**str【】**，任务是检查给定字符串是否存在[子串](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得该子串仅由两个字符组成，并且**1<sup>ST</sup>T11】字符的频率= 2 * 2**2<sup>nd</sup>T15】字符的频率。****

**示例:**

> **输入:**str[]=“aaaaa BC”
> **输出:**是
> **说明:**给定字符串的子字符串 str[0…5]=“aaaaa bb”只由两个字符‘a’和‘b’组成，‘a’的频率= 2 * b’的频率，即 4 = 2 * 2。有效子串的另一个例子是 str[4…6]=“BBC”。
> 
> **输入:**str[]=“abcdefg”
> T3】输出:否

**天真方法:**给定的问题可以通过[迭代给定字符串的所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)并检查该字符串是否仅由两个字符组成以及*的**1<sup>ST</sup>T8】字符的频率= 2 *的**2<sup>nd</sup>T12】字符的频率*****来解决。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)进行优化。仔细观察，可以注意到，任何子串要有效，必须存在该串的大小为 **3** 的[子串](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得它仅由两个字符组成，并且 **1 <sup>st</sup>** 字符的*频率= 2 *字符 **2 <sup>nd</sup>** 字符的*频率。因此，给定的问题可以通过[迭代给定的字符串](https://www.geeksforgeeks.org/range-based-loop-c/)来解决，对于长度为 **3** 的每个子字符串，检查是否存在形式为“ **xxy** ”、“ **xyx** ”或“ **yxx** 的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there exist a
// substring such that it is made up of
// only two characters and freq of 1st
// char is equal to 2 * freq of 2nd char
bool isPossible(string str)
{
    // Loop to iterate over the string
    for (int i = 0; i + 2 < str.size(); i++) {

        // If the string is of
        // the form "xxy"
        if (str[i] == str[i + 1]
            && str[i] != str[i + 2]) {
            return true;
        }

        // If the string is of
        // the form "xyx"
        if (str[i] == str[i + 2]
            && str[i] != str[i + 1]) {
            return true;
        }

        // If the string is of
        // the form "yxx"
        if (str[i + 1] == str[i + 2]
            && str[i] != str[i + 1]) {
            return true;
        }
    }

    // If no valid substring exist
    return false;
}

// Driver Code
int main()
{
    string str = "aaaabbc";

    if (isPossible(str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to check if there exist a
    // substring such that it is made up of
    // only two characters and freq of 1st
    // char is equal to 2 * freq of 2nd char
    public static boolean isPossible(String str)
    {

        // Loop to iterate over the string
        for (int i = 0; i + 2 < str.length(); i++) {

            // If the string is of
            // the form "xxy"
            if (str.charAt(i) == str.charAt(i + 1)
                    && str.charAt(i) != str.charAt(i + 2)) {
                return true;
            }

            // If the string is of
            // the form "xyx"
            if (str.charAt(i) == str.charAt(i + 2)
                    && str.charAt(i) != str.charAt(i + 1)) {
                return true;
            }

            // If the string is of
            // the form "yxx"
            if (str.charAt(i + 1) == str.charAt(i + 2)
                    && str.charAt(i) != str.charAt(i + 1)) {
                return true;
            }
        }

        // If no valid substring exist
        return false;
    }

    // Driver Code
    public static void main(String args[]) {
        String str = "aaaabbc";

        if (isPossible(str))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there exist a
# substring such that it is made up of
# only two characters and freq of 1st
# char is equal to 2 * freq of 2nd char
def isPossible(str):

    # Loop to iterate over the string
    for i in range(0, len(str) - 2):

        # If the string is of
        # the form "xxy"
        if (str[i] == str[i + 1] and
            str[i] != str[i + 2]):
            return True

        # If the string is of
        # the form "xyx"
        if (str[i] == str[i + 2] and
            str[i] != str[i + 1]):
            return True

        # If the string is of
        # the form "yxx"
        if (str[i + 1] == str[i + 2] and
            str[i] != str[i + 1]):
            return True

    # If no valid substring exist
    return False

# Driver Code
if __name__ == "__main__":

    str = "aaaabbc"

    if (isPossible(str)):
        print("Yes")
    else:
        print("No")

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to check if there exist a
    // substring such that it is made up of
    // only two characters and freq of 1st
    // char is equal to 2 * freq of 2nd char
    public static bool isPossible(String str)
    {

        // Loop to iterate over the string
        for (int i = 0; i + 2 < str.Length; i++)
        {

            // If the string is of
            // the form "xxy"
            if (str[i] == str[i + 1]
                    && str[i] != str[i + 2])
            {
                return true;
            }

            // If the string is of
            // the form "xyx"
            if (str[i] == str[i + 2]
                    && str[i] != str[i + 1])
            {
                return true;
            }

            // If the string is of
            // the form "yxx"
            if (str[i + 1] == str[i + 2]
                    && str[i] != str[i + 1])
            {
                return true;
            }
        }

        // If no valid substring exist
        return false;
    }

    // Driver Code
    public static void Main()
    {
        String str = "aaaabbc";

        if (isPossible(str))
            Console.Write("Yes");
        else
            Console.Write("No");

    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to check if there exist a
// substring such that it is made up of
// only two characters and freq of 1st
// char is equal to 2 * freq of 2nd char
function isPossible( str)
{

    // Loop to iterate over the string
    for (let i = 0; i + 2 < str.length; i++) {

        // If the string is of
        // the form "xxy"
        if (str[i] == str[i + 1]
            && str[i] != str[i + 2]) {
            return true;
        }

        // If the string is of
        // the form "xyx"
        if (str[i] == str[i + 2]
            && str[i] != str[i + 1]) {
            return true;
        }

        // If the string is of
        // the form "yxx"
        if (str[i + 1] == str[i + 2]
            && str[i] != str[i + 1]) {
            return true;
        }
    }

    // If no valid substring exist
    return false;
}

// Driver Code
    let str = "aaaabbc";
    if (isPossible(str))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)