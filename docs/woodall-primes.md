# 木本保费

> 原文:[https://www.geeksforgeeks.org/woodall-primes/](https://www.geeksforgeeks.org/woodall-primes/)

**伍达尔素数**是素数，也是[伍德豪尔数](https://www.geeksforgeeks.org/woodall-number/)。

### 找出小于 N 的伍达尔素数

给定一个数字 **N** ，打印所有小于或等于 N 的伍达尔素数

**示例:**

> **输入:**N = 10
> T3】输出: 7
> 
> **输入:**N = 500
> T3】输出: 7，23，383

**方法:**想法是使用厄拉多塞的[筛来检查一个数是否是质数。然后，迭代从 1 到 N 的整数，对于每个数，检查它是否是质数，它是否是伍德尔数。如果一个数也是质数，那么它就是伍达尔质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述算法的实现:

## 蟒蛇 3

```
# Python3 implementation to print all Woodall  
# primes smaller than or equal to n.  

# Function to check if a number 
# N is Woodall   
def isWoodall(x) : 

    # If number is even, return false. 
    if (x % 2 == 0) : 
        return False

    # If x is 1, return true. 
    if (x == 1) : 
        return True

    x = x + 1  # Add 1 to make x even 

    # While x is divisible by 2 
    p = 0
    while (x % 2 == 0) : 

        # Divide x by 2 
        x = x / 2

        # Count the power 
        p = p + 1

        # If at any point power and  
        # x became equal, return true. 
        if (p == x) : 
            return True

    return False

# Function to generate all primes and checking  
# whether number is Woodall or not  
def printWoodallPrimesLessThanN(n): 

    # Create a boolean array "prime[0..n]" and  
    # initialize all entries it as true. A value  
    # in prime[i] will finally be false if i is  
    # Not a prime, else true.  
    prime = [True] * (n + 1);  
    p = 2; 
    while (p * p <= n): 

        # If prime[p] is not changed,  
        # then it is a prime  
        if (prime[p]):  

            # Update all multiples of p  
            for i in range(p * 2, n + 1, p):  
                prime[i] = False; 
        p += 1; 

    # Print all Woodall prime numbers  
    for p in range(2, n + 1):  

        # checking whether the given number  
        # is prime Woodall or not  
        if (prime[p] and isWoodall(p)):  
            print(p, end = " ");  

# Driver Code  
n = 1000; 
printWoodallPrimesLessThanN(n)
```

**Output:**

```
7 23 383

```