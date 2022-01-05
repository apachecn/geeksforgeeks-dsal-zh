# 使用追加和删除最后一个操作将一个字符串转换为另一个字符串

> 原文:[https://www . geesforgeks . org/converting-one-string-use-append-delete-last-operations/](https://www.geeksforgeeks.org/converting-one-string-using-append-delete-last-operations/)

给定一个整数 k 和两个字符串，str1 和 str2 决定我们是否可以通过对 str1 执行以下 k 个操作来将 str1 转换为 str2。
a)在 str1 的末尾附加一个小写的英文字母。
b)删除 str1 中的最后一个字符(对空字符串执行此操作会产生空字符串)
**示例:**

```
Input : k = 7, str1 = aba, str2 = aba
Output : Yes
(4 operations to convert str1 to an 
empty string(to make string empty we 
have to perform one more delete 
operation) and 3 append operations)

Input : k = 5, str1 = pqruvs, str2 = pqrxy 
Output : Yes
(3 delete operations and 2 append operations)
```

首先，我们确定两个字符串的公共前缀，然后根据公共前缀的值，即 str1.length、str2.length 和 k，我们可以得出结论。以下是案例。
**案例 A:** 我们可以将 str1 更改为 str2 的案例:

*   如果 str1.length + str2.length <= k，那么我们可以完全删除 str1，轻松地重新构建 str2。
*   如果*【k-(str1 . length-prefix . length+str2 . length-prefix . length)】*是偶数，那么我们可以很容易地从 str 1 构造出 str 2。这是因为 str1.length-prefix.length 是要删除的字母数，而 str2.length-prefix.length 是删除不常见字母后要在 str1 中添加的字母数。在这之后，如果剩下的操作是偶数，那么我们可以添加和删除任何需要偶数个操作的随机字母。

**病例 B:** 在其余所有病例中，我们无法从 str1 构建 str2。

## C++

