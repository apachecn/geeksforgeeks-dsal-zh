# 句子回文(去除空格、圆点后的回文，..等)

> 原文:[https://www . geesforgeks . org/句子-回文-回文-删除-空格-圆点-etc/](https://www.geeksforgeeks.org/sentence-palindrome-palindrome-removing-spaces-dots-etc/)

写一个程序来检查一个句子是否是回文。可以忽略空格等字符，将句子视为回文。
示例:

```
Input : str = "Too hot to hoot."
Output : Sentence is palindrome.

Input : str = "Abc def ghi jklm."
Output : Sentence is not palindrome.
```

请注意，两个单词之间可能有多个空格和/或点。

要找出一个句子是否是[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)，从左到右比较每个字符。如果它们相等，进行比较，直到字符串的左边和右边相等，或者右边小于左边。请记住忽略字符串中的空格和其他字符。

## C++

```
// CPP program to find if a sentence is
// palindrome
#include <bits/stdc++.h>
using namespace std;

// To check sentence is palindrome or not
bool sentencePalindrome(string str)
{
    int l = 0, h = str.length() - 1;

    // Lowercase string
    for (int i = 0; i <= h; i++)
        str[i] = tolower(str[i]);

    // Compares character until they are equal
    while (l <= h) {

        // If there is another symbol in left
        // of sentence
        if (!(str[l] >= 'a' && str[l] <= 'z'))
            l++;

        // If there is another symbol in right
        // of sentence
        else if (!(str[h] >= 'a' && str[h] <= 'z'))
            h--;

        // If characters are equal
        else if (str[l] == str[h])
            l++, h--;

        // If characters are not equal then
        // sentence is not palindrome
        else
            return false;
    }

    // Returns true if sentence is palindrome
    return true;
}

// Driver program to test sentencePalindrome()
int main()
{
    string str = "Too hot to hoot.";

    if (sentencePalindrome(str))
        cout << "Sentence is palindrome.";
    else
        cout << "Sentence is not palindrome.";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a sentence is
// palindrome
public class GFG
{
    // To check sentence is palindrome or not
    static boolean sentencePalindrome(String str)
    {   
        int l = 0;
        int h = str.length()-1;

        // Lowercase string
        str = str.toLowerCase();

        // Compares character until they are equal
        while(l <= h)
        {

            char getAtl = str.charAt(l);
            char getAth = str.charAt(h);

            // If there is another symbol in left
            // of sentence
            if (!(getAtl >= 'a' && getAtl <= 'z'))
                l++;

            // If there is another symbol in right
            // of sentence
            else if(!(getAth >= 'a' && getAth <= 'z'))
                h--;

            // If characters are equal
            else if( getAtl == getAth)
            {
                l++;
                h--;
            }

            // If characters are not equal then
            // sentence is not palindrome
            else
                return false;
        }

        // Returns true if sentence is palindrome
        return true;   
    }

    // Driver program to test sentencePallindrome()
    public static void main(String[] args)
    {
        String str = "Too hot to hoot.";
        if( sentencePalindrome(str))
          System.out.println("Sentence is palindrome");
        else
          System.out.println("Sentence is not" + " " +
                                         "palindrome");
    }
}

//This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to find if a sentence is
# palindrome
# To check sentence is palindrome or not
def sentencePalindrome(s):
    l, h = 0, len(s) - 1

    # Lowercase string
    s = s.lower()

    # Compares character until they are equal
    while (l <= h):

        # If there is another symbol in left
        # of sentence
        if (not(s[l] >= 'a' and s[l] <= 'z')):
            l += 1

        # If there is another symbol in right
        # of sentence
        elif (not(s[h] >= 'a' and s[h] <= 'z')):
            h -= 1

        # If characters are equal
        elif (s[l] == s[h]):
            l += 1
            h -= 1

        # If characters are not equal then
        # sentence is not palindrome
        else:
            return False
    # Returns true if sentence is palindrome
    return True

# Driver program to test sentencePalindrome()
s = "Too hot to hoot."
if (sentencePalindrome(s)):
    print "Sentence is palindrome."
else:
    print "Sentence is not palindrome."

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find if a
// sentence is palindrome
using System;

public class GFG
{

    // To check sentence is
    // palindrome or not
    static bool sentencePalindrome(String str)
    {
        int l = 0;
        int h = str.Length - 1;

        // Lowercase string
        str = str.ToLower();

        // Compares character until
        // they are equal
        while(l <= h)
        {

            char getAtl = str[l];
            char getAth = str[h];

            // If there is another symbol
            // in left of sentence
            if (!(getAtl >= 'a' &&
                  getAtl <= 'z'))
                l++;

            // If there is another symbol 
            // in right of sentence
            else if(! (getAth >= 'a' &&
                       getAth <= 'z'))
                h--;

            // If characters are equal
            else if( getAtl == getAth)
            {
                l++;
                h--;
            }

            // If characters are not equal then
            // sentence is not palindrome
            else
                return false;
        }

        // Returns true if sentence
        // is palindrome
        return true;
    }

    // Driver Code
    public static void Main()
    {
        String str = "Too hot to hoot.";
        if( sentencePalindrome(str))
        Console.Write("Sentence is palindrome");
        else
        Console.Write("Sentence is not" + " " +
                                     "palindrome");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a sentence is
// palindrome

// To check sentence is palindrome or not
function sentencePalindrome($str)
{
    $l = 0;
    $h = strlen($str)-1;

    // Lowercase string
    for ($i = 0; $i < $h; $i++)
        $str[$i] = strtolower($str[$i]);

    // Compares character until they are equal
    while ($l <= $h) {

        // If there is another symbol in left
        // of sentence
        if (!($str[$l] >= 'a' && $str[$l] <= 'z'))
            $l++;

        // If there is another symbol in right
        // of sentence
        else if (!($str[$h] >= 'a' && $str[$h] <= 'z'))
            $h--;

        // If characters are equal
        else if ($str[$l] == $str[$h])
        {
             $l++;
            $h--;
        }

        // If characters are not equal then
        // sentence is not palindrome
        else
            return false;
    }

    // Returns true if sentence is palindrome
    return true;
}

// Driver program to test sentencePalindrome()

$str = "Too hot to hoot.";

if (sentencePalindrome($str))
    echo "Sentence is palindrome.";
else
    echo "Sentence is not palindrome.";

return 0;
?>
```

## java 描述语言

```
<script>
// Javascript program to find if a sentence is
// palindrome

    // To check sentence is palindrome or not
    function sentencePalindrome(str)
    {
        let l = 0;
        let h = str.length-1;

        // Lowercase string
        str = str.toLowerCase();

        // Compares character until they are equal
        while(l <= h)
        {

            let getAtl = str[l];
            let getAth = str[h];

            // If there is another symbol in left
            // of sentence
            if (!(getAtl >= 'a' && getAtl <= 'z'))
                l++;

            // If there is another symbol in right
            // of sentence
            else if(!(getAth >= 'a' && getAth <= 'z'))
                h--;

            // If characters are equal
            else if( getAtl == getAth)
            {
                l++;
                h--;
            }

            // If characters are not equal then
            // sentence is not palindrome
            else
                return false;
        }

        // Returns true if sentence is palindrome
        return true;  
    }

    // Driver program to test sentencePallindrome()
    let str = "Too hot to hoot.";
    if( sentencePalindrome(str))
        document.write("Sentence is palindrome");
    else
        document.write("Sentence is not" + " " +
                                         "palindrome");

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Sentence is palindrome.
```

***时间复杂度:** O(N)其中 N 是句子的长度*
***空间复杂度:** O(1)*

本文由 [**核素**](https://www.facebook.com/nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。