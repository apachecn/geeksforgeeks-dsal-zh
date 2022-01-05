# Python |计数范围内的设置位

> 原文:[https://www.geeksforgeeks.org/python-count-set-bits-range/](https://www.geeksforgeeks.org/python-count-set-bits-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是在 **n** 的二进制表示中对 **l** 到 **r** 范围内的置位位数进行计数，即从最右边的 **lth** 位计数到最右边的 **rth** 位。

**约束:** 1 < = l < = r < =二进制表示中的位数 **n** 。

示例:

```
Input : n = 42, l = 2, r = 5
Output : 2
(42)<sub>10</sub> = (101010)2
There are '2' set bits in the range 2 to 5.

Input : n = 79, l = 1, r = 4
Output : 4

```

这个问题我们已经有了解决方案，请参考[在一定范围内计数设置位](https://www.geeksforgeeks.org/count-set-bits-range/)链接。我们可以用 Python 快速解决这个问题。方法很简单，

1.  Use the [bin (num)](https://www.geeksforgeeks.org/bin-in-python/) function to convert decimal to binary.
2.  Now delete the first two characters of the output binary string, because by default, the bin function appends' 0b' to the output string as a prefix.
3.  Starting from index **(l-1)** , the string is sliced into index **r** and inverted, and then the setting bits in the middle are counted.

```
# Function to count set bits in a range

def countSetBits(n,l,r):

    # convert n into it's binary
    binary = bin(n)

    # remove first two characters
    binary = binary[2:]

    # reverse string
    binary = binary[-1::-1]

    # count all set bit '1' starting from index l-1
    # to r, where r is exclusive
    print (len([binary[i] for i in range(l-1,r) if binary[i]=='1']))

# Driver program
if __name__ == "__main__":
    n=42
    l=2
    r=5
    countSetBits(n,l,r)
```

输出:

```
2

```