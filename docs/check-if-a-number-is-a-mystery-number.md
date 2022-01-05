# 检查一个号码是否是神秘号码

> 原文:[https://www . geesforgeks . org/check-如果一个数字是一个神秘的数字/](https://www.geeksforgeeks.org/check-if-a-number-is-a-mystery-number/)

给定一个数字，检查它是否是一个神秘的数字。神秘数字是一个可以表示为两个数字之和的数字，这两个数字应该是相反的。

**示例:**

> 输入:n = 121
> 输出:29 92
> 
> 输入:n = 22
> 输出:11 11

**来源** : [Paytm 访谈集 23](https://www.geeksforgeeks.org/paytm-interview-experience-set-23-2-years-experienced/)
想法是尝试每一对小于或等于 n 的可能配对

下面是上述方法的实现。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Finds reverse of given num x.
int reverseNum(int x)
{
    string s = to_string(x);
    reverse(s.begin(), s.end());
    stringstream ss(s);
    int rev = 0;
    ss >> rev;
    return rev;
}

bool isMysteryNumber(int n)
{
    for (int i=1; i <= n/2; i++)
    {
        // if found print the  pair, return
        int j = reverseNum(i);
        if (i + j == n)
        {
            cout << i << " " << j;
            return true;
        }
    }

    cout << "Not a Mystery Number";
    return false;
}

int main()
{
    int n = 121;
    isMysteryNumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG
{
    // Finds reverse of given num x.
    static int reverseNum(int x)
    {
        String s = Integer.toString(x);
        String str="";
        for(int i=s.length()-1;i>=0;i--)
        {

            str=str+s.charAt(i);
        }

        int rev=Integer.parseInt(str);
        return rev;
    }

    static boolean isMysteryNumber(int n)
    {
        for (int i=1; i <= n/2; i++)
        {
            // if found print the pair, return
            int j = reverseNum(i);
            if (i + j == n)
            {
                System.out.println( i + " " + j);
                return true;
            }
        }

         System.out.println("Not a Mystery Number");
        return false;
    }

    public static void main(String []args)
    {
        int n = 121;
        isMysteryNumber(n);

    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Finds reverse of given num x.
def reverseNum(x):
    s = str(x)
    s = s[::-1]
    return int(s)

def isMysteryNumber(n):

    for i in range(1, n // 2 + 1):

        # if found print the pair, return
        j = reverseNum(i)

        if i + j == n:
            print(i, j)
            return True

    print("Not a Mystery Number")
    return False

# Driver Code
n = 121
isMysteryNumber(n)

# This code is contributed by
# Mohit Kumar 29 (IIIT gwalior)
```

## C#

```
// C# implementation of above approach

using System;
class GFG
{
    // Finds reverse of given num x.
    static int reverseNum(int x)
    {
        string s = x.ToString();
        string str="";
        for(int i=s.Length-1;i>=0;i--)
        {

            str=str+s[i];
        }

        int rev=Int32.Parse(str);
        return rev;
    }

    static bool isMysteryNumber(int n)
    {
        for (int i=1; i <= n/2; i++)
        {
            // if found print the pair, return
            int j = reverseNum(i);
            if (i + j == n)
            {
                Console.WriteLine( i + " " + j);
                return true;
            }
        }

        Console.WriteLine("Not a Mystery Number");
        return false;
    }

    public static void Main()
    {
        int n = 121;
        isMysteryNumber(n);

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Finds reverse of given num x.
function reverseNum($x)
{
    $s = (string)$x;
    $s = strrev($s);
    $rev = (int)$s;
    return $rev;
}

function isMysteryNumber($n)
{
    for ($i=1; $i <= $n/2; $i++)
    {
        // if found print the  pair, return
        $j = reverseNum($i);
        if ($i + $j == $n)
        {
            echo $i . " ".$j;
            return true;
        }
    }

    echo "Not a Mystery Number";
    return false;
}

$n = 121;
isMysteryNumber($n);
return 0;
// This code is contribute by Ita_c.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

    // Finds reverse of given num x.
    function reverseNum(x)
    {
        let s = x.toString();
        let str="";
        for(let i=s.length-1;i>=0;i--)
        {

            str=str+s[i];
        }

        let rev=parseInt(str);
        return rev;
    }

    function isMysteryNumber(n)
    {
        for (let i=1; i <= Math.floor(n/2); i++)
        {
            // if found print the pair, return
            let j = reverseNum(i);
            if (i + j == n)
            {
                document.write( i + " " + j+"<br>");
                return true;
            }
        }

         document.write("Not a Mystery Number<br>");
        return false;
    }

    let n = 121;
    isMysteryNumber(n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
29 92
```