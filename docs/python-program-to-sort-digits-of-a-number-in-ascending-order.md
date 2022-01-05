# Python 程序对数字的数字进行升序排序

> 原文:[https://www . geesforgeks . org/python-程序-按升序对数字进行排序/](https://www.geeksforgeeks.org/python-program-to-sort-digits-of-a-number-in-ascending-order/)

给定一个整数 **N** ，任务是[按照升序](https://www.geeksforgeeks.org/smallest-number-rearranging-digits-given-number/)对数字进行排序。打印排除前导零后获得的新数字。

**示例:**

> **输入:** N = 193202042
> **输出:** 1222349
> **说明:**
> 对给定号码的所有数字进行排序生成 001222349。
> 去除前导 0 后得到的最终数字为 1222349。
> 
> **输入:** N = 78291342023
> **输出:** 1222334789

**方法:**按照以下步骤解决问题:

*   [将给定的整数转换成它的等价字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)
*   [使用](https://www.geeksforgeeks.org/sort-string-characters/) [**join()**](https://www.geeksforgeeks.org/join-function-python/) 和 [**对字符串**](https://www.geeksforgeeks.org/sorted-function-python/)中的字符进行排序() **。**
*   [使用类型转换](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)将字符串转换为整数
*   打印得到的整数。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to
# implement the above approach

# Function to sort the digits
# present in the number n
def getSortedNumber(n):

    # Convert to equivalent string
    number = str(n)

    # Sort the string
    number = ''.join(sorted(number))

    # Convert to equivalent integer
    number = int(number)

    # Return the integer
    return number

# Driver Code
n = 193202042

print(getSortedNumber(n))
```

**Output:**

```
1222349

```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*