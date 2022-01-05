# 给定一个二进制字符串，计算以 1 开始和结束的子字符串的数量。

> 原文:[https://www . geesforgeks . org/given-binary-string-count-number-substrings-start-end-1/](https://www.geeksforgeeks.org/given-binary-string-count-number-substrings-start-end-1/)

给定一个二进制字符串，计算以 1 开头和结尾的子字符串的数量。例如，如果输入字符串是“00100101”，则有三个子字符串“1001”、“100101”和“101”。
来源:[亚马逊面试体验|第 162 集](https://www.geeksforgeeks.org/amazon-interview-experience-set-162/)
**难度等级:**菜鸟

一个**简单的解决方案**是运行两个循环。外循环选择每 1 作为起点，内循环搜索结束 1，并在找到 1 时递增计数。

## C++

```
// A simple C++ program to count number of
// substrings starting and ending with 1
#include<iostream>

using namespace std;

int countSubStr(char str[])
{
int res = 0; // Initialize result

// Pick a starting point
for (int i=0; str[i] !='\0'; i++)
{
        if (str[i] == '1')
        {
            // Search for all possible ending point
            for (int j=i+1; str[j] !='\0'; j++)
            if (str[j] == '1')
                res++;
        }
}
return res;
}

// Driver program to test above function
int main()
{
char str[] = "00100101";
cout << countSubStr(str);
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple C++ program to count number of
//substrings starting and ending with 1

class CountSubString
{
    int countSubStr(char str[],int n)
    {
        int res = 0;  // Initialize result

        // Pick a starting point
        for (int i = 0; i<n; i++)
        {
            if (str[i] == '1')
            {
                // Search for all possible ending point
                for (int j = i + 1; j< n; j++)
                {
                    if (str[j] == '1')
                        res++;
                }
            }
        }
        return res;
    }

    // Driver program to test the above function
    public static void main(String[] args)
    {
        CountSubString count = new CountSubString();
        String string = "00100101";
        char str[] = string.toCharArray();
        int n = str.length;
        System.out.println(count.countSubStr(str,n));
    }
}
```

## 蟒蛇 3

```
# A simple Python 3 program to count number of
# substrings starting and ending with 1

def countSubStr(st, n) :

    # Initialize result
    res = 0  

   # Pick a starting point
    for i in range(0, n) :
        if (st[i] == '1') :

            # Search for all possible ending point
            for j in range(i+1, n) :
                if (st[j] == '1') :
                    res = res + 1

    return res

# Driver program to test above function
st = "00100101";
list(st)
n= len(st)
print(countSubStr(st, n), end="")

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// A simple C# program to count number of
// substrings starting and ending with 1
using System;

class GFG
{
public virtual int countSubStr(char[] str,
                               int n)
{
    int res = 0; // Initialize result

    // Pick a starting point
    for (int i = 0; i < n; i++)
    {
        if (str[i] == '1')
        {
            // Search for all possible
            // ending point
            for (int j = i + 1; j < n; j++)
            {
                if (str[j] == '1')
                {
                    res++;
                }
            }
        }
    }
    return res;
}

// Driver Code
public static void Main(string[] args)
{
    GFG count = new GFG();
    string s = "00100101";
    char[] str = s.ToCharArray();
    int n = str.Length;
    Console.WriteLine(count.countSubStr(str,n));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to count number of
// substrings starting and ending with 1

function countSubStr($str)
{
    $res = 0; // Initialize result

    // Pick a starting point
    for ($i = 0; $i < strlen($str); $i++)
    {
            if ($str[$i] == '1')
            {
                // Search for all possible
                // ending point
                for ($j = $i + 1;
                     $j < strlen($str); $j++)
                if ($str[$j] == '1')
                    $res++;
            }
    }
    return $res;
}

// Driver Code
$str = "00100101";
echo countSubStr($str);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// A simple javascript program to count number of
// substrings starting and ending with 1

    function countSubStr(str,n)
    {
        let res = 0;  // Initialize result
        // Pick a starting point
        for (let i = 0; i<n; i++)
        {
            if (str[i] == '1')
            {
                // Search for all possible ending point
                for (let j = i + 1; j< n; j++)
                {
                    if (str[j] == '1')
                        res++;
                }
            }
        }
        return res;
    }

    // Driver program to test the above function
    let string = "00100101";
    let n=string.length;
    document.write(countSubStr(string,n));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
3
```

上述解的时间复杂度为 O(n <sup>2</sup> )。使用输入字符串的单次遍历，我们可以在 O(n)中找到计数**。以下是步骤。
a)计算 1 的数量。让 1 的数量为 m。
b)返回 m(m-1)/2
想法是计算 1 的可能对的总数。** 

## C++

```
// A O(n) C++ program to count number of
// substrings starting and ending with 1
#include<iostream>

using namespace std;

int countSubStr(char str[])
{
   int m = 0; // Count of 1's in input string

   // Traverse input string and count of 1's in it
   for (int i=0; str[i] !='\0'; i++)
   {
        if (str[i] == '1')
           m++;
   }

   // Return count of possible pairs among m 1's
   return m*(m-1)/2;
}

// Driver program to test above function
int main()
{
  char str[] = "00100101";
  cout << countSubStr(str);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(n) C++ program to count number of substrings
//starting and ending with 1

class CountSubString
{
    int countSubStr(char str[], int n)
    {
        int m = 0; // Count of 1's in input string

        // Traverse input string and count of 1's in it
        for (int i = 0; i < n; i++)
        {
            if (str[i] == '1')
                m++;
        }

        // Return count of possible pairs among m 1's
        return m * (m - 1) / 2;
    }

    // Driver program to test the above function
    public static void main(String[] args)
    {
        CountSubString count = new CountSubString();
        String string = "00100101";
        char str[] = string.toCharArray();
        int n = str.length;
        System.out.println(count.countSubStr(str, n));
    }
}
```

## 蟒蛇 3

```
# A Python3 program to count number of
# substrings starting and ending with 1

def countSubStr(st, n) :

    # Count of 1's in input string
    m = 0 

    # Traverse input string and
    # count of 1's in it
    for i in range(0, n) :
        if (st[i] == '1') :
            m = m + 1

    # Return count of possible
    # pairs among m 1's
    return m * (m - 1) // 2

# Driver program to test above function
st = "00100101";
list(st)
n= len(st)
print(countSubStr(st, n), end="")

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// A O(n) C# program to count
// number of substrings starting
// and ending with 1
using System;

class GFG
{
int countSubStr(char []str, int n)
{
    int m = 0; // Count of 1's in
               // input string

    // Traverse input string and
    // count of 1's in it
    for (int i = 0; i < n; i++)
    {
        if (str[i] == '1')
            m++;
    }

    // Return count of possible
    // pairs among m 1's
    return m * (m - 1) / 2;
}

// Driver Code
public static void Main(String[] args)
{
    GFG count = new GFG();
    String strings = "00100101";
    char []str = strings.ToCharArray();
    int n = str.Length;
    Console.Write(count.countSubStr(str, n));
}
}

// This code is contributed by princiraj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to count number of
// substrings starting and ending with 1

function countSubStr($str)
{
    $m = 0; // Initialize result

    // Pick a starting point
    for ($i = 0; $i < strlen($str); $i++)
    {
        if ($str[$i] == '1')
        {
            $m++;
        }
    }

    // Return count of possible
    // pairs among m 1's
    return $m * ($m - 1) / 2;
}

// Driver Code
$str = "00100101";
echo countSubStr($str);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// A O(n) javascript program to count number of substrings
//starting and ending with 1

    function countSubStr(str,n)
    {
        let m = 0; // Count of 1's in input string

        // Traverse input string and count of 1's in it
        for (let i = 0; i < n; i++)
        {
            if (str[i] == '1')
                m++;
        }

        // Return count of possible pairs among m 1's
        return m * Math.floor((m - 1) / 2);
    }

    // Driver program to test the above function
    let str = "00100101";
    let n = str.length;
    document.write(countSubStr(str, n));

    //  This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
3
```

本文由**希瓦姆**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息