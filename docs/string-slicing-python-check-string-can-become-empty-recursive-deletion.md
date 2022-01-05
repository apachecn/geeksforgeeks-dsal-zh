# Python 中的字符串切片，检查字符串是否可以通过递归删除变空

> 原文:[https://www . geesforgeks . org/string-slicing-python-check-string-can-变空-递归-删除/](https://www.geeksforgeeks.org/string-slicing-python-check-string-can-become-empty-recursive-deletion/)

给定一个字符串“str”和另一个字符串“sub_str”。我们可以多次从“字符串”中删除“sub_str”。还假定“sub_str”一次只出现一次。任务是通过一次又一次地移除“sub_str”来发现“str”是否可以变成空的。

示例:

```
Input  : str = "GEEGEEKSKS", sub_str = "GEEKS"
Output : Yes
Explanation : In the string GEEGEEKSKS, we can first 
              delete the substring GEEKS from position 4.
              The new string now becomes GEEKS. We can 
              again delete sub-string GEEKS from position 1\. 
              Now the string becomes empty.

Input  : str = "GEEGEEKSSGEK", sub_str = "GEEKS"
Output : No
Explanation : In the string it is not possible to make the
              string empty in any possible manner.

```

对于这个问题，我们已经有了解决方案，请参考[通过递归删除给定的子字符串](https://www.geeksforgeeks.org/check-string-can-become-empty-recursively-deleting-given-sub-string/)链接来检查字符串是否可以变成空的。我们将使用[字符串切片](https://www.geeksforgeeks.org/how-to-split-a-string-in-cc-python-and-java/)在 python 中解决这个问题。方法很简单，

1.  使用字符串的 [find()](https://www.geeksforgeeks.org/python-string-methods-set-1-find-rfind-startwith-endwith-islower-isupper-lower-upper-swapcase-title/) 方法搜索给定的模式子字符串。
2.  如果子字符串位于主字符串中，那么 find 函数将返回它第一次出现的索引。
3.  现在将字符串分成两部分，(I)从字符串的开始直到创建的子字符串的索引-1，(ii)(从创建的子字符串的第一个索引开始+子字符串的长度)直到字符串的结束。
4.  连接这两个分割部分，从第 1 步开始重复，直到原始字符串变成空的，或者我们不再找到子字符串。

```
def checkEmpty(input, pattern): 

    # If both are empty  
    if len(input)== 0 and len(pattern)== 0: 
         return 'true'

    # If only pattern is empty 
    if len(pattern)== 0: 
         return 'true'

    while (len(input) != 0): 

        # find sub-string in main string 
        index = input.find(pattern) 

        # check if sub-string founded or not 
        if (index ==(-1)): 
          return 'false'

        # slice input string in two parts and concatenate 
        input = input[0:index] + input[index + len(pattern):]              

    return 'true'

# Driver program 
if __name__ == "__main__": 
    input ='GEEGEEKSKS'
    pattern ='GEEKS'
    print (checkEmpty(input, pattern))
```

输出:

```
true

```