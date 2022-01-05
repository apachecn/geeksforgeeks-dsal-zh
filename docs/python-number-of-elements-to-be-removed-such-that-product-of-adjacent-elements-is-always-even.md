# Python |要移除的元素数量，以便相邻元素的乘积总是偶数

> 原文:[https://www . geesforgeks . org/python-待移除元素的数量-这样相邻元素的乘积总是偶数/](https://www.geeksforgeeks.org/python-number-of-elements-to-be-removed-such-that-product-of-adjacent-elements-is-always-even/)

给定一个 N 个整数的数组。任务是消除元素的数量，以便在结果数组中任何两个相邻值的乘积是偶数。

**示例:**

```
Input  : arr[] = {1, 2, 3}
Output : 0

Input  : arr[] = {1, 3, 5, 4, 2}
Output : 2
Remove 1 and 3.
```

**逼近:**2 个数的乘积是偶数，即使其中任何一个是偶数。这意味着，对于每对连续的数字，如果两者都是奇数，则消除其中一个。
所以，要使相邻元素的乘积为偶数，要么所有元素都应为偶数，要么交替出现奇偶元素。所以下面的贪婪算法是有效的:

*   按顺序浏览所有元素。
*   如果所有元素都是偶数，则返回“0”。
*   如果所有元素都是奇数，则返回“n”。
*   否则，计算连续奇数对的数量。
*   返回最小计数。

下面是 Python 实现–

## 蟒蛇 3

```
# Python 3 implementation of the 
# above approach

# Function to find minimum number of 
# eliminations such that product of all 
# adjacent elements is even
def min_elimination(n, arr):
    countOdd = 0
    counteven = 0
    # Stores the new value
    for i in range(n):

        # Count odd and even  numbers
        if (arr[i] % 2):
            countOdd += 1
        else:
            counteven+= 1
    # if all are even
    if counteven == n:
        return 0

    # if all are odd
    if countOdd == n:
        return n
    else:
        countpair = 0
        for i in range(1, n):
            if (arr[i] % 2 == 1 and arr[i-1] % 2 == 1):
                countpair+= 1
        return countpair

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 7, 9]
    n = len(arr)

    print(min_elimination(n, arr))
```

**输出:**

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(N)