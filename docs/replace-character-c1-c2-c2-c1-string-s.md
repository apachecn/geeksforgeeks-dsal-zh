# 在字符串 S 中用 c2 替换字符 c1，用 c1 替换字符 C2

> 原文:[https://www . geesforgeks . org/replace-character-C1-C2-C2-C1-string-s/](https://www.geeksforgeeks.org/replace-character-c1-c2-c2-c1-string-s/)

给定字符串 S、c1 和 c2。用 c2 替换字符 c1，用 c1 替换 c2。
**例:**

```
Input : grrksfoegrrks,
        c1 = e, c2 = r 
Output : geeksforgeeks 

Input : ratul,
        c1 = t, c2 = h 
Output : rahul
```

遍历字符串并检查 c1 和 c2 的出现。如果找到 c1，用 c2 替换它，否则如果找到 c2，用 c1 替换它。

## C++

```
// CPP program to replace c1 with c2
// and c2 with c1
#include <bits/stdc++.h>
using namespace std;
string replace(string s, char c1, char c2)
{
    int l = s.length();

    // loop to traverse in the string
    for (int i = 0; i < l; i++) {

        // check for c1 and replace
        if (s[i] == c1)
            s[i] = c2;

        // check for c2 and replace
        else if (s[i] == c2)
            s[i] = c1;
    }
    return s;
}

// Driver code to check the above function
int main()
{
    string s = "grrksfoegrrks";
    char c1 = 'e', c2 = 'r';
    cout << replace(s, c1, c2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace c1 with c2
// and c2 with c1
class GFG
{

static String replace(String s,
                    char c1, char c2)
{
    int l = s.length();
    char []arr = s.toCharArray();

    // loop to traverse in the string
    for (int i = 0; i < l; i++)
    {

        // check for c1 and replace
        if (arr[i] == c1)
            arr[i] = c2;

        // check for c2 and replace
        else if (arr[i] == c2)
            arr[i] = c1;
    }

    return String.valueOf(arr);
}

// Driver code
public static void main(String []args)
{
    String s = "grrksfoegrrks";
    char c1 = 'e', c2 = 'r';
    System.out.println(replace(s, c1, c2));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 program to replace c1 with c2
# and c2 with c1
def replace(s, c1, c2):
    l = len(s)

    # loop to traverse in the string
    for i in range(l):

        # check for c1 and replace
        if (s[i] == c1):
            s = s[0:i] + c2 + s[i + 1:]

        # check for c2 and replace
        elif (s[i] == c2):
            s = s[0:i] + c1 + s[i + 1:]
    return s

# Driver Code
if __name__ == '__main__':
    s = "grrksfoegrrks"
    c1 = 'e'
    c2 = 'r'
    print(replace(s, c1, c2))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# program to replace c1 with c2
// and c2 with c1
using System;
public class GFG{

    static String replace(String s,
                        char c1, char c2)
    {
        int l = s.Length;
        char []arr = s.ToCharArray();

        // loop to traverse in the string
        for (int i = 0; i < l; i++)
        {

            // check for c1 and replace
            if (arr[i] == c1)
                arr[i] = c2;

            // check for c2 and replace
            else if (arr[i] == c2)
                arr[i] = c1;
        }

        return string.Join("", arr);
    }

    // Driver code
    public static void Main()
    {
        String s = "grrksfoegrrks";
        char c1 = 'e', c2 = 'r';
        Console.WriteLine(replace(s, c1, c2));
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace c1
// with c2 and c2 with c1
function replace($s, $c1, $c2)
{
    $l = strlen($s);

    // loop to traverse
    // in the string
    for ($i = 0; $i < $l; $i++)
    {

        // check for c1 and replace
        if ($s[$i] == $c1)
            $s[$i] = $c2;

        // check for c2 and replace
        else if ($s[$i] == $c2)
            $s[$i] = $c1;
    }
    return $s;
}

// Driver Code
$s = "grrksfoegrrks";
$c1 = 'e'; $c2 = 'r';
echo replace($s, $c1, $c2);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to replace c1 with c2
// and c2 with c1

    function replace(s,c1,c2)
    {
        let l = s.length;
    let arr = s.split("");

    // loop to traverse in the string
    for (let i = 0; i < l; i++)
    {

        // check for c1 and replace
        if (arr[i] == c1)
            arr[i] = c2;

        // check for c2 and replace
        else if (arr[i] == c2)
            arr[i] = c1;
    }

    return arr.join("");
    }

    // Driver code
    let s = "grrksfoegrrks";
    let c1 = 'e', c2 = 'r';
    document.write(replace(s, c1, c2));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
geeksforgeeks
```

**时间复杂度:O(n)**