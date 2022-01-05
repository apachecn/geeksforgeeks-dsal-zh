# 在 Python 中删除给定字符串的所有重复项

> 原文:[https://www . geesforgeks . org/remove-duplicates-given-string-python/](https://www.geeksforgeeks.org/remove-duplicates-given-string-python/)

给我们一个字符串，我们需要删除其中的所有重复项？如果字符的顺序很重要，输出会是什么？
示例:

```
Input : geeksforgeeks
Output : efgkos

```

此问题已有解决方案，请参考[从给定字符串](https://www.geeksforgeeks.org/remove-all-duplicates-from-the-input-string/)中删除所有重复项。
T3【方法一:

```
from collections import OrderedDict 

# Function to remove all duplicates from string 
# and order does not matter 
def removeDupWithoutOrder(str): 

    # set() --> A Set is an unordered collection 
    #         data type that is iterable, mutable, 
    #         and has no duplicate elements. 
    # "".join() --> It joins two adjacent elements in 
    #             iterable with any symbol defined in 
    #             "" ( double quotes ) and returns a 
    #             single string 
    return "".join(set(str)) 

# Function to remove all duplicates from string 
# and keep the order of characters same 
def removeDupWithOrder(str): 
    return "".join(OrderedDict.fromkeys(str)) 

# Driver program 
if __name__ == "__main__": 
    str = "geeksforgeeks"
    print ("Without Order = ",removeDupWithoutOrder(str)) 
    print ("With Order = ",removeDupWithOrder(str)) 
```

输出:

```
Without Order =  egfkosr
With Order    =  geksfor

```

**方法二:**

```
def removeDuplicate(str):
    s=set(str)
    s="".join(s)
    print("Without Order:",s)
    t=""
    for i in str:
        if(i in t):
            pass
        else:
            t=t+i
        print("With Order:",t)

str="geeksforgeeks"
removeDuplicate(str)
```

**输出:**

```
Without Order: rofgeks
With Order: geksfor
```

**ordereddct 和 fromkeys()是做什么的？**

OrderedDict 是一个记住最先插入的键的顺序的字典。如果新条目覆盖现有条目，则原始插入位置保持不变。

例如，请参见下面的代码片段:

```
from collections import OrderedDict

ordinary_dictionary = {}
ordinary_dictionary['a'] = 1
ordinary_dictionary['b'] = 2
ordinary_dictionary['c'] = 3
ordinary_dictionary['d'] = 4
ordinary_dictionary['e'] = 5

# Output = {'a': 1, 'c': 3, 'b': 2, 'e': 5, 'd': 4}
print (ordinary_dictionary)    

ordered_dictionary = OrderedDict()
ordered_dictionary['a'] = 1
ordered_dictionary['b'] = 2
ordered_dictionary['c'] = 3
ordered_dictionary['d'] = 4
ordered_dictionary['e'] = 5

# Output = {'a':1,'b':2,'c':3,'d':4,'e':5}
print (ordered_dictionary)      
```

**fromkeys()** 用 seq 中的键和值创建一个新字典，并返回键列表， **fromkeys(seq[，value])** 是 fromkeys()方法的语法。

**<u>参数:</u>**

*   **序列:**这是将用于字典键准备的值列表。
*   **值:**这是可选的，如果提供，则值将被设置为该值。

例如，请参见下面的代码片段:

```
from collections import OrderedDict
seq = ('name', 'age', 'gender')
dict = OrderedDict.fromkeys(seq)

# Output = {'age': None, 'name': None, 'gender': None}
print (str(dict)) 
dict = OrderedDict.fromkeys(seq, 10)

# Output = {'age': 10, 'name': 10, 'gender': 10}
print (str(dict))       
```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。