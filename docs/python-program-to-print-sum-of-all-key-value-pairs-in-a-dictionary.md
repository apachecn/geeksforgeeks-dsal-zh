# Python 程序打印字典中所有键值对的总和

> 原文:[https://www . geesforgeks . org/python-program-to-print-sum-all-key-value-pairs-in-a-dictionary/](https://www.geeksforgeeks.org/python-program-to-print-sum-of-all-key-value-pairs-in-a-dictionary/)

给定由 **N** 项组成的[字典](https://www.geeksforgeeks.org/python-dictionary/) **arr** ，其中键和值都是整数类型，任务是在字典中找到所有键和值对的总和。

**示例:**

> **输入:** arr = {1: 10，2: 20，3: 30}
> **输出:** 11 22 33
> **解释:**
> 字典中第一项的键和值之和= 1 + 10 = 11。
> 字典中第二项的键值之和= 2 + 20 = 22。
> 字典中第三项的键值之和= 3 + 30 = 33。
> 
> **输入:** arr = {10 : -5，5 : -10，100:-50 }
> T3】输出: 5 -5 50

**方法使用[字典遍历](https://www.geeksforgeeks.org/iterate-over-a-dictionary-in-python/)技术:**想法是[遍历用于循环的字典的键](https://www.geeksforgeeks.org/iterate-over-a-dictionary-in-python/)。按照以下步骤解决问题:

*   初始化一个[列表](https://www.geeksforgeeks.org/python-list/)，说 **l** ，存储结果。
*   [遍历字典](https://www.geeksforgeeks.org/iterate-over-a-dictionary-in-python/) **arr** 然后[将**I+arr【I】**追加到列表](https://www.geeksforgeeks.org/append-extend-python/) **l** 中。
*   完成以上步骤后，打印列表 **l** 作为所需答案。

以下是上述方法的实现:

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to print the list containing
# the sum of key and value pairs of
# each item of a dictionary
def FindSum(arr):

    # Stores the list containing the
    # sum of keys and values of each item
    l = []

    # Traverse the dictionary
    for i in arr:

        l.append(i + arr[i])

    # Print the list l
    print(*l)

# Driver Code

arr = {1: 10, 2: 20, 3: 30}

FindSum(arr)
```

**Output:**

```
11 22 33

```

***时间复杂度:** O(N)
**辅助空间:** O(N)*

**使用[键()的方法](https://www.geeksforgeeks.org/python-dictionary-keys-method/)方法:**解决问题的替代方法是使用[键()方法](https://www.geeksforgeeks.org/python-dictionary-keys-method/)。按照以下步骤解决问题:

*   初始化一个[列表](https://www.geeksforgeeks.org/python-list/)，说 **l** ，存储结果。
*   [遍历字典](https://www.geeksforgeeks.org/iterate-over-a-dictionary-in-python/) **arr** 的键列表，然后[追加](https://www.geeksforgeeks.org/append-extend-python/)。
*   完成以上步骤后，打印列表 **l** 作为答案。

以下是上述方法的实现:

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to print the list
# containing the sum of key and
# value pairs from a dictionary
def FindSum(arr):

    # Stores the list containing the
    # sum of keys and values of each item
    l = []

    # Traverse the list of keys of arr
    for i in arr.keys():

        l.append(i + arr[i])

    # Print the list l
    print(*l)

# Driver Code

arr = {1: 10, 2: 20, 3: 30}

FindSum(arr)
```

**Output:**

```
11 22 33

```

***时间复杂度:** O(N)
**辅助空间:** O(N)*