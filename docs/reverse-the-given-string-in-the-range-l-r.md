# 反转范围[L，R]

内的给定字符串

> 原文:[https://www . geesforgeks . org/反向给定范围内的字符串-l-r/](https://www.geeksforgeeks.org/reverse-the-given-string-in-the-range-l-r/)

给定一个字符串 **str** ，和两个整数 **L** 和 **R** ，任务是在范围**【L，R】**内反转字符串，即**str【L…R】**。
**举例:**

> **输入:**str =“geeks forgeeks”，L = 5，R = 7
> **输出:**geeks forgeks
> 将范围 str[5…7]=“geeks”**中的字符反转为**geeks”
> ，新字符串将为“geeks**ROF**geeks”
> **输入:**str =“ijklmn”，L = 1，R = 2

**进场:**

1.  如果范围无效，即 **L < 0** 或 **R ≥ len** 或 **L > R** 则打印原始字符串。
2.  如果范围有效，则在每次交换操作后继续交换字符 **str[L]** 和 **str[R]** 同时 **L < R** 并更新 **L = L + 1** 和**R = R–1**。最后打印更新后的字符串。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the string after
// reversing characters in the range [L, R]
string reverse(string str, int len, int l, int r)
{

    // Invalid range
    if (l < 0 || r >= len || l > r)
        return str;

    // While there are characters to swap
    while (l < r) {

        // Swap(str[l], str[r])
        char c = str[l];
        str[l] = str[r];
        str[r] = c;

        l++;
        r--;
    }

    return str;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int len = str.length();
    int l = 5, r = 7;

    cout << reverse(str, len, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the string after
    // reversing characters in the range [L, R]
    static String reverse(char[] str, int len,
                               int l, int r)
    {

        // Invalid range
        if (l < 0 || r >= len || l > r)
            return "Invalid range!";

        // While there are characters to swap
        while (l < r)
        {

            // Swap(str[l], str[r])
            char c = str[l];
            str[l] = str[r];
            str[r] = c;

            l++;
            r--;
        }
        String string = new String(str);
        return string;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "geeksforgeeks";
        int len = str.length();
        int l = 5, r = 7;

        System.out.println(reverse(str.toCharArray(),
                                         len, l, r));
    }
}

// This code is contributed by Ashutosh450
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the string after
# reversing characters in the range [L, R]
def reverse(string, length, l, r) :

    # Invalid range
    if (l < 0 or r >= length or l > r) :
        return string;

    string = list(string)

    # While there are characters to swap
    while (l < r) :

        # Swap(str[l], str[r])
        c = string[l];
        string[l] = string[r];
        string[r] = c;

        l += 1;
        r -= 1;

    return "".join(string);

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";
    length = len(string);
    l = 5; r = 7;

    print(reverse(string, length, l, r));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the string after
    // reversing characters in the range [L, R]
    static String reverse(char[] str, int len,
                          int l, int r)
    {

        // Invalid range
        if (l < 0 || r >= len || l > r)
            return "Invalid range!";

        // While there are characters to swap
        while (l < r)
        {

            // Swap(str[l], str[r])
            char c = str[l];
            str[l] = str[r];
            str[r] = c;

            l++;
            r--;
        }
        return String.Join("",str);
    }

    // Driver code
    public static void Main (String[] args)
    {
        String str = "geeksforgeeks";
        int len = str.Length;
        int l = 5, r = 7;

        Console.WriteLine(reverse(str.ToCharArray(),
                                        len, l, r));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the string after
    // reversing characters in the range [L, R]
    function reverse(str, len, l, r)
    {

        // Invalid range
        if (l < 0 || r >= len || l > r)
            return "Invalid range!";

        // While there are characters to swap
        while (l < r)
        {

            // Swap(str[l], str[r])
            let c = str[l];
            str[l] = str[r];
            str[r] = c;

            l++;
            r--;
        }
        return str.join("");
    }

    let str = "geeksforgeeks";
    let len = str.length;
    let l = 5, r = 7;

    document.write(reverse(str.split(''), len, l, r));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
geeksrofgeeks
```