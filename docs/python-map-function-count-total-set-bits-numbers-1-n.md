# Python 映射功能|统计从 1 到 n 的所有数字中的总设置位

> 原文:[https://www . geesforgeks . org/python-map-function-count-total-set-bits-numbers-1-n/](https://www.geeksforgeeks.org/python-map-function-count-total-set-bits-numbers-1-n/)

给定一个正整数 n，计算从 1 到 n 的所有数字的二进制表示中的总位数。

示例:

```
Input: n = 3
Output:  4
Binary representations are 1, 2 and 3
1, 10 and 11 respectively. Total set
bits are 1 + 1 + 2 = 4.

Input: n = 6
Output: 9

Input: n = 7
Output: 12

Input: n = 8
Output: 13

```

对于这个问题，我们已经有了解决方案，请参考[计算从 1 到 n 的所有数字中的总设置位](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n/)链接。我们可以使用 [map()](https://www.geeksforgeeks.org/python-lambda-anonymous-functions-filter-map-reduce/) 函数在 python 中解决这个问题。方法很简单，

1.  Write a function. First, use the [bin (num)](https://www.geeksforgeeks.org/bin-in-python/) function to convert numbers into binary, and return the count of the set bits.
2.  Map the user-defined functions to the list of numbers from 1 to n, and we will get a separate list of the set bits in each number.
3.  Add the counts of all set bits.

```
# Function to Count total set bits in all numbers
# from 1 to n

# user defined function
def countSetBit(num):

     # convert decimal value into binary and
     # count all 1's in it
     binary = bin(num)

     return len([ch for ch in binary if ch=='1'])

# function which count set bits in each number
def countSetBitAll(input):

    # map count function on each number
    print (sum(map(countSetBit,input)))

# Driver program
if __name__ == "__main__":
    n = 8
    input=[]
    for i in range(1,n+1):
         input.append(i)
    countSetBitAll(input)
```

输出:

```
13

```