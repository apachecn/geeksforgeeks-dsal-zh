# 最小的数 S，使得 N 是 S 阶乘或 S 的因子！

> 原文:[https://www . geesforgeks . org/minist-number-s-n-factor-s-factor-s/](https://www.geeksforgeeks.org/smallest-number-s-n-factor-s-factorial-s/)

给定一个数 N，你的任务是找到最小的数 S，这样 N 就是 S 的因子！(S 阶乘)。n 可以非常大。
示例:

```
Input  : 6
Output : 3
The value of 3! is 6
This is the smallest number which can have 6 as a factor.

Input  : 997587429953
Output : 998957
If we calculate out 998957!, 
we shall find that it is divisible by 997587429953.
Factors of 997587429953 are 998957 and 998629.
```

**天真方法**
我们从 1 迭代到 N，计算每种情况下的阶乘。当我们找到一个可以用 N 作为因子的阶乘时，我们输出它。这个方法对于大 N 来说很难实现，因为阶乘会变得非常大。
时间复杂度:O(N^2)
**优化朴素方法**
我们用二分搜索法代替了从 1 到 n 的迭代。这仍然是一个糟糕的方法，因为我们还在试图计算 N！
时间复杂度 O(N log N)
**最优解**
我们首先可以计算 N 的所有素因子，然后我们把问题简化为寻找一个包含 N 的所有素因子的阶乘，至少与它们在 N 中出现的次数一样多，然后我们对从 1 到 N 的元素进行二分搜索法运算，我们可以利用[勒让德公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)来检查一个数的阶乘是否包含所有相同的素因子。然后我们找到最小的这个数。

## C++

```
// Program to find factorial that N belongs to
#include <bits/stdc++.h>
using namespace std;

#define ull unsigned long long

// Calculate prime factors for a given number
map<ull, int> primeFactors(ull num)
{
    // Container for prime factors
    map<ull, int> ans;

    // Iterate from 2 to i^2 finding all factors
    for (ull i = 2; i * i <= num; i++)
    {
        while (num % i == 0)
        {
            num /= i;
            ans[i]++;
        }
    }

    // If we still have a remainder
    // it is also a prime factor
    if (num > 1)
        ans[num]++;
    return ans;
}

// Calculate occurrence of an element
// in factorial of a number
ull legendre(ull factor, ull num)
{
    ull count = 0, fac2 = factor;
    while (num >= factor)
    {
        count += num / factor;
        factor *= fac2;
    }
    return count;
}

bool possible(map<ull, int> &factors, ull num)
{
    // Iterate through prime factors
    for (map<ull, int>::iterator it = factors.begin();
            it != factors.end(); ++it)
    {
        // Check if factorial contains less
        // occurrences of prime factor
        if (legendre(it->first, num) < it->second)
            return false;
    }
    return true;
}

// Function to binary search 1 to N
ull search(ull start, ull end, map<ull, int> &factors)
{
    ull mid = (start + end) / 2;

    // Prime factors are not in the factorial
    // Increase the lowerbound
    if (!possible(factors, mid))
        return search(mid + 1, end, factors);

    // We have reached smallest occurrence
    if (start == mid)
        return mid;

    // Smaller factorial satisfying
    // requirements may exist, decrease upperbound
    return search(start, mid, factors);
}

// Calculate prime factors and search
ull findFact(ull num)
{
    map<ull, int> factors = primeFactors(num);
    return search(1, num, factors);
}

// Driver function
int main()
{
    cout << findFact(6) << "n";
    cout << findFact(997587429953) << "n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find factorial that N belongs to

import java.util.HashMap;
import java.util.Iterator;
import java.util.Set;

class Test
{
    // Calculate prime factors for a given number
    static HashMap<Long, Integer> primeFactors(long num)
    {

        // Container for prime factors
        HashMap<Long, Integer> ans = new HashMap<Long, Integer>(){
            @Override
            public Integer get(Object key) {
                if(containsKey(key)){
                    return super.get(key);                         
            }
            return 0;
        }
    };

        // Iterate from 2 to i^2 finding all factors
        for (long i = 2; i * i <= num; i++)
        {
            while (num % i == 0)
            {
                num /= i;
                ans.put(i, ans.get(i)+1);
            }
        }

        // If we still have a remainder
        // it is also a prime factor
        if (num > 1)
            ans.put(num, ans.get(num)+1);;
        return ans;
    }

    // Calculate occurrence of an element
    // in factorial of a number
    static long legendre(long factor, long num)
    {
        long count = 0, fac2 = factor;
        while (num >= factor)
        {
            count += num / factor;
            factor *= fac2;
        }
        return count;
    }

    static boolean possible(HashMap<Long, Integer> factors, long num)
    {
        Set<Long> s = factors.keySet();

        // Iterate through prime factors
        Iterator<Long> itr = s.iterator();

        while (itr.hasNext()) {
            long temp = itr.next();
             // Check if factorial contains less
            // occurrences of prime factor
            if (legendre(temp, num) < factors.get(temp))
                return false;
        }

        return true;
    }

    // Method to binary search 1 to N
    static long search(long start, long end, HashMap<Long, Integer> factors)
    {
        long mid = (start + end) / 2;

        // Prime factors are not in the factorial
        // Increase the lowerbound
        if (!possible(factors, mid))
            return search(mid + 1, end, factors);

        // We have reached smallest occurrence
        if (start == mid)
            return mid;

        // Smaller factorial satisfying
        // requirements may exist, decrease upperbound
        return search(start, mid, factors);
    }

    // Calculate prime factors and search
    static long findFact(long num)
    {
        HashMap<Long, Integer>  factors = primeFactors(num);
        return search(1, num, factors);
    }

    // Driver method
    public static void main(String args[])
    {
        System.out.println(findFact(6));
        System.out.println(findFact(997587429953L));
    }
}
// This code is contributed by Gaurav Miglani
```

## 蟒蛇 3

```
# Python Program to find factorial that N belongs to

# Calculate prime factors for a given number
def primeFactors(num):

    # Container for prime factors
    ans = dict()
    i = 2

    # Iterate from 2 to i^2 finding all factors
    while(i * i <= num):  
        while (num % i == 0):
            num //= i;
            if i not in ans:
              ans[i] = 0
            ans[i] += 1

    # If we still have a remainder
    # it is also a prime factor
    if (num > 1):
      if num not in ans:
        ans[num] = 0
      ans[num] += 1
    return ans;

# Calculate occurrence of an element
# in factorial of a number
def legendre(factor, num):
    count = 0
    fac2 = factor;
    while (num >= factor):   
        count += num // factor;
        factor *= fac2; 
    return count;

def possible(factors, num):

    # Iterate through prime factors
    for it in factors.keys():

        # Check if factorial contains less
        # occurrences of prime factor
        if (legendre(it, num) < factors[it]):
            return False;   
    return True;

# Function to binary search 1 to N
def search(start, end, factors):
    mid = (start + end) // 2;

    # Prime factors are not in the factorial
    # Increase the lowerbound
    if (not possible(factors, mid)):
        return search(mid + 1, end, factors);

    # We have reached smallest occurrence
    if (start == mid):
        return mid;

    # Smaller factorial satisfying
    # requirements may exist, decrease upperbound
    return search(start, mid, factors);

# Calculate prime factors and search
def findFact(num):
    factors = primeFactors(num);
    return search(1, num, factors);

# Driver function
if __name__=='__main__':

    print(findFact(6))
    print(findFact(997587429953))

# This code is contributed by pratham76.
```

## C#

```
// C# Program to find factorial that N belongs to
using System;
using System.Collections;
using System.Collections.Generic;

class Test
{

  // Calculate prime factors for a given number
  static Dictionary<long, int> primeFactors(long num)
  {

    // Container for prime factors
    Dictionary<long, int> ans = new Dictionary<long, int>();

    // Iterate from 2 to i^2 finding all factors
    for (long i = 2; i * i <= num; i++)
    {
      while (num % i == 0)
      {
        num /= i;
        if(!ans.ContainsKey(i))
        {
          ans[i] = 0;
        }
        ans[i]++;
      }
    }

    // If we still have a remainder
    // it is also a prime factor
    if (num > 1)
    {
      if(!ans.ContainsKey(num))
      {
        ans[num] = 0;
      }
      ans[num]++;
    }
    return ans;
  }

  // Calculate occurrence of an element
  // in factorial of a number
  static long legendre(long factor, long num)
  {
    long count = 0, fac2 = factor;
    while (num >= factor)
    {
      count += num / factor;
      factor *= fac2;
    }
    return count;
  }

  static bool possible(Dictionary<long, int> factors, long num)
  {

    foreach (int itr in factors.Keys)
    {
      // Check if factorial contains less
      // occurrences of prime factor
      if (legendre(itr, num) < factors[itr])
        return false;
    }      
    return true;
  }

  // Method to binary search 1 to N
  static long search(long start, long end, Dictionary<long, int> factors)
  {
    long mid = (start + end) / 2;

    // Prime factors are not in the factorial
    // Increase the lowerbound
    if (!possible(factors, mid))
      return search(mid + 1, end, factors);

    // We have reached smallest occurrence
    if (start == mid)
      return mid;

    // Smaller factorial satisfying
    // requirements may exist, decrease upperbound
    return search(start, mid, factors);
  }

  // Calculate prime factors and search
  static long findFact(long num)
  {
    Dictionary<long, int>  factors = primeFactors(num);
    return search(1, num, factors);
  }

  // Driver method
  public static void Main()
  {
    Console.WriteLine(findFact(6));
    Console.WriteLine(findFact(997587429953L));
  }
}

// This code is contributed by rutvik_56.
```

输出:

```
3
998957
```

我们从来没有真正计算过阶乘。这意味着我们不必担心阶乘太大而无法存储。
拉格朗日公式以 O(对数 N)运行。
二分搜索法为 O(对数 N)。
计算质因数是 O(sqrt(N))
迭代质因数是 O(Log N)。
时间复杂度变为:O(sqrt(N) + (Log N)^3)
本文由 **Aditya Kamath** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。