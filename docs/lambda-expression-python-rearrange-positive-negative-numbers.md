# Python 中 Lambda 表达式重新排列正数和负数

> 原文:[https://www . geesforgeks . org/lambda-expression-python-重排-正数-负数/](https://www.geeksforgeeks.org/lambda-expression-python-rearrange-positive-negative-numbers/)

给定一个由正数和负数组成的数组，将它们排列成所有的负数都出现在数组中所有的正整数之前。出场顺序要保持。

示例:

```
Input :  arr[] = [12, 11, -13, -5, 6, -7, 5, -3, -6]
Output : arr[] = [-13, -5, -7, -3, -6, 12, 11, 6, 5]

Input :  arr[] = [-12, 11, 0, -5, 6, -7, 5, -3, -6]
Output : arr[] =  [-12, -5, -7, -3, -6, 11, 0, 6, 5]

```

这个问题有很多解决方法请参考[重新排列正负数字](https://www.geeksforgeeks.org/rearrange-positive-negative-numbers-using-inbuilt-sort-function/)链接，但是我们将用 python 中的单行代码使用 [Lambda 表达式](https://www.geeksforgeeks.org/python-lambda-anonymous-functions-filter-map-reduce/)来解决这个问题。

```
# Function to rearrange positive and negative elements
def Rearrange(arr):

    # First lambda expression returns list of negative numbers
    # in arr.
    # Second lambda expression returns list of positive numbers
    # in arr.
    return [x for x in arr if x < 0] + [x for x in arr if x >= 0]

# Driver function
if __name__ == "__main__":
    arr = [12, 11, -13, -5, 6, -7, 5, -3, -6]
    print (Rearrange(arr))
```

输出:

```
arr[] = [-13, -5, -7, -3, -6, 12, 11, 6, 5]

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。