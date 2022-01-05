# Python 程序检查字符串是否相互旋转

> 原文:[https://www . geesforgeks . org/python-program-to-check-string-if-rotations-other-or-not/](https://www.geeksforgeeks.org/python-program-to-check-if-strings-are-rotations-of-each-other-or-not/)

给定一个字符串 s1 和一个字符串 s2，写一个片段来说明 s2 是否是 s1 的旋转？
(如给定 s1 = ABCD，s2 = CDAB，返回真，给定 s1 = ABCD，s2 = ACBD，返回假)

 **算法:**旋转(str1，str2)

```
    1\. Create a temp string and store concatenation of str1 to
       str1 in temp.
                          temp = str1.str1
    2\. If str2 is a substring of temp then str1 and str2 are 
       rotations of each other.

    Example:                 
                     str1 = "ABACD"
                     str2 = "CDABA"

     temp = str1.str1 = "ABACDABACD"
     Since str2 is a substring of temp, str1 and str2 are 
     rotations of each other.

```

## 计算机编程语言

```

# Python program to check if strings are rotations of
# each other or not

# Function checks if passed strings (str1 and str2)
# are rotations of each other
def areRotations(string1, string2):
    size1 = len(string1)
    size2 = len(string2)
    temp = ''

    # Check if sizes of two strings are same
    if size1 != size2:
        return 0

    # Create a temp string with value str1.str1
    temp = string1 + string1

    # Now check if str2 is a substring of temp
    # string.count returns the number of occurrences of
    # the second string in temp
    if (temp.count(string2)> 0):
        return 1
    else:
        return 0

# Driver program to test the above function
string1 = "AACD"
string2 = "ACDA"

if areRotations(string1, string2):
    print "Strings are rotations of each other"
else:
    print "Strings are not rotations of each other"

# This code is contributed by Bhavya Jain
```

**Output:**

```
Strings are rotations of each other
```

**使用的库函数:**
strtr:
strtr 在字符串中查找子字符串。
原型:char * strtr(const char * S1，const char * S2)；
见[http://www.lix.polytechnique.fr/Labo/Leo.liberti/public/computing/Prog/C/C/MAN/strtr . htm](http://www.lix.polytechnique.fr/Labo/Leo.Liberti/public/computing/prog/c/C/MAN/strstr.htm)了解更多详情

strcat:
strcat 串联两个字符串
原型:char *strcat(char *dest，const char * src)；
见[http://www.lix.polytechnique.fr/Labo/Leo.更多详情请访问](http://www.lix.polytechnique.fr/Labo/Leo.Liberti/public/computing/prog/c/C/MAN/strcat.htm)

**时间复杂度:**这个问题的时间复杂度取决于 strstr 函数的实现。
如果使用 KMP 匹配器实现 strstr，那么上述程序的复杂度为(-)(n1 + n2)，其中 n1 和 n2 是字符串的长度。KMP 匹配器花费(-)(n)时间在长度为 n 的字符串中找到子字符串，其中假设子字符串的长度小于该字符串。
详情请参考 [A 程序查看琴弦是否相互旋转](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)的完整文章！