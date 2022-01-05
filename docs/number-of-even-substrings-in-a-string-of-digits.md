# 一串数字中偶数子串的数量

> 原文:[https://www . geesforgeks . org/数字串中的偶数子串数/](https://www.geeksforgeeks.org/number-of-even-substrings-in-a-string-of-digits/)

给定一串数字 0–9。任务是计算子串的数量，当转换为整数时，这些子串形成一个偶数。
**例:**

```
Input : str = "1234".
Output : 6
"2", "4", "12", "34", "234", "1234" 
are 6 substring which are even.

Input : str = "154".
Output : 3

Input : str = "15".
Output : 0
```

对于偶数，子串必须以偶数结尾。我们找到字符串中所有的偶数数字，对于每个偶数数字，计算以它结尾的子字符串的数量。现在，观察子串的数量将是偶数加 1 的索引。

## C++

```
// C++ program to count number of substring
// which are even integer in a string of digits.
#include<bits/stdc++.h>
using namespace std;

// Return the even number substrings.
int evenNumSubstring(char str[])
{
    int len = strlen(str);
    int count = 0;

    for (int i = 0; i < len; i++)
    {
        int temp = str[i] - '0';

        // If current digit is even, add
        // count of substrings ending with
        // it. The count is (i+1)
        if (temp % 2 == 0)
            count += (i + 1);
    }

    return count;
}

// Driven Program
int main()
{
    char str[] = "1234";
    cout << evenNumSubstring(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// substring which are even integer
// in a string of digits.
public class GFG {

    // Return the even number substrings.
    static int evenNumSubstring(String str)
    {
        int len = str.length();
        int count = 0;

        for (int i = 0; i < len; i++)
        {
            int temp = str.charAt(i) - '0';

            // If current digit is even, add
            // count of substrings ending with
            // it. The count is (i+1)
            if (temp % 2 == 0)
                count += (i + 1);
        }

        return count;
    }

    public static void main(String args[])
    {

        String str= "1234";

        System.out.println(evenNumSubstring(str));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python 3 program to count number of substring
# which are even integer in a string of digits.

# Return the even number substrings.
def evenNumSubstring(str):
    length = len(str)
    count = 0

    for i in range(0,length,1):
        temp = ord(str[i]) - ord('0')

        # If current digit is even, add
        # count of substrings ending with
        # it. The count is (i+1)
        if (temp % 2 == 0):
            count += (i + 1)

    return count

# Driven Program
if __name__ == '__main__':
    str = ['1','2','3','4']
    print(evenNumSubstring(str))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count number of
// substring which are even integer
// in a string of digits.
using System;

public class GFG {

    // Return the even number substrings.
    static int evenNumSubstring(string str)
    {
        int len = str.Length;
        int count = 0;

        for (int i = 0; i < len; i++)
        {
            int temp = str[i] - '0';

            // If current digit is even,
            // add count of substrings
            // ending with it. The count
            // is (i+1)
            if (temp % 2 == 0)
                count += (i + 1);
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        string str= "1234";

        Console.Write(
            evenNumSubstring(str));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of substring which are even
// integer in a string of digits.

// Return the even number substrings.
function evenNumSubstring($str)
{
    $len = strlen($str);
    $count = 0;

    for ($i = 0; $i < $len; $i++)
    {
        $temp = $str[$i] - '0';

        // If current digit is even, add
        // count of substrings ending with
        // it. The count is (i+1)
        if ($temp % 2 == 0)
            $count += ($i + 1);
    }

    return $count;
}

// Driver Code
$str = "1234";
echo evenNumSubstring($str),"\n" ;

// This code is contributed by jit_t   
?>
```

## java 描述语言

```
<script>

    // Javascript program to count number of
    // substring which are even integer
    // in a string of digits.

    // Return the even number substrings.
    function evenNumSubstring(str)
    {
        let len = str.length;
        let count = 0;

        for (let i = 0; i < len; i++)
        {
            let temp = str[i] - '0';

            // If current digit is even,
            // add count of substrings
            // ending with it. The count
            // is (i+1)
            if (temp % 2 == 0)
                count += (i + 1);
        }

        return count;
    }

    let str= "1234";

    document.write(evenNumSubstring(str));

</script>
```

**输出:**

```
6
```

**时间复杂度:** O(字符串长度)。

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。