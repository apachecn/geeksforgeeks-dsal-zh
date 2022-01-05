# 移除小于 X 的值后，按相关值的降序对字符串进行排序

> 原文:[https://www . geesforgeks . org/sort-a-string-in-降序-值关联-移除后-小于-x/](https://www.geeksforgeeks.org/sort-a-string-in-decreasing-order-of-values-associated-after-removal-of-values-smaller-than-x/)

给定一个交替放置的**整数 X** 和一个由空格分隔的**文本**和**数字**组成的字符串**字符串**，任务是对该字符串进行排序，以便在移除所有小于 **X** 的数字后，文本和数字按照相关数字的降序显示。如果两个字符串具有相同的值，则按照字符串的字典顺序对它们进行排序。

**示例:**

> **输入:** X = 79，str =“Geek 78 代表 99 Geeks 88 Gfg 86”
> **输出:**
> 代表 99 Geeks 88 Gfg 86
> **说明:**
> “Eve 99”被移除，因为与其关联的数字小于 X(= 79)
> 现在，基于关联数字降序的重新排序的字符串是“Bob 99 Suzy 88 Alice 86”。
> 
> **输入:**x = 77.str = " axc 78 CZT 60 "
> T3】输出: Axc 78

**方法:**想法是使用[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)技术。按照以下步骤解决问题:

*   将字符串分割成一个**列表**，然后删除小于给定值的条目，即 **X** 。
*   使用冒泡排序方法，根据与之关联的数字对列表进行排序。
*   如果数字不相等，请按降序对数字进行排序，同时对名称进行排序。
*   如果数字相等，那么按照字典顺序对它们进行排序。
*   将字符串和数字交换在一起，以便将它们保持在一起。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to split the input
# string into a list
def tokenizer(Str):
    List = Str.split()
    return List

# Function to sort the given list based
# on values at odd indices of the list
def SortListByOddIndices(List, x):

    l = len(List)

# Function to remove the values
# less than the given value x
    for i in range(l - 1, 0, -2):
        if int(List[i]) < x:
            del(List[i - 1: i + 1])

    l = len(List)

    for i in range(1, l, 2):
        for j in range(1, l - i, 2):

            # Compares values at odd indices of
            # the list to sort the list
            if List[j] < List[j + 2] \
            or (List[j - 1] > List[j + 1] \
            and List[j] == List[j + 2]):

                List[j], List[j + 2] \
                = List[j + 2], List[j]

                List[j - 1], List[j + 1] \
                = List[j + 1], List[j - 1]

    return ' '.join(List)

# Driver Code
Str = "Axc 78 Czy 60"
x = 77

# Function call
List = tokenizer(Str)

Str = SortListByOddIndices(List, x)

print(Str)
```

**Output:**

```
Axc 78

```

***时间复杂度:** O(N <sup>2</sup> )
**辅助空间:** O(N)*