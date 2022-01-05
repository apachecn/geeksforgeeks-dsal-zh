# Python |切换大小写相同的单词中的字符

> 原文:[https://www . geesforgeks . org/python-toggle-in-characters-in-words-同名/](https://www.geeksforgeeks.org/python-toggle-characters-in-words-having-same-case/)

给定一个字符串，切换那些所有字符都是相同大小写的单词的字符。

**示例:**

> **输入:** Geeks for Geeks
> **输出:** Geeks for Geeks
> **解释:**该字符串包含三个单词“Geeks”、“FOR”、“Geeks”，其中“FOR”一词包含其所有字符作为小写，因此，切换该词的大小写。按原样打印剩余字符。
> 
> **输入:**HELLO WORLD
> T3】输出: hello WORLD

**简单方法:**
分别考虑字符串中的每个单词。设置两个标志，一个检查字符的所有大小写是否相同，另一个检查字符是大写还是小写。

```
if all the characters are in the same case 
    if all the characters are lower case 
       then convert into upper case
    else convert into lower case
else print the same word
```

下面是实现:

```
# Python program to toggle character in 
# a string only with same case

# Function to toggle case 
def toggle(s):

    word_list = s.split()

    # traverse through each word of the string
    for word in word_list:

        # initially assume all the characters in word
        # are in the same case and set the flag to 1
        flag = 1

        # check the case of the first
        # character in the word
        if word[0].islower():

            # if the case is lower set the r value to 1
            r = 1

            # traverse through the remaining 
            # characters in the word
            for j in word:

                # if any of the characters are in upper case
                if j.isupper():

                    # then set the flag to 0
                    flag = 0
                    break

        else:
            # if the case is upper 
            # set the r value to 1
            r = 0

            # traverse through the remaining
            # characters in the word
            for j in word:

                # if any of the characters are in lower case
                if j.islower():

                    # then set the flag to 0
                    flag = 0
                    break

        # if the flag is 0 then print the word as it is     
        if flag == 0: print(word, end =" ")

        else:
            # if the word is in lower case 
            # then print the word in upper case
            if r == 1: print(word.upper(), end =" ")

            # if the word is in upper case 
            # then print the word in lower case
            else: print(word.lower(), end =" ")

# driver code
s = 'Geeks for Geeks'
toggle(s)
```

**Output:**

```
Geeks FOR Geeks

```

**使用库函数:**
我们也可以使用直接库函数来检查单个[单词是低还是高。](https://www.geeksforgeeks.org/isupper-islower-lower-upper-python-applications/)

```
# Python program to toggle character in 
# a string only with same case

# Function to toggle case 
def toggle(s):

    word_list = s.split()

    # traverse through each word of the string
    for word in word_list:

        if word.islower() :
            print(word.upper(), end =" ")
        elif word.isupper() :
            print(word.lower(), end =" ")
        else :
            print(word, end =" ")

# driver code
s = 'Geeks for Geeks'
toggle(s)
```

**Output:**

```
Geeks FOR Geeks

```