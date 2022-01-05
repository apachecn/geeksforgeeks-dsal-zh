# 无符号整数不可恢复除法算法的实现

> 原文:[https://www . geeksforgeeks . org/无符号整数除法算法的实现/](https://www.geeksforgeeks.org/implementation-of-non-restoring-division-algorithm-for-unsigned-integer/)

在前一篇文章中，我们已经讨论了[非恢复除法算法](https://www.geeksforgeeks.org/non-restoring-division-unsigned-integer/)。在本文中，我们将讨论该算法的实现。

非恢复除法算法用于除法两个无符号整数。这个算法的另一种形式是[恢复除法](https://www.geeksforgeeks.org/restoring-division-algorithm-unsigned-integer/)。该算法不同于其他算法，因为这里没有恢复的概念，并且该算法没有恢复除法算法复杂。设被除数 Q = 0110，除数 M = 0100。下表演示了给定值的逐步解决方案:

|  | 累加器-A(0) | 股息-问题(6) | 状态 |
| --- | --- | --- | --- |
| 

```
Initial Values
```

 | 0000 | 0111 | 0101(M) |
| 

```
Step1:Left-Shift
```

 | 0000 | 111_ |  |
| 运营:上午 | One thousand and eleven | One thousand one hundred and ten | 下一步不成功(-ve)
A+M |
| 

```
Step2:Left-Shift
```

 | 0111 | 110_ |  |
| 运营:A + M | One thousand one hundred | One thousand one hundred | 下一步不成功(-ve)
A+M |
| 

```
Step3:Left-Shift
```

 | One thousand and one | 100_ |  |
| 运营:A + M | One thousand one hundred and ten | One thousand | 下一步不成功(-ve)
A+M |
| 

```
Step4:Left-Shift
```

 | One thousand one hundred and one | 000_ |  |
| 运营:A + M | 0010 | 0001 | 成功(+ve) |
|  | 余数(2) | 商(1) |  |

**方法:**从上面的解决方案来看，思路是观察计算所需商和余数所需的步数等于被除数中的位数。最初，假设被除数为 Q，除数为 M，累加器 A = 0。因此:

1.  每走一步，向左移动红利 1 个位置。
2.  从 A(A–M)中减去除数。
3.  如果结果是肯定的，那么该步骤被称为“成功”。在这种情况下，商位将为“1”，并且不需要恢复。所以，下一步也将是减法。
4.  如果结果是否定的，那么该步骤被称为“不成功”。在这种情况下，商位将为“0”。这里，恢复不像恢复分割算法那样执行。相反，下一步将是加法代替减法。
5.  对被除数的所有位重复步骤 1 至 4。

下面是上述方法的实现:

```
# Python program to divide two 
# unsigned integers using 
# Non-Restoring Division Algorithm

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
# Non-Restoring Division Algorithm
def nonRestoringDivision(Q, M, A):

    # Computing the length of the
    # number
    count = len(M)

    comp_M = compliment(M)

    # Variable to determine whether 
    # addition or subtraction has 
    # to be computed for the next step
    flag = 'successful'    

    # Printing the initial values
    # of the accumulator, dividend
    # and divisor
    print ('Initial Values: A:', A, 
           ' Q:', Q, ' M:', M)

    # The number of steps is equal to the 
    # length of the binary number
    while (count):

        # Printing the values at every step
        print ("\nstep:", len(M)-count + 1, 
               end = '')

        # Step1: Left Shift, assigning LSB of Q 
        # to MSB of A.
        print (' Left Shift and ', end = '')
        A = A[1:] + Q[0]

        # Choosing the addition
        # or subtraction based on the
        # result of the previous step
        if (flag == 'successful'):
            A = add(A, comp_M)
            print ('subtract: ')
        else:
            A = add(A, M)
            print ('Addition: ')

        print('A:', A, ' Q:', 
              Q[1:]+'_', end ='')

        if (A[0] == '1'):

            # Step is unsuccessful and the 
            # quotient bit will be '0'
            Q = Q[1:] + '0'
            print ('  -Unsuccessful')

            flag = 'unsuccessful'
            print ('A:', A, ' Q:', Q, 
                   ' -Addition in next Step')

        else:

            # Step is successful and the quotient 
            # bit will be '1'
            Q = Q[1:] + '1'
            print ('  Successful')

            flag = 'successful'
            print ('A:', A, ' Q:', Q, 
                   ' -Subtraction in next step')
        count -= 1
    print ('\nQuotient(Q):', Q, 
           ' Remainder(A):', A)

# Driver code
if __name__ == "__main__":

    dividend = '0111'
    divisor = '0101'

    accumulator = '0' * len(dividend)

    nonRestoringDivision(dividend,
                         divisor, 
                         accumulator)
```

**Output:**

```
Initial Values: A: 0000  Q: 0111  M: 0101

step: 1 Left Shift and subtract: 
A: 1011  Q: 111_  -Unsuccessful
A: 1011  Q: 1110  -Addition in next Step

step: 2 Left Shift and Addition: 
A: 1100  Q: 110_  -Unsuccessful
A: 1100  Q: 1100  -Addition in next Step

step: 3 Left Shift and Addition: 
A: 1110  Q: 100_  -Unsuccessful
A: 1110  Q: 1000  -Addition in next Step

step: 4 Left Shift and Addition: 
A: 0010  Q: 000_  Successful
A: 0010  Q: 0001  -Subtraction in next step

Quotient(Q): 0001  Remainder(A): 0010

```