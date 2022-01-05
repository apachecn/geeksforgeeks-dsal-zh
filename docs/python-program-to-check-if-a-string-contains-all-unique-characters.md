# Python 程序检查字符串是否包含所有唯一字符

> 原文:[https://www . geesforgeks . org/python-程序检查字符串是否包含所有唯一字符/](https://www.geeksforgeeks.org/python-program-to-check-if-a-string-contains-all-unique-characters/)

实现一种算法来确定字符串是否包含所有唯一字符。
示例:

> **输入:**s = " ABCD "
> T3】输出:True
> “ABCD”不包含任何重复项。因此输出为真。
> 
> **输入:**s = " abbd "
> T3】输出:False
> “abbd”包含重复项。因此输出为假。

一种解决方案是创建一个布尔值数组，其中索引 I 处的标志指示字符串中是否包含字母表中的字符 I。第二次看到这个字符时，可以立即返回 false。
如果字符串长度超过字母表中唯一字符的数量，也可以返回 false。

## 计算机编程语言

```
def isUniqueChars(st):

    # String length cannot be more than
    # 256.
    if len(st) > 256:
        return False

    # Initialize occurrences of all characters
    char_set = [False] * 128

    # For every character, check if it exists
    # in char_set
    for i in range(0, len(st)):

        # Find ASCII value and check if it
        # exists in set.
        val = ord(st[i])
        if char_set[val]:
            return False

        char_set[val] = True

    return True

# driver code
st = "abcd"
print(isUniqueChars(st))
```

**Output:** 

```
True
```

#### 方法 2:使用内置的 Python 函数:

*   使用 [**【计数器】(**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能统计字符频率
*   如果频率字典中的关键字(给出不同字符的计数)等于字符串长度，则打印“真”或“假”

下面是实现:

## 蟒蛇 3

```
from collections import Counter

def isUniqueChars(string):

    # Counting frequency
    freq = Counter(string)

    if(len(freq) == len(string)):
        return True
    else:
        return False

# driver code
st = "abcd"
print(isUniqueChars(st))
# This code is contributed by vikkycirus
```

**输出:**

```
True
```

**时间复杂度:** O(N)