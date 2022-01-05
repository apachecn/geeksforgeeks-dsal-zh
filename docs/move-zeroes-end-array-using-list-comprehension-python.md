# 使用 Python 中的列表理解将所有零移动到数组末尾

> 原文:[https://www . geesforgeks . org/move-zero-end-array-use-list-intensity-python/](https://www.geeksforgeeks.org/move-zeroes-end-array-using-list-comprehension-python/)

给定一个随机数数组，将给定数组的所有零推到数组的末尾。例如，如果给定的数组是{1，9，8，4，0，0，2，7，0，6，0}，则应该将其更改为{1，9，8，4，2，7，6，0，0，0，0}。所有其他元素的顺序应该相同。预期时间复杂度为 0(n)，额外空间为 0(1)。

示例:

```
Input :  arr = [1, 2, 0, 4, 3, 0, 5, 0]
Output : arr = [1, 2, 4, 3, 5, 0, 0, 0]

Input : arr  = [1, 2, 0, 0, 0, 3, 6]
Output : arr = [1, 2, 3, 6, 0, 0, 0]

```

对于这个问题，我们已经有了解决方案，请参考[将所有零移到数组末尾](https://www.geeksforgeeks.org/move-zeroes-end-array/)链接。我们将用 python 在一行代码中使用[列表理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)来解决这个问题。

```
# Function to append all zeros at the end 
# of array
def moveZeros(arr):

    # first expression returns a list of
    # all non zero elements in arr in the 
    # same order they were inserted into arr
    # second expression returns a list of 
    # zeros present in arr
    return [nonZero for nonZero in arr if nonZero!=0] + \
           [Zero for Zero in arr if Zero==0]

# Driver function
if __name__ == "__main__":
    arr = [1, 2, 0, 4, 3, 0, 5, 0]
    print (moveZeros(arr))
```

输出:

```
[1, 2, 4, 3, 5, 0, 0, 0]

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。