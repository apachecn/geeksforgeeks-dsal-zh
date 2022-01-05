# 模方程的解的数量

> 原文:[https://www . geesforgeks . org/number-solutions-modular-equations/](https://www.geeksforgeeks.org/number-solutions-modular-equations/)

给定 A 和 B，任务是找到 X 可以取的可能值的数量，使得给定的模方程 **(A mod X) = B** 成立。这里，X 也称为模方程的解。

示例:

```
Input : A = 26, B = 2
Output : 6
Explanation
X can be equal to any of {3, 4, 6, 8,
12, 24} as A modulus any of these values
equals 2 i. e., (26 mod 3) = (26 mod 4) 
= (26 mod 6) = (26 mod 8) = .... = 2 

Input : 21 5
Output : 2
Explanation
X can be equal to any of {8, 16} as A modulus 
any of these values equals 5 i.e. (21 mod 
8) = (21 mod 16) = 5
```

如果我们仔细分析方程式 A mod X = B，很容易注意到，如果(A = B)，那么 X 可以取比 A 大无限多的值。在(甲< B), there cannot be any possible value of X for which the modular equation holds. So the only case we are left to investigate is when (A >乙)的情况下。所以现在我们深入关注这个案例。
现在，在这种情况下，我们可以使用一个众所周知的关系

```
Dividend = Divisor * Quotient + Remainder
```

我们正在寻找所有可能的除数，即给定的被除数和余数。所以，

```
We can say,
A = X * Quotient + B

Let Quotient be represented as Y
∴ A = X * Y + B
A - B = X * Y

∴ To get integral values of Y, 
we need to take all X such that X divides (A - B)

∴ X is a divisor of (A - B)
```

所以，问题简化为求(A–B)的除数，这样的除数的数目就是 X 可以取的可能值。
**但是**正如我们所知道的，一个模 X 会产生从(0 到 X–1)的值，我们必须取所有这样的 X，这样 X > B.
因此，我们可以得出结论说,( A–B)大于 B 的除数，是 X 满足一个模 X = B 所能取的所有可能值

## C++

```
/* C++ Program to find number of possible
   values of X to satisfy A mod X = B */
#include <bits/stdc++.h>
using namespace std;

/* Returns the number of divisors of (A - B)
   greater than B */
int calculateDivisors(int A, int B)
{
    int N = (A - B);
    int noOfDivisors = 0;

    for (int i = 1; i <= sqrt(N); i++) {

        // if N is divisible by i
        if ((N % i) == 0) {

            // count only the divisors greater than B
            if (i > B)
                noOfDivisors++;

            // checking if a divisor isnt counted twice
            if ((N / i) != i && (N / i) > B)
                noOfDivisors++;
        }
    }

    return noOfDivisors;
}

/* Utility function to calculate number of all
   possible values of X for which the modular
   equation holds true */
int numberOfPossibleWaysUtil(int A, int B)
{

    /* if A = B there are infinitely many solutions
       to equation  or we say X can take infinitely
       many values > A. We return -1 in this case */
    if (A == B)
        return -1;

    /* if A < B, there are no possible values of
       X satisfying the equation */
    if (A < B)
        return 0;

    /* the last case is when A > B, here we calculate
       the number of divisors of (A - B), which are
       greater than B */
    int noOfDivisors = 0;
    noOfDivisors = calculateDivisors(A, B);
    return noOfDivisors;
}

/* Wrapper function for numberOfPossibleWaysUtil() */
void numberOfPossibleWays(int A, int B)
{
    int noOfSolutions = numberOfPossibleWaysUtil(A, B);

    // if infinitely many solutions available
    if (noOfSolutions == -1) {
        cout << "For A = " << A << " and B = " << B
             << ", X can take Infinitely many values"
             " greater than "  << A << "\n";
    }

    else {
        cout << "For A = " << A << " and B = " << B
             << ", X can take " << noOfSolutions
              << " values\n";
    }
}

// Driver code
int main()
{
    int A = 26, B = 2;
    numberOfPossibleWays(A, B);
    A = 21, B = 5;
    numberOfPossibleWays(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to find number of possible
   values of X to satisfy A mod X = B */
import java.lang.*;

class GFG
{
    /* Returns the number of divisors of (A - B)
       greater than B */
    public static int calculateDivisors(int A, int B)
    {
        int N = (A - B);
        int noOfDivisors = 0;

        for (int i = 1; i <= Math.sqrt(N); i++)
        {

            // if N is divisible by i
            if ((N % i) == 0)
            {

                // count only the divisors greater than B
                if (i > B)
                    noOfDivisors++;

                // checking if a divisor isnt counted twice
                if ((N / i) != i && (N / i) > B)
                    noOfDivisors++;
            }
        }
        return noOfDivisors;
    }

    /* Utility function to calculate number of all
       possible values of X for which the modular
       equation holds true */
    public static int numberOfPossibleWaysUtil(int A, int B)
    {
        /* if A = B there are infinitely many solutions
           to equation  or we say X can take infinitely
           many values > A. We return -1 in this case */
        if (A == B)
            return -1;

        /* if A < B, there are no possible values of
           X satisfying the equation */
        if (A < B)
            return 0;

        /* the last case is when A > B, here we calculate
           the number of divisors of (A - B), which are
           greater than B */
        int noOfDivisors = 0;
        noOfDivisors = calculateDivisors(A, B);
        return noOfDivisors;
    }

    /* Wrapper function for numberOfPossibleWaysUtil() */
    public static void numberOfPossibleWays(int A, int B)
    {
        int noOfSolutions = numberOfPossibleWaysUtil(A, B);

        // if infinitely many solutions available
        if (noOfSolutions == -1)
        {
            System.out.print("For A = " + A + " and B = " + B
                             + ", X can take Infinitely many values"
                             + " greater than "  + A + "\n");
        }

        else
        {
            System.out.print("For A = " + A + " and B = " + B
                             + ", X can take " + noOfSolutions
                             + " values\n");
        }
    }
    // Driver program
    public static void main(String[] args)
    {
        int A = 26, B = 2;
        numberOfPossibleWays(A, B);
        A = 21;
        B = 5;
        numberOfPossibleWays(A, B);
    }
}
// Contributed by _omg
```

## 蟒蛇 3

```
# Python Program to find number of possible
# values of X to satisfy A mod X = B
import math

# Returns the number of divisors of (A - B)
# greater than B
def calculateDivisors (A, B):
    N = A - B
    noOfDivisors = 0

    a = math.sqrt(N)
    for i in range(1, int(a + 1)):
        # if N is divisible by i
        if ((N % i == 0)):
            # count only the divisors greater than B
            if (i > B):
                noOfDivisors +=1

            # checking if a divisor isnt counted twice
            if ((N / i) != i and (N / i) > B):
                noOfDivisors += 1;

    return noOfDivisors

# Utility function to calculate number of all
# possible values of X for which the modular
# equation holds true

def numberOfPossibleWaysUtil (A, B):
    # if A = B there are infinitely many solutions
    # to equation  or we say X can take infinitely
    # many values > A. We return -1 in this case
    if (A == B):
        return -1

    # if A < B, there are no possible values of
    # X satisfying the equation
    if (A < B):
        return 0

    # the last case is when A > B, here we calculate
    # the number of divisors of (A - B), which are
    # greater than B   

    noOfDivisors = 0
    noOfDivisors = calculateDivisors;
    return noOfDivisors

# Wrapper function for numberOfPossibleWaysUtil()
def numberOfPossibleWays(A, B):
    noOfSolutions = numberOfPossibleWaysUtil(A, B)

    #if infinitely many solutions available
    if (noOfSolutions == -1):
        print ("For A = " , A , " and B = " , B
                , ", X can take Infinitely many values"
                , " greater than "  , A)

    else:
        print ("For A = " , A , " and B = " , B
                , ", X can take " , noOfSolutions
                , " values")
# main()
A = 26
B = 2
numberOfPossibleWays(A, B)

A = 21
B = 5
numberOfPossibleWays(A, B)

# Contributed by _omg
```

## C#

```
/* C# Program to find number of possible
   values of X to satisfy A mod X = B */
using System;

class GFG
{
    /* Returns the number of divisors of (A - B)
       greater than B */
    static int calculateDivisors(int A, int B)
    {
        int N = (A - B);
        int noOfDivisors = 0;

        double a = Math.Sqrt(N);
        for (int i = 1; i <= (int)(a); i++)
        {

            // if N is divisible by i
            if ((N % i) == 0)
            {

                // count only the divisors greater than B
                if (i > B)
                    noOfDivisors++;

                // checking if a divisor isnt counted twice
                if ((N / i) != i && (N / i) > B)
                    noOfDivisors++;
            }
        }
        return noOfDivisors;
    }

    /* Utility function to calculate number of all
       possible values of X for which the modular
       equation holds true */
    static int numberOfPossibleWaysUtil(int A, int B)
    {
        /* if A = B there are infinitely many solutions
           to equation  or we say X can take infinitely
           many values > A. We return -1 in this case */
        if (A == B)
            return -1;

        /* if A < B, there are no possible values of
           X satisfying the equation */
        if (A < B)
            return 0;

        /* the last case is when A > B, here we calculate
           the number of divisors of (A - B), which are
           greater than B */
        int noOfDivisors = 0;
        noOfDivisors = calculateDivisors(A, B);
        return noOfDivisors;
    }

    /* Wrapper function for numberOfPossibleWaysUtil() */
    public static void numberOfPossibleWays(int A, int B)
    {
        int noOfSolutions = numberOfPossibleWaysUtil(A, B);

        // if infinitely many solutions available
        if (noOfSolutions == -1)
        {
            Console.Write ("For A = " + A + " and B = " + B
                           + ", X can take Infinitely many values"
                           + " greater than "  + A + "\n");
        }

        else
        {
            Console.Write ("For A = " + A + " and B = " + B
                           + ", X can take " + noOfSolutions
                           + " values\n");
        }
    }

    public static void Main()
    {
        int A = 26, B = 2;
        numberOfPossibleWays(A, B);
        A = 21;
        B = 5;
        numberOfPossibleWays(A, B);
    }
}
// Contributed by _omg
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* PHP Program to find number of possible
values of X to satisfy A mod X = B */

/* Returns the number of divisors of (A - B)
greater than B */

function calculateDivisors($A, $B)
{
    $N = ($A - $B);
    $noOfDivisors = 0;

    for ($i = 1; $i <= sqrt($N); $i++) {

        // if N is divisible by i
        if (($N % $i) == 0) {

            // count only the divisors greater than B
            if ($i > $B)
                $noOfDivisors++;

            // checking if a divisor isnt counted twice
            if (($N / $i) != $i && ($N / $i) > $B)
                $noOfDivisors++;
        }
    }

    return $noOfDivisors;
}

/* Utility function to calculate number of all
possible values of X for which the modular
equation holds true */
function numberOfPossibleWaysUtil($A, $B)
{

    /* if A = B there are infinitely many solutions
    to equation or we say X can take infinitely
    many values > A. We return -1 in this case */
    if ($A == $B)
        return -1;

    /* if A < B, there are no possible values of
    X satisfying the equation */
    if ($A < $B)
        return 0;

    /* the last case is when A > B, here we calculate
    the number of divisors of (A - B), which are
    greater than B */
    $noOfDivisors = 0;
    $noOfDivisors = calculateDivisors($A, $B);
    return $noOfDivisors;
}

/* Wrapper function for numberOfPossibleWaysUtil() */
function numberOfPossibleWays($A, $B)
{
    $noOfSolutions = numberOfPossibleWaysUtil($A, $B);

    // if infinitely many solutions available
    if ($noOfSolutions == -1) {
        echo "For A = " , $A, " and B = " ,$B,
            "X can take Infinitely many values
            greater than " , $A , "\n";
    }

    else {
        echo "For A = ", $A , " and B = " ,$B,
            " X can take ",$noOfSolutions,
            " values\n";
    }
}

// Driver code

    $A = 26; $B = 2;
    numberOfPossibleWays($A, $B);
    $A = 21; $B = 5;
    numberOfPossibleWays($A, $B);

// This code is contributed ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find number of possible
// values of X to satisfy A mod X = B

// Returns the number of divisors of (A - B)
// greater than B
function calculateDivisors(A, B)
{
    let N = (A - B);
    let noOfDivisors = 0;

    for(let i = 1; i <= Math.sqrt(N); i++)
    {

        // If N is divisible by i
        if ((N % i) == 0)
        {

            // Count only the divisors
            // greater than B
            if (i > B)
                noOfDivisors++;

            // Checking if a divisor
            // isnt counted twice
            if ((N / i) != i && (N / i) > B)
                noOfDivisors++;
        }
    }

    return noOfDivisors;
}

// Utility function to calculate number of all
// possible values of X for which the modular
// equation holds true
function numberOfPossibleWaysUtil(A, B)
{

    // If A = B there are infinitely many solutions
    // to equation  or we say X can take infinitely
    // many values > A. We return -1 in this case
    if (A == B)
        return -1;

    // If A < B, there are no possible values of
    // X satisfying the equation
    if (A < B)
        return 0;

    // The last case is when A > B, here
    // we calculate the number of divisors
    // of (A - B), which are greater than B
    let noOfDivisors = 0;
    noOfDivisors = calculateDivisors(A, B);
    return noOfDivisors;
}

// Wrapper function for numberOfPossibleWaysUtil()
function numberOfPossibleWays(A, B)
{
    let noOfSolutions = numberOfPossibleWaysUtil(A, B);

    // If infinitely many solutions available
    if (noOfSolutions == -1)
    {
        document.write("For A = " + A + " and B = " +
                       B + ", X can take Infinitely " +
                       "many values" + " greater than " +
                       A + "<br/>");
    }
    else
    {
        document.write("For A = " + A + " and B = " +
                       B + ", X can take " +
                       noOfSolutions + " values "  +
                       "<br/>");
    }
}

// Driver code
let A = 26, B = 2;
numberOfPossibleWays(A, B);

A = 21, B = 5;
numberOfPossibleWays(A, B);

// This code is contributed by splevel62

</script>
```

**输出:**

```
For A = 26 and B = 2, X can take 6 values
For A = 21 and B = 5, X can take 2 values
```

上述方法的时间复杂度无非是求(A–B)ie O 的除数的时间复杂度(√(A–B))