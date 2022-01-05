# 删除第一个字符串中出现在第二个字符串中的字符

> 原文:[https://www . geesforgeks . org/从第一个字符串中删除第二个字符串中存在的字符/](https://www.geeksforgeeks.org/remove-characters-from-the-first-string-which-are-present-in-the-second-string/)

**编写一个高效的 C 函数，将两个字符串作为参数，从** **第一个字符串中删除出现在** **第二个字符串(掩码字符串)中的字符。**

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/remove-character3815/1)

**算法:**假设第一个输入字符串是一个“测试字符串”，从第一个字符串中删除字符的字符串是一个“掩码”

1.  初始化:res_ind = 0 /*索引以跟踪 i/p 字符串中每个字符的处理情况*/
    ip_ind = 0 /*索引以跟踪结果字符串中每个字符的处理情况*/
2.  从 mask_str 构造计数数组。计数数组应该是:
    (我们可以在这里使用布尔数组来代替 int 计数数组，因为我们不需要计数，我们只需要知道字符是否出现在掩码字符串中)
    计数【‘a’】= 1
    计数【‘k’】= 1
    计数【‘m’】= 1
    计数【‘s’】= 1
3.  处理输入字符串中的每个字符，如果该字符的计数为 0，则只将该字符添加到结果字符串中。
    str = " Tet string "//' s '已被删除，因为' s '出现在 mask_str 中，但是我们有两个额外的字符" ng "
    IP _ ind = 11
    RES _ ind = 9
    在字符串的末尾放一个' \0 '？

**实现:**

## C++

```
// C++ program to remove duplicates, the order of
// characters is not maintained in this progress
#include <bits/stdc++.h>
#define NO_OF_CHAR 256
using namespace std;

int* getcountarray(string str2)
{
    int* count = (int*)calloc(sizeof(int), NO_OF_CHAR);

    for (int i = 0; i < str2.size(); i++)
    {
        count[str2[i]]++;
    }

    return count;
}

/* removeDirtyChars takes two
string as arguments: First
string (str1)  is the one from
where function removes dirty
characters. Second  string(str2)
is the string which contain
all dirty characters which need
to be removed  from first
string */
string removeDirtyChars(string str1, string str2)
{
    // str2 is the string
    // which is to be removed
    int* count = getcountarray(str2);
    string res;

    // ip_idx helps to keep
    // track of the first string
    int ip_idx = 0;

    while (ip_idx < str1.size())
    {
        char temp = str1[ip_idx];
        if (count[temp] == 0)
        {
            res.push_back(temp);
        }
        ip_idx++;
    }

    return res;
}

// Driver Code
int main()
{
    string str1 = "geeksforgeeks";
    string str2 = "mask";

    // Function call
    cout << removeDirtyChars(str1, str2) << endl;
}
```

## C

```
#include <stdio.h>
#include <stdlib.h>
#define NO_OF_CHARS 256

/* Returns an array of size 256 containing count
   of characters in the passed char array */
int* getCharCountArray(char* str)
{
    int* count = (int*)calloc(sizeof(int), NO_OF_CHARS);
    int i;
    for (i = 0; *(str + i); i++)
        count[*(str + i)]++;
    return count;
}

/* removeDirtyChars takes two
string as arguments: First
string (str)  is the one from
where function removes dirty
characters. Second  string is
the string which contain all
dirty characters which need to
be removed  from first string
*/
char* removeDirtyChars(char* str, char* mask_str)
{
    int* count = getCharCountArray(mask_str);
    int ip_ind = 0, res_ind = 0;
    while (*(str + ip_ind))
    {
        char temp = *(str + ip_ind);
        if (count[temp] == 0)
        {
            *(str + res_ind) = *(str + ip_ind);
            res_ind++;
        }
        ip_ind++;
    }

    /* After above step string is ngring.
      Removing extra "iittg" after string*/
    *(str + res_ind) = '\0';

    return str;
}

/* Driver code*/
int main()
{
    char str[] = "geeksforgeeks";
    char mask_str[] = "mask";
    printf("%s", removeDirtyChars(str, mask_str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove duplicates, the order of
// characters is not maintained in this program

public class GFG {
    static final int NO_OF_CHARS = 256;

    /* Returns an array of size 256 containing count
       of characters in the passed char array */
    static int[] getCharCountArray(String str)
    {
        int count[] = new int[NO_OF_CHARS];
        for (int i = 0; i < str.length(); i++)
            count[str.charAt(i)]++;

        return count;
    }

    /* removeDirtyChars takes two
    string as arguments: First
    string (str)  is the one from
    where function removes
    dirty characters. Second 
    string is the string which
    contain all dirty characters
    which need to be removed
    from first string */
    static String removeDirtyChars(String str,
                                   String mask_str)
    {
        int count[] = getCharCountArray(mask_str);
        int ip_ind = 0, res_ind = 0;

        char arr[] = str.toCharArray();

        while (ip_ind != arr.length)
        {
            char temp = arr[ip_ind];
            if (count[temp] == 0) {
                arr[res_ind] = arr[ip_ind];
                res_ind++;
            }
            ip_ind++;
        }

        str = new String(arr);

        /* After above step string is ngring.
        Removing extra "iittg" after string*/

        return str.substring(0, res_ind);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        String mask_str = "mask";
        System.out.println(removeDirtyChars(str, mask_str));
    }
}
```

