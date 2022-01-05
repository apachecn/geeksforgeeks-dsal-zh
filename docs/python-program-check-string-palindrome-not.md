# Python 程序检查字符串是否回文

> 原文:[https://www . geesforgeks . org/python-program-check-string-回文-not/](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)

给定一个字符串，编写一个 python 函数来检查它是否是回文。如果字符串的反义词与 string 相同，则称该字符串为回文。比如“雷达”是回文，但“基数”不是回文。

**示例:**

```
Input : malayalam
Output : Yes

Input : geeks
Output : No
```

**方法#1**

1.  查找字符串的反向
2.  检查反面和原件是否相同。

## 计算机编程语言

```
# function which return reverse of a string

def isPalindrome(s):
    return s == s[::-1]

# Driver code
s = "malayalam"
ans = isPalindrome(s)

if ans:
    print("Yes")
else:
    print("No")
```

**输出:**

```
Yes
```

**迭代法:**此法由 ***沙里克·拉扎*** 贡献。从开始到长度/2 运行一个循环，检查字符串的第一个字符到最后一个字符，第二个到第二个最后一个字符，以此类推。如果任何字符不匹配，字符串就不是回文。

下面是上述方法的实现:

## 计算机编程语言

```
# function to check string is
# palindrome or not
def isPalindrome(str):

    # Run loop from 0 to len/2
    for i in range(0, int(len(str)/2)):
        if str[i] != str[len(str)-i-1]:
            return False
    return True

# main function
s = "malayalam"
ans = isPalindrome(s)

if (ans):
    print("Yes")
else:
    print("No")
```

**输出:**

```
Yes
```

**使用** **内置函数反转字符串的方法:**该方法由 ***Shariq Raza*** 贡献。在此方法中，预定义功能**' '。join(reversed(string))** 用于反转字符串。

下面是上述方法的实现:

## 计算机编程语言

```
# function to check string is
# palindrome or not
def isPalindrome(s):

    # Using predefined function to
    # reverse to string print(s)
    rev = ''.join(reversed(s))

    # Checking if both string are
    # equal or not
    if (s == rev):
        return True
    return False

# main function
s = "malayalam"
ans = isPalindrome(s)

if (ans):
    print("Yes")
else:
    print("No")
```

**输出:**

```
Yes
```

**使用一个额外变量的方法:**在该方法中，用户一个接一个地获取字符串的一个字符，并将其存储在一个空变量中。存储所有字符后，用户将比较两个字符串，并检查它是否是回文。

## 计算机编程语言

```
# Python program to check
# if a string is palindrome
# or not

x = "malayalam"

w = ""
for i in x:
    w = i + w

if (x == w):
    print("Yes")
else:
    print("No")

```

**输出:**

```
Yes
```

**使用标志的方法:**在该方法中，用户在 for 循环中比较从开始到结束的每个字符，如果字符不匹配，则将改变标志的状态。然后它会检查标志的状态，并相应地打印它是否是回文。

## 计算机编程语言

```
# Python program to check
# if a string is palindrome
# or not
st = 'malayalam'
j = -1
flag = 0
for i in st:
    if i != st[j]:
      j = j - 1
      flag = 1
      break
    j = j - 1
if flag == 1:
    print("NO")
else:
    print("Yes")
```

**输出:**

```
Yes
```

**使用递归的方法**:

此方法比较字符串的第一个和最后一个元素，并将子字符串的其余部分作为对自身的递归调用。

## 蟒蛇 3

```
# Recursive function to check if a
# string is palindrome

def isPalindrome(s):

    #to change it the string is similar case
    s = s.lower()
    # length of s
    l = len(s)

    # if length is less than 2
    if l < 2:
        return True

    # If s[0] and s[l-1] are equal
    elif s[0] == s[l - 1]:

        # Call is pallindrome form substring(1,l-1)
        return isPalindrome(s[1: l - 1])

    else:
        return False

# Driver Code
s = "MalaYaLam"
ans = isPalindrome(s)

if ans:
    print("Yes")

else:
    print("No")
```

**Output**

```
Yes
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。