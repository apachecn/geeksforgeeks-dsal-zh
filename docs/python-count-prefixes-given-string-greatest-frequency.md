# Python |统计给定字符串中出现频率最高的所有前缀

> 原文:[https://www . geesforgeks . org/python-count-前缀-给定-字符串-最大频率/](https://www.geeksforgeeks.org/python-count-prefixes-given-string-greatest-frequency/)

给定一个字符串，打印并计算第一个字母比第二个字母出现频率高的所有前缀。
从用户处取两个字母进行比较。第一个字母给出的前缀比第二个字母出现的频率高，这样的前缀会被打印出来，否则结果将是 0。
**例:**

```
Input : string1 = "geek", 
        alphabet1 = "e", alphabet2 = "k"
Output :
ge
gee
geek
3

Input : string1 = "geek",
        alphabet1 = "k", alphabet2 = "e"
Output :
0
```

**方法:**取一个空字符串，存储所有形成的前缀的字符串值。然后检查字母的频率是否比第二个字母高。如果没有发现这样的情况，那么结果将是 **0** 前缀。
下面是实现:

## 蟒蛇 3

```
# Python program to Count all
# prefixes in given string with
# greatest frequency

# Function to print the prefixes
def prefix(string1, alphabet1, alphabet2):
    count = 0
    non_empty_string = ""

    string2 = list(string1)

    # Loop for iterating the length of
    # the string and print the prefixes
    # and the count of query prefixes.
    for i in range(0, len(string2)):
        non_empty_string = non_empty_string + (string2[i])

        if (non_empty_string.count(alphabet1) >
            non_empty_string.count(alphabet2)):

            # prints all required prefixes
            print(non_empty_string)

            # increment count
            count += 1

    # returns count of the
    # required prefixes
    return(count)

# Driver Code
print(prefix("geeksforgeeks", "e", "g"))
```

**Output :** 

```
gee
geek
geeks
geeksf
geeksfo
geeksfor
geeksforge
geeksforgee
geeksforgeek
geeksforgeeks
10
```

**时间复杂度:** O(N)，其中 N 为字符串的长度

**辅助空间:** O(N)