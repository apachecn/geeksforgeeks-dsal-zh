# n 中 k 的最大幂！(阶乘)其中 k 可能不是素数

> 原文:[https://www . geesforgeks . org/maximum-power-k-n-factorial-k-may-not-prime/](https://www.geeksforgeeks.org/largest-power-k-n-factorial-k-may-not-prime/)

给定两个数 k 和 n，求 k 除以 n 的最大幂！
**约束:**

```
 K > 1
```

示例:

```
Input : n = 7, k = 2
Output : 4
Explanation : 7! = 5040
The largest power of 2 that
divides 5040 is 24.

Input : n = 10, k = 9
Output :  2
The largest power of 9 that
divides 10! is 92.
```

当 k 总是素数时，我们在下面的帖子中讨论了一个解决方案。
[勒让德公式(给定 p 和 n，求最大的 x，使得 p^x 除以 n！)](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)
现在来寻找 n 中任意非质数 k 的幂！，我们首先[找到数字 k 的所有质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)以及它们出现的次数。然后，对于每个质因数，我们使用 [Legendre 公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)来计算出现次数，该公式指出 n 中质数 p 的最大可能幂是⌊n/p⌋+⌊n/(p<sup>2</sup>)⌋+⌊n/(p<sup>3</sup>)⌋+……
在 k 的所有质因数 p 上，findPowerOfK(n，p)/count 的最小值将是我们的答案，其中 count 是 p 在 k 中出现的次数

## C++

```
// CPP program to find the largest power
// of k that divides n!
#include <bits/stdc++.h>
using namespace std;

// To find the power of a prime p in
// factorial N
int findPowerOfP(int n, int p)
{
    int count = 0;
    int r=p;
    while (r <= n) {

        // calculating floor(n/r)
        // and adding to the count
        count += (n / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
vector<pair<int, int> > primeFactorsofK(int k)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of k
    vector<pair<int, int> > ans;

    for (int i = 2; k != 1; i++) {
        if (k % i == 0) {
            int count = 0;
            while (k % i == 0) {
                k = k / i;
                count++;
            }

            ans.push_back(make_pair(i, count));
        }
    }
    return ans;
}

// Returns largest power of k that
// divides n!
int largestPowerOfK(int n, int k)
{
    vector<pair<int, int> > vec;
    vec = primeFactorsofK(k);
    int ans = INT_MAX;
    for (int i = 0; i < vec.size(); i++)

        // calculating minimum power of all
        // the prime factors of k
        ans = min(ans, findPowerOfP(n,
              vec[i].first) / vec[i].second);

    return ans;
}

// Driver code
int main()
{
    cout << largestPowerOfK(7, 2) << endl;
    cout << largestPowerOfK(10, 9) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find the largest power
// of k that divides n!
import java.util.*;

class GFG
{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}
// To find the power of a prime p in
// factorial N
static int findPowerOfP(int n, int p)
{
    int count = 0;
    int r = p;
    while (r <= n)
    {

        // calculating Math.floor(n/r)
        // and adding to the count
        count += (n / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
static Vector<pair > primeFactorsofK(int k)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of k
    Vector<pair> ans = new Vector<pair>();

    for (int i = 2; k != 1; i++)
    {
        if (k % i == 0)
        {
            int count = 0;
            while (k % i == 0)
            {
                k = k / i;
                count++;
            }

            ans.add(new pair(i, count));
        }
    }
    return ans;
}

// Returns largest power of k that
// divides n!
static int largestPowerOfK(int n, int k)
{
    Vector<pair > vec = new Vector<pair>();
    vec = primeFactorsofK(k);
    int ans = Integer.MAX_VALUE;
    for (int i = 0; i < vec.size(); i++)

        // calculating minimum power of all
        // the prime factors of k
        ans = Math.min(ans, findPowerOfP(n,
            vec.get(i).first) / vec.get(i).second);

    return ans;
}

// Driver code
public static void main(String[] args)
{
    System.out.print(largestPowerOfK(7, 2) +"\n");
    System.out.print(largestPowerOfK(10, 9) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the largest power
# of k that divides n!
import sys

# To find the power of a prime p in
# factorial N
def findPowerOfP(n, p) :

    count = 0
    r = p
    while (r <= n) :

        # calculating floor(n/r)
        # and adding to the count
        count += (n // r)

        # increasing the power of p
        # from 1 to 2 to 3 and so on
        r = r * p

    return count

# returns all the prime factors of k
def primeFactorsofK(k) :

    # vector to store all the prime factors
    # along with their number of occurrence
    # in factorization of k
    ans = []
    i = 2
    while k != 1 :
        if k % i == 0 :
            count = 0
            while k % i == 0 :
                k = k // i
                count += 1
            ans.append([i , count])
        i += 1

    return ans

# Returns largest power of k that
# divides n!
def largestPowerOfK(n, k) :

    vec = primeFactorsofK(k)
    ans = sys.maxsize
    for i in range(len(vec)) :

        # calculating minimum power of all
        # the prime factors of k
        ans = min(ans, findPowerOfP(n, vec[i][0]) // vec[i][1])

    return ans

print(largestPowerOfK(7, 2))
print(largestPowerOfK(10, 9))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the largest power
// of k that divides n!
using System;
using System.Collections.Generic;

class GFG
{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// To find the power of a prime p in
// factorial N
static int findPowerOfP(int n, int p)
{
    int count = 0;
    int r = p;
    while (r <= n)
    {

        // calculating Math.Floor(n/r)
        // and adding to the count
        count += (n / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
static List<pair > primeFactorsofK(int k)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of k
    List<pair> ans = new List<pair>();

    for (int i = 2; k != 1; i++)
    {
        if (k % i == 0)
        {
            int count = 0;
            while (k % i == 0)
            {
                k = k / i;
                count++;
            }

            ans.Add(new pair(i, count));
        }
    }
    return ans;
}

// Returns largest power of k that
// divides n!
static int largestPowerOfK(int n, int k)
{
    List<pair > vec = new List<pair>();
    vec = primeFactorsofK(k);
    int ans = int.MaxValue;
    for (int i = 0; i < vec.Count; i++)

        // calculating minimum power of all
        // the prime factors of k
        ans = Math.Min(ans, findPowerOfP(n,
            vec[i].first) / vec[i].second);

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    Console.Write(largestPowerOfK(7, 2) +"\n");
    Console.Write(largestPowerOfK(10, 9) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the largest power
// of k that divides n!

class pair
{
    constructor(first,second)
    {
        this.first = first;
        this.second = second;
    }
}

// To find the power of a prime p in
// factorial N
function findPowerOfP(n,p)
{
    let count = 0;
    let r = p;
    while (r <= n)
    {

        // calculating Math.floor(n/r)
        // and adding to the count
        count += Math.floor(n / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
function primeFactorsofK(k)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of k
    let ans = [];

    for (let i = 2; k != 1; i++)
    {
        if (k % i == 0)
        {
            let count = 0;
            while (k % i == 0)
            {
                k = Math.floor(k / i);
                count++;
            }

            ans.push(new pair(i, count));
        }
    }
    return ans;
}

// Returns largest power of k that
// divides n!
function largestPowerOfK(n,k)
{
    let vec = [];
    vec = primeFactorsofK(k);
    let ans = Number.MAX_VALUE;
    for (let i = 0; i < vec.length; i++)

        // calculating minimum power of all
        // the prime factors of k
        ans = Math.min(ans, findPowerOfP(n,
            vec[i].first) / vec[i].second);

    return ans;
}

// Driver code
document.write(largestPowerOfK(7, 2) +"<br>");
document.write(largestPowerOfK(10, 9) +"<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
4
2
```

本文由 [**ShivamKD**](https://auth.geeksforgeeks.org/profile.php?user=ShivamKD) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。