# 查找是否可以使用一个外部数字使数组元素相同

> 原文： [https://www.geeksforgeeks.org/find-whether-possible-make-array-elements-using-one-external-number/](https://www.geeksforgeeks.org/find-whether-possible-make-array-elements-using-one-external-number/)

给定一个数组，可以使用任何外部数字`x`执行三个操作。

1.  一次将`x`添加到元素

2.  一次从元素中减去`x`

3.  对元素不执行任何操作

查找是否存在数字`x`，以便如果使用数字`x`执行上述操作，则所得数组具有相等的元素。

如果存在数字，则打印`"YES"`，并以空格分隔值，否则打印`"NO"`。

**示例**：

```
Input : [1, 1, 3, 5, 5]
Output : YES, x = 2
Explanation : The number 2 can be added to the 
first two elements and can be subtracted from 
the last two elements to obtain a common element
3 throughout the array

Input : [1, 3, 5, 7, 9]
Output : NO

```



这个想法是从给定的数组中形成一组独特的元素。 出现以下情况：

1.  唯一元素的数量为 1。`x = 0`时，答案为是。

2.  唯一元素的数量为 2。`x`为两个唯一元素的差，答案为是。

3.  唯一元素的数量为 3。

    *   如果中值和最大值之间的差异与中值和最小值之间的差异相同，则答案为是，其中`x`为中值和最大值之间或中值和最小值之间的差异。

    *   否则答案为否。

在 Python 中，我们可以使用 Python 集合[快速查找唯一元素](https://www.geeksforgeeks.org/sets-in-python/)。

```

# Program in python 2.x to find an element X 
# that can be used to operate on an array and 
# get equal elements 

# Prints "YES" and an element x if we can 
# equalize array using x. Else prints "NO" 
def canEqualise(array): 

    # We all the unique elements (using set 
    # function). Then we sort unique elements. 
    uniques = sorted(set(array)) 

    # if there are only 1 or 2 unique elements, 
    # then we can add or subtract x from one of them 
    # to get the other element 
    if len(uniques) == 1: 
        print("YES " + "0") 
    elif len(uniques) == 2: 
        print("YES " + str(uniques[1] - uniques[0])) 

    # If count of unique elements is three, then 
    # difference between the middle and minimum 
    # should be same as difference between maximum 
    # and middle 
    elif len(uniques) == 3: 
        if uniques[2] - uniques[1] == uniques[1] - uniques[0]: 
            X = uniques[2] - uniques[1] 
            print("YES " + str(X)) 
        else: 
            print("NO") 

    # if there are more than three unique elements, then 
    # we cannot add or subtract the same value from all 
    # the elements. 
    else: 
        print("NO") 

# Driver code 
array = [55, 52, 52, 49, 52] 
canEqualise(array) 

```

输出：

```
YES 3

```

此代码具有复杂性`O(N log N)`。

可以扩展相同的问题，以要求使用两个数字来均衡数组。 按照相同的过程，我们将需要数组中的 5 个唯一元素来要求两个数字来使数组相等。 因此，要使用`n`个数字来均衡一个数组，我们将需要`2n + 1`个数组中的唯一元素。

