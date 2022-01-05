# Python 程序从字符串中删除最后 N 个字符

> 原文:[https://www . geesforgeks . org/python-从字符串中删除最后 n 个字符的程序/](https://www.geeksforgeeks.org/python-program-to-remove-last-n-characters-from-a-string/)

给定一个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 和一个整数 **N** ，任务是从字符串 **S** 的末尾移除 **N** 字符。

> **输入:** S = "GeeksForGeeks "，N = 5
> **输出:** GeeksFor
> **解释:**删除“GeeksForGeeks”的最后 5 个字符将字符串修改为“GeeksFor”。
> 
> **输入:** S = "欢迎"，N = 3
> T3】输出: Welc

**方法 1:** 按照以下步骤解决问题:

*   初始化一个空字符串，比如 **res，**来存储结果字符串。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 的字符，直到索引[T5】len](https://www.geeksforgeeks.org/python-string-length-len/)**(S)–N**。
*   继续将遇到的字符插入 **res** 。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to remove last N
# characters from string
def removeLastN(S, N):

    # Stores the resultant string
    res = ''

    # Traverse the string
    for i in range(len(S)-N):

          # Insert current character
        res += S[i]

    # Return the string
    return res

# Driver Code

# Input
S = "GeeksForGeeks"
N = 5

print(removeLastN(S, N))
```

**Output:**

```
GeeksFor

```

***时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(N)*

**方法 2:** 这个问题可以用[替换()](https://www.geeksforgeeks.org/python-string-replace/)解决。按照以下步骤解决问题:

1.  初始化一个字符串，比如 **res，**来存储结果字符串。
2.  [反弦](https://www.geeksforgeeks.org/reverse-string-python-5-different-ways/)T2【S】T3。
3.  使用 [replace()](https://www.geeksforgeeks.org/python-string-replace/) 方法，删除 **S** 的第一个 **N** 字符的第一个出现，并将其存储在 **res** 中。
4.  [反转弦](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/) **res** 。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to remove last N
# characters from string S
def removeLastN(S, N):

    # Stores resultant string
    res = ''

    # Reversing S
    S = S[::-1]

    # Removing last N characters
    res = S.replace(S[:N], '', 1)

    # Reversing back res
    res = res[::-1]

    # Return the string
    return res

# Driver Code

# Input
S = "GeeksForGeeks"
N = 5

print(removeLastN(S, N))
```

**Output:**

```
GeeksFor

```

***时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(N)*

[](https://www.geeksforgeeks.org/string-slicing-in-python/)****为主的方法:**按照以下步骤解决问题:**

*   **初始化一个字符串，比如说 **res** ，来存储结果字符串。**
*   **将 **res** 更新为**S[:len(S)–N]，**以存储除 **S** 的最后一个 **N** 字符之外的所有字符。**

**下面是上述方法的实现:**

## **蟒蛇 3**

```
# Python3 code for the above approach

# Function to remove last N
# characters from string S
def removeLastN(S, N):

    S = S[:len(S)-N]

    # Return the string
    return S

# Driver Code

# Input
S = "GeeksForGeeks"
N = 5

print(removeLastN(S, N))
```

****Output:**

```
GeeksFor

```** 

*****时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(1)***