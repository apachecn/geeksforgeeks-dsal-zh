# 不使用%运算符的 3 和 5 的倍数

> 原文:[https://www . geesforgeks . org/multiples-3-5-不使用运算符/](https://www.geeksforgeeks.org/multiples-3-5-without-using-operator/)

写一个短程序，在新的一行上打印从 1 到 n 的每个数字。

1.  对于 3 的每个倍数，打印“3 的倍数”而不是数字。
2.  对于每个 5 的倍数，打印“5 的倍数”而不是数字。
3.  对于 3 和 5 的倍数的数字，打印“3 的倍数”。5 的倍数。”而不是号码。

**例:**

```
Input  : 15 
Output : 1
         2
         Multiple of 3.
         4
         Multiple of 5.
         Multiple of 3.
         7
         8
         Multiple of 3.
         Multiple of 5.
         11
         Multiple of 3.
         13
         14
         Multiple of 3\. Multiple of 5.
```

这个想法是从 1 迭代到 n，并通过将 3 和 5 加到当前倍数来跟踪 3 和 5 的倍数。如果当前数字与倍数匹配，我们会相应地更新输出。

## C++

```
// C++ program to print multiples
// of 3 and 5 without using % operator.
#include <iostream>
using namespace std;

void findMultiples(int n)
{
    int a = 3; // To keep track of multiples of 3
    int b = 5; // To keep track of multiples of 5
    for (int i = 1; i <= n; i++)
    {
        string s = "";

        // Found multiple of 3
        if (i == a)
        {
            a = a + 3; // Update next multiple of 3
            s = s + "Multiple of 3\. ";
        }

        // Found multiple of 5
        if (i == b)
        {
            b = b + 5; // Update next multiple of 5
            s = s + "Multiple of 5.";
        }

        if (s == "")
            cout << (i) << endl;
        else
        cout << (s) << endl;
    }
}

// Driver Code
int main()
{
    findMultiples(20);

    return 0;
}

// This code is contributed
// by Sach_Code
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print multiples of 3 and
// 5 without using % operator.
import java.io.*;

class GFG
{
    static void findMultiples(int n)
    {
        int a = 3;  // To keep track of multiples of 3
        int b = 5;  // To keep track of multiples of 5
        for (int i=1; i<=n; i++)
        {
            String s = "";

            // Found multiple of 3
            if (i==a)
            {
                a = a + 3;  // Update next multiple of 3
                s = s + "Multiple of 3\. ";
            }

            // Found multiple of 5
            if (i==b)
            {
                b = b+5;  // Update next multiple of 5
                s = s + "Multiple of 5.";
            }

            if (s == "")
                System.out.println(i);
            else  System.out.println(s);
        }
    }

    public static void main (String[] args)
    {
        findMultiples(20);
    }
}
```

## C#

```
// C# program to print multiples of 3 and
// 5 without using % operator.
using System;

public class GFG {

    static void findMultiples(int n)
    {

        // To keep track of multiples of 3
        int a = 3;

        // To keep track of multiples of 5
        int b = 5;
        for (int i = 1; i <= n; i++)
        {
            String s = "";

            // Found multiple of 3
            if (i == a)
            {

                // Update next multiple of 3
                a = a + 3;
                s = s + "Multiple of 3\. ";
            }

            // Found multiple of 5
            if (i == b)
            {

                // Update next multiple of 5
                b = b + 5;
                s = s + "Multiple of 5.";
            }

            if (s == "")
                Console.WriteLine(i);
            else
                Console.WriteLine(s);
        }
    }

    // Driver code
    public static void Main ()
    {
        findMultiples(20);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print multiples
// of 3 and 5 without using % operator.

function findMultiples($n)
{
    $a = 3; // To keep track of multiples of 3
    $b = 5; // To keep track of multiples of 5
    for ($i = 1; $i <= $n; $i++)
    {
        $s = "";

        // Found multiple of 3
        if ($i == $a)
        {
            $a = $a + 3; // Update next multiple of 3
            $s = $s . "Multiple of 3\. ";
        }

        // Found multiple of 5
        if ($i == $b)
        {
            $b = $b + 5; // Update next multiple of 5
            $s = $s . "Multiple of 5.";
        }

        if ($s == "")
            echo ($i). "\n";
        else
            echo ($s). "\n";
    }
}

// Driver Code
findMultiples(20);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    function findMultiples(n)
    {
        let a = 3;  // To keep track of multiples of 3
        let b = 5;  // To keep track of multiples of 5
        for (let i=1; i<=n; i++)
        {
            let s = "";

            // Found multiple of 3
            if (i==a)
            {
                a = a + 3;  // Update next multiple of 3
                s = s + "Multiple of 3\. ";
            }

            // Found multiple of 5
            if (i==b)
            {
                b = b+5;  // Update next multiple of 5
                s = s + "Multiple of 5.";
            }

            if (s == "") {
                document.write(i);
                document.write("<br />");
             }
            else {
                document.write(s);
                document.write("<br />");
            }
        }
    }

// Driver Code
    findMultiples(20);

   // This code is contributed by susmitakundugoaldanga.
</script>
```

## 蟒蛇 3

```
# Python 3 program to print multiples
# of 3 and 5 without using % operator.

def findMultiples(n):
    a = 3 # To keep track of multiples of 3
    b = 5 # To keep track of multiples of 5
    for i in range(1,n+1):
        s = ""

        # Found multiple of 3
        if (i == a):
            a = a + 3 # Update next multiple of 3
            s = s + "Multiple of 3\. "

        # Found multiple of 5
        if (i == b):
            b = b + 5 # Update next multiple of 5
            s = s + "Multiple of 5."
        if (s == ""):
            print(i)
        else:
            print(s) 

# Driver Code
if __name__ == '__main__':
    findMultiples(20)
```

**输出:**

```
1
2
Multiple of 3\. 
4
Multiple of 5.
Multiple of 3\. 
7
8
Multiple of 3\. 
Multiple of 5.
11
Multiple of 3\. 
13
14
Multiple of 3\. Multiple of 5.
16
17
Multiple of 3\. 
19
Multiple of 5.
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)
本文由**尼米什·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。