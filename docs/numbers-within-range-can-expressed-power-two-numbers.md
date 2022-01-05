# 可表示为两个数的幂的范围内的数

> 原文:[https://www . geesforgeks . org/numbers-在范围内-可以表示-幂-二-numbers/](https://www.geeksforgeeks.org/numbers-within-range-can-expressed-power-two-numbers/)

给定两个整数 L 和 R，求给定范围[L，R]内[完美幂](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)的个数。如果存在一些整数 a > 0，p > 1，这样 x = a <sup>p</sup> ，则称数字 x 为完美幂。

示例:

```
Input : 1 4
Output : 2
Explanation : 
Suitable numbers are 1 and 4 where 1
can be expressed as 1 = 12 
and 4 can be expressed as 4 = 22

Input : 12 29
Output : 3
Explanation : 
Suitable numbers are 16, 25 and 27.

```

**先决条件:** [检查一个数是否可以表示为 x^y](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-xy-x-raised-to-power-y/) 、[二分搜索法](https://www.geeksforgeeks.org/binary-search/)和[完美幂(1，4，8，9，16，25，27，…)](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)

**方法:**我们来固定一些功率 p，很明显不超过 10 个 <sup>18/p</sup> 的数字 x，使得 x <sup>p</sup> 对于特定的 p 不超过 10 个 <sup>18</sup> ，同时，只有对于 p = 2，这个量是比较巨大的，对于所有其他 p ≥ 3，这些数字的总量将是 10 个 <sup>6</sup> 的数量级。在【1，10 <sup>18</sup> 范围内有 10 个 <sup>9</sup> 方块，无法存储它们来回答我们的查询。

要么生成 p ≥ 2 的所有幂，并处理其中的所有完美平方，要么只生成 3、5、7 等数的奇次幂。那么对查询(L，R)的回答等于 L 和 R 之间生成数的数量加上范围内的一些完美平方。

1.  范围内的完美平方数是 R 的平方根的楼层值与(L–1)的平方根的楼层值之差，即(**floor(sqrt(R))–floor(sqrt(L–1)**)。*请注意，由于精度问题，标准 sqrt 可能会产生不正确的值，因此请使用二分搜索法或 **sqrtl** 在 cmath 中定义的内置函数(有关 sqrtl 的更多描述，请查看这里的)。*
2.  产生那些奇数的幂。首先，做预计算找到这样的数，可以表示为某个数的幂直到 10 <sup>18</sup> ，这样我们就可以回答很多查询，而不需要为每个查询反复处理。从迭代一个从 2 到 10 的循环开始 <sup>6</sup> (因为我们计算的是 p ≥ 3 的幂和 10 <sup>6</sup> 是幂升到 3 的最大值，不能超过 10 <sup>18</sup> )，对于每个值，我们将其平方插入一个集合，并进一步检查该值是否已经是完美平方(已经存在于集合中)，我们找不到该数的任何其他幂(因为完美平方的任何幂也是完美平方)。否则，运行一个内部循环来寻找该数的奇数次幂，直到它超过 10 <sup>18</sup> 并插入另一个集合，比如“s”。通过这种方法，我们没有在集合中推进任何完美的正方形。

因此，最终答案将是范围内的完美平方数之和以及 R 的上限值和 L 的下限值之差(使用二分搜索法)。
**下图是上述方法在 C++中的实现。**

```
// CPP Program to count the numbers
// within a range such that number
// can be expressed as power of some
// other number
#include <bits/stdc++.h>

using namespace std;

#define N 1000005
#define MAX 1e18

// Vector to store powers greater than 3
vector<long int> powers;

// set to store perfect squares
set<long int> squares;

// set to store powers other
// than perfect squares
set<long int> s;

void powersPrecomputation()
{
    for (long int i = 2; i < N; i++) 
    {
        // pushing squares
        squares.insert(i * i);

        // if the values is already
        // a perfect square means
        // present in the set
        if (squares.find(i) != squares.end())
                continue;

        long int temp = i;

        // run loop until some
        // power of current number
        // doesn't exceed MAX
        while (i * i <= MAX / temp) 
        {
            temp *= (i * i);

            /* pushing only odd powers
            as even power of a number
            can always be expressed as 
            a perfect square which is
            already present in set squares  */
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
    // calculate perfect squares in 
    // range using sqrtl function
    long int perfectSquares = floor(sqrtl(R)) - 
                            floor(sqrtl(L - 1));

    // calculate upper value of R 
    // in vector using binary search
    long int high = (upper_bound(powers.begin(), 
            powers.end(), R) - powers.begin());

    // calculate lower value of L 
    // in vector using binary search
    long int low = (lower_bound(powers.begin(),
            powers.end(), L) - powers.begin());

    // add into final answer
    perfectSquares += (high - low);

    return perfectSquares;
}

// Driver Code
int main()
{
    // precompute the powers
    powersPrecomputation();

    // left value of range
    long int L = 12;

    // right value of range
    long int R = 29;

    cout << "Number of powers between " << L 
            << " and " << R << " = " << 
            calculateAnswer(L, R) << endl;

    L = 1;
    R = 100000000000;

    cout << "Number of powers between " << L
            << " and " << R << " = " << 
            calculateAnswer(L, R) << endl;

    return 0;
}
```

**Output:**

```
Number of powers between 12 and 29 = 3
Number of powers between 1 and 100000000000 = 320990

```