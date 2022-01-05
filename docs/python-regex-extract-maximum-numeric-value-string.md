# Python Regex 从字符串中提取最大数值

> 原文:[https://www . geesforgeks . org/python-regex-extract-maximum-numeric-value-string/](https://www.geeksforgeeks.org/python-regex-extract-maximum-numeric-value-string/)

给定一个字母数字字符串，从该字符串中提取最大数值。字母只会用小写字母。

示例:

```
Input : 100klh564abc365bg
Output : 564
Maximum numeric value among 100, 564 
and 365 is 564.

Input : abchsd0sdhs
Output : 0

```

此问题已有解决方案，请参考[从给定字符串中提取最大数值|设置 1(一般方法)](https://www.geeksforgeeks.org/extract-maximum-numeric-value-given-string/)链接。我们将使用 [Regex](https://www.geeksforgeeks.org/regular-expression-python-examples-set-1/) 在 python 中快速解决这个问题。方法很简单，

1.  Use the [re. find all (expression, string)](https://www.geeksforgeeks.org/regular-expressions-python-set-1-search-match-find/) method to find a list of all integers separated by lowercase characters in the string.
2.  Convert each number in the form of a string into a decimal number, and then find its maximum value.

```
# Function to extract maximum numeric value from 
# a given string
import re

def extractMax(input):

     # get a list of all numbers separated by 
     # lower case characters 
     # \d+ is a regular expression which means
     # one or more digit
     # output will be like ['100','564','365']
     numbers = re.findall('\d+',input)

     # now we need to convert each number into integer
     # int(string) converts string into integer
     # we will map int() function onto all elements 
     # of numbers list
     numbers = map(int,numbers)

     print max(numbers)

# Driver program
if __name__ == "__main__":
    input = '100klh564abc365bg'
    extractMax(input)
```

输出:

```
564

```