```
// CPP Program to convert str1 to str2 in
// exactly k operations
#include <bits/stdc++.h>
using namespace std;

// Returns true if it is possible to convert
// str1 to str2 using k operations.
bool isConvertible(string str1, string str2,
                                      int k)
{
    // Case A (i)
    if ((str1.length() + str2.length()) < k)
        return true;

    // finding common length of both string
    int commonLength = 0;
    for (int i = 0; i < min(str1.length(),
                           str2.length()); i++) {
        if (str1[i] == str2[i])
            commonLength++;
        else
            break;
    }

    // Case A (ii)-
    if ((k - str1.length() - str2.length() +
                     2 * commonLength) % 2 == 0)
        return true;

    // Case B-
    return false;
}

// driver program
int main()
{
    string str1 = "geek", str2 = "geek";
    int k = 7;
    if (isConvertible(str1, str2, k))
       cout << "Yes";
    else
       cout << "No";

    str1 = "geeks",  str2 = "geek";
    k = 5;   
    cout << endl;
    if (isConvertible(str1, str2, k))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java Program to convert str1 to
// str2 in exactly k operations
import java.io.*;

class GFG {

    // Returns true if it is possible to convert
    // str1 to str2 using k operations.
    static boolean isConvertible(String str1, String str2,
                                                     int k)
    {
        // Case A (i)
        if ((str1.length() + str2.length()) < k)
            return true;

        // finding common length of both string
        int commonLength = 0;
        for (int i = 0; i < Math.min(str1.length(),
                                str2.length()); i++)
        {
            if (str1 == str2)
                commonLength++;
            else
                break;
        }

        // Case A (ii)-
        if ((k - str1.length() - str2.length() +
                     2 * commonLength) % 2 == 0)
            return true;

        // Case B
        return false;
    }

    // Driver program
    public static void main (String[] args)
    {
        String str1 = "geek";
        String str2 = "geek";
        int k = 7;
        if (isConvertible(str1, str2, k))
        System.out.println( "Yes");
        else
        System.out.println ( "No");

        str1 = "geeks";
        str2 = "geek";
        k = 5;

        if (isConvertible(str1, str2, k))
        System.out.println( "Yes");
        else
        System.out.println ( "No");

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 Program to convert str1 to
# str2 in exactly k operations

# Returns true if it is possible to convert
# str1 to str2 using k operations.
def isConvertible(str1, str2, k):

    # Case A (i)
    if ((len(str1) + len(str2)) < k):
        return True

    # finding common length of both string
    commonLength = 0
    for i in range(0, min(len(str1),
                          len(str2)), 1):
        if (str1[i] == str2[i]):
            commonLength += 1
        else:
            break

    # Case A (ii)-
    if ((k - len(str1) - len(str2) + 2 *
                commonLength) % 2 == 0):
        return True

    # Case B-
    return False

# Driver Code
if __name__ == '__main__':
    str1 = "geek"
    str2 = "geek"
    k = 7
    if (isConvertible(str1, str2, k)):
        print("Yes")
    else:
        print("No")

    str1 = "geeks"
    str2 = "geek"
    k = 5
    if (isConvertible(str1, str2, k)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# Program to convert str1 to
// str2 in exactly k operations
using System;

class GFG {

    // Returns true if it is possible to convert
    // str1 to str2 using k operations.
    static bool isConvertible(string str1, string str2,
                                                    int k)
    {
        // Case A (i)
        if ((str1.Length + str2.Length) < k)
            return true;

        // finding common length of both string
        int commonLength = 0;
        for (int i = 0; i < Math.Min(str1.Length,
                                str2.Length); i++)
        {
            if (str1 == str2)
                commonLength++;
            else
                break;
        }

        // Case A (ii)-
        if ((k - str1.Length - str2.Length +
                    2 * commonLength) % 2 == 0)
            return true;

        // Case B
        return false;
    }

    // Driver program
    public static void Main ()
    {
        string str1 = "geek";
        string str2 = "geek";
        int k = 7;
        if (isConvertible(str1, str2, k))
        Console.WriteLine( "Yes");
        else
        Console.WriteLine ( "No");

        str1 = "geeks";
        str2 = "geek";
        k = 5;

        if (isConvertible(str1, str2, k))
        Console.WriteLine( "Yes");
        else
        Console.WriteLine ( "No");

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to convert str1 to str2 in
// exactly k operations

// Returns true if it is possible to convert
// str1 to str2 using k operations.
function isConvertible($str1, $str2, $k)

{
    // Case A (i)
    if ((strlen($str1) + strlen($str2)) < $k)
        return true;

    // finding common length of both string
    $commonLength = 0;
    for ($i = 0; $i < min(strlen($str1),
                          strlen($str2)); $i++)
    {
        if ($str1 == $str2)
            $commonLength += 1;
        else
            break;
    }

    // Case A (ii)-
    if (($k - strlen($str1) - strlen($str2) +
                 2 * $commonLength) % 2 == 0)
        return true;

    // Case B
    return false;
}

// Driver Code
$str1 = "geek";
$str2 = "geek";
$k = 7;

if (isConvertible($str1, $str2, $k))
    echo "Yes" . "\n";
else
    echo "No" . "\n";

$str1 = "geeks";
$str2 = "geek";
$k = 5;

if (isConvertible($str1, $str2, $k))
    echo "Yes" . "\n";
else
    echo "No" . "\n";

// This code is contributed by
// Mukul Singh
?>
```

## java 描述语言

```
<script>

// Javascript Program to convert str1 to str2 in
// exactly k operations

// Returns true if it is possible to convert
// str1 to str2 using k operations.
function isConvertible(str1, str2, k)
{
    // Case A (i)
    if ((str1.length + str2.length) < k)
        return true;

    // finding common length of both string
    var commonLength = 0;
    for (var i = 0; i < Math.min(str1.length,
                           str2.length); i++) {
        if (str1[i] == str2[i])
            commonLength++;
        else
            break;
    }

    // Case A (ii)-
    if ((k - str1.length - str2.length +
                     2 * commonLength) % 2 == 0)
        return true;

    // Case B-
    return false;
}

// driver program
var str1 = "geek", str2 = "geek";
var k = 7;
if (isConvertible(str1, str2, k))
   document.write( "Yes");
else
   document.write( "No");
str1 = "geeks",  str2 = "geek";
k = 5;   
document.write("<br>");
if (isConvertible(str1, str2, k))
   document.write( "Yes");
else
   document.write("No");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
No
Yes
```