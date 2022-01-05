# Python 中包含不常见字符的串联字符串

> 原文:[https://www . geeksforgeeks . org/串接-字符串-不常见字符-python/](https://www.geeksforgeeks.org/concatenated-string-uncommon-characters-python/)

给出两个字符串，您必须修改第一个字符串，这样第二个字符串的所有常见字符都必须删除，第二个字符串的不常见字符必须与第一个字符串的不常见字符连接。

**例:**

```
Input : S1 = "aacdb"
        S2 = "gafd"
Output : "cbgf"

Input : S1 = "abcs";
        S2 = "cxzca";
Output : "bsxz"

```

此问题已有解决方案请参考[两串不常见字符的串接串](https://www.geeksforgeeks.org/concatenated-string-uncommon-characters-two-strings/)链接。我们可以使用[设置](https://www.geeksforgeeks.org/sets-in-python/)和[列表理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)在 Python 中快速解决这个问题。方法很简单，

1.  Convert both strings into a collection so that they can only have unique characters. Now take the intersection of the two sets and get the common characters of the two strings.
2.  Now separate out the uncommon characters in each string and connect them.

```
# Function to concatenated string with uncommon 
# characters of two strings 

def uncommonConcat(str1, str2): 

    # convert both strings into set 
    set1 = set(str1) 
    set2 = set(str2) 

    # take intersection of two sets to get list of 
    # common characters 
    common = list(set1 & set2) 

    # separate out characters in each string 
    # which are not common in both strings 
    result = [ch for ch in str1 if ch not in common] + [ch for ch in str2 if ch not in common] 

    # join each character without space to get 
    # final string 
    print( ''.join(result) )

# Driver program 
if __name__ == "__main__": 
    str1 = 'aacdb'
    str2 = 'gafd'
    uncommonConcat(str1,str2) 
```

输出:

```
cbgf

```