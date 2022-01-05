# 两个大数之和

> 原文:[https://www.geeksforgeeks.org/sum-two-large-numbers/](https://www.geeksforgeeks.org/sum-two-large-numbers/)

给定两个数字作为字符串。这些数字可能非常大(可能不适合 long long int)，任务是找到这两个数字的总和。

**示例:**

```
Input  : str1 = "3333311111111111", 
         str2 =   "44422222221111"
Output : 3377733333332222

Input  : str1 = "7777555511111111", 
         str2 =    "3332222221111"
Output : 7780887733332222
```

这个想法是基于学校数学。我们从头到尾遍历两个字符串，一个接一个地添加数字并跟踪进位。为了简化过程，我们执行以下操作:
1)反转两个字符串。
2)从第 0 个索引(在反向字符串中)开始，将数字一个接一个地添加到较小字符串的末尾，将总和% 10 附加到结果的末尾，并将进位记录为总和/10。
3)最终扭转结果。

## C++

```
// C++ program to find sum of two large numbers.
#include<bits/stdc++.h>
using namespace std;

// Function for finding sum of larger numbers
string findSum(string str1, string str2)
{
    // Before proceeding further, make sure length
    // of str2 is larger.
    if (str1.length() > str2.length())
        swap(str1, str2);

    // Take an empty string for storing result
    string str = "";

    // Calculate length of both string
    int n1 = str1.length(), n2 = str2.length();

    // Reverse both of strings
    reverse(str1.begin(), str1.end());
    reverse(str2.begin(), str2.end());

    int carry = 0;
    for (int i=0; i<n1; i++)
    {
        // Do school mathematics, compute sum of
        // current digits and carry
        int sum = ((str1[i]-'0')+(str2[i]-'0')+carry);
        str.push_back(sum%10 + '0');

        // Calculate carry for next step
        carry = sum/10;
    }

    // Add remaining digits of larger number
    for (int i=n1; i<n2; i++)
    {
        int sum = ((str2[i]-'0')+carry);
        str.push_back(sum%10 + '0');
        carry = sum/10;
    }

    // Add remaining carry
    if (carry)
        str.push_back(carry+'0');

    // reverse resultant string
    reverse(str.begin(), str.end());

    return str;
}

// Driver code
int main()
{
    string str1 = "12";
    string str2 = "198111";
    cout << findSum(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of two large numbers.
import java.util.*;
class GFG
{
// Function for finding sum of larger numbers
static String findSum(String str1, String str2)
{
    // Before proceeding further, make sure length
    // of str2 is larger.
    if (str1.length() > str2.length()){
        String t = str1;
        str1 = str2;
        str2 = t;
    }

    // Take an empty String for storing result
    String str = "";

    // Calculate length of both String
    int n1 = str1.length(), n2 = str2.length();

    // Reverse both of Strings
    str1=new StringBuilder(str1).reverse().toString();
    str2=new StringBuilder(str2).reverse().toString();

    int carry = 0;
    for (int i = 0; i < n1; i++)
    {
        // Do school mathematics, compute sum of
        // current digits and carry
        int sum = ((int)(str1.charAt(i) - '0') +
                    (int)(str2.charAt(i) - '0') + carry);
        str += (char)(sum % 10 + '0');

        // Calculate carry for next step
        carry = sum / 10;
    }

    // Add remaining digits of larger number
    for (int i = n1; i < n2; i++)
    {
        int sum = ((int)(str2.charAt(i) - '0') + carry);
        str += (char)(sum % 10 + '0');
        carry = sum / 10;
    }

    // Add remaining carry
    if (carry > 0)
        str += (char)(carry + '0');

    // reverse resultant String
    str = new StringBuilder(str).reverse().toString();

    return str;
}

// Driver code
public static void main(String[] args)
{
    String str1 = "12";
    String str2 = "198111";
    System.out.println(findSum(str1, str2));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find sum of
# two large numbers.

# Function for finding sum of
# larger numbers
def findSum(str1, str2):

    # Before proceeding further,
    # make sure length of str2 is larger.
    if (len(str1) > len(str2)):
        t = str1;
        str1 = str2;
        str2 = t;

    # Take an empty string for
    # storing result
    str = "";

    # Calculate length of both string
    n1 = len(str1);
    n2 = len(str2);

    # Reverse both of strings
    str1 = str1[::-1];
    str2 = str2[::-1];

    carry = 0;
    for i in range(n1):

        # Do school mathematics, compute
        # sum of current digits and carry
        sum = ((ord(str1[i]) - 48) +
              ((ord(str2[i]) - 48) + carry));
        str += chr(sum % 10 + 48);

        # Calculate carry for next step
        carry = int(sum / 10);

    # Add remaining digits of larger number
    for i in range(n1, n2):
        sum = ((ord(str2[i]) - 48) + carry);
        str += chr(sum % 10 + 48);
        carry = (int)(sum / 10);

    # Add remaining carry
    if (carry):
        str += chr(carry + 48);

    # reverse resultant string
    str = str[::-1];

    return str;

# Driver code
str1 = "12";
str2 = "198111";
print(findSum(str1, str2));

# This code is contributed by mits
```

