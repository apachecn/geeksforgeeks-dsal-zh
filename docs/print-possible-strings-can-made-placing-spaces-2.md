# 打印所有可能的字符串，这些字符串可以通过放置空格

来制作

> 原文:[https://www . geesforgeks . org/print-可能-strings-can-make-plating-spaces-2/](https://www.geeksforgeeks.org/print-possible-strings-can-made-placing-spaces-2/)

给定一个字符串，您需要打印所有可能的字符串，可以通过在它们之间放置空格(零或一)来实现

**示例:**

```
Input :  str[] = "ABC"
Output : ABC
         AB C
         A BC
         A B C

Input : str[] = "ABCD"
Output : ABCD
         A BCD
         AB CD
         A B CD
         ABC D
         A BC D
         AB C D
         A B C D
```

如果我们仔细看一下，可以发现这个问题归结为[功率设置问题](https://www.geeksforgeeks.org/power-set/)。我们基本上需要生成所有子集，其中每个元素都是不同的空间。

## C++

```
// C++ program to print all strings that can be
// made by placing spaces
#include <bits/stdc++.h>
using namespace std;

void printSubsequences(string str)
{
    int n = str.length();
    unsigned int opsize = pow(2, n - 1);

    for (int counter = 0; counter < opsize; counter++) {
        for (int j = 0; j < n; j++) {

            cout << str[j];
            if (counter & (1 << j))
                cout << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    string str = "ABC";
    printSubsequences(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all strings that can be
// made by placing spaces
import java.util.*;
class GFG
{
static void printSubsequences(String s)
{
    char[] str= s.toCharArray();
    int n = str.length;
    int opsize = (int)(Math.pow(2, n - 1));

    for (int counter = 0; counter < opsize; counter++) {
        for (int j = 0; j < n; j++) {

            System.out.print(str[j]);
            if ((counter & (1 << j)) > 0)
                System.out.print(" ");
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "AB";
    printSubsequences(str);
}
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python 3 program to print all strings 
# that can be made by placing spaces
from math import pow

def printSubsequences(str):
    n = len(str)
    opsize = int(pow(2, n - 1))

    for counter in range(opsize):
        for j in range(n):
            print(str[j], end = "")
            if (counter & (1 << j)):
                print(" ", end = "")

        print("\n", end = "")

# Driver code
if __name__ == '__main__':
    str = "ABC"
    printSubsequences(str)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print all strings
// that can be made by placing spaces
using System;

class GFG {

    // Function to print all subsequences
    static void printSubsequences(String s)
    {
        char[] str= s.ToCharArray();
        int n = str.Length;
        int opsize = (int)(Math.Pow(2, n - 1));

        for (int counter = 0; counter < opsize;
                                     counter++) 
        {
            for (int j = 0; j < n; j++) 
            {
                Console.Write(str[j]);

                if ((counter & (1 << j)) > 0)
                    Console.Write(" ");
            }
            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main()
    {
        String str = "ABC";
        printSubsequences(str);
    }
}

// This code is contributed by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print 
// all strings that can be
// made by placing spaces

function printSubsequences($str)
{
    $n = strlen($str);
    $opsize = pow(2, $n - 1);

    for ($counter = 0; 
         $counter < $opsize; 
         $counter++) 
    {
        for ($j = 0; $j < $n; $j++) 
        {
            echo $str[$j];
            if ($counter & (1 << $j))
                echo " ";
        }
        echo "\n";
    }
}

// Driver code
$str = "ABC";
printSubsequences($str);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to print all strings
// that can be made by placing spaces

// Function to print all subsequences
function printSubsequences(s)
{
    let str= s.split('');
    let n = str.length;
    let opsize = Math.pow(2, n - 1);

    for(let counter = 0; counter < opsize; counter++) 
    {
        for(let j = 0; j < n; j++) 
        {
            document.write(str[j]);

            if ((counter & (1 << j)) > 0)
                document.write(" ");
        }
        document.write("</br>");
    }
}

// Driver code
let str = "ABC";
printSubsequences(str);

// This code is contributed by rameshtravel07
</script>
```

**输出:**

```
ABC
A BC
AB C
A B C
```

问于:[亚马逊](https://practice.geeksforgeeks.org/company/Amazon/)
本文由**杰贝辛和忍者供稿。**

如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。