# 将公里转换为英里的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-convert-km-miles/](https://www.geeksforgeeks.org/python-program-convert-kilometers-miles/)

**公里**是公制中相当于 1000 米的长度单位。

**英里**也是长度单位，等于 1760 码。

示例:

```
Input: 5.5 
Output: 3.418 

Input: 6.5
Output: 4.039

```

**公式:**

```
1 kilometer equals 0.62137 miles.
Miles = kilometer * 0.62137   
Kilometer = Miles / 0.62137

```

```
# Python3 program to convert
# kilometers to miles

# driver code
kilometers = 5.5

# conversion factor
conv = 0.621371

# calculate miles
miles = kilometers * conv
print('%0.3f kilometers is equal to %0.3f miles' %(kilometers,miles))

kilometers = 6.5

# calculate miles
miles = kilometers * conv
print('%0.3f kilometers is equal to %0.3f miles' %(kilometers,miles))
```

输出:

```
5.500 kilometers is equal to 3.418 miles
6.500 kilometers is equal to 4.039 miles

```