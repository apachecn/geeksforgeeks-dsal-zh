# Prime Fibonacci | TCS mock vita 2020

> 原文:[https://www . geesforgeks . org/prime-fibonnaci-TCS-mock vita-2020/](https://www.geeksforgeeks.org/prime-fibonnaci-tcs-mockvita-2020/)

#### **问题描述**

给定两个数字 **N1** 和 **N2** 。

1.  找到 **N1** 和 **N2** 之间的质数，然后
2.  从第 1 步中找到的素数列表中找出所有可能的唯一数字组合。
3.  从这个新列表中，再次找到所有质数。
4.  从第二个生成的列表中找到最小的 **A** 和最大的 **B** 号，也算这个列表。
5.  将最小和最大的数字分别作为第一和第二个数字，生成斐波那契数列，直到计数(第二个列表中的素数)。
6.  打印斐波那契数列的最后一个数字作为输出

**约束**

2 < = N2 N1 < = 100

N2-N1 > = 35

**示例:**

> **输入:** N1 = 2、N2 = 40
> **输出:** 13158006689
> **说明:**
> 首个质数列表=【2、3、5、7、11、13、17、19、23、29、31、37】
> 
> 所有素数的组合= [23，25，27，211，213，217，219，223，229，231，32，35，37，311，313，319，323，329，331，337，52，53，57，511，513，517，519，523，529，531，537，72 192, 193, 195, 197, 1911, 1913, 1917, 1923, 1929, 1931, 1937, 232, 233, 235, 237, 2311, 2313, 2317, 2319, 2329, 2331, 2337, 292, 293, 295, 297, 2911, 2913, 2917, 2919, 2923, 2931, 2937, 312, 315, 317, 3111, 3113, 3117, 3119, 3123, 3129, 3137, 372, 373, 375, 377, 3711, 3713, 3717, 3719, 3723, 3729, 3731]
> 
> 第二素数列表=[193，3137，197，2311，3719，73，137，331，523，1931，719，337，211，23，1117，223，1123，229，37，293，2917，1319，1129，233，173，3119，113，53，373
> 
> 最小( **A** ) = 23
> 
> 最大( **B** ) = 3719
> 因此，斐波那契数列的最后一个数，即数列中以 23 和 3719 作为前 2 个数的第 34 个斐波那契数是 13158006689
> 
> **输入:** N1 = 30，N2 = 70
> **输出:** 2027041
> **说明:**
> 
> 第一个素数列表= [31，37，41，43，47，53，59，61，67]
> 
> 第二素数列表由第一素数列表= [3137，5953，5347，6761，3761，4337，6737，6131，3767，4759，4153，3167，4159，6143]
> 第二列表中的最小素数=3137
> 第二列表中的最大素数=6761
> 因此，斐波那契数列的最后一个数即

**方法:**思路是利用厄拉多塞的[筛，在 O(1)时间内检查某个特定数是否为素数。因此，迭代从 **N1** 到 **N2** 的所有数字，并将该范围内的所有质数存储在一个数组中，然后使用嵌套循环找到质数的所有唯一可能组合。最后，从所有的组合中找出质数，然后找出这些质数的最小值和最大值。使用最小素数和最大素数，我们可以生成斐波那契数列来计算斐波那契数列的最后一项(所有组合中的素数)。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation to compute the
// combination of every possible
// prime numbers of the range

#include <bits/stdc++.h>
using namespace std;

long long maxN = 1e5;

// Seive of Eratosthenes
void seive(vector<bool>& primes)
{
    for (long long num = 2;
         num * num < maxN; num++) {
        if (primes[num]) {
            for (long long i = num * num;
                       i < maxN; i += num)
                primes[i] = false;
        }
    }
}

// Function to find the Nth term of
// of the Fibonacci series
long long solve(long long N1,
                long long N2)
{
    vector<bool> primes(maxN, true);
    // 1 in not prime
    primes[1] = false;
    // generate all prime in range
    // using sieve of eratosthenes
    seive(primes);

    vector<string> filteredPrimes;
    vector<long long> comb;
    set<long long> lst;

    // filter required primes and
    // put them into filteredPrimes
    // as strings
    for (long long i = N1; i <= N2; i++)
        if (primes[i])
            filteredPrimes.push_back(
                          to_string(i));

    // make all possible combinations
    for (long long i = 0;
         i < (long long)(filteredPrimes.size());
                                        i++) {
        for (long long j = 0;
             j < (long long)(filteredPrimes.size());
                                        j++) {
            if (i == j)
                continue;

            string tmp = filteredPrimes[i] +
                         filteredPrimes[j];
            comb.push_back(stoi(tmp));
        }
    }

    // Filter only prime numbers
    // for generated combinations
    for (long long x : comb)
        if (primes[x])
            lst.insert(x);

    auto it = lst.end();
    it--;

    // take smallest and largest element
    long long a = *(lst.begin()), b = *it, c;

    // Now find last element
    // of fibonacci series
    for (long long i = 3;
         i <= (long long)(lst.size());
                                 i++) {
        c = a + b;
        a = b;
        b = c;
    }

    return c;
}

// Driver Code
int main()
{
    long long N1 = 2, N2 = 40;

    cout << solve(N1, N2);

    return 0;
}
```

**Output**

```
13158006689
```