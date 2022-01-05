# 在第二个字符串上执行交换后，找到两个字符串之间最长的公共前缀

> 原文:[https://www . geeksforgeeks . org/find-第二个字符串执行交换后两个字符串之间最长的公共前缀/](https://www.geeksforgeeks.org/find-the-longest-common-prefix-between-two-strings-after-performing-swaps-on-second-string/)

给定两根弦![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")和![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。在对字符串![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")执行零个或多个操作后，找到它们之间最长的公共前缀。在每个操作中，您可以交换任意两个字母。
T4【示例】T5:

```
Input : a = "here", b = "there"
Output : 4
The 2nd string can be made "heret" by just 
swapping characters and thus the longest
prefix is of length 4.

Input : a = "you", b = "me"
Output : 0
```

假设我们只允许在字符串![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")中执行交换，前缀的长度应该最大化。所以想法是遍历字符串![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")，检查字符串![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")中当前字符的频率是否与字符串![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")中相同或更少。如果是，则在字符串中向前移动，否则会中断并打印字符串中与字符匹配的部分的长度![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。
以下是上述方法的实施:

## C++

```
// C++ program to find the longest
// common prefix between two strings
// after performing swaps on the second string
#include <bits/stdc++.h>
using namespace std;

void LengthLCP(string x, string y)
{

    int fr[26]={0};

    int a = x.length(); // length of x
    int b = y.length(); // length of y

    for (int i=0 ;i<b ; i++)
    {
        // creating frequency array of
        // characters of y
        fr[y[i] - 97] += 1;
    }
    // storing the length of
    // longest common prefix
    int c = 0;

    for (int i=0 ;i<a ; i++)
    {
        // checking if the frequency of the character at
        // position i in x in b is greater than zero or not
        // if zero we increase the prefix count by 1
        if (fr[x[i] - 97] > 0){
            c += 1;
            fr[x[i] - 97] -= 1;
        }
        else
            break;
    }
    cout<<(c)<<endl;
}
// Driver Code
int main()
{
string x="here", y =  "there";

LengthLCP(x, y);

return 0;
}
//contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest
// common prefix between two strings
// after performing swaps on the second string

public class GFG {

    static void LengthLCP(String x, String y)
    {

        int fr[]=new int [26];

        int a = x.length(); // length of x
        int b = y.length(); // length of y

        for (int i=0 ;i<b ; i++)
        {
            // creating frequency array of
            // characters of y
            fr[y.charAt(i) - 97] += 1;
        }
        // storing the length of
        // longest common prefix
        int c = 0;

        for (int i=0 ;i<a ; i++)
        {
            // checking if the frequency of the character at
            // position i in x in b is greater than zero or not
            // if zero we increase the prefix count by 1
            if (fr[x.charAt(i) - 97] > 0){
                c += 1;
                fr[x.charAt(i) - 97] -= 1;
            }
            else
                break;
        }
        System.out.println((c)) ;
    }

    public static void main(String args[])
    {
        String x="here", y =  "there";

        LengthLCP(x, y);

    }
    // This code is contributed by ANKITRAI1
}

```

## 蟒蛇 3

```
# Python program to find the longest
# common prefix between two strings
# after performing swaps on the second string

def LengthLCP(x, y):
    fr = [0] * 26

    a = len(x) # length of x
    b = len(y) # length of y

    for i in range(b):
        # creating frequency array of
        # characters of y
        fr[ord(y[i]) - 97] += 1

    # storing the length of
    # longest common prefix
    c = 0

    for i in range(a):
        # checking if the frequency of the character at
        # position i in x in b is greater than zero or not
        # if zero we increase the prefix count by 1
        if (fr[ord(x[i]) - 97] > 0):
            c += 1
            fr[ord(x[i]) - 97] -= 1
        else:
            break
    print(c)

# Driver Code

x, y = "here", "there"

LengthLCP(x, y)
```

## C#

```
// C# program to find the longest
// common prefix between two strings
// after performing swaps on the
// second string
using System;

class GFG
{

static void LengthLCP(String x, String y)
{
    int []fr = new int [26];

    int a = x.Length; // length of x
    int b = y.Length; // length of y

    for (int i = 0 ; i < b; i++)
    {
        // creating frequency array
        // of characters of y
        fr[y[i] - 97] += 1;
    }

    // storing the length of
    // longest common prefix
    int c = 0;

    for (int i = 0 ; i < a; i++)
    {
        // checking if the frequency of
        // the character at position i
        // in x in b is greater than zero
        // or not if zero we increase the
        // prefix count by 1
        if (fr[x[i] - 97] > 0)
        {
            c += 1;
            fr[x[i] - 97] -= 1;
        }
        else
            break;
    }
    Console.Write((c)) ;
}

// Driver Code
public static void Main()
{
    String x = "here", y = "there";

    LengthLCP(x, y);
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the longest
// common prefix between two strings
// after performing swaps on the second string

function LengthLCP($x, $y)
{

    $fr = array_fill(0,26,NULL);

    $a = strlen($x); // length of x
    $b = strlen($y); // length of y

    for ($i = 0 ;$i < $b ; $i++)
    {
        // creating frequency array of
        // characters of y
        $fr[ord($y[$i]) - 97] += 1;
    }

    // storing the length of
    // longest common prefix
    $c = 0;

    for ($i = 0 ;$i < $a ; $i++)
    {
        // checking if the frequency of the character at
        // position i in x in b is greater than zero or not
        // if zero we increase the prefix count by 1
        if ($fr[ord($x[$i]) - 97] > 0)
        {
            $c += 1;
            $fr[ord($x[$i]) - 97] -= 1;
        }
        else
            break;
    }
    echo $c;
}

// Driver Code
$x="here";
$y = "there";

LengthLCP($x, $y);

return 0;

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the long
// common prefix between two strings
// after performing swaps on the second string

    function LengthLCP(x, y)
    {

        let fr = Array(26).fill(0);

        let a = x.length; // length of x
        let b = y.length; // length of y

        for (let i=0 ;i<b ; i++)
        {
            // creating frequency array of
            // characters of y
            fr[y[i].charCodeAt() - 97] += 1;
        }
        // storing the length of
        // longest common prefix
        let c = 0;

        for (let i=0 ;i<a ; i++)
        {
            // checking if the
            // frequency of the character at
            // position i in x in b is greater
            // than zero or not
            // if zero we increase the
            // prefix count by 1
            if (fr[x[i].charCodeAt() - 97] > 0){
                c += 1;
                fr[x[i].charCodeAt() - 97] -= 1;
            }
            else
                break;
        }
        document.write((c)) ;
    }

// driver code

    let x="here", y =  "there";

        LengthLCP(x, y);

</script>
```

**Output:** 

```
4
```