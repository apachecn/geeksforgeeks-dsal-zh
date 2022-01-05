# 无符号整数恢复除法算法的实现

> 原文:[https://www . geeksforgeeks . org/恢复无符号整数除法算法的实现/](https://www.geeksforgeeks.org/implementation-of-restoring-division-algorithm-for-unsigned-integer/)

在前一篇文章中，我们已经讨论了[恢复除法算法](https://www.geeksforgeeks.org/restoring-division-algorithm-unsigned-integer/)。在本文中，我们将讨论该算法的实现。

[恢复除法算法](https://www.geeksforgeeks.org/restoring-division-algorithm-unsigned-integer/)用于对两个无符号整数进行除法运算。该算法用于计算机组织与体系结构。这种算法被称为恢复，因为它在每次或一些迭代后恢复**累加器(A)** 的值。还有一种类型，即[不恢复除法算法](https://www.geeksforgeeks.org/non-restoring-division-unsigned-integer/)不恢复 A 的值。设被除数 Q = 0110，除数 M = 0100。下表演示了给定值的逐步解决方案:

|  | 累加器-A(0) | 股息-问题(6) | 状态 |
| --- | --- | --- | --- |
| 初始值 | 0000 | 0110 | 0100 |
| 第一步:向左移动 | 0000 | 110_ |  |
| 上午 | One thousand one hundred |  | 不成功(-ve) |
| 恢复 | 0000 | One thousand one hundred |  |
| 第二步:向左移动 | 0001 | 100_ |  |
| 上午 | One thousand one hundred and one |  | 不成功(-ve) |
| 恢复 | 0001 | One thousand |  |
| 第三步:向左移动 | 0011 | 000_ |  |
| 上午 | One thousand one hundred and eleven |  | 不成功(-ve) |
| 恢复 | 0011 | 0000 |  |
| 第四步:向左移动 | 0110 | 000_ |  |
| 上午 | 0010 | 0001 | 成功(+ve) |
|  | 余数(2) | 商(1) |  |

**方法:**从上面的解决方案来看，思路是观察计算所需商和余数所需的步数等于被除数中的位数。最初，假设被除数为 Q，除数为 M，累加器 A = 0。因此:

1.  每走一步，向左移动红利 1 个位置。
2.  从 A(A–M)中减去除数。
3.  如果结果是肯定的，那么该步骤被认为是成功的。在这种情况下，商位将为“1”，不需要恢复。
4.  如果结果是否定的，那么该步骤被认为是不成功的。在这种情况下，商位将为“0”，需要恢复。
5.  对被除数的所有位重复上述步骤。

**注意:**这里，通过将除数加回 a 来执行恢复。

```
# Python program to divide two 
# unsigned integers using 
# Restoring Division Algorithm

# Function to add two binary numbers
def add(A, M):
    carry = 0
    Sum = ''

    # Iterating through the number
    # A. Here, it is assumed that 
    # the length of both the numbers
    # is same
    for i in range (len(A)-1, -1, -1):

        # Adding the values at both 
        # the indices along with the 
        # carry
        temp = int(A[i]) + int(M[i]) + carry

        # If the binary number exceeds 1
        if (temp>1):
            Sum += str(temp % 2)
            carry = 1
        else:
            Sum += str(temp)
            carry = 0

    # Returning the sum from 
    # MSB to LSB
    return Sum[::-1]    

# Function to find the compliment
# of the given binary number
def compliment(m):
    M = ''

    # Iterating through the number
    for i in range (0, len(m)):

        # Computing the compliment
        M += str((int(m[i]) + 1) % 2)

    # Adding 1 to the computed 
    # value
    M = add(M, '0001')
    return M

# Function to find the quotient
# and remainder using the 
# Restoring Division Algorithm
def restoringDivision(Q, M, A):

    # Computing the length of the
    # number
    count = len(M)

    # Printing the initial values
    # of the accumulator, dividend
    # and divisor
    print ('Initial Values: A:', A, 
           ' Q:', Q, ' M:', M)

    # The number of steps is equal to the 
    # length of the binary number
    while (count):

        # Printing the values at every step
        print ("\nstep:", len(M)-count + 1, end = '')

        # Step1: Left Shift, assigning LSB of Q 
        # to MSB of A.
        print (' Left Shift and Subtract: ', end = '')
        A = A[1:] + Q[0]

        # Step2: Subtract the Divisor from A 
        # (Perform A - M).
        comp_M = compliment(M)

        # Taking the complement of M and 
        # adding to A.
        A = add(A, comp_M)
        print(' A:', A)
        print('A:', A, ' Q:', Q[1:]+'_', end ='')

        if (A[0] == '1'):

            # The step is unsuccessful 
            # and the quotient bit 
            # will be '0'
            Q = Q[1:] + '0'
            print ('  -Unsuccessful')

            # Restoration of A is required
            A = add(A, M)
            print ('A:', A, ' Q:', Q, ' -Restoration')

        else:

            # Else, the step is successful 
            # and the quotient bit 
            # will be '1'
            Q = Q[1:] + '1'
            print (' Successful')

            # No Restoration of A.
            print ('A:', A, ' Q:',
                   Q, ' -No Restoration')
        count -= 1

    # Printing the final quotient 
    # and remainder of the given 
    # dividend and divisor. 
    print ('\nQuotient(Q):', Q,
           ' Remainder(A):', A)

# Driver code
if __name__ == "__main__":

    dividend = '0110'
    divisor = '0100'

    accumulator = '0' * len(dividend)

    restoringDivision(dividend,
                      divisor, 
                      accumulator)
```

**Output:**

```
Initial Values: A: 0000  Q: 0110  M: 0100

step: 1 Left Shift and Subtract:  A: 1100
A: 1100  Q: 110_  -Unsuccessful
A: 0000  Q: 1100  -Restoration

step: 2 Left Shift and Subtract:  A: 1101
A: 1101  Q: 100_  -Unsuccessful
A: 0001  Q: 1000  -Restoration

step: 3 Left Shift and Subtract:  A: 1111
A: 1111  Q: 000_  -Unsuccessful
A: 0011  Q: 0000  -Restoration

step: 4 Left Shift and Subtract:  A: 0010
A: 0010  Q: 000_ Successful
A: 0010  Q: 0001  -No Restoration

Quotient(Q): 0001  Remainder(A): 0010

```