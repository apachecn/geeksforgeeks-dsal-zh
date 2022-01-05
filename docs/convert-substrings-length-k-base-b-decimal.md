# 将长度为‘k’的所有子串从基数‘b’转换为十进制

> 原文:[https://www . geesforgeks . org/convert-substrings-length-k-base-B- decimal/](https://www.geeksforgeeks.org/convert-substrings-length-k-base-b-decimal/)

给出了一个定义有效数字的字符串。输出长度为“k”的子字符串从基数“b”到基数 10 的所有基数转换。

**示例:**

```
Input :  str = "12212", 
      k = 3, b = 3.
Output : 17 25 23
Explanation :
All the substrings of length 'k' are : 122, 221, 212.
Base conversion can be computed using the formula.
```

**方法 1(简单)**

一个简单的方法是使用简单的基础转换技术。对于以 b 为基数的数字串，其十进制等效值为 str[0]* b<sup>0</sup>+str[1]* b<sup>1</sup>+str[2]* b<sup>2</sup>+…+str[n-1]* b<sup>n-1</sup>

## C++

```
// Simple C++ program to convert all substrings from
// decimal to given base.
#include <bits/stdc++.h>
using namespace std;

int substringConversions(string str, int k, int b)
{
    for (int i=0; i + k <= str.size(); i++)
    {
        // Saving substring in sub
        string sub = str.substr(i, k);       

        // Evaluating decimal for current substring
        // and printing it.
        int sum = 0, counter = 0;
        for (int i = sub.size() - 1; i >= 0; i--)
        {
            sum = sum + ((sub.at(i) - '0') * pow(b, counter));
            counter++;
        }       
        cout << sum << " ";
    }
}

// Driver code
int main()
{
    string str = "12212";
    int b = 3, k = 3;
    substringConversions(str, b, k);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to convert all substrings from
// decimal to given base.

class GFG
{

static void substringConversions(String str, int k, int b)
{
    for (int i=0; i + k <= str.length(); i++)
    {
        // Saving substring in sub
        String sub = str.substring(i, i+k);    

        // Evaluating decimal for current substring
        // and printing it.
        int sum = 0, counter = 0;
        for (int j = sub.length() - 1; j >= 0; j--)
        {
            sum = (int) (sum + ((sub.charAt(j) - '0') *
                                    Math.pow(b, counter)));
            counter++;
        }    
        System.out.print(sum + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "12212";
    int b = 3, k = 3;
    substringConversions(str, b, k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Simple Python3 program to convert
# all substrings from decimal to given base.
import math

def substringConversions(s, k, b):

    l = len(s);
    for i in range(l):

        if((i + k) < l + 1):

            # Saving substring in sub
            sub = s[i : i + k];    

            # Evaluating decimal for current
            # substring and printing it.
            sum, counter = 0, 0;
            for i in range(len(sub) - 1, -1, -1):

                sum = sum + ((ord(sub[i]) - ord('0')) *    
                              pow(b, counter));
                counter += 1;

            print(sum , end = " ");

# Driver code
s = "12212";
b, k = 3, 3;
substringConversions(s, b, k);

# This code is contributed
# by Princi Singh
```

## C#

```
// Simple C# program to convert all substrings from
// decimal to given base.
using System;

class GFG
{

static void substringConversions(String str, int k, int b)
{
    for (int i = 0; i + k <= str.Length; i++)
    {
        // Saving substring in sub
        String sub = str.Substring(i, k);    

        // Evaluating decimal for current substring
        // and printing it.
        int sum = 0, counter = 0;
        for (int j = sub.Length - 1; j >= 0; j--)
        {
            sum = (int) (sum + ((sub[j] - '0') *
                                    Math.Pow(b, counter)));
            counter++;
        }    
        Console.Write(sum + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "12212";
    int b = 3, k = 3;
    substringConversions(str, b, k);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Simple Javascript program to convert
// all substrings from decimal to given base.
function substringConversions(str, k, b)
{
    for(let i = 0; i + k <= str.length; i++)
    {

        // Saving substring in sub
        let sub = str.substring(i, i+k);    

        // Evaluating decimal for current substring
        // and printing it.
        let sum = 0, counter = 0;
        for(let j = sub.length - 1; j >= 0; j--)
        {
            sum =  (sum + ((sub[j].charCodeAt(0) -
                               '0'.charCodeAt(0)) *
                               Math.pow(b, counter)));
            counter++;
        }    
        document.write(sum + " ");
    }
}

// Driver code
let str = "12212";
let b = 3, k = 3;

substringConversions(str, b, k);

// This code is contributed by patel2127

</script>
```

**输出:**

```
17 25 23
```

**时间复杂度:** O(n*k)

**方法 2(使用滑动窗口)**

我们可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)在线性时间内求解。每次滑动窗口，我们都会减去第一个元素**的权重，即(元素* pow(b，k-1) )** 。现在，将前面的总和乘以“b”会将每个元素的权重增加 3 倍，这是必需的。此外，我们将简单地在窗口中添加新元素，因为它的权重将是**元素* pow(b，0)** 。

下面是实现:

## C++

```
// Efficient C++ program to convert all substrings from
// decimal to given base.
#include <bits/stdc++.h>
using namespace std;

int substringConversions(string str, int k, int b)
{
   int i = 0, sum = 0, counter = k-1;

    // Computing the decimal of first window
    for (i; i < k; i++)
    {
        sum = sum + ((str.at(i) - '0') * pow(b, counter));
        counter--;
    }
    cout << sum << " ";

    // prev stores the previous decimal
    int prev = sum;

    // Computing decimal equivalents of all other windows
    sum = 0, counter = 0;
    for (i; i < str.size(); i++)
    {
        // Subtracting weight of the element pushed out of window
        sum = prev - ((str.at(i - k) - '0') * pow(b, k-1));

        // Multiplying the decimal by base to formulate other window
        sum = sum * b;

        // Adding the new element of window to sum
        sum = sum + (str.at(i) - '0');

        // Decimal of current window
        cout << sum << " ";

        // Updating prev
        prev = sum;

        counter++;
    }
}

// Driver code
int main()
{
    string str = "12212";
    int b = 3, k = 3;
    substringConversions(str, b, k);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to convert
// all substrings from decimal to given base.
import java.util.*;

class GFG
{
static void substringConversions(String str,
                                 int k, int b)
{
    int i = 0, sum = 0, counter = k-1;

    // Computing the decimal of first window
    for (i = 0; i < k; i++)
    {
        sum = (int) (sum + ((str.charAt(i) - '0') *
                             Math.pow(b, counter)));
        counter--;
    }
    System.out.print(sum + " ");

    // prev stores the previous decimal
    int prev = sum;

    // Computing decimal equivalents of all other windows
    sum = 0; counter = 0;
    for (; i < str.length(); i++)
    {
        // Subtracting weight of the element
        // pushed out of window
        sum = (int) (prev - ((str.charAt(i - k) - '0') *
                              Math.pow(b, k - 1)));

        // Multiplying the decimal by base
        // to formulate other window
        sum = sum * b;

        // Adding the new element of window to sum
        sum = sum + (str.charAt(i) - '0');

        // Decimal of current window
        System.out.print(sum + " ");

        // Updating prev
        prev = sum;

        counter++;
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "12212";
    int b = 3, k = 3;
    substringConversions(str, b, k);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Simple Python3 program to convert all
# substrings from decimal to given base.
import math as mt

def substringConversions(str1, k, b):

    for i in range(0, len(str1) - k + 1):

        # Saving subin sub
        sub = str1[i:k + i]

        # Evaluating decimal for current
        # substring and printing it.
        Sum = 0
        counter = 0
        for i in range(len(sub) - 1, -1, -1):
            Sum = (Sum + ((ord(sub[i]) - ord('0')) *
                           pow(b, counter)))
            counter += 1

        print(Sum, end = " ")

# Driver code
str1 = "12212"
b = 3
k = 3
substringConversions(str1, b, k)

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// Efficient C# program to convert
// all substrings from decimal to given base.
using System;

class GFG
{
static void substringConversions(String str,
                                 int k, int b)
{
    int i = 0, sum = 0, counter = k-1;

    // Computing the decimal of first window
    for (i = 0; i < k; i++)
    {
        sum = (int) (sum + ((str[i] - '0') *
                             Math.Pow(b, counter)));
        counter--;
    }
    Console.Write(sum + " ");

    // prev stores the previous decimal
    int prev = sum;

    // Computing decimal equivalents
    // of all other windows
    sum = 0; counter = 0;
    for (; i < str.Length; i++)
    {
        // Subtracting weight of the element
        // pushed out of window
        sum = (int) (prev - ((str[i - k] - '0') *
                               Math.Pow(b, k - 1)));

        // Multiplying the decimal by base
        // to formulate other window
        sum = sum * b;

        // Adding the new element of window to sum
        sum = sum + (str[i] - '0');

        // Decimal of current window
        Console.Write(sum + " ");

        // Updating prev
        prev = sum;

        counter++;
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "12212";
    int b = 3, k = 3;
    substringConversions(str, b, k);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Efficient Javascript program to convert
// all substrings from decimal to given base.
function substringConversions(str, k, b)
{
    let i = 0, sum = 0, counter = k-1;

    // Computing the decimal of first window
    for(i = 0; i < k; i++)
    {
        sum =  (sum + ((str[i].charCodeAt(0) -
                           '0'.charCodeAt(0)) *
                           Math.pow(b, counter)));
        counter--;
    }
    document.write(sum + " ");

    // prev stores the previous decimal
    let prev = sum;

    // Computing decimal equivalents of
    // all other windows
    sum = 0; counter = 0;
    for(; i < str.length; i++)
    {

        // Subtracting weight of the element
        // pushed out of window
        sum =  (prev - ((str[i - k].charCodeAt(0) -
                                '0'.charCodeAt(0)) *
                                Math.pow(b, k - 1)));

        // Multiplying the decimal by base
        // to formulate other window
        sum = sum * b;

        // Adding the new element of window to sum
        sum = sum + (str[i].charCodeAt(0) -
                        '0'.charCodeAt(0));

        // Decimal of current window
        document.write(sum + " ");

        // Updating prev
        prev = sum;

        counter++;
    }
}

// Driver code
let str = "12212";
let b = 3, k = 3;

substringConversions(str, b, k);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
17 25 23
```

**时间复杂度:** O(n)

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。