## 计算机编程语言

```
# Python program to remove characters
# from first string which
# are present in the second string
NO_OF_CHARS = 256

# Utility function to convert
# from string to list

def toList(string):
    temp = []
    for x in string:
        temp.append(x)
    return temp

# Utility function to
# convert from list to string

def toString(List):
    return ''.join(List)

# Returns an array of size
# 256 containing count of characters
# in the passed char array

def getCharCountArray(string):
    count = [0] * NO_OF_CHARS
    for i in string:
        count[ord(i)] += 1
    return count

# removeDirtyChars takes two
# string as arguments: First
# string (str)  is the one
# from where function removes dirty
# characters. Second  string
# is the string which contain all
# dirty characters which need
# to be removed  from first string

def removeDirtyChars(string, mask_string):
    count = getCharCountArray(mask_string)
    ip_ind = 0
    res_ind = 0
    temp = ''
    str_list = toList(string)

    while ip_ind != len(str_list):
        temp = str_list[ip_ind]
        if count[ord(temp)] == 0:
            str_list[res_ind] = str_list[ip_ind]
            res_ind += 1
        ip_ind += 1

    # After above step string is ngring.
     # Removing extra "iittg" after string
    return toString(str_list[0:res_ind])

# Driver code
mask_string = "mask"
string = "geeksforgeeks"
print removeDirtyChars(string, mask_string)

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to remove
// duplicates, the order
// of characters is not
// maintained in this program
using System;
class GFG {
    static int NO_OF_CHARS = 256;

    /* Returns an array of size
    256 containing count of
    characters in the passed
    char array */
    static int[] getCharCountArray(String str)
    {
        int[] count = new int[NO_OF_CHARS];
        for (int i = 0; i < str.Length; i++)
            count[str[i]]++;

        return count;
    }

    /* removeDirtyChars takes two
    string as arguments: First
    string (str) is the one from
    where function removes dirty
    characters. Second string is
    the string which contain all
    dirty characters which need
    to be removed from first string */
    static String removeDirtyChars(String str,
                                   String mask_str)
    {
        int[] count = getCharCountArray(mask_str);
        int ip_ind = 0, res_ind = 0;

        char[] arr = str.ToCharArray();

        while (ip_ind != arr.Length)
        {
            char temp = arr[ip_ind];
            if (count[temp] == 0) {
                arr[res_ind] = arr[ip_ind];
                res_ind++;
            }
            ip_ind++;
        }

        str = new String(arr);

        /* After above step string
        is ngring. Removing extra
        "iittg" after string*/
        return str.Substring(0, res_ind);
    }

    // Driver Code
    public static void Main()
    {
        String str = "geeksforgeeks";
        String mask_str = "mask";
        Console.WriteLine(removeDirtyChars(str, mask_str));
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
//Javascript Implementation
let NO_OF_CHARS  = 256;
function getcountarray(str2)
{
    var count = new Array(NO_OF_CHARS).fill(0);

    for (var i = 0; i < str2.length; i++)
    {
        count[str2.charCodeAt(i)]++;
    }
    return count;
}

/* removeDirtyChars takes two
string as arguments: First
string (str1)  is the one from
where function removes dirty
characters. Second  string(str2)
is the string which contain
all dirty characters which need
to be removed  from first
string */
function removeDirtyChars(str1, str2)
{
    // str2 is the string
    // which is to be removed
    var count = getcountarray(str2);
    var res ="";

    // ip_idx helps to keep
    // track of the first string
    var ip_idx = 0;

    while (ip_idx < str1.length)
    {
        var temp = str1[ip_idx];
        if (count[temp.charCodeAt(0)] == 0)
        {
            res = res.concat(temp);
        }
        ip_idx++;
    }

    return res;
}

// Driver Code
var mask_string = "mask"
var string = "geeksforgeeks"
document.write(removeDirtyChars(string, mask_string));

// This code is contributed by shivani
</script>
```

**Output**

```
geeforgee
```