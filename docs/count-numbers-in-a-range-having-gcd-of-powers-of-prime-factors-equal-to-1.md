# 在质因数的幂的 GCD 等于 1 的范围内计数数字

> 原文:[https://www . geesforgeks . org/count-numbers-in-a-range-having-gcd-of-power-of-prime-factors-equal-1/](https://www.geeksforgeeks.org/count-numbers-in-a-range-having-gcd-of-powers-of-prime-factors-equal-to-1/)

给定由两个正整数 **L** 和 **R** 表示的范围。任务是从质因数的幂等于 1 的范围 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 中计算数字。换句话说，如果一个数 **X** 有其形式**2<sup>p<sub>1</sub>T12】* 3<sup>p<sub>2</sub>T16】* 5<sup>p<sub>3</sub>T20】*……</sup></sup></sup>**那么 **p <sub>1</sub> 的 GCD，p <sub>2</sub> ，p<sub>3【T27</sub>**

**示例:**

> **输入:** L = 2，R = 5
> **输出:** 3
> 2，3 和 5 是质因数的幂的 GCD 等于 1 的所需数字。
> 2 = 2<sup>1</sup>
> 3 = 3<sup>1</sup>
> 5 = 5<sup>1</sup>
> 
> **输入:** L = 13，R = 20
> T3】输出: 7

**先决条件:** [范围内的完美幂](https://www.geeksforgeeks.org/numbers-within-range-can-expressed-power-two-numbers/)
**天真方法:**迭代从 **L** 到 **R** 的所有数字，并对每个数字进行质因数分解，然后计算质因数幂的 GCD。如果 **GCD = 1** ，增加一个**计数**变量，最后作为答案返回。

**有效方法:**这里的关键思想是注意到有效数不是完美幂，因为质因数数的幂是这样的，它们的 GCD 总是大于 1。换句话说，所有的完美幂都不是有效数字。
**例如**

> 2500 是完美幂，其素因子分解为 2500 = 2 <sup>2</sup> * 5 <sup>4</sup> 。现在(2，4) = 2 的 GCD 大于 1。
> 如果某个数在它的素因子分解中有某个因子的 x <sup>次方</sup>次方，那么其他素因子的次方必须是 x 的倍数，这个数才是无效的。

因此，我们可以找到位于该范围内的[完美幂](https://www.geeksforgeeks.org/numbers-within-range-can-expressed-power-two-numbers/)的总数，并将其从总数中减去。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>

using namespace std;

#define N 1000005
#define MAX 1e18

// Vector to store powers greater than 3
vector<long int> powers;

// Set to store perfect squares
set<long int> squares;

// Set to store powers other than perfect squares
set<long int> s;

void powersPrecomputation()
{
    for (long int i = 2; i < N; i++) {

        // Pushing squares
        squares.insert(i * i);

        // if the values is already a perfect square means
        // present in the set
        if (squares.find(i) != squares.end())
            continue;

        long int temp = i;

        // Run loop until some power of current number
        // doesn't exceed MAX
        while (i * i <= MAX / temp) {
            temp *= (i * i);

            // Pushing only odd powers as even power of a number 
            // can always be expressed as a perfect square 
            // which is already present in set squares
            s.insert(temp);
        }
    }

    // Inserting those sorted
    // values of set into a vector
    for (auto x : s)
        powers.push_back(x);
}

long int calculateAnswer(long int L, long int R)
{

    // Precompute the powers
    powersPrecomputation();

    // Calculate perfect squares in
    // range using sqrtl function
    long int perfectSquares = floor(sqrtl(R)) - floor(sqrtl(L - 1));

    // Calculate upper value of R
    // in vector using binary search
    long int high = upper_bound(powers.begin(),
                                powers.end(), R)
                    - powers.begin();

    // Calculate lower value of L
    // in vector using binary search
    long int low = lower_bound(powers.begin(),
                               powers.end(), L)
                   - powers.begin();

    // Calculate perfect powers
    long perfectPowers = perfectSquares + (high - low);

    // Compute final answer
    long ans = (R - L + 1) - perfectPowers;
    return ans;
}

// Driver Code
int main()
{
    long int L = 13, R = 20;
    cout << calculateAnswer(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above idea
import java.util.*;

class GFG 
{

    static int N = 1000005;
    static long MAX = (long) 1e18;

    // Vector to store powers greater than 3
    static Vector<Long> powers = new Vector<>();

    // Set to store perfect squares
    static TreeSet<Long> squares = new TreeSet<>();

    // Set to store powers other than perfect squares
    static TreeSet<Long> s = new TreeSet<>();

    static void powersPrecomputation()
    {
        for (long i = 2; i < N; i++)
        {

            // Pushing squares
            squares.add(i * i);

            // if the values is already a perfect square means
            // present in the set
            if (squares.contains(i))
                continue;

            long temp = i;

            // Run loop until some power of current number
            // doesn't exceed MAX
            while (i * i <= MAX / temp)
            {
                temp *= (i * i);

                // Pushing only odd powers as even power of a number
                // can always be expressed as a perfect square
                // which is already present in set squares
                s.add(temp);
            }
        }

        // Inserting those sorted
        // values of set into a vector
        for (long x : s)
            powers.add(x);
    }

    static long calculateAnswer(long L, long R)
    {

        // Precompute the powers
        powersPrecomputation();

        // Calculate perfect squares in
        // range using sqrtl function
        long perfectSquares = (long) (Math.floor(Math.sqrt(R)) - 
                                Math.floor(Math.sqrt(L - 1)));

        // Calculate upper value of R
        // in vector using binary search
        long high = Collections.binarySearch(powers, R);

        // Calculate lower value of L
        // in vector using binary search
        long low = Collections.binarySearch(powers, L);

        // Calculate perfect powers
        long perfectPowers = perfectSquares + (high - low);

        // Compute final answer
        long ans = (R - L + 1) - perfectPowers;
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        long L = 13, R = 20;
        System.out.println(calculateAnswer(L, R));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from bisect import bisect as upper_bound
from bisect import bisect_left as lower_bound
from math import floor
N = 1000005
MAX = 10**18

# Vector to store powers greater than 3
powers = []

# Set to store perfect squares
squares = dict()

# Set to store powers other than perfect squares
s = dict()

def powersPrecomputation():

    for i in range(2, N):

        # Pushing squares
        squares[i * i] = 1

        # if the values is already a perfect square means
        # present in the set
        if (i not in squares.keys()):
            continue

        temp = i

        # Run loop until some power of current number
        # doesn't exceed MAX
        while (i * i <= (MAX // temp)):
            temp *= (i * i)

            # Pushing only odd powers as even power of a number
            # can always be expressed as a perfect square
            # which is already present in set squares
            s[temp]=1

    # Inserting those sorted
    # values of set into a vector
    for x in s:
        powers.append(x)

def calculateAnswer(L, R):

    # Precompute the powers
    powersPrecomputation()

    # Calculate perfect squares in
    # range using sqrtl function
    perfectSquares = floor((R)**(.5)) - floor((L - 1)**(.5))

    # Calculate upper value of R
    # in vector using binary search
    high = upper_bound(powers,R)

    # Calculate lower value of L
    # in vector using binary search
    low = lower_bound(powers,L)

    # Calculate perfect powers
    perfectPowers = perfectSquares + (high - low)

    # Compute final answer
    ans = (R - L + 1) - perfectPowers

    return ans

# Driver Code

L = 13
R = 20
print(calculateAnswer(L, R))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above idea
using System;
using System.Collections.Generic;

public class GFG 
{

    static int N = 100005;
    static long MAX = (long) 1e18;

    // List to store powers greater than 3
    static List<long> powers = new List<long>();

    // Set to store perfect squares
    static HashSet<long> squares = new HashSet<long>();

    // Set to store powers other than perfect squares
    static HashSet<long> s = new HashSet<long>();

    static void powersPrecomputation()
    {
        for (long i = 2; i < N; i++)
        {

            // Pushing squares
            squares.Add(i * i);

            // if the values is already a perfect square means
            // present in the set
            if (squares.Contains(i))
                continue;

            long temp = i;

            // Run loop until some power of current number
            // doesn't exceed MAX
            while (i * i <= MAX / temp)
            {
                temp *= (i * i);

                // Pushing only odd powers as even power of a number
                // can always be expressed as a perfect square
                // which is already present in set squares
                s.Add(temp);
            }
        }

        // Inserting those sorted
        // values of set into a vector
        foreach (long x in s)
            powers.Add(x);
    }

    static long calculateAnswer(long L, long R)
    {

        // Precompute the powers
        powersPrecomputation();

        // Calculate perfect squares in
        // range using sqrtl function
        long perfectSquares = (long) (Math.Floor(Math.Sqrt(R)) - 
                                Math.Floor(Math.Sqrt(L - 1)));

        // Calculate upper value of R
        // in vector using binary search
        long high = Array.BinarySearch(powers.ToArray(), R);

        // Calculate lower value of L
        // in vector using binary search
        long low = Array.BinarySearch(powers.ToArray(), L);

        // Calculate perfect powers
        long perfectPowers = perfectSquares + (high - low);

        // Compute readonly answer
        long ans = (R - L + 1) - perfectPowers;
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        long L = 13, R = 20;
        Console.WriteLine(calculateAnswer(L, R));
    }
}

// This code is contributed by 29AjayKumar
```

**Output:**

```
7

```