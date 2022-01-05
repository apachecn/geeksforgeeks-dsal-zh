# 构建词典上最小的回文

> 原文:[https://www . geeksforgeeks . org/construct-字典序-最小-回文/](https://www.geeksforgeeks.org/construct-lexicographically-smallest-palindrome/)

给定一串小写字母。给定字符串的某些字符已损坏，现在用*表示。我们可以用任何小写字母替换*。你必须构造字典上最小的回文串。如果无法构建回文打印“不可能”。
**例:**

```
Input : str[] = "bc*b" 
Output : bccb

Input : str[] = "bc*a*cb"
Output : bcaaacb

Input : str[] = "bac*cb"
Output : Not Possible
```

从两端开始遍历字符串。假设 i=0，j=strlen-1，每次迭代后继续增加 I 和减少 j，直到 I 超过 j。现在在任何中间位置，我们有五种可能的情况:

1.  str[i]和 str[j]都是相同的，也不等于' * '。在这种情况下，继续。
2.  str[i]和 str[j]都是相同的，都等于' * '。在这里，您必须填充 str[i] = str[j] = 'a '以获得最小可能的回文。
3.  str[i]等于' * '，str[j]是一些字母表。这里填充 str[i] = str[j]，使我们的字符串成为回文。
4.  str[j]等于' * '，str[i]是一些字母表。这里填充 str[j] = str[i]，使我们的字符串成为回文。
5.  str[i]不等于 str[j],而且两者都是一些字母表。在这种情况下，回文结构是不可能的。所以，打印“不可能”并中断循环。

I 超过 j 后表示我们得到了所需的回文。否则我们得到“不可能”的结果。

## C++

```
// CPP for constructing smallest palindrome
#include <bits/stdc++.h>
using namespace std;

// function for printing palindrome
string constructPalin(string str, int len)
{
    int i = 0, j = len - 1;

    // iterate till i<j
    for (; i < j; i++, j--) {

        // continue if str[i]==str[j]
        if (str[i] == str[j] && str[i] != '*')
            continue;

        // update str[i]=str[j]='a' if both are '*'
        else if (str[i] == str[j] && str[i] == '*') {
            str[i] = 'a';
            str[j] = 'a';
            continue;
        }

        // update str[i]=str[j] if only str[i]='*'
        else if (str[i] == '*') {
            str[i] = str[j];
            continue;
        }

        // update str[j]=str[i] if only str[j]='*'
        else if (str[j] == '*') {
            str[j] = str[i];
            continue;
        }

        // else print not possible and return
        cout << "Not Possible";
        return "";
    }
    return str;
}

// driver program
int main()
{
    string str = "bca*xc**b";
    int len = str.size();
    cout << constructPalin(str, len);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java for constructing smallest palindrome
class GFG
{

// function for printing palindrome
static String constructPalin(char []str, int len)
{
    int i = 0, j = len - 1;

    // iterate till i<j
    for (; i < j; i++, j--)
    {

        // continue if str[i]==str[j]
        if (str[i] == str[j] && str[i] != '*')
            continue;

        // update str[i]=str[j]='a' if both are '*'
        else if (str[i] == str[j] &&
                        str[i] == '*')
        {
            str[i] = 'a';
            str[j] = 'a';
            continue;
        }

        // update str[i]=str[j] if only str[i]='*'
        else if (str[i] == '*')
        {
            str[i] = str[j];
            continue;
        }

        // update str[j]=str[i] if only str[j]='*'
        else if (str[j] == '*')
        {
            str[j] = str[i];
            continue;
        }

        // else print not possible and return
        System.out.println("Not Possible");
        return "";
    }
    return String.valueOf(str);
}

// Driver code
public static void main(String[] args)
{
    String str = "bca*xc**b";
    int len = str.length();
    System.out.println(constructPalin(str.toCharArray(), len));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 for constructing smallest palindrome

# function for printing palindrome
def constructPalin(string, l):
    string = list(string)
    i = -1
    j = l

    # iterate till i<j
    while i < j:
        i += 1
        j -= 1

        # continue if str[i]==str[j]
        if (string[i] == string[j] and
            string[i] != '*'):
            continue

        # update str[i]=str[j]='a' if both are '*'
        elif (string[i] == string[j] and
              string[i] == '*'):
            string[i] = 'a'
            string[j] = 'a'
            continue

        # update str[i]=str[j] if only str[i]='*'
        elif string[i] == '*':
            string[i] = string[j]
            continue

        # update str[j]=str[i] if only str[j]='*'
        elif string[j] == '*':
            string[j] = string[i]
            continue

        # else print not possible and return
        print("Not Possible")
        return ""
    return ''.join(string)

# Driver Code
if __name__ == "__main__":
    string = "bca*xc**b"
    l = len(string)
    print(constructPalin(string, l))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# for constructing smallest palindrome
using System;

class GFG
{

// function for printing palindrome
static String constructPalin(char []str, int len)
{
    int i = 0, j = len - 1;

    // iterate till i<j
    for (; i < j; i++, j--)
    {

        // continue if str[i]==str[j]
        if (str[i] == str[j] && str[i] != '*')
            continue;

        // update str[i]=str[j]='a' if both are '*'
        else if (str[i] == str[j] &&
                        str[i] == '*')
        {
            str[i] = 'a';
            str[j] = 'a';
            continue;
        }

        // update str[i]=str[j] if only str[i]='*'
        else if (str[i] == '*')
        {
            str[i] = str[j];
            continue;
        }

        // update str[j]=str[i] if only str[j]='*'
        else if (str[j] == '*')
        {
            str[j] = str[i];
            continue;
        }

        // else print not possible and return
        Console.WriteLine("Not Possible");
        return "";
    }
    return String.Join("",str);
}

// Driver code
public static void Main(String[] args)
{
    String str = "bca*xc**b";
    int len = str.Length;
    Console.WriteLine(constructPalin(str.ToCharArray(), len));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP for constructing smallest palindrome

// function for printing palindrome
function constructPalin($str, $len)
{
    $i = 0;
    $j = $len - 1;

    // iterate till i<j
    for (; $i < $j; $i++, $j--)
    {

        // continue if str[i]==str[j]
        if ($str[$i] == $str[$j] &&
            $str[$i] != '*')
            continue;

        // update str[i]=str[j]='a' if both are '*'
        else if ($str[$i] == $str[$j] &&
                 $str[$i] == '*')
        {
            $str[$i] = 'a';
            $str[$j] = 'a';
            continue;
        }

        // update str[i]=str[j] if only str[i]='*'
        else if ($str[$i] == '*')
        {
            $str[$i] = $str[$j];
            continue;
        }

        // update str[j]=str[i] if only str[j]='*'
        else if ($str[$j] == '*')
        {
            $str[$j] = $str[$i];
            continue;
        }

        // else print not possible and return
        echo "Not Possible";
        return "";
    }
    return $str;
}

// Driver Code
$str = "bca*xc**b";
$len = strlen($str);
echo constructPalin($str, $len);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// javascript for constructing smallest palindrome

// function for printing palindrome
function constructPalin(str, len)
{
    var i = 0, j = len - 1;

    // iterate till i<j
    for (; i < j; i++, j--) {

        // continue if str[i]==str[j]
        if (str[i] == str[j] && str[i] != '*')
            continue;

        // update str[i]=str[j]='a' if both are '*'
        else if (str[i] == str[j] && str[i] == '*') {
            str[i] = 'a';
            str[j] = 'a';
            continue;
        }

        // update str[i]=str[j] if only str[i]='*'
        else if (str[i] == '*') {
            str[i] = str[j];
            continue;
        }

        // update str[j]=str[i] if only str[j]='*'
        else if (str[j] == '*') {
            str[j] = str[i];
            continue;
        }

        // else print not possible and return
        document.write( "Not Possible");
        return "";
    }
    return str.join("");
}

// driver program
var str = "bca*xc**b".split("");
var len = str.length;
document.write( constructPalin(str, len));

</script>
```

**输出:**

```
bcacxcacb
```