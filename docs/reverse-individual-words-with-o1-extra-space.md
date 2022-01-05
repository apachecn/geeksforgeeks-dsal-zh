# 用 O(1)个多余的空格将单个单词反过来

> 原文:[https://www . geesforgeks . org/reverse-personal-word-with-O1-extra-space/](https://www.geeksforgeeks.org/reverse-individual-words-with-o1-extra-space/)

给定一个字符串 **str** ，任务是反转所有的单个单词。

**示例:**

> **输入:**str = " Hello World "
> T3】输出: olleH dlroW
> 
> **输入:** str = "极客换极客"
> T3】输出:斯基格罗夫斯基格

**方法:**上述问题的解决方案已经在[这篇](https://www.geeksforgeeks.org/reverse-individual-words/)帖子中讨论过了。它的时间复杂度为 O(n)，并且使用 O(n)个额外空间。在这篇文章中，我们将讨论一个使用 O(1)额外空间的解决方案。

*   遍历字符串，直到我们遇到一个空格。
*   遇到空格后，我们使用两个变量“开始”和“结束”，分别指向单词的第一个和最后一个字符，并反转该特定单词。
*   重复以上步骤，直到最后一个单词。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the string after
// reversing the individual words
string reverseWords(string str)
{

    // Pointer to the first character
    // of the first word
    int start = 0;
    for (int i = 0; i <= str.size(); i++) {

        // If the current word has ended
        if (str[i] == ' ' || i == str.size()) {

            // Pointer to the last character
            // of the current word
            int end = i - 1;

            // Reverse the current word
            while (start < end) {
                swap(str[start], str[end]);
                start++;
                end--;
            }

            // Pointer to the first character
            // of the next word
            start = i + 1;
        }
    }

    return str;
}

// Driver code
int main()
{
    string str = "Geeks for Geeks";

    cout << reverseWords(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static String swap(String str, int i, int j)
    {
        StringBuilder sb = new StringBuilder(str);
        sb.setCharAt(i, str.charAt(j));
        sb.setCharAt(j, str.charAt(i));
        return sb.toString();
    }

    // Function to return the string after
    // reversing the individual words
    static String reverseWords(String str)
    {

        // Pointer to the first character
        // of the first word
        int start = 0;
        for (int i = 0; i < str.length(); i++)
        {

            // If the current word has ended
            if (str.charAt(i) == ' ' ||
                    i == str.length()-1 )
            {

                // Pointer to the last character
                // of the current word
                int end;
                if (i == str.length()-1)
                    end = i ;
                else
                    end = i - 1 ;

                // Reverse the current word
                while (start < end)
                {
                    str = swap(str,start,end) ;
                    start++;
                    end--;
                }

                // Pointer to the first character
                // of the next word
                start = i + 1;
            }
        }

        return str ;
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "Geeks for Geeks";

        System.out.println(reverseWords(str));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the after
# reversing the individual words
def reverseWords(Str):

    # Pointer to the first character
    # of the first word

    start = 0
    for i in range(len(Str)):
        # If the current word has ended
        if (Str[i] == ' ' or i == len(Str)-1):

            # Pointer to the last character
            # of the current word
            end = i - 1
            if(i == len(Str)-1):
                end = i

            # Reverse the current word
            while (start < end):
                Str[start], Str[end]=Str[end],Str[start]
                start+=1
                end-=1

            # Pointer to the first character
            # of the next word
            start = i + 1

    return "".join(Str)

# Driver code
Str = "Geeks for Geeks"
Str=[i for i in Str]

print(reverseWords(Str))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the string after
    // reversing the individual words
    // Function to return the string after
    // reversing the individual words
    static String reverseWords(String str)
    {

        // Pointer to the first character
        // of the first word
        int start = 0;
        for (int i = 0; i < str.Length; i++)
        {

            // If the current word has ended
            if (str[i] == ' ' ||
                    i == str.Length-1 )
            {

                // Pointer to the last character
                // of the current word
                int end;
                if (i == str.Length-1)
                    end = i ;
                else
                    end = i - 1 ;

                // Reverse the current word
                while (start < end)
                {
                    str = swap(str,start,end) ;
                    start++;
                    end--;
                }

                // Pointer to the first character
                // of the next word
                start = i + 1;
            }
        }

        return str ;
    }

    static String swap(String str, int i, int j)
    {
        char []ch = str.ToCharArray();
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return String.Join("",ch);
    }

    // Driver code
    public static void Main(String []args)
    {
        String str = "Geeks for Geeks";

        Console.WriteLine(reverseWords(str));
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
function swap(str, i, j)
{
    let sb = str.split("");
    sb[i] = str[j];
    sb[j] = str[i];
    return sb.join("");
}

// Function to return the string after
// reversing the individual words
function reverseWords(str)
{

    // Pointer to the first character
    // of the first word
    let start = 0;
    for(let i = 0; i < str.length; i++)
    {

        // If the current word has ended
        if (str[i] == ' ' ||
                 i == str.length-1 )
        {

            // Pointer to the last character
            // of the current word
            let end;
            if (i == str.length-1)
                end = i ;
            else
                end = i - 1 ;

            // Reverse the current word
            while (start < end)
            {
                str = swap(str, start, end);
                start++;
                end--;
            }

            // Pointer to the first character
            // of the next word
            start = i + 1;
        }
    }
    return str;
}

// Driver code
let  str = "Geeks for Geeks";
document.write(reverseWords(str));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
skeeG rof skeeG
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)