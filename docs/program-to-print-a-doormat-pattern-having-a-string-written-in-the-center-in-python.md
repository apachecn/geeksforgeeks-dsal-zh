# 用 Python 打印中心写有字符串的门垫图案的程序

> 原文:[https://www . geesforgeks . org/program-to-print-a-door mat-pattern-with-string-in-center-in-python/](https://www.geeksforgeeks.org/program-to-print-a-doormat-pattern-having-a-string-written-in-the-center-in-python/)

给定行数 R 和列数 C，任务是打印门垫图案，如下例所示。垫子设计中的列数必须是设计中行数的 3 倍。门垫的中央应该印有极客头像。垫子的宽度等于图案中的列数。
**注意**字符串“GeeksforGeeks”包含 13 个字符，这是一个奇数，因此行数必须是奇数，以通过保持对称性来正确设计垫子。

**示例:**

```
Input: R = 11, C = 33 
Output:
    ---------------|*|---------------
    ------------|*||*||*|------------
    ---------|*||*||*||*||*|---------
    ------|*||*||*||*||*||*||*|------
    ---|*||*||*||*||*||*||*||*||*|---
    ----------GeeksforGeeks----------
    ---|*||*||*||*||*||*||*||*||*|---
    ------|*||*||*||*||*||*||*|------
    ---------|*||*||*||*||*|---------
    ------------|*||*||*|------------
    ---------------|*|---------------

Input: R = 9, C = 27
Output:
    ------------|*|------------
    ---------|*||*||*|---------
    ------|*||*||*||*||*|------
    ---|*||*||*||*||*||*||*|---
    -------GeeksforGeeks-------
    ---|*||*||*||*||*||*||*|---
    ------|*||*||*||*||*|------
    ---------|*||*||*|---------
    ------------|*|------------

```

**方法:**整个图案可以分为 3 个不同的部分。第一部分包含一个有三角形的图案。第二部分包含一个字符串“GeeksforGeeks”，第三部分包含一个倒三角形的模式。通过使用内置的字符串对齐功能，可以轻松打印出顶部为倒三角形的图案。

1.  **[ljust](https://www.geeksforgeeks.org/python-string-ljust-rjust-center/)** :此方法返回长度为 l 的左对齐字符串
2.  **[居中](https://www.geeksforgeeks.org/string-center-python/) :** 该方法返回长度为 l 的居中对齐字符串
3.  **[rjust](https://www.geeksforgeeks.org/string-rjust-ljust-python/) :** 此方法返回长度为 l 的右对齐字符串

下面是上述方法的实现:

```
# Python3 implementation of the approach

# Function to print the doormat pattern
def doormatPattern(rows, columns):
    width = columns

    # Print the pattern having a top triangle
    for i in range (0, int (rows / 2)):
        pattern = "|*|" * ((2 * i) + 1)
        print (pattern.center (width, '-'))

    # Print GeeksforGeeks in the center
    print ("GeeksforGeeks".center (width, '-'))

    # Print the pattern having 
    # an inverted triangle
    i = int (rows / 2)
    while i > 0:
        pattern = "|*|" * ((2 * i) - 1)
        print (pattern.center (width, '-'))
        i = i-1
    return

# Driver code
rows = 7
columns = rows * 3
doormatPattern(rows, columns)
```

**Output:**

```
---------|*|---------
------|*||*||*|------
---|*||*||*||*||*|---
----GeeksforGeeks----
---|*||*||*||*||*|---
------|*||*||*|------
---------|*|---------

```