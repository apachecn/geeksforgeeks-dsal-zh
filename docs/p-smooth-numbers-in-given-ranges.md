# P–给定范围内的平滑数字

> 原文:[https://www . geesforgeks . org/p-给定范围内的平滑数字/](https://www.geeksforgeeks.org/p-smooth-numbers-in-given-ranges/)

给定多个范围**【L，R】**和一个素数 P，我们需要在给定的单个范围内找到所有**[P-光滑数](https://www.geeksforgeeks.org/p-smooth-numbers-p-friable-number/)** 。

> **什么是 P–光滑数？**
> 如果一个整数的最大质因数< = p. 1(被 [OEIS](http://oeis.org/wiki/P-smooth_numbers) 认为)对于任何可能的 P 值都是 P-光滑数，因为它没有任何质因数。

示例:

```
Input : p = 7   
        ranges[] = {[1, 17],  [10, 25]}

Output : 
For first range : 1 2 3 4 5 6 7 8 9 12 14 15 16
For second range : 15 16 18 20 21 24 25
Explanation : Largest prime factors of numbers
printed above are less than or equal to 7.

```

假设，我们正在检查 7-平滑数字。
1。考虑一个整数 56。这里，56 = 2 * 2 * 2 * 7。
所以，56 有两个质因数(2 和 7)，它们是< =7。所以，56 是 7-光滑数。
2。考虑另一个整数 66。这里，66 = 2 * 3 * 11。
66 有三个质因数(2、3、11)。其中 11 > 7。所以 66 不是 7-光滑数。

**蛮力法:**让 P 和范围[L，R]给定。这里 L < = R .创建一个循环并检查包含范围内的所有数字[L : R]。如果该数字具有最大质因数< = p，则打印该数字(即 P 平滑数字)。使用**最大质因数(n)** 函数计算其最大质因数/除数。

**有效方法:**想法是预先计算所有范围最大值的 p 光滑数。一旦我们进行了预先计算，我们就可以一个接一个地快速打印所有范围。

```
# Python program to display p-smooth 
# number in given range.
# P-smooth numbers' array
p_smooth = [1] 

def maxPrimeDivisor(n):

    # Returns Maximum Prime 
    # Divisor of n
    MPD = -1

    if n == 1 : 
        return 1

    while n % 2 == 0:
        MPD = 2
        n = n // 2

    # math.sqrt(n) + 1
    size = int(n ** 0.5) + 1
    for odd in range( 3, size, 2 ):
        while n % odd == 0:

            # Make sure no multiples 
            # of prime, enters here
            MPD = odd
            n = n // odd

    # When n is prime itself
    MPD = max (n, MPD) 

    return MPD 

def generate_p_smooth(p, MAX_LIMIT):    

    # generates p-smooth numbers.
    global p_smooth

    for i in range(2, MAX_LIMIT + 1):
        if maxPrimeDivisor(i) <= p:

            # Satisfies the condition 
            # of p-smooth number
            p_smooth.append(i)

def find_p_smooth(L, R):

    # finds p-smooth number in the
    # given [L:R] range.
    global p_smooth
    if L <= p_smooth[-1]:

        # If user input exceeds MAX_LIMIT
        # range, no checking
        for w in p_smooth :
            if w > R : break
            if w >= L and w <= R :

                # Print P-smooth numbers 
                # within range : L to R.
                print(w, end =" ")

        print()

# p_smooth number : p = 7
# L <= R
p = 7
L, R = 1, 100

# Maximum possible value of R
MAX_LIMIT = 1000

# generate the p-smooth numbers
generate_p_smooth(p, MAX_LIMIT) 

# Find an print the p-smooth numbers
find_p_smooth(L, R) 
```