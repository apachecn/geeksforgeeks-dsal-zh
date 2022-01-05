# 使用 map()函数对 Python 中的 2D 数组求和

> 原文:[https://www . geesforgeks . org/sum-2d-array-python-using-map-function/](https://www.geeksforgeeks.org/sum-2d-array-python-using-map-function/)

给定一个二维矩阵，我们需要求矩阵中所有元素的和？

示例:

```
Input  : arr = [[1, 2, 3], 
                [4, 5, 6], 
                [2, 1, 2]]
Output : Sum = 26

```

通过迭代整个矩阵，使用两个 for 循环可以很容易地解决这个问题，但是我们可以使用 map()函数在 python 中快速解决这个问题。

```
# Function to calculate sum of all elements in matrix
# sum(arr) is a python inbuilt function which calculates
# sum of each element in a iterable ( array, list etc ).
# map(sum,arr) applies a given function to each item of 
# an iterable and returns a list of the results.
def findSum(arr):

    # inner map function applies inbuilt function  
    # sum on each row of matrix arr and returns 
    # list of sum of elements of each row
    return sum(map(sum,arr))  

# Driver function
if __name__ == "__main__":
    arr = [[1, 2, 3], [4, 5, 6], [2, 1, 2]]
    print ("Sum = ",findSum(arr))
```

输出:

```
26

```

**map()是做什么的？**
map()函数将一个给定的函数应用于一个可列表(列表、元组等)的每个项目。)并返回结果列表。例如见下面给出的例子:

```
# Python code to demonstrate working of map()

# Function to calculate square of any number
def calculateSquare(n):
    return n*n

# numbers is a list of elements
numbers = [1, 2, 3, 4]

# Here map function is mapping calculateSquare 
# function to each element of numbers list.
# It is similar to pass each element of numbers 
# list one by one into calculateSquare function 
# and store result in another list
result = map(calculateSquare, numbers)

# resultant output will be [1,4,9,16]
print (result)
```

输出:

```
[1, 4, 9, 16]
```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。