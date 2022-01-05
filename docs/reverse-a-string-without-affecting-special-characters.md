# 在不影响特殊字符的情况下反转字符串

> 原文:[https://www . geesforgeks . org/reverse-a-string-not-impact-special-characters/](https://www.geeksforgeeks.org/reverse-a-string-without-affecting-special-characters/)

给定一个包含特殊字符和字母的字符串(“A”到“Z”和“A”到“Z”)，以不影响特殊字符的方式反转该字符串。
示例:

```
Input:   str = "a,b$c"
Output:  str = "c,b$a"
Note that $ and , are not moved anywhere.  
Only subsequence "abc" is reversed

Input:   str = "Ab,c,de!{content}quot;
Output:  str = "ed,c,bA!{content}quot;
```

**简单解决方案:**
1)创建一个临时字符数组，比如 temp[]。
2)将给定数组中的字母字符复制到 temp[]。
3)使用标准[字符串反转算法](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)反转温度【】。
4)现在在单个循环中遍历输入字符串和 temp。只要输入字符串中有字母字符，就用当前字符 temp[]替换它。
**高效解:**
上述解的时间复杂度为 O(n)，但需要额外的空间，并且对一个输入字符串做两次遍历。
我们可以一次遍历反向，不需要额外的空间。下面是算法。

```
1) Let input string be 'str[]' and length of string be 'n'
2) l = 0, r = n-1
3) While l is smaller than r, do following
    a) If str[l] is not an alphabetic character, do l++
    b) Else If str[r] is not an alphabetic character, do r--
    c) Else swap str[l] and str[r]
```

下面是上述算法的实现。

## C++

```
// C++ program to reverse a string
// with special characters
#include<bits/stdc++.h>
using namespace std;

// Returns true if x is an alphabetic
// character, false otherwise
bool isAlphabet(char x)
{
    return ( (x >= 'A' && x <= 'Z') ||
            (x >= 'a' && x <= 'z') );
}

void reverse(char str[])
{
    // Initialize left and right pointers
    int r = strlen(str) - 1, l = 0;

    // Traverse string from both ends until
    // 'l' and 'r'
    while (l < r)
    {
        // Ignore special characters
        if (!isAlphabet(str[l]))
            l++;
        else if(!isAlphabet(str[r]))
            r--;

        else // Both str[l] and str[r] are not special
        {
            swap(str[l], str[r]);
            l++;
            r--;
        }
    }
}

// Driver code
int main()
{
    char str[] = "a!!!b.c.d,e'f,ghi";
    cout << "Input string: " << str << endl;
    reverse(str);
    cout << "Output string: " << str << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to illustrate how to reverse
// an array without affecting special characters.
class GFG
{
    public static void reverse(char str[])
    {
        // Initialize left and right pointers
        int r = str.length - 1, l = 0;

        // Traverse string from both ends until
        // 'l' and 'r'
        while (l < r)
        {
            // Ignore special characters
            if (!Character.isAlphabetic(str[l]))
                l++;
            else if(!Character.isAlphabetic(str[r]))
                r--;

            // Both str[l] and str[r] are not spacial
            else
            {
                char tmp = str[l];
                str[l] = str[r];
                str[r] = tmp;
                l++;
                r--;
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "a!!!b.c.d,e'f,ghi";
        char[] charArray = str.toCharArray();

        System.out.println("Input string: " + str);
                            reverse(charArray);
        String revStr = new String(charArray);

        System.out.println("Output string: " + revStr);
    }
}

// This code is contributed by panwarabhishek345
```

## 蟒蛇 3

```
def reverseSting(text):
    index = -1

    # Loop from last index until half of the index    
    for i in range(len(text)-1, int(len(text)/2), -1):

        # match character is alphabet or not        
        if text[i].isalpha():
            temp = text[i]
            while True:
                index += 1
                if text[index].isalpha():
                    text[i] = text[index]
                    text[index] = temp
                    break
    return text

# Driver code
string = "a!!!b.c.d,e'f,ghi"
print ("Input string: ", string)
string = reverseSting(list(string))
print ("Output string: ", "".join(string))

# This code is contributed by shiva9610
```

## C#

```
// C# code to illustrate how to reverse
// an array without affecting special characters.
using System;
public class GFG
{
    public static void reverse(char []str)
    {
        // Initialize left and right pointers
        int r = str.Length - 1, l = 0;

        // Traverse string from both ends until
        // 'l' and 'r'
        while (l < r)
        {
            // Ignore special characters
            if (!char.IsLetter(str[l]))
                l++;
            else if(!char.IsLetter(str[r]))
                r--;

            // Both str[l] and str[r] are not spacial
            else
            {
                char tmp = str[l];
                str[l] = str[r];
                str[r] = tmp;
                l++;
                r--;
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        String str = "a!!!b.c.d,e'f,ghi";
        char[] charArray = str.ToCharArray();

        Console.WriteLine("Input string: " + str);
                            reverse(charArray);
        String revStr = new String(charArray);

        Console.WriteLine("Output string: " + revStr);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to reverse a string
// with special characters

// Returns true if x is an alphabetic
// character, false otherwise
function isAlphabet( x)
{
    return ( (x >= 'A' && x <= 'Z') ||
             (x >= 'a' && x <= 'z') );
}
function swap(str,a,b)
{
    var c="";
    for(var i=0;i<str.length;i++)
    {
        if(i==a)
         c= c+ str[b];
         else
            if(i==b)
                c=c+str[a];
               else
               c=c+str[i];

    }
    return c;
   }

function reverse( str)
{
    // Initialize left and right pointers
    var r = str.length - 1, l = 0;

    // Traverse string from both ends until
    // 'l' and 'r'
    while (l < r)
    {
        // Ignore special characters
        if (!isAlphabet(str[l]))
            l++;
        else if(!isAlphabet(str[r]))
            r--;

        else // Both str[l] and str[r] are not spacial
        {
            str=swap(str,l, r);
            l++;
            r--;
        }
    }
    document.write("Output string: "+ str +"<br>");
}

    var str= "a!!!b.c.d,e'f,ghi";
    document.write( "Input string: " + str +"<br>");
    reverse(str);

</script>
```

**输出:**

```
Input string: a!!!b.c.d,e'f,ghi
Output string: i!!!h.g.f,e'd,cba
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息