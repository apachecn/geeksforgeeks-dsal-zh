# 弦的左右旋转

> 原文:[https://www . geesforgeks . org/left-rotation-right-rotation-string-2/](https://www.geeksforgeeks.org/left-rotation-right-rotation-string-2/)

给定大小为 n 的字符串，编写函数对字符串执行以下操作-

1.  向左(或逆时针)旋转给定的字符串 d 个元素(其中 d <= n)
2.  向右(或顺时针)旋转给定的字符串 d 个元素(其中 d <= n)。

**示例:**

```
Input : s = "GeeksforGeeks"
        d = 2
Output : Left Rotation  : "eksforGeeksGe" 
         Right Rotation : "ksGeeksforGee"  

Input : s = "qwertyu" 
        d = 2
Output : Left rotation : "ertyuqw"
         Right rotation : "yuqwert"
```

一个**简单的解决方法**就是用一个临时的字符串做旋转。对于左旋转，首先，复制最后 n-d 个字符，然后按照临时字符串的顺序复制前 d 个字符。对于右旋转，首先复制最后 d 个字符，然后复制 n-d 个字符。

**原地旋转和 O(n)时间都可以吗？**
这个想法是基于一个[反转算法进行旋转](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)。

```
// Left rotate string s by d (Assuming d <= n)
leftRotate(s, d)
  reverse(s, 0, d-1); // Reverse substring s[0..d-1]
  reverse(s, d, n-1); // Reverse substring s[d..n-1]
  reverse(s, 0, n-1); // Reverse whole string.  

// Right rotate string s by d (Assuming d <= n)
rightRotate(s, d)

  // We can also call above reverse steps
  // with d = n-d.
  leftRotate(s, n-d)  
```

下面是上述步骤的实现:

## C++

```
// C program for Left Rotation and Right
// Rotation of a String
#include<bits/stdc++.h>
using namespace std;

// In-place rotates s towards left by d
void leftrotate(string &s, int d)
{
    reverse(s.begin(), s.begin()+d);
    reverse(s.begin()+d, s.end());
    reverse(s.begin(), s.end());
}

// In-place rotates s towards right by d
void rightrotate(string &s, int d)
{
   leftrotate(s, s.length()-d);
}

// Driver code
int main()
{
    string str1 = "GeeksforGeeks";
    leftrotate(str1, 2);
    cout << str1 << endl;

    string str2 = "GeeksforGeeks";
    rightrotate(str2, 2);
    cout << str2 << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Left Rotation and Right
// Rotation of a String
import java.util.*;
import java.io.*;

class GFG
{

    // function that rotates s towards left by d
    static String leftrotate(String str, int d)
    {
            String ans = str.substring(d) + str.substring(0, d);
            return ans;
    }

    // function that rotates s towards right by d
    static String rightrotate(String str, int d)
    {
            return leftrotate(str, str.length() - d);
    }

    // Driver code
    public static void main(String args[])
    {
            String str1 = "GeeksforGeeks";
            System.out.println(leftrotate(str1, 2));

            String str2 = "GeeksforGeeks";
            System.out.println(rightrotate(str2, 2));
    }
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 program for Left
# Rotation and Right
# Rotation of a String

# In-place rotates s towards left by d
def leftrotate(s, d):
    tmp = s[d : ] + s[0 : d]
    return tmp

# In-place rotates s
# towards right by d
def rightrotate(s, d):

   return leftrotate(s, len(s) - d)

# Driver code
if __name__=="__main__":

    str1 = "GeeksforGeeks"
    print(leftrotate(str1, 2))

    str2 = "GeeksforGeeks"
    print(rightrotate(str2, 2))

# This code is contributed by Rutvik_56
```

## C#

```
// C# program for Left Rotation and Right
// Rotation of a String
using System;

class GFG
{

    // function that rotates s towards left by d
    static String leftrotate(String str, int d)
    {
            String ans = str.Substring(d,str.Length-d) + str.Substring(0, d);
            return ans;
    }

    // function that rotates s towards right by d
    static String rightrotate(String str, int d)
    {
            return leftrotate(str, str.Length - d);
    }

    // Driver code
    public static void Main(String []args)
    {
            String str1 = "GeeksforGeeks";
            Console.WriteLine(leftrotate(str1, 2));

            String str2 = "GeeksforGeeks";
            Console.WriteLine(rightrotate(str2, 2));
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program for Left Rotation and Right
// Rotation of a String

// Function that rotates s towards left by d
function leftrotate(str, d)
{
    var ans = str.substring(d, str.length) +
              str.substring(0, d);
    return ans;
}

// Function that rotates s towards right by d
function rightrotate(str, d)
{
    return leftrotate(str, str.length - d);
}

// Driver code
var str1 = "GeeksforGeeks";
document.write(leftrotate(str1, 2) + "<br>");

var str2 = "GeeksforGeeks";
document.write(rightrotate(str2, 2) + "<br>");

// This code is contributed by rdtank

</script>
```

**输出:**

```
Left rotation:  eksforGeeksGe
Right rotation:  ksGeeksforGee                 
```

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。