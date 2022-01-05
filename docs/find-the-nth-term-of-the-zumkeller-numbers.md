# 求祖姆凯勒数的第 n 项

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-zum Keller-numbers/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-zumkeller-numbers/)

**祖姆凯勒数**是一组数，其除数可以被分成两个不相交的集合，这两个集合的和等于同一个值。最初的几个祖姆凯勒数字是 **6，12，20，24，28，30，40，42，48，54，…** 。

在这篇文章中，我们将找到第 N <sup>个</sup>祖姆凯勒数。

**找到第 N <sup>个</sup>祖姆凯勒号:**给定一个号 **N** ，任务是找到第 N <sup>个</sup>祖姆凯勒号。

**示例:**

> **输入:** N = 2
> **输出:** 12
> **解释:**
> 第二个祖姆凯勒数是 12。
> 
> **输入:**N = 5
> T3】输出: 28

**方法:**按照以下步骤计算答案。

1.  得到数字 n。
2.  循环迭代，从 i = 1 开始，直到找到第 n 个 Zumkeller 数。
3.  检查号码“I”是否是 zumkeller 号码。
4.  如果是，则对 i+1 重复上述步骤，并递增计数器。
5.  如果否，则对 i+1 重复上述步骤，不增加计数器。
6.  最后，当计数器等于数 N 时，这个数就是第 N 个 zumkeller 数。打印“I”的值并打破循环。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to find the
# N-th Zumkeller number

# Function to find all the
# divisiors
def Divisors(n) : 
    l = []
    i = 1
    while i <= n : 
        if (n % i == 0) : 
            l.append(i)
        i = i + 1
    return l

# Function to check if the sum 
# of the subset of divisors is
# equal to sum / 2 or not
def PowerSet(arr, n, s): 

    # List to find all the 
    # subsets of the given set. 
    # Any repeated subset is 
    # considered only  
    # once in the output 
    _list = [] 

    # Run a counter i  
    for i in range(2**n): 
        subset = "" 

        # Consider each element 
        # in the set 
        for j in range(n): 

            # Check if j-th bit in 
            # the i is set.  
            # If the bit is set, 
            # we consider  
            # j-th element from set 
            if (i & (1 << j)) != 0: 
                subset += str(arr[j]) + "|"

        # Check if the subset is 
        # encountered for the first time. 
        if subset not in _list and len(subset) > 0: 
            _list.append(subset) 

    # Consider every subset 
    for subset in _list: 
        sum = 0

        # Split the subset and 
        # sum of its elements 
        arr = subset.split('|') 
        for string in arr[:-1]: 
            sum += int(string)

            # If the sum is equal
            # to S
            if sum == s:
                return True

    return False

# Function to check if a number 
# is a Zumkeller number
def isZumkeller(n):

    # To find all the divisors 
    # of a number N
    d = Divisors(n)

    # Finding the sum of
    # all the divisors
    s = sum(d)

    # Check for the condition that 
    # sum must be even and the 
    # maximum divisor is less than
    # or equal to sum / 2. 
    # If the sum is odd and the 
    # maximum divisor is greater than
    # sum / 2, then it is not possible 
    # to divide the divisors into 
    # two sets
    if not s % 2 and max(d) <= s / 2:

        # For all the subsets of
        # the divisors
        if PowerSet(d, len(d), s / 2) :
                return True

    return False

# Function to print N-th 
# Zumkeller number
def printZumkellers(N):
    val = 0
    ans = 0

    # Iterating through all
    # the numbers
    for n in range(1, 10**5):

        # Check if n is a 
        # Zumkeller number
        if isZumkeller(n):
            ans = n
            val += 1

            # Check if N-th Zumkeller number
            # is obtained or not
            if val >= N:
                break               

    print(ans)

# Driver code
if __name__ == '__main__':

    N = 4

    printZumkellers(N)
```

**Output:**

```
24

```