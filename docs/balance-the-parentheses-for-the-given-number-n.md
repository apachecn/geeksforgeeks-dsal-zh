# 平衡给定数字 N 的括号

> 原文:[https://www . geeksforgeeks . org/给定数字圆括号平衡-n/](https://www.geeksforgeeks.org/balance-the-parentheses-for-the-given-number-n/)

给定一个数字 **N** ，任务是将最小数量的左圆括号和右圆括号插入到数字 **N** 中，这样得到的字符串是平衡的，并且每个数字 **D** 都正好在匹配圆括号的 **D** 对中。

**示例:**

> **输入:** N = 312
> **输出:**((3)1(2))
> **说明:**
> 数字中的每个数字都在 D 括号内。
> 还有其他可能的字符串，如((3)))(1)((2))，但获得的字符串是可以用最少数量的括号组成的字符串。
> 
> **输入:** N = 111000
> **输出:** (111)000
> **说明:**
> 数字中的每个数字都正好在 D 括号内。
> 还有其他可能的字符串，如(1)(1)(1)000、(11)(1)000，但获得的字符串是可以用最少数量的括号组成的字符串。

**方法:**思路是用一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)来记录需要添加的[括号](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)的个数。

对于任何数字，只能通过将数字嵌套在括号中来添加最小数量的括号。

**例如:**设 N = 321。

*   最初，会创建一个空数组 A[]。
*   给定的数字按数字方式迭代。
*   最初，为了存储数字，在数组中添加 D 个左括号。因此，对于数字 3，在数组中添加了 3 个左括号。
*   在下一次迭代中，该数字可以大于或小于前一个数字。如果下一个数字较小，如上面示例中的 2，则 3–2 = 1 括号被关闭。
*   同样，如果下一个数字更大，括号的绝对差数将被打开。
*   对给定数字 n 中的所有数字重复上述两个步骤。最后，得到的字符串由最少数量的括号组成。

下面是上述方法的实现:

```
# Python program to find the balanced
# parentheses using the given number

# Function to find the balanced 
# parentheses using the given number
def balance(m):

    # Making the list of the
    # given number
    m = [int(i) for i in m]

    # Empty list to store the 
    # parentheses
    n = []

    # Iterating through the 
    # digits of the number
    for i in m: 

        # Calculating the difference between
        # opening and closing braces for the 
        # digit
        if (n.count('(')-n.count(')'))<= i:

            # If the next digit is greater, 
            # then open the brackets
            while (n.count('(')-n.count(')')) != i:
                n.append('(')         
            n.append(i)     

        # Similarly, find the difference 
        # between opening and closing braces
        elif (n.count('(')-n.count(')'))>i:

            # If the next digit is smaller,
            # then close the brackets
            while (n.count('(')-n.count(')'))!= i:
                n.append(')')
            n.append(i) 

    # Finally, close the remaining brackets
    while (n.count('(')-n.count(')'))!= 0:
        n.append(')')

    # Returning the string
    return ''.join(map(str, n))

# Driver code
if __name__ == "__main__":

    N = 312

    print(balance(str(N)))
```

**Output:**

```
(((3))1(2))

```

**时间复杂度:** *O(K <sup>2</sup> )* ，其中 K 为数字 n 的位数之和