# 对字母数字字符串进行排序，使字母和数字的位置保持不变

> 原文:[https://www . geeksforgeeks . org/sort-一个字母数字字符串，这样字母和数字的位置保持不变/](https://www.geeksforgeeks.org/sort-an-alphanumeric-string-such-that-the-positions-of-alphabets-and-numbers-remain-unchanged/)

给定一个字母数字字符串 **str** ，任务是以这样一种方式对字符串进行排序:如果一个位置被一个字母占据，它在排序后必须被一个字母占据，如果被一个数字占据，它在排序后必须被一个数字占据。
**例:**

> **输入:**输入:输入:【d4c3b2a 1】
> 输出: a1b2c3d4

**方法:**我们将字符串转换为字符数组，然后对字符数组 **c[]** 进行排序。对字符数组进行排序后，数字字符将占据数组的起始索引，字母将占据数组的剩余部分。
数字部分将被排序，字母部分也将被排序。我们将保留两个索引，一个在字母部分 **al_c** 的起始索引处，一个在数字部分 **nu_c** 的起始索引处，现在我们将检查原始字符串，如果某个位置被字母占据，那么我们将使用**c【al _ c】**替换它，并增加 **al_c** 否则我们将使用**c【nu _ c】**替换它，并增加 **nu_c** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the string s
// in sorted form such that the
// positions of alphabets and numeric
// digits remain unchanged
string sort(string s)
{
    char c[s.length() + 1];

    // String to character array
    strcpy(c, s.c_str());

    // Sort the array
    sort(c, c + s.length());

    // Count of alphabets and numbers
    int al_c = 0, nu_c = 0;

    // Get the index from where the
    // alphabets start
    while (c[al_c] < 97)
        al_c++;

    // Now replace the string with sorted string
    for (int i = 0; i < s.length(); i++) {

        // If the position was occupied by an
        // alphabet then replace it with alphabet
        if (s[i] < 97)
            s[i] = c[nu_c++];

        // Else replace it with a number
        else
            s[i] = c[al_c++];
    }

    // Return the sorted string
    return s;
}

// Driver code
int main()
{
    string s = "d4c3b2a1";

    cout << sort(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns the string s
// in sorted form such that the
// positions of alphabets and numeric
// digits remain unchanged
static String sort(String s)
{
    char []c = new char[s.length() + 1];

    // String to character array
    c = s.toCharArray();

    // Sort the array
    Arrays.sort(c);

    // Count of alphabets and numbers
    int al_c = 0, nu_c = 0;

    // Get the index from where the
    // alphabets start
    while (c[al_c] < 97)
        al_c++;

    // Now replace the string with sorted string
    for (int i = 0; i < s.length(); i++)
    {

        // If the position was occupied by an
        // alphabet then replace it with alphabet
        if (s.charAt(i) < 97)
            s = s.substring(0,i)+ c[nu_c++]+s.substring(i+1);

        // Else replace it with a number
        else
            s = s.substring(0,i)+ c[al_c++]+s.substring(i+1);
    }

    // Return the sorted string
    return s;
}

// Driver code
public static void main(String[] args)
{
    String s = "d4c3b2a1";

    System.out.println(sort(s));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the string s
# in sorted form such that the
# positions of alphabets and numeric
# digits remain unchanged
def sort(s):

    # String to character array
    c, s = list(s), list(s)

    # Sort the array
    c.sort()

    # Count of alphabets and numbers
    al_c = 0
    nu_c = 0

    # Get the index from where the
    # alphabets start
    while ord(c[al_c]) < 97:
        al_c += 1

    # Now replace the string with sorted string
    for i in range(len(s)):

        # If the position was occupied by an
        # alphabet then replace it with alphabet
        if s[i] < 'a':
            s[i] = c[nu_c]
            nu_c += 1

        # Else replace it with a number
        else:
            s[i] = c[al_c]
            al_c += 1

    # Return the sorted string
    return ''.join(s)

# Driver Code
if __name__ == "__main__":
    s = "d4c3b2a1"
    print(sort(s))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns the string s
    // in sorted form such that the
    // positions of alphabets and numeric
    // digits remain unchanged
    static string sort(string s)
    {
        char []c = new char[s.Length + 1];

        // String to character array
        c = s.ToCharArray();

        // Sort the array
        Array.Sort(c);

        // Count of alphabets and numbers
        int al_c = 0, nu_c = 0;

        // Get the index from where the
        // alphabets start
        while (c[al_c] < 97)
            al_c++;

        // Now replace the string with sorted string
        for (int i = 0; i < s.Length; i++)
        {

            // If the position was occupied by an
            // alphabet then replace it with alphabet
            if (s[i] < 97)
                s = s.Substring(0,i)+ c[nu_c++]+s.Substring(i+1);

            // Else replace it with a number
            else
                s = s.Substring(0,i)+ c[al_c++]+s.Substring(i+1);
        }

        // Return the sorted string
        return s;
    }

    // Driver code
    public static void Main()
    {
        string s = "d4c3b2a1";

        Console.WriteLine(sort(s));
    }
}

/* This code contributed by AnkitRai01 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns the string s
// in sorted form such that the
// positions of alphabets and numeric
// digits remain unchanged
function sort(s)
{
    var c = s.split('');

    c.sort();

    // Count of alphabets and numbers
    var al_c = 0, nu_c = 0;

    // Get the index from where the
    // alphabets start
    while (c[al_c].charCodeAt(0) < 97)
        al_c++;

    // Now replace the string with sorted string
    for (var i = 0; i < s.length; i++) {

        // If the position was occupied by an
        // alphabet then replace it with alphabet
        if (s[i].charCodeAt(0) < 97)
            s = s.substring(0,i)+ c[nu_c++]+s.substring(i+1);

        // Else replace it with a number
        else
        s = s.substring(0,i)+ c[al_c++]+s.substring(i+1);
    }

    // Return the sorted string
    return s;
}

// Driver code
var s = "d4c3b2a1";
document.write( sort(s));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
a1b2c3d4
```

**时间复杂度:** O(N * log(N))其中 N 是字符串的长度。