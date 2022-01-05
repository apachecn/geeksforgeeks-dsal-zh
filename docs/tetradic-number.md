# 四进制数

> 原文:[https://www.geeksforgeeks.org/tetradic-number/](https://www.geeksforgeeks.org/tetradic-number/)

一个**四进制数**(有时称为一个**四进制数**)是一个在前后翻转、上下镜像或上下翻转时保持不变的数。

换句话说，**四进制数**是一个回文数，在数字中只包含 0、1 和 8 作为数字。

前几个四分位数是:

> 0, 1, 8, 11, 88, 101, 111, 181, 808, 818, 888, 1001, 1111, 1881, ….

### 检查 N 是否为四进制数

给定一个数字 **N** ，任务是检查 **N** 是否为**四进制数**。
**示例:**

> **输入:** N = 101
> **输出:**是
> **说明:**
> 101 是回文数字，在数字中只包含 0、1、8 作为数字。
> **输入:** N = 1221
> **输出:**否

**做法:**思路是检查数字是不是回文。如果数字是回文，检查数字中的数字。如果所有的数字都在集合中(0，1，8)，那么这个数就是一个四进制数。
**例如:**

> 对于 N = 101
> //由于 N 是回文数字
> //数字中的所有数字都是
> //来自集合{0，1，8}
> //因此，N 是四进制数

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 implementation for
# the above approach

# Function to check if the number
# N having all digits lies in
# the set (0, 1, 8)
def isContaindigit(n):
    temp = str(n)
    for i in temp:
        if i not in ['0', '1', '8']:
            return False
    return True

# Function to check if the number
# N is palindrome
def ispalindrome(n):
    temp = str(n)
    if temp == temp[::-1]:
        return True
    return False

# Function to check if a number
# N is Tetradic  
def isTetradic(n):      
    if ispalindrome(n):
        if isContaindigit(n):
            return True
    return False

# Driver Code
N = 101

# Function Call
if(isTetradic(N)): 
    print("Yes")
else: 
    print("No")
```

**Output:** 

```
Yes
```