# 频闪数字

> 原文:[https://www.geeksforgeeks.org/strobogrammatic-number/](https://www.geeksforgeeks.org/strobogrammatic-number/)

对于给定的长度 n，找出所有 n 长度的 Strobogrammatic 数。

**频闪数**是一个数字旋转对称的数字，旋转 180 度后看起来是一样的。换句话说，Strobogrammatic Number 上下颠倒地出现在相同的右侧。

> 180°旋转后的 0:(0→0)
> 180°旋转后的 1:(1→1)
> 180°旋转后的 8:(8→8)
> 180°旋转后的 6:(6→**9**)
> 180°旋转后的 9:(9→**6**)

**示例:**

```
Input : n = 2
Output : 88  11  96  69

Input : n = 4
Output : 8008 1001 9006 6009 8888 1881 9886 6889 8118 1111
         9116 6119 8968 1961 9966 6969 8698 1691 9696 6699

```

下面是 Python3 的实现:

```
# Python program to print all
# Strobogrammatic number of length n

# strobogrammatic function 
def strobogrammatic_num(n):

    result = numdef(n, n)
    return result

# definition function
def numdef(n, length):

    if n == 0: return [""]
    if n == 1: return ["1", "0", "8"]

    middles = numdef(n - 2, length)
    result = []

    for middle in middles:
        if n != length:            
            result.append("0" + middle + "0")

        result.append("8" + middle + "8")
        result.append("1" + middle + "1")
        result.append("9" + middle + "6")
        result.append("6" + middle + "9")
    return result

# Driver Code
if __name__ == '__main__':

    # Print all Strobogrammatic 
    # number for n = 3
    print(strobogrammatic_num(3))
```

**输出:**

```
['818', '111', '916', '619', '808', '101', '906', '609', '888', '181', '986', '689']

```

**参考:**[https://en.wikipedia.org/wiki/Strobogrammatic_number](https://en.wikipedia.org/wiki/Strobogrammatic_number)