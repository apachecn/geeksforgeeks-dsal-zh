# Python 程序，使用给定字符串中的集合计算元音数量

> 原文:[https://www . geesforgeks . org/python-program-count-number-元音-使用-set-给定-string/](https://www.geeksforgeeks.org/python-program-count-number-vowels-using-sets-given-string/)

给定一个字符串，使用 set 计算给定字符串中元音的数量。

**先决条件:**[Python 中的集合](https://www.geeksforgeeks.org/sets-in-python/)

示例:

```
Input : GeeksforGeeks
Output : No. of vowels : 5

Input : Hello World
Output : No. of vowels :  3

```

**进场:**
1。使用 set()创建一组元音，并将计数变量初始化为 0。
2。遍历字符串中的字母，并检查字符串中的字母是否出现在设置元音中。
3。如果存在，元音计数会增加。

下面是上述方法的实现:

```
# Python3 code to count vowel in 
# a string using set

# Function to count vowel
def vowel_count(str):

    # Initializing count variable to 0
    count = 0

    # Creating a set of vowels
    vowel = set("aeiouAEIOU")

    # Loop to traverse the alphabet
    # in the given string
    for alphabet in str:

        # If alphabet is present
        # in set vowel
        if alphabet in vowel:
            count = count + 1

    print("No. of vowels :", count)

# Driver code 
str = "GeeksforGeeks"

# Function Call
vowel_count(str)
```

输出:

```
No. of vowels : 5

```