# 使用 Python 中的 itertools 打印字符串的前 n 个不同排列

> 原文:[https://www . geeksforgeeks . org/print-first-n-distinct-排列字符串-使用 itertools-in-python/](https://www.geeksforgeeks.org/print-first-n-distinct-permutations-of-string-using-itertools-in-python/)

给定一个允许重复字符的字符串，首先打印给定字符串的 *n* 个排列，这样就不会重复排列。

**示例:**

```
Input : string = "abcab", n = 10
Output : aabbc aabcb aacbb ababc abacb
                abbac abbca abcab abcba acabb

Input : string = "okok", n = 4
Output : kkoo koko kook okko

```

**方法:**
Python 提供了一种内置的方法来查找`itertools` 包中存在的任何给定序列的排列。但是这种方法不能提供唯一的排列。因此，为了确保任何排列都不会重复，我们使用**设置**并遵循以下条件:

*   如果置换不在集合中，打印它并将其插入集合中。增加唯一排列的计数。
*   否则，继续下一个排列。

下面是上述方法的实现:

```
# Python3 program to print first n unique 
# permutations of the string using itertools
from itertools import permutations

# Function to print first n unique 
# permutation using itertools 
def nPermute(string, n): 

    # Convert the string to list and sort 
    # the characters in alphabetical order
    strList = sorted(list(string))

    # Create an iterator
    permList = permutations(strList)

    # Keep iterating until we 
    # reach nth unique permutation
    i = 0
    permSet = set()
    tempStr = '' 

    while i < n:
        tempStr = ''.join(permList.__next__())

        # Insert the string in the set
        # if it is not already included
        # and print it out.
        if tempStr not in permSet:
            permSet.add(tempStr)
            print(tempStr)
            i += 1

# Driver code 
if __name__ == "__main__":

    string = "ababc"
    n = 10
    nPermute(string, n) 
```

**Output:**

```
aabbc
aabcb
aacbb
ababc
abacb
abbac
abbca
abcab
abcba
acabb

```