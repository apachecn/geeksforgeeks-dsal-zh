# 用于在数组中分隔 0 和 1 的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-program-for-separate-0s-and-1s-in-a-array/](https://www.geeksforgeeks.org/python-program-for-segregate-0s-and-1s-in-an-array/)

给你一个随机排列的 0 和 1 的数组。将阵列左侧的 0 和右侧的 1 分开。仅遍历数组一次。

```
Input array   =  [0, 1, 0, 1, 0, 0, 1, 1, 1, 0] 
Output array =  [0, 0, 0, 0, 0, 1, 1, 1, 1, 1] 
```

**方法 1(计数 0s 或 1s)**
感谢纳文提出这个方法。
1)统计 0 的个数。让计数为 C.
2)一旦我们有了计数，我们可以将 C 0 放在数组的开头，将 1 放在剩余的 n–C 位置。
**时间复杂度:** O(n)

**输出:**

```
Array after segregation is 0 0 1 1 1 1 
```

方法 1 遍历数组两次。方法 2 在一次传递中做同样的事情。

**方法二(用两个指标遍历)**
维护两个指标。将第一索引*左侧*初始化为 0，将第二索引*右侧*初始化为 n-1。
当*左侧* < *右侧*
a)保持递增索引*左侧*当其中有 0 时
b)保持递减索引*右侧*当其中有 1 时
c)如果左侧<右侧，则交换 arr[左]和 arr[右]

实施:

## 计算机编程语言

```
# Python program to sort a binary array in one pass

# Function to put all 0s on left and all 1s on right
def segregate0and1(arr, size):
    # Initialize left and right indexes
    left, right = 0, size-1

    while left < right:
        # Increment left index while we see 0 at left
        while arr[left] == 0 and left < right:
            left += 1

        # Decrement right index while we see 1 at right
        while arr[right] == 1 and left < right:
            right -= 1

        # If left is smaller than right then there is a 1 at left
        # and a 0 at right. Exchange arr[left] and arr[right]
        if left < right:
            arr[left] = 0
            arr[right] = 1
            left += 1
            right -= 1

    return arr

# driver program to test
arr = [0, 1, 0, 1, 1, 1]
arr_size = len(arr)
print("Array after segregation")
print(segregate0and1(arr, arr_size))

# This code is contributed by Pratik Chhajer
```

**输出:**

```
Array after segregation is 0 0 1 1 1 1 
```

**时间复杂度:** O(n)

**另一种做法:**
1。取两个指针类型 0(对于元素 0)从开始(索引= 0)开始，类型 1(对于元素 1)从结束(索引= array.length-1)开始。
初始化类型 0 = 0 和类型 1 =数组。长度-1
2。打算将 1 放在数组的右侧。一旦完成，那么 0 肯定会向数组的左侧移动。

**输出:**

```
Array after segregation is 0 0 1 1 1 1 
```

**时间复杂度:** O(n)
更多详情请参考[将 0 和 1 分隔成一个数组](https://www.geeksforgeeks.org/segregate-0s-and-1s-in-an-array-by-traversing-array-once/)的完整文章！