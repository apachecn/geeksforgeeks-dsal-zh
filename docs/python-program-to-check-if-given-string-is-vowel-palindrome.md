# Python 程序检查给定字符串是否是元音回文

> 原文:[https://www . geesforgeks . org/python-program-to-check-if-given-string-is-元音-回文/](https://www.geeksforgeeks.org/python-program-to-check-if-given-string-is-vowel-palindrome/)

给定一个字符串(可能包含元音和辅音字母)，去掉所有辅音，然后检查结果字符串是否是回文。

**示例:**

```
Input :  abcuhuvmnba
Output : YES
Explanation :
The consonants in the string "abcuhuvmnba"
are removed. Now the string becomes "auua".

Input : xayzuezyax
Output : NO

Input : bkldhgcj
Output : -1

```

**方法:**
去掉字符串中所有的辅音。检查元音串是否是回文。如果是回文打印是，否则打印否。如果字符串不包含元音，则打印-1。

下面是 Python 实现:

```
# Python program to check if given 
# string is vowel Palindrome

# Function to check if a given string is a vowel
def vowel(c):

    # creating a list of vowels
    v = list("aeiou")

    # if the character is a vowel return True
    if c in v: return True
    return False

# Function to check if a vowel
# string is palindrome
def palindrome(s):

    # create a empty list
    v = []

    # append all vowels into the list
    for i in s:
        if vowel(i):v.append(i)

    # if the length of the vowel
    # string is 0 then print -1
    if len(v)== 0: print("-1")

    # else check if it is a palindrome
    else:
        # create a reversed string
        x = v[::-1]

        # initialize a flag
        f = 1
        for i in range(len(x)):

            # if the characters are not the same 
            if x[i]!= v[i]:

                # set the flag to 0
                f = 0
                break

        if f == 1: print("YES")
        else: print("NO")

# Driver Code
s = 'abcuhuvmnba'

# calling the main function
palindrome(s.strip())
```

**Output:**

```
YES

```