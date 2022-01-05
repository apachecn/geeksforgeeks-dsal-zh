# 对字符串进行降序排序的程序

> 原文:[https://www . geesforgeks . org/program-sort-string-降序/](https://www.geeksforgeeks.org/program-sort-string-descending-order/)

给定一个字符串，按降序排序。
**例:**

```
Input : alkasingh
Output : snlkihgaa 

Input : nupursingh
Output : uusrpnnihg 

Input : geeksforgeeks
Output : ssrokkggfeeee 
```

一个**简单的解决方案**就是使用库排序功能[STD::sort()](https://www.geeksforgeeks.org/sort-c-stl/)T4】

## C++

```
// CPP program to sort a string in descending
// order using library function
#include <bits/stdc++.h>
using namespace std;

void descOrder(string s)
{
    sort(s.begin(), s.end(), greater<char>());
}

int main()
{
    string s = "geeksforgeeks";
    descOrder(s); // function call
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort a string in descending
// order using library function
import java.util.*;

class GFG
{

    static void descOrder(char[] s)
    {
        Arrays.sort(s);
        reverse(s);
    }

    static void reverse(char[] a)
    {
        int i, n = a.length;
        char t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        char[] s = "geeksforgeeks".toCharArray();
        descOrder(s); // function call
        System.out.println(String.valueOf(s));
    }
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python program to sort
# a string in descending
# order using library function

def descOrder(s):
    s.sort(reverse = True)
    str1 = ''.join(s)
    print(str1)

def main():
    s = list('geeksforgeeks')

    # function call
    descOrder(s)

if __name__=="__main__":
    main()

# This code is contributed by
# prabhat kumar singh
```

## C#

```
// C# program to sort a string in descending
// order using library function
using System;

class GFG
{

    static void descOrder(char[] s)
    {
        Array.Sort(s);
        reverse(s);
    }

    static void reverse(char[] a)
    {
        int i, n = a.Length;
        char t;
        for (i = 0; i < n / 2; i++)
        {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        char[] s = "geeksforgeeks".ToCharArray();
        descOrder(s); // function call
        Console.WriteLine(String.Join("",s));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort a string in descending
// order using library function

function descOrder($s)
{
    $s = str_split($s);
    rsort($s);
    echo implode('', $s);
}

// Driver Code
$s = "geeksforgeeks";
descOrder($s); // function call

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

      //  JavaScript program to sort
      //  a string in descending
      //  order using library function

      function descOrder(s) {
        s.sort().reverse();
        str1 = s.join("");
        document.write(str1);
      }

      var s = "geeksforgeeks";
      s = s.split("");

    // function call
      descOrder(s);

 </script>
```

**输出:**

```
 ssrokkggfeeee 
```

时间复杂度为:O(n log n)
一种**有效的方法**是首先观察总共只能有 26 个唯一字符。因此，我们可以在散列数组中存储从“a”到“z”的所有字符的出现次数。散列数组的第一个索引将代表字符“a”，第二个将代表“b”等等。最后，我们将简单地遍历散列数组，并打印从“z”到“a”的字符在输入字符串中出现的次数。
以下是上述思路的实现:

## C++

```
// C++ program to sort a string of characters
// in descending order
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// function to print string in sorted order
void sortString(string& str)
{
    // Hash array to keep count of characters.
    // Initially count of all charters is
    // initialized to zero.
    int charCount[MAX_CHAR] = { 0 };

    // Traverse string and increment
    // count of characters
    for (int i = 0; i < str.length(); i++)

        // 'a'-'a' will be 0, 'b'-'a' will be 1,
        // so for location of character in count
        // array we wil do str[i]-'a'.
        charCount[str[i] - 'a']++;

    // Traverse the hash array and print
    // characters
    for (int i = MAX_CHAR - 1; i >= 0; i--)
        for (int j = 0; j < charCount[i]; j++)
            cout << (char)('a' + i);
}

// Driver program to test above function
int main()
{
    string s = "alkasingh";
    sortString(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort a string of characters
// in descending order

class GFG
{

    static int MAX_CHAR = 26;

    // function to print string in sorted order
    static void sortString(String str)
    {

        // Hash array to keep count of characters.
        // Initially count of all charters is
        // initialized to zero.
        int charCount[] = new int[MAX_CHAR];

        // Traverse string and increment
        // count of characters
        // 'a'-'a' will be 0, 'b'-'a' will be 1,
        for (int i = 0; i < str.length(); i++)
        {

            // so for location of character in count
            // array we wil do str[i]-'a'.
            charCount[str.charAt(i) - 'a']++;
        }

        // Traverse the hash array and print
        // characters
        for (int i = MAX_CHAR - 1; i >= 0; i--)
        {
            for (int j = 0; j < charCount[i]; j++)
            {
                System.out.print((char) ('a' + i));
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "alkasingh";
        sortString(s);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to sort a string of characters
# in descending order

MAX_CHAR = 26;

# function to print string in sorted order
def sortString(str):

    # Hash array to keep count of characters.
    # Initially count of all charters is
    # initialized to zero.
    charCount = [0]*MAX_CHAR;

    # Traverse string and increment
    # count of characters
    for i in range(len(str)):

        # 'a'-'a' will be 0, 'b'-'a' will be 1,
        # so for location of character in count
        # array we wil do str[i]-'a'.
        charCount[ord(str[i]) - ord('a')]+=1;

    # Traverse the hash array and print
    # characters
    for i in range(MAX_CHAR - 1,-1, -1):
        for j in range(charCount[i]):
            print(chr(97+i),end="");

# Driver program to test above function
s = "alkasingh";
sortString(s);

# This code is contributed by Princi Singh
```

## C#

```
// C# program to sort a string of characters
// in descending order
using System;

class GFG
{
    static int MAX_CHAR = 26;

    // function to print string in sorted order
    static void sortString(String str)
    {

        // Hash array to keep count of characters.
        // Initially count of all charters is
        // initialized to zero.
        int []charCount = new int[MAX_CHAR];

        // Traverse string and increment
        // count of characters
        // 'a'-'a' will be 0, 'b'-'a' will be 1,
        for (int i = 0; i < str.Length; i++)
        {

            // so for location of character in 
            // count array we wil do str[i]-'a'.
            charCount[str[i] - 'a']++;
        }

        // Traverse the hash array and print
        // characters
        for (int i = MAX_CHAR - 1; i >= 0; i--)
        {
            for (int j = 0; j < charCount[i]; j++)
            {
                Console.Write((char) ('a' + i));
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "alkasingh";
        sortString(s);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to sort a string of characters
// in descending order
    let MAX_CHAR = 26;

    // function to print string in sorted order
    function sortString(str)
    {

        // Hash array to keep count of characters.
        // Initially count of all charters is
        // initialized to zero.
        let charCount = new Array(MAX_CHAR);
        for(let i = 0; i < charCount.length; i++)
        {
            charCount[i] = 0;
        }

        // Traverse string and increment
        // count of characters
        // 'a'-'a' will be 0, 'b'-'a' will be 1,
        for (let i = 0; i < str.length; i++)
        {

            // so for location of character in count
            // array we wil do str[i]-'a'.
            charCount[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        // Traverse the hash array and print
        // characters
        for (let i = MAX_CHAR - 1; i >= 0; i--)
        {
            for (let j = 0; j < charCount[i]; j++)
            {
                document.write(String.fromCharCode ('a'.charCodeAt(0) + i));
            }
        }
    }

    // Driver code
    let s = "alkasingh";
    sortString(s);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
snlkihgaa
```

**时间复杂度:** O( n)，其中 n 为输入字符串的长度。
**辅助空间:** O( 1)。
本文由**普拉巴特库马尔辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。