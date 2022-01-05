# Python 程序打印两个给定数字中所有不同的不常见数字

> 原文:[https://www . geesforgeks . org/python-program-to-print-all-distinct-不凡-数字-二进制数字/](https://www.geeksforgeeks.org/python-program-to-print-all-distinct-uncommon-digits-present-in-two-given-numbers/)

给定两个正整数 **A** 和 **B** ，任务是按降序打印不同的数字，这在两个数字中并不常见。

**示例:**

> **输入:** A = 378212，B = 78124590
> **输出:** 9 5 4 3 0
> **解释:**两个数字中出现的所有不同数字都是{0，1，2，3，4，5，6，7，8，9}。数字{1，2，6，7}在两个数字中都很常见。
> 
> **输入:** A = 100，B = 273
> **输出:** 7 3 2 1 0
> **说明:**两个数字中出现的所有不同数字都是{0，1，2，3，7}。数字{0，1，2，3，7}在两个数字中都很常见。

**处理方式:**使用[设置](https://www.geeksforgeeks.org/python-sets/)，[用 python 列出](https://www.geeksforgeeks.org/python-list/)即可解决问题。按照以下步骤解决问题:

*   [将两个整数转换成字符串](https://www.geeksforgeeks.org/convert-integer-to-string-in-python/)。
*   现在，使用 [map()](https://www.geeksforgeeks.org/python-map-function/) 功能，在[列表](https://www.geeksforgeeks.org/python-list/) **lis1** 和 **lis2** 中存储字符串 **A** 和 **B** 字符的等效整数值。
*   使用[设置()方法](https://www.geeksforgeeks.org/python-set-method/)将列表 **lis1** 和 **lis2** 转换为设置 **lis1** 和 **lis2** 。
*   现在，使用功能[对称 _ 差()](https://www.geeksforgeeks.org/python-set-symmetric_difference-2/)找到两组 **lis1** 和 **lis2** 的不常见数字，并存储在一组中，比如 **lis** 。
*   完成上述步骤后，使用[列表()方法](https://www.geeksforgeeks.org/list-methods-python/)将设置的**列表**转换为列表**列表**。
*   最后[对列表进行降序排序](https://www.geeksforgeeks.org/python-list-sort/)[打印列表](https://www.geeksforgeeks.org/print-lists-in-python-4-different-ways/) **列出**作为答案。

以下是上述方法的实现:

## 蟒蛇 3

```
# Python implementation
# of the above approach

# Function to print uncommon digits
# of two numbers in descending order
def disticntUncommonDigits(A, B):

    # Stores digits of A as string
    A = str(A)

    # Stores digits of B as string
    B = str(B)

    # Stores the characters
    # of A in a integer list
    lis1 = list(map(int, A))

    # Stores the characters
    # of B in a integer list
    lis2 = list(map(int, B))

    # Converts lis1 to set
    lis1 = set(lis1)

    # Converts lis2 to set
    lis2 = set(lis2)

    # Stores the uncommon digits present
    # in the sets lis1 and lis2
    lis = lis1.symmetric_difference(lis2)

    # Converts lis to list
    lis = list(lis)

    # Sort the list in descending order
    lis.sort(reverse = True)

    # Print the list lis
    for i in lis:
        print(i, end =" ")

# Driver Code

# Input
A = 378212
B = 78124590

disticntUncommonDigits(A, B)
```

**Output:**

```
9 5 4 3 0

```

***时间复杂度:**O(log<sub>10</sub>(A)+log<sub>10</sub>(B))
**辅助空间:**O(log<sub>10</sub>(A)+log<sub>10</sub>(B))*