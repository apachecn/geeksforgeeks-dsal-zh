# Python 中的字符串切片旋转字符串

> 原文:[https://www . geesforgeks . org/string-slicing-python-rotate-string/](https://www.geeksforgeeks.org/string-slicing-python-rotate-string/)

给定大小为 n 的字符串，编写函数对字符串执行以下操作。

1.  Rotate d elements of a given string to the left (or counterclockwise) (where d < = n).
2.  Rotate d elements of a given string to the right (or clockwise) (where d < = n).

示例:

```
Input : s = "GeeksforGeeks"
        d = 2
Output : Left Rotation  : "eksforGeeksGe" 
         Right Rotation : "ksGeeksforGee"  

Input : s = "qwertyu" 
        d = 2
Output : Left rotation : "ertyuqw"
         Right rotation : "yuqwert"

```

这个问题我们已经有了解决方案，请参考[弦的左旋转和右旋转](https://www.geeksforgeeks.org/left-rotation-right-rotation-string-2/)链接。我们将使用[字符串切片](https://www.geeksforgeeks.org/interesting-facts-about-strings-in-python-set-2/)在 python 中快速解决这个问题。方法很简单，

1.  Divide the string into two parts **, the first & and the second** . For **, left rotation** , Lfirst = str[0: d] and Lsecond = str[d :]. For **right rotation** LFIRST = STR [0: len (STR)-D] and Rsecond = str[len(str)-d:].
2.  Now connect the second+first of these two parts **correspondingly.**

```
# Function to rotate string left and right by d length 

def rotate(input,d): 

    # slice string in two parts for left and right 
    Lfirst = input[0 : d] 
    Lsecond = input[d :] 
    Rfirst = input[0 : len(input)-d] 
    Rsecond = input[len(input)-d : ] 

    # now concatenate two parts together 
    print ("Left Rotation : ", (Lsecond + Lfirst) )
    print ("Right Rotation : ", (Rsecond + Rfirst)) 

# Driver program 
if __name__ == "__main__": 
    input = 'GeeksforGeeks'
    d=2
    rotate(input,d) 
```

输出:

```
Left Rotation  : eksforGeeksGe 
Right Rotation : ksGeeksforGee

```