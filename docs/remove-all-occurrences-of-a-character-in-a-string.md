# 删除字符串中出现的所有字符

> 原文:[https://www . geesforgeks . org/remove-字符串中出现的所有字符/](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-character-in-a-string/)

给定一个字符串。编写一个程序来删除字符串中出现的所有字符。

**示例:**

```
Input : s = "geeksforgeeks"
        c = 'e'
Output : s = "gksforgks"

Input : s = "geeksforgeeks"
        c = 'g'
Output : s = "eeksforeeks"
```

其思想是维护结果字符串的索引。

## C++

```
// C++ program to remove a particular character
// from a string.
#include <bits/stdc++.h>
using namespace std;

void removeChar(char* s, char c)
{

    int j, n = strlen(s);
    for (int i = j = 0; i < n; i++)
        if (s[i] != c)
            s[j++] = s[i];

    s[j] = '\0';
}

int main()
{
    char s[] = "geeksforgeeks";
    removeChar(s, 'g');
    cout << s;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove
// a particular character
// from a string.
class GFG
{
static void removeChar(String s, char c)
{
    int j, count = 0, n = s.length();
    char []t = s.toCharArray();
    for (int i = j = 0; i < n; i++)
    {
        if (t[i] != c)
        t[j++] = t[i];
        else
            count++;
    }

    while(count > 0)
    {
        t[j++] = '\0';
        count--;
    }

    System.out.println(t);
}

// Driver Code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    removeChar(s, 'g');
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 program to remove
# a particular character
# from a string.

# function for removing the
# occurrence of character
def removeChar(s, c) :

    # find total no. of
    # occurrence of character
    counts = s.count(c)

    # convert into list
    # of characters
    s = list(s)

    # keep looping until
    # counts become 0
    while counts :

        # remove character
        # from the list
        s.remove(c)

        # decremented by one
        counts -= 1

    # join all remaining characters
    # of the list with empty string
    s = '' . join(s)

    print(s)

# Driver code
if __name__ == '__main__' :

    s = "geeksforgeeks"
    removeChar(s,'g')

# This code is contributed
# by Ankit Rai
```

## C#

```
// C# program to remove a
// particular character
// from a string.
using System;

class GFG
{
static void removeChar(string s,
                       char c)
{
    int j, count = 0, n = s.Length;
    char[] t = s.ToCharArray();
    for (int i = j = 0; i < n; i++)
    {
        if (s[i] != c)
        t[j++] = s[i];
        else
            count++;
    }

    while(count > 0)
    {
        t[j++] = '\0';
        count--;
    }

    Console.Write(t);
}

// Driver Code
public static void Main()
{
    string s = "geeksforgeeks";
    removeChar(s, 'g');
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to remove a
// particular character
// from a string.

function removeChar($s, $c)
{

    $n = strlen($s);
    $count = 0;
    for ($i = $j = 0; $i < $n; $i++)
    {
    if ($s[$i] != $c)
        $s[$j++] = $s[$i];
    else
        $count++;
    }
    while($count--)
    {
        $s[$j++] = NULL;
    }
    echo $s;
}

// Driver code
$s = "geeksforgeeks";
removeChar($s, 'g');

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to remove
// a particular character
// from a string.
function removeChar(s, c)
{
    let j, count = 0, n = s.length;
    let t = s.split("");

    for(let i = j = 0; i < n; i++)
    {
        if (t[i] != c)
            t[j++] = t[i];
        else
            count++;
    }

    while (count > 0)
    {
        t[j++] = '\0';
        count--;
    }
    document.write(t.join(""));
}

// Driver Code
let s = "geeksforgeeks";
removeChar(s, 'g');

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
eeksforeeks
```

**时间复杂度:** O(n)，其中 n 为输入字符串的长度。
**辅助空间:** O(1)