# Python |计算范围内未设置的位数

> 原文:[https://www . geesforgeks . org/python-count-unset-bits-range/](https://www.geeksforgeeks.org/python-count-unset-bits-range/)

给定一个非负数 n 和两个值 l 和 r，问题是在 n 的二进制表示中计算 l 到 r 范围内的未设置位的数量，即从最右边的第 1 位到最右边的第 1 位计算未设置位。

示例:

```
Input : n = 42, l = 2, r = 5
Output : 2
(42)10 = (101010)2
There are '2' unset bits in the range 2 to 5.

Input : n = 80, l = 1, r = 4
Output : 4

```

对于这个问题，我们有现有的解决方案，请参考[计算范围内未设置的位](https://www.geeksforgeeks.org/count-unset-bits-range/)链接。我们可以用 Python 快速解决这个问题。方法很简单，

1.  Use the [bin (num)](https://www.geeksforgeeks.org/bin-in-python/) function to convert decimal to binary.
2.  Now delete the first two characters of the output binary string, because by default, the bin function appends' 0b' to the output string as a prefix.
3.  Slice the string from the index **(l-1)** to index **r** and invert it, and then calculate the unset bits in the middle.

```
# Function to count unset bits in a range

def unsetBits(n,l,r):

    # convert n into it's binary
    binary = bin(n)

    # remove first two characters
    binary = binary[2:]

    # reverse string
    binary = binary[-1::-1]

    # count all unset bit '0' starting from index l-1
    # to r, where r is exclusive
    print (len([binary[i] for i in range(l-1,r) if binary[i]=='0']))

# Driver program
if __name__ == "__main__":
    n=42
    l=2
    r=5
    unsetBits(n,l,r)
```

输出:

```
2

```