## C#

```
// C# program to find sum of two large numbers.
using System;
class GFG
{
// Function for finding sum of larger numbers
static string findSum(string str1, string str2)
{
    // Before proceeding further, make sure length
    // of str2 is larger.
    if (str1.Length > str2.Length){
        string t = str1;
        str1 = str2;
        str2 = t;
    }

    // Take an empty string for storing result
    string str = "";

    // Calculate length of both string
    int n1 = str1.Length, n2 = str2.Length;

    // Reverse both of strings
    char[] ch = str1.ToCharArray();
    Array.Reverse( ch );
    str1 = new string( ch );
    char[] ch1 = str2.ToCharArray();
    Array.Reverse( ch1 );
    str2 = new string( ch1 );

    int carry = 0;
    for (int i = 0; i < n1; i++)
    {
        // Do school mathematics, compute sum of
        // current digits and carry
        int sum = ((int)(str1[i] - '0') +
                (int)(str2[i] - '0') + carry);
        str += (char)(sum % 10 + '0');

        // Calculate carry for next step
        carry = sum/10;
    }

    // Add remaining digits of larger number
    for (int i = n1; i < n2; i++)
    {
        int sum = ((int)(str2[i] - '0') + carry);
        str += (char)(sum % 10 + '0');
        carry = sum/10;
    }

    // Add remaining carry
    if (carry > 0)
        str += (char)(carry + '0');

    // reverse resultant string
    char[] ch2 = str.ToCharArray();
    Array.Reverse( ch2 );
    str = new string( ch2 );

    return str;
}

// Driver code
static void Main()
{
    string str1 = "12";
    string str2 = "198111";
    Console.WriteLine(findSum(str1, str2));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of two large numbers.

// Function for finding sum of larger numbers
function findSum($str1, $str2)
{
    // Before proceeding further, make sure length
    // of str2 is larger.
    if (strlen($str1) > strlen($str2)) {
        $t=$str1;
        $str1=$str2;
        $str2=$t;
    }

    // Take an empty string for storing result
    $str = "";

    // Calculate length of both string
    $n1 = strlen($str1);
    $n2 = strlen($str2);

    // Reverse both of strings
    $str1 = strrev($str1);
    $str2 = strrev($str2);

    $carry = 0;
    for ($i=0; $i<$n1; $i++)
    {
        // Do school mathematics, compute sum of
        // current digits and carry
        $sum = ((ord($str1[$i])-48)+((ord($str2[$i])-48)+$carry));
        $str.=chr($sum%10 + 48);

        // Calculate carry for next step
        $carry = (int)($sum/10);
    }

    // Add remaining digits of larger number
    for ($i=$n1; $i<$n2; $i++)
    {
        $sum = ((ord($str2[$i])-48)+$carry);
        $str.=chr($sum%10 + 48);
        $carry = (int)($sum/10);
    }

    // Add remaining carry
    if ($carry)
        $str.=chr($carry+48);

    // reverse resultant string
    $str=strrev($str);

    return $str;
}

// Driver code

    $str1 = "12";
    $str2 = "198111";
    echo findSum($str1, $str2);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of
// two large numbers.

// Function for finding sum of larger numbers
function findSum(str1, str2)
{

    // Before proceeding further, make
    // sure length of str2 is larger.
    if (str1.length > str2.length)
    {
        let t = str1;
        str1 = str2;
        str2 = t;
    }

    // Take an empty String for storing result
    let str = "";

    // Calculate length of both String
    let n1 = str1.length, n2 = str2.length;

    // Reverse both of Strings
    str1 = str1.split("").reverse().join("");
    str2 = str2.split("").reverse().join("");

    let carry = 0;
    for(let i = 0; i < n1; i++)
    {

        // Do school mathematics, compute sum of
        // current digits and carry
        let sum = ((str1[i].charCodeAt(0) -
                        '0'.charCodeAt(0)) +
                   (str2[i].charCodeAt(0) -
                        '0'.charCodeAt(0)) + carry);
        str += String.fromCharCode(sum % 10 +
                        '0'.charCodeAt(0));

        // Calculate carry for next step
        carry = Math.floor(sum / 10);
    }

    // Add remaining digits of larger number
    for(let i = n1; i < n2; i++)
    {
        let sum = ((str2[i].charCodeAt(0) -
                        '0'.charCodeAt(0)) + carry);
        str += String.fromCharCode(sum % 10 +
                        '0'.charCodeAt(0));
        carry = Math.floor(sum / 10);
    }

    // Add remaining carry
    if (carry > 0)
        str += String.fromCharCode(carry +
                       '0'.charCodeAt(0));

    // reverse resultant String
    str = str.split("").reverse().join("");

    return str;
}

// Driver code
let str1 = "12";
let str2 = "198111";

document.write(findSum(str1, str2))

// This code is contributed by rag2127

</script>
```

**输出:**

```
198123
```

**优化:**
我们可以通过从头到尾遍历来避免前两个字符串反向操作。下面是优化的解决方案。

## C++

```
// C++ program to find sum of two large numbers.
#include<bits/stdc++.h>
using namespace std;

// Function for finding sum of larger numbers
string findSum(string str1, string str2)
{
    // Before proceeding further, make sure length
    // of str2 is larger.
    if (str1.length() > str2.length())
        swap(str1, str2);

    // Take an empty string for storing result
    string str = "";

    // Calculate length of both string
    int n1 = str1.length(), n2 = str2.length();
    int diff = n2 - n1;

    // Initially take carry zero
    int carry = 0;

    // Traverse from end of both strings
    for (int i=n1-1; i>=0; i--)
    {
        // Do school mathematics, compute sum of
        // current digits and carry
        int sum = ((str1[i]-'0') +
                   (str2[i+diff]-'0') +
                   carry);
        str.push_back(sum%10 + '0');
        carry = sum/10;
    }

    // Add remaining digits of str2[]
    for (int i=n2-n1-1; i>=0; i--)
    {
        int sum = ((str2[i]-'0')+carry);
        str.push_back(sum%10 + '0');
        carry = sum/10;
    }

    // Add remaining carry
    if (carry)
        str.push_back(carry+'0');

    // reverse resultant string
    reverse(str.begin(), str.end());

    return str;
}

// Driver code
int main()
{
    string str1 = "12";
    string str2 = "198111";
    cout << findSum(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of two large numbers.
import java.util.*;

class GFG{

 // Function for finding sum of larger numbers
static String findSum(String str1, String str2)
{
    // Before proceeding further, make sure length
    // of str2 is larger.
    if (str1.length() > str2.length()){
        String t = str1;
        str1 = str2;
        str2 = t;
    }

    // Take an empty String for storing result
    String str = "";

    // Calculate length of both String
    int n1 = str1.length(), n2 = str2.length();
    int diff = n2 - n1;

    // Initially take carry zero
    int carry = 0;

    // Traverse from end of both Strings
    for (int i = n1 - 1; i>=0; i--)
    {
        // Do school mathematics, compute sum of
        // current digits and carry
        int sum = ((int)(str1.charAt(i)-'0') +
            (int)(str2.charAt(i+diff)-'0') + carry);
        str += (char)(sum % 10 + '0');
        carry = sum / 10;
    }

    // Add remaining digits of str2[]
    for (int i = n2 - n1 - 1; i >= 0; i--)
    {
        int sum = ((int)(str2.charAt(i) - '0') + carry);
        str += (char)(sum % 10 + '0');
        carry = sum / 10;
    }

    // Add remaining carry
    if (carry > 0)
        str += (char)(carry + '0');

    // reverse resultant String
    return new StringBuilder(str).reverse().toString();
}

// Driver code
public static void main(String[] args)
{
    String str1 = "12";
    String str2 = "198111";
    System.out.println(findSum(str1, str2));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# python 3 program to find sum of two large numbers.

# Function for finding sum of larger numbers
def findSum(str1, str2):

    # Before proceeding further, make sure length
    # of str2 is larger.
    if len(str1)> len(str2):
        temp = str1
        str1 = str2
        str2 = temp

    # Take an empty string for storing result
    str3 = ""

    # Calculate length of both string
    n1 = len(str1)
    n2 = len(str2)
    diff = n2 - n1

    # Initially take carry zero
    carry = 0

    # Traverse from end of both strings
    for i in range(n1-1,-1,-1):

        # Do school mathematics, compute sum of
        # current digits and carry

        sum = ((ord(str1[i])-ord('0')) +
                   int((ord(str2[i+diff])-ord('0'))) + carry)

        str3 = str3+str(sum%10 )

        carry = sum//10

    # Add remaining digits of str2[]
    for i in range(n2-n1-1,-1,-1):

        sum = ((ord(str2[i])-ord('0'))+carry)
        str3 = str3+str(sum%10 )
        carry = sum//10

    # Add remaining carry
    if (carry):
        str3+str(carry+'0')

    # reverse resultant string
    str3 = str3[::-1]

    return str3

# Driver code
if __name__ == "__main__":
    str1 = "12"
    str2 = "198111"
    print(findSum(str1, str2))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to find sum of two large numbers.
using System;

class GFG{

// Function for finding sum of larger numbers
static string findSum(string str1, string str2)
{
    // Before proceeding further, make sure length
    // of str2 is larger.
    if (str1.Length > str2.Length)
    {
        string t = str1;
        str1 = str2;
        str2 = t;
    }

    // Take an empty string for storing result
    string str = "";

    // Calculate length of both string
    int n1 = str1.Length, n2 = str2.Length;
    int diff = n2 - n1;

    // Initially take carry zero
    int carry = 0;

    // Traverse from end of both strings
    for (int i = n1 - 1; i >= 0; i--)
    {
        // Do school mathematics, compute sum of
        // current digits and carry
        int sum = ((int)(str1[i] - '0') +
                (int)(str2[i + diff]-'0') + carry);
        str += (char)(sum % 10 + '0');
        carry = sum / 10;
    }

    // Add remaining digits of str2[]
    for (int i = n2 - n1 - 1; i >= 0; i--)
    {
        int sum = ((int)(str2[i] - '0') + carry);
        str += (char)(sum % 10 + '0');
        carry = sum / 10;
    }

    // Add remaining carry
    if (carry > 0)
        str += (char)(carry + '0');

    // reverse resultant string
    char[] ch2 = str.ToCharArray();
    Array.Reverse(ch2);
    return new string(ch2);
}

// Driver code
static void Main()
{
    string str1 = "12";
    string str2 = "198111";
    Console.WriteLine(findSum(str1, str2));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of two large numbers.

// Function for finding sum of larger numbers
function findSum($str1, $str2)
{
    // Before proceeding further, make
    // sure length of str2 is larger.
    if(strlen($str1)> strlen($str2))
    {
        $temp = $str1;
        $str1 = $str2;
        $str2 = $temp;
    }

    // Take an empty string for storing result
    $str3 = "";

    // Calculate length of both string
    $n1 = strlen($str1);
    $n2 = strlen($str2);
    $diff = $n2 - $n1;

    // Initially take carry zero
    $carry = 0;

    // Traverse from end of both strings
    for ($i = $n1 - 1; $i >= 0; $i--)
    {
        // Do school mathematics, compute sum 
        // of current digits and carry
        $sum = ((ord($str1[$i]) - ord('0')) +
               ((ord($str2[$i + $diff]) -
                 ord('0'))) + $carry);

        $str3 .= chr($sum % 10 + ord('0'));

        $carry = (int)($sum / 10);
    }

    // Add remaining digits of str2[]
    for ($i = $n2 - $n1 - 1; $i >= 0; $i--)
    {
        $sum = ((ord($str2[$i]) - ord('0')) + $carry);
        $str3 .= chr($sum % 10 + ord('0'));
        $carry = (int)($sum / 10);
    }

    // Add remaining carry
    if ($carry)
        $str3 .= chr($carry + ord('0'));

    // reverse resultant string
    return strrev($str3);
}

// Driver code
$str1 = "12";
$str2 = "198111";
print(findSum($str1, $str2));

// This code is contributed by mits
?>
```

**输出:**

```
198123
```

**时间复杂度:** O(n1 + n2)，其中 n1 和 n2 是表示数字的两个输入字符串的长度。

**辅助空间:** O(最大值(n1，n2))

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。