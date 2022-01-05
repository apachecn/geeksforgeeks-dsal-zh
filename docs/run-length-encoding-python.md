# Python 中的游程编码

> 原文:[https://www.geeksforgeeks.org/run-length-encoding-python/](https://www.geeksforgeeks.org/run-length-encoding-python/)

给定一个输入字符串，编写一个函数，返回输入字符串的[游程编码的](https://en.wikipedia.org/wiki/Run-length_encoding)字符串。

例如，如果输入字符串是“wwwwwwaaadexxxxx”，那么函数应该返回“w4a3d1e1x6”。

示例:

```
Input  :  str = 'wwwwaaadexxxxxx'
Output : 'w4a3d1e1x6'

```

此问题已有解决方案请参考[游程编码](https://www.geeksforgeeks.org/run-length-encoding/)链接。这里我们将使用[ordereddct](https://www.geeksforgeeks.org/remove-duplicates-given-string-python/)在 python 中快速解决这个问题。方法很简单，首先我们创建一个有序字典，其中包含输入字符串的字符作为键，0 作为它们的默认值，现在我们运行一个循环来计算每个字符的频率，并将它映射到它对应的键。

```
# Python code for run length encoding
from collections import OrderedDict
def runLengthEncoding(input):

    # Generate ordered dictionary of all lower
    # case alphabets, its output will be 
    # dict = {'w':0, 'a':0, 'd':0, 'e':0, 'x':0}
    dict=OrderedDict.fromkeys(input, 0)

    # Now iterate through input string to calculate 
    # frequency of each character, its output will be 
    # dict = {'w':4,'a':3,'d':1,'e':1,'x':6}
    for ch in input:
        dict[ch] += 1

    # now iterate through dictionary to make 
    # output string from (key,value) pairs
    output = ''
    for key,value in dict.items():
         output = output + key + str(value)
    return output

# Driver function
if __name__ == "__main__":
    input="wwwwaaadexxxxxx"
    print (runLengthEncoding(input))
```

输出:

```
'w4a3d1e1x6'

```

 **另一个代号:**

```
def encode(message):
    encoded_message = ""
    i = 0

    while (i <= len(message)-1):
        count = 1
        ch = message[i]
        j = i
        while (j < len(message)-1):
            if (message[j] == message[j+1]):
                count = count+1
                j = j+1
            else:
                break
        encoded_message=encoded_message+str(count)+ch
        i = j+1
    return encoded_message

#Provide different values for message and test your program
encoded_message=encode("ABBBBCCCCCCCCAB")
print(encoded_message)
```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。