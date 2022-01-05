# 通过将两个字符串的字符复制到相邻的字符串中来检查两个字符串是否可以相等

> 原文:[https://www . geeksforgeeks . org/check-两个字符串是否可以通过将它们的字符与相邻的字符复制来相等/](https://www.geeksforgeeks.org/check-whether-two-strings-can-be-made-equal-by-copying-their-characters-with-the-adjacent-ones/)

给定两个字符串 **str1** 和 **str2** ，任务是通过复制字符串的任意字符及其相邻字符来检查这两个字符串是否可以相等。**注意**该操作可以执行任意次。
**举例:**

> **输入:**str 1 =“ABC”，str 2 =“def”
> **输出:**否
> 因为两个字符串中的所有字符都不同。
> 所以，没有办法让他们平等。
> **输入:**str 1 =“ABC”，str 2 =“fac”
> **输出:**是
> str 1 =“ABC”->“AAC”
> str 2 =“fac”->“AAC”

**方法:**为了用给定的操作使字符串相等，它们必须具有相等的长度，并且必须至少有一个字符在两个字符串中是公共的。为了检查这一点，创建一个频率数组 **freq[]** ，它将存储所有字符的频率 **str1** 然后对于每个字符 **str2** 如果它在 **str1** 中的频率大于 **0** ，那么有可能使两个字符串相等。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 26

// Function that returns true if both
// the strings can be made equal
// with the given operation
bool canBeMadeEqual(string str1, string str2)
{
    int len1 = str1.length();
    int len2 = str2.length();

    // Lengths of both the strings
    // have to be equal
    if (len1 == len2) {

        // To store the frequency of the
        // characters of str1
        int freq[MAX];
        for (int i = 0; i < len1; i++) {
            freq[str1[i] - 'a']++;
        }

        // For every character of str2
        for (int i = 0; i < len2; i++) {

            // If current character of str2
            // also appears in str1
            if (freq[str2[i] - 'a'] > 0)
                return true;
        }
    }

    return false;
}

// Driver code
int main()
{
    string str1 = "abc", str2 = "defa";

    if (canBeMadeEqual(str1, str2))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    static int MAX = 26;

    // Function that returns true if both
    // the strings can be made equal
    // with the given operation
    static boolean canBeMadeEqual(String str1,
                                  String str2)
    {
        int len1 = str1.length();
        int len2 = str2.length();

        // Lengths of both the strings
        // have to be equal
        if (len1 == len2)
        {

            // To store the frequency of the
            // characters of str1
            int freq[] = new int[MAX];

            for (int i = 0; i < len1; i++)
            {
                freq[str1.charAt(i) - 'a']++;
            }

            // For every character of str2
            for (int i = 0; i < len2; i++)
            {

                // If current character of str2
                // also appears in str1
                if (freq[str2.charAt(i) - 'a'] > 0)
                    return true;
            }
        }
        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str1 = "abc", str2 = "defa";

        if (canBeMadeEqual(str1, str2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26

# Function that returns true if both
# the strings can be made equal
# with the given operation
def canBeMadeEqual(str1, str2):
    len1 = len(str1)
    len2 = len(str2)

    # Lengths of both the strings
    # have to be equal
    if (len1 == len2):

        # To store the frequency of the
        # characters of str1
        freq = [0 for i in range(MAX)]
        for i in range(len1):
            freq[ord(str1[i]) - ord('a')] += 1

        # For every character of str2
        for i in range(len2):

            # If current character of str2
            # also appears in str1
            if (freq[ord(str2[i]) - ord('a')] > 0):
                return True

    return False

# Driver code
str1 = "abc"
str2 = "defa"

if (canBeMadeEqual(str1, str2)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int MAX = 26;

    // Function that returns true if both
    // the strings can be made equal
    // with the given operation
    static Boolean canBeMadeEqual(String str1,
                                   String str2)
    {
        int len1 = str1.Length;
        int len2 = str2.Length;

        // Lengths of both the strings
        // have to be equal
        if (len1 == len2)
        {

            // To store the frequency of the
            // characters of str1
            int []freq = new int[MAX];

            for (int i = 0; i < len1; i++)
            {
                freq[str1[i] - 'a']++;
            }

            // For every character of str2
            for (int i = 0; i < len2; i++)
            {

                // If current character of str2
                // also appears in str1
                if (freq[str2[i] - 'a'] > 0)
                    return true;
            }
        }
        return false;
    }

    // Driver code
    public static void Main (String []args)
    {
        String str1 = "abc", str2 = "defa";

        if (canBeMadeEqual(str1, str2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    let MAX = 26;

    // Function that returns true if both
    // the strings can be made equal
    // with the given operation
    function canBeMadeEqual(str1, str2)
    {
        let len1 = str1.length;
        let len2 = str2.length;

        // Lengths of both the strings
        // have to be equal
        if (len1 == len2)
        {

            // To store the frequency of the
            // characters of str1
            let freq = new Array(MAX);
            freq.fill(0);

            for (let i = 0; i < len1; i++)
            {
                freq[str1[i].charCodeAt() -
                'a'.charCodeAt()]++;
            }

            // For every character of str2
            for (let i = 0; i < len2; i++)
            {

                // If current character of str2
                // also appears in str1
                if (freq[str2[i].charCodeAt() -
                'a'.charCodeAt()] > 0)
                    return true;
            }
        }
        return false;
    }

    let str1 = "abc", str2 = "defa";

    if (canBeMadeEqual(str1, str2))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output:** 

```
No
```