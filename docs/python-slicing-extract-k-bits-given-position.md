# Python 切片|从给定位置提取“k”位

> 原文:[https://www . geesforgeks . org/python-slicing-extract-k-bits-给定位置/](https://www.geeksforgeeks.org/python-slicing-extract-k-bits-given-position/)

如何从数字中给定的位置“p”提取“k”位？

**例:**

```
Input : number = 171
             k = 5 
             p = 2
Output : The extracted number is 21
171 is represented as 10101011 in binary,
so, you should get only 10101 i.e. 21.

Input : number = 72
            k = 5 
            p = 1
Output : The extracted number is 8
72 is represented as 1001000 in binary,
so, you should get only 01000 i.e 8.

```

我们有这个问题的现有解决方案，请参考[从数字](https://www.geeksforgeeks.org/extract-k-bits-given-position-number/)链接中的给定位置提取“k”位。我们可以使用[切片](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)在 python 中快速解决这个问题。方法很简单，

1.  Use the [bin ()](https://www.geeksforgeeks.org/bin-in-python/) function to convert the given number into its binary, and delete the first two characters' 0b' from it, because the bin function appends' 0b' as a prefix in the output binary string.
2.  We need to extract k bits from the start position p from the right, which means that the end index of the extracted substring will be **end = (len (binary)–p)** , and the start index will be **start = end–k+1** of the original binary string.
3.  Convert the extracted substring to decimal again.

```
# Function to extract ‘k’ bits from a given
# position in a number

def extractKBits(num,k,p):

     # convert number into binary first
     binary = bin(num)

     # remove first two characters
     binary = binary[2:]

     end = len(binary) - p
     start = end - k + 1

     # extract k  bit sub-string
     kBitSubStr = binary[start : end+1]

     # convert extracted sub-string into decimal again
     print (int(kBitSubStr,2))

# Driver program
if __name__ == "__main__":
    num = 171
    k = 5
    p = 2
    extractKBits(num,k,p)

```

**输出:**

```
21

```