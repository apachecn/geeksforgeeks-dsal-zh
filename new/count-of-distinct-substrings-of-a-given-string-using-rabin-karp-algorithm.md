# 使用 Rabin Karp 算法计算字符串的不同子字符串

> 原文：[https://www.geeksforgeeks.org/count-of-distinct-substrings-of-a-given-string-using-rabin-karp-algorithm/](https://www.geeksforgeeks.org/count-of-distinct-substrings-of-a-given-string-using-rabin-karp-algorithm/)

给定一个字符串，使用 Rabin Karp 算法计算不同子字符串的数量。

**示例**：

```
Input  : str = "aba"
Output : 5
Explanation :
Total number of distinct substring are 5 - "a", "ab", "aba", "b" ,"ba" 

Input  : str = "abcd"
Output : 10
Explanation :
Total number of distinct substring are 10 - "a", "ab", "abc", "abcd", "b", "bc", "bcd", "c", "cd", "d" 

```

**方法**：

**前提条件**：[用于模式搜索的 Rabin-Karp 算法](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)

计算当前字符的当前哈希值，并将其存储在字典/映射中，以避免重复。

要按照 Rabin-Karp 算法计算哈希值（滚动哈希值），请执行以下操作：

Rabin 和 Karp 建议的哈希函数计算一个整数值。 字符串的整数值是字符串的数值。 例如，如果所有可能的字符都为 1 到 10，则`"122"`的数值将为 122。可能的字符数大于 10（通常为 256），并且图案长度可能很大。 因此，数值实际上不能存储为整数。 因此，使用模块化算法来计算数值，以确保可以将哈希值存储在整数变量中（可以适合存储字）。 要进行重新哈希处理，我们需要删除最高有效位并为哈希值添加新的最低有效位。 使用以下公式进行重新哈希处理。

```
hash( txt[s+1 .. s+m] ) = ( d ( hash( txt[s .. s+m-1]) – txt[s]*h ) + txt[s + m] ) mod q
```

`hash( txt[s .. s+m-1] )`：移位`s`时的哈希值。

`hash( txt[s+1 .. s+m] )`：下一个移位（或移位`s + 1`）。

`d`：字母中的字符数。

`q`：质数。

`h`：`d^(m-1)`。

当我们评估数学表达式时，这个想法是相似的。 例如，我们有一个字符串`"1234"`，我们计算出子字符串`"12"`的值是 12，我们想计算出子字符串`"123"`的值，可以计算为`((12) * 10 + 3) = 123`，此处应用类似的逻辑。

## Python3

```py

# importing libraries
import sys
import math as mt
t = 1
# store prime to reduce overflow
mod = 9007199254740881

for ___ in range(t):

    # string to check number of distinct substring
    s = 'abcd'

    # to store substrings
    l = []

    # to store hash values by Rabin Karp algorithm
    d = {}

    for i in range(len(s)):
        suma = 0
        pre = 0

        # Number of input alphabets
        D = 256

        for j in range(i, len(s)):

            # calculate new hash value by adding next element
            pre = (pre*D+ord(s[j])) % mod

            # strore string length if non repeat
            if d.get(pre, -1) == -1:
                l.append([i, j])
            d[pre] = 1

    # resulting length
    print(len(l))

    # resulting distinct substrings
    for i in range(len(l)):
        print(s[l[i][0]:l[i][1]+1], end=" ")

```

**输出**：

```
10
a ab abc abcd b bc bcd c cd d 

```

**时间复杂度**：`O(N ^ 2)`，`N`是字符串的长度。



* * *

* * *



