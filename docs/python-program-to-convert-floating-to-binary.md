# Python 程序将浮点转换为二进制

> 原文:[https://www . geesforgeks . org/python-程序到转换-浮点到二进制/](https://www.geeksforgeeks.org/python-program-to-convert-floating-to-binary/)

Python 没有提供任何内置的方法来轻松地将浮点十进制数转换为二进制数。所以，让我们手动操作。
**做法:**
将一个浮点十进制数转换为二进制，先将整数部分转换为二进制形式，再将小数部分转换为二进制形式，最后将两个结果合并得到最终答案。
对于整数部分，继续将数字除以 2，并记下余数，直到且除非被除数小于 2。如果是这样，停下来，把所有的余数抄在一起。
对于小数部分，继续将小数部分乘以 2，直到 0 作为小数部分。第一次相乘后，记下整数部分，再次将新值的小数部分乘以 2。继续这样做，直到达到一个完美的数字。

> **以上步骤可以写成:**
> 1(基数 10) = 1(基数 2)和. 234(基数 10) = .0011(基数 2)
> 现在，为了得到 1.234 的二进制数，将两个结果合并为一个完整的数。
> (1)10 =(1)2
> (. 234)10 =(. 0011)2
> (1.234)10 =(1.0011……)2
> (1.234)10 =(1.0011)2【约。]

下面是实现:

## 蟒蛇 3

```
# Python program to convert float
# decimal to binary number

# Function returns octal representation
def float_bin(number, places = 3):

    # split() separates whole number and decimal
    # part and stores it in two separate variables
    whole, dec = str(number).split(".")

    # Convert both whole number and decimal 
    # part from string type to integer type
    whole = int(whole)
    dec = int (dec)

    # Convert the whole number part to it's
    # respective binary form and remove the
    # "0b" from it.
    res = bin(whole).lstrip("0b") + "."

    # Iterate the number of times, we want
    # the number of decimal places to be
    for x in range(places):

        # Multiply the decimal value by 2
        # and separate the whole number part
        # and decimal part
        whole, dec = str((decimal_converter(dec)) * 2).split(".")

        # Convert the decimal part
        # to integer again
        dec = int(dec)

        # Keep adding the integer parts
        # receive to the result variable
        res += whole

    return res

# Function converts the value passed as
# parameter to it's decimal representation
def decimal_converter(num):
    while num > 1:
        num /= 10
    return num

# Driver Code

# Take the user input for
# the floating point number
n = input("Enter your floating point value : \n")

# Take user input for the number of
# decimal places user want result as
p = int(input("Enter the number of decimal places of the result : \n"))

print(float_bin(n, places = p))
```

**输出:**

```
Enter your floating point value : 
1.234
Enter the number of decimal places of the result :
4

1.0011
```

```
Enter your floating point value : 
11.234
Enter the number of decimal places of the result : 
4

1011.0011
```