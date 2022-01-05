# 由给定范围内的素数对串联而成的斐波那契素数序列的第 n 项

> 原文:[https://www . geeksforgeeks . org/n-Fibonacci 数列的第 n 项-通过连接给定范围内的素数对生成/](https://www.geeksforgeeks.org/nth-term-of-a-fibonacci-series-of-primes-generated-by-concatenating-pairs-of-primes-in-a-given-range/)

给定两个整数 **X** 和 **Y** ，任务是执行以下操作:

*   找出**【X，Y】**范围内的所有素数。
*   通过组合给定范围内的每对素数，生成所有可能的数。
*   从上面生成的所有可能的数字中找出质数。计算其中素数的个数，说 **N** 。
*   打印斐波那契数列的第 N<sup>项，该数列由上面列表中最小和最大的素数组成，作为数列的前两项。</sup>

**示例:**

> **输入:** X = 2 Y = 40
> **输出:** 13158006689
> **解释:**
> 范围内的所有素数[X，Y] = [2，3，5，7，11，13，17，19，23，29，31，37]
> 
> 通过串联每对质数= [23，25，27，211，213，217，219，223，229，231，32，35，37，311，313，319，323，329，331，337，52，53，57，511，513，517，519，523，529，531，551，531 1719, 1723, 1729, 1731, 1737, 192, 193, 195, 197, 1911, 1913, 1917, 1923, 1929, 1931, 1937, 232, 233, 235, 237, 2311, 2313, 2317, 2319, 2329, 2331, 2337, 292, 293, 295, 297, 2911, 2913, 2917, 2919, 2923, 2931, 2937, 312, 315, 317, 3111, 3113, 3117, 3119, 3123, 3129, 3137, 372, 373, 375, 377, 3711, 3713, 3717, 3719, 3723, 3729, 3731]
> 
> 生成的数字中的所有素数=[193，3137，197，2311，3719，73，137，331，523，1931，719，337，211，23，1117，223，1123，229，37，293，2917，1319，1129，233，173，3119，113，53
> 
> 素数计数= 34
> 最小素数= 23
> 最大素数= 3719
> 因此，斐波那契数列的第 34 项，前两项为 23 和 3719，为 13158006689。
> 
> **输入:** X = 1，Y = 10
> T3】输出: 1053

**方法:**
按照以下步骤解决问题:

*   使用厄拉多塞的 [**筛子**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成所有可能的素数。
*   遍历**【X，Y】**范围，借助上一步生成的**素数[]** 数组生成该范围内的所有素数。
*   遍历素数列表，从列表中生成所有可能的对。
*   对于每一对，连接两个质数并检查它们的连接是否是质数。
*   找出所有这样的素数的**最大值**和**最小值**，并计算得到的所有这样的素数。
*   最后，将在上述步骤中获得的具有**最小值**和**最大值**的斐波那契数列的**计数** <sup>第</sup>列为数列的前两项。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;
#define int long long int

// Stores at each index if it's a
// prime or not
int prime[100001];

// Sieve of Eratosthenes to
// generate all possible primes
void SieveOfEratosthenes()
{
    for(int i = 0; i < 100001; i++)
        prime[i] = 1;

    int p = 2;
    while (p * p <= 100000)
    {

        // If p is a prime
        if (prime[p] == 1)
        {

            // Set all multiples of
            // p as non-prime
            for(int i = p * p;
                    i < 100001;
                    i += p)
                prime[i] = 0;
        }    
        p += 1;
    }    
}

int join(int a, int b)
{
    int mul = 1;
    int bb = b;

    while(b != 0)
    {
        mul *= 10;
        b /= 10;
    }
    a *= mul;
    a += bb;
    return a;
}

// Function to generate the
// required Fibonacci Series
void fibonacciOfPrime(int n1, int n2)
{
    SieveOfEratosthenes();

    // Stores all primes between
    // n1 and n2
    vector<int>initial;

    // Generate all primes between
    // n1 and n2
    for(int i = n1; i <= n2; i++)
        if (prime[i])
            initial.push_back(i);

    // Stores all concatenations
    // of each pair of primes
    vector<int>now;

    // Generate all concatenations
    // of each pair of primes
    for(auto a:initial)
        for(auto b:initial)
            if (a != b)
            {
                int c = join(a,b);
                now.push_back(c);
            }

    // Stores the primes out of the
    // numbers generated above
    vector<int>current;

    for(auto x:now)
        if (prime[x])
            current.push_back(x);

    // Store the unique primes
    set<int>current_set;
    for(auto i:current)
        current_set.insert(i);

    // Find the minimum
    int first = *min_element(current_set.begin(),
                             current_set.end());

    // Find the minimum
    int second = *max_element(current_set.begin(),
                              current_set.end());

    // Find N
    int count = current_set.size() - 1;
    int curr = 1;
    int c;

    while( curr < count)
    {
        c = first + second;
        first = second;
        second = c;
        curr += 1;
    }

    // Print the N-th term
    // of the Fibonacci Series
    cout << (c) << endl;
}

// Driver Code
int32_t main()
{
    int x = 2;
    int y = 40;

    fibonacciOfPrime(x, y);
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Stores at each index if it's a 
// prime or not    
static int prime[] = new int [100001];

// Sieve of Eratosthenes to
// generate all possible primes
static void SieveOfEratosthenes()
{
    for(int i = 0; i < 100001; i++)
        prime[i] = 1;

    int p = 2;
    while (p * p <= 100000)
    {

        // If p is a prime
        if (prime[p] == 1)
        {

            // Set all multiples of
            // p as non-prime
            for(int i = p * p;
                    i < 100001;
                    i += p)
                prime[i] = 0;
        }    
        p += 1;
    }    
}

static int join(int a,int b)
{
    int mul = 1;
    int bb = b;

    while(b != 0)
    {
        mul *= 10;
        b /= 10;
    }
    a *= mul;
    a += bb;
    return a;
}

// Function to generate the
// required Fibonacci Series
static void fibonacciOfPrime(int n1, int n2)
{
    SieveOfEratosthenes();

    // Stores all primes between
    // n1 and n2
    Vector<Integer> initial = new Vector<>();

    // Generate all primes between
    // n1 and n2
    for(int i = n1; i <= n2; i++)
        if (prime[i] == 1)
            initial.add(i);

    // Stores all concatenations
    // of each pair of primes
    Vector<Integer> now = new Vector<>();

    // Generate all concatenations
    // of each pair of primes
    for(int i = 0; i < initial.size(); i++)
    {
        for(int j = 0; j < initial.size(); j++)
        {
            int a = (int)initial.get(i);
            int b = (int)initial.get(j);

            if (a != b)
            {
                int c = join(a, b);
                now.add(c);
            }
        }
    }

    // Stores the primes out of the
    // numbers generated above
    Vector<Integer> current = new Vector<>();

    for(int i = 0; i < now.size(); i++)
        if (prime[(int)now.get(i)] == 1)
            current.add((int)now.get(i));

    // Store the unique primes
    int cnt[] = new int[1000009];
    for(int i = 0; i < 1000001; i++)
        cnt[i] = 0;

    Vector<Integer> current_set = new Vector<>();
    for(int i = 0; i < current.size(); i++)
    {
        cnt[(int)current.get(i)]++;
        if (cnt[(int)current.get(i)] == 1)
            current_set.add((int)current.get(i));
    }

    // Find the minimum
    long first = 1000000000;
    for(int i = 0; i < current_set.size(); i++)
        first = Math.min(first,
                         (int)current_set.get(i));

    // Find the minimum
    long second = 0;
    for(int i = 0; i < current_set.size(); i++)
        second = Math.max(second,
                         (int)current_set.get(i));

    // Find N
    int count = current_set.size() - 1;
    long curr = 1;
    long c = 0;

    while(curr < count)
    {
        c = first + second;
        first = second;
        second = c;
        curr += 1;
    }

    // Print the N-th term
    // of the Fibonacci Series
    System.out.println(c);
}

// Driver code
public static void main(String[] args)
{
    int x = 2;
    int y = 40;

    fibonacciOfPrime(x, y);
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Stores at each index if it's a
# prime or not
prime = [True for i in range(100001)]

# Sieve of Eratosthenes to
# generate all possible primes
def SieveOfEratosthenes():

    p = 2
    while (p * p <= 100000):

        # If p is a prime
        if (prime[p] == True):

            # Set all multiples of p as non-prime
            for i in range(p * p, 100001, p):
                prime[i] = False

        p += 1

# Function to generate the
# required Fibonacci Series
def fibonacciOfPrime(n1, n2):

    SieveOfEratosthenes()

    # Stores all primes between
    # n1 and n2
    initial = []

    # Generate all primes between
    # n1 and n2
    for i in range(n1, n2):
        if prime[i]:
            initial.append(i)

    # Stores all concatenations
    # of each pair of primes
    now = []

    # Generate all concatenations
    # of each pair of primes
    for a in initial:
        for b in initial:
            if a != b:
                c = str(a) + str(b)
                now.append(int(c))

    # Stores the primes out of the
    # numbers generated above
    current = []

    for x in now:
        if prime[x]:
            current.append(x)

    # Store the unique primes
    current = set(current)

    # Find the minimum
    first = min(current)

    # Find the minimum
    second = max(current)

    # Find N
    count = len(current) - 1
    curr = 1

    while curr < count:
        c = first + second
        first = second
        second = c
        curr += 1

    # Print the N-th term
    # of the Fibonacci Series
    print(c)

# Driver Code
if __name__ == "__main__":

    x = 2
    y = 40
    fibonacciOfPrime(x, y)
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Stores at each index if it's a  
// prime or not     
static int[] prime = new int[100001];

// Sieve of Eratosthenes to 
// generate all possible primes
static void SieveOfEratosthenes()
{
  for(int i = 0; i < 100001; i++)
    prime[i] = 1;

  int p = 2;
  while (p * p <= 100000)
  {
    // If p is a prime
    if (prime[p] == 1)
    {
      // Set all multiples of
      // p as non-prime
      for(int i = p * p;
              i < 100001; i += p)
        prime[i] = 0;
    }

    p += 1;
  }     
}

static int join(int a,
                int b)
{
  int mul = 1;
  int bb = b;

  while(b != 0)
  {
    mul *= 10;
    b /= 10;
  }

  a *= mul;
  a += bb;
  return a;
}

// Function to generate the 
// required Fibonacci Series
static void fibonacciOfPrime(int n1,
                             int n2)
{
  SieveOfEratosthenes();

  // Stores all primes
  // between n1 and n2
  List<int> initial =
            new List<int>();

  // Generate all primes
  // between n1 and n2
  for(int i = n1; i <= n2; i++)
    if (prime[i] == 1)
      initial.Add(i);

  // Stores all concatenations
  // of each pair of primes
  List<int> now =
            new List<int>();

  // Generate all concatenations
  // of each pair of primes
  for(int i = 0; i < initial.Count; i++)
  {
    for(int j = 0; j < initial.Count; j++)
    {
      int a = initial[i];
      int b = initial[j];

      if (a != b)
      {
        int C = join(a, b);
        now.Add(C);
      }
    }
  }

  // Stores the primes out of the
  // numbers generated above
  List<int> current =
            new List<int>();

  for(int i = 0; i < now.Count; i++)
    if (prime[now[i]] == 1)
      current.Add(now[i]);

  // Store the unique primes
  int[] cnt = new int[1000009];

  for(int i = 0; i < 1000001; i++)
    cnt[i] = 0;

  List<int> current_set =
            new List<int>();

  for(int i = 0; i < current.Count; i++)
  {
    cnt[current[i]]++;

    if (cnt[current[i]] == 1)
      current_set.Add(current[i]);
  }

  // Find the minimum
  long first = 1000000000;

  for(int i = 0;
          i < current_set.Count; i++)
    first = Math.Min(first,
                     current_set[i]);

  // Find the minimum
  long second = 0;

  for(int i = 0;
          i < current_set.Count; i++)
    second = Math.Max(second,
                      current_set[i]);

  // Find N
  int count = current_set.Count - 1;
  long curr = 1;
  long c = 0;

  while(curr < count)
  {
    c = first + second;
    first = second;
    second = c;
    curr += 1;
  }

  // Print the N-th term
  // of the Fibonacci Series
  Console.WriteLine(c);
}

// Driver code
static void Main()
{
  int x = 2;
  int y = 40;
  fibonacciOfPrime(x, y);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Stores at each index if it's a prime or not   
    let prime = new Array(100001);

    // Sieve of Eratosthenes to
    // generate all possible primes
    function SieveOfEratosthenes()
    {
        for(let i = 0; i < 100001; i++)
            prime[i] = 1;

        let p = 2;
        while (p * p <= 100000)
        {

            // If p is a prime
            if (prime[p] == 1)
            {

                // Set all multiples of
                // p as non-prime
                for(let i = p * p; i < 100001; i += p)
                    prime[i] = 0;
            }   
            p += 1;
        }   
    }

    function join(a, b)
    {
        let mul = 1;
        let bb = b;

        while(b != 0)
        {
            mul *= 10;
            b = parseInt(b / 10, 10);
        }
        a *= mul;
        a += bb;
        return a;
    }

    // Function to generate the
    // required Fibonacci Series
    function fibonacciOfPrime(n1, n2)
    {
        SieveOfEratosthenes();

        // Stores all primes between
        // n1 and n2
        let initial = [];

        // Generate all primes between
        // n1 and n2
        for(let i = n1; i <= n2; i++)
            if (prime[i] == 1)
                initial.push(i);

        // Stores all concatenations
        // of each pair of primes
        let now = [];

        // Generate all concatenations
        // of each pair of primes
        for(let i = 0; i < initial.length; i++)
        {
            for(let j = 0; j < initial.length; j++)
            {
                let a = initial[i];
                let b = initial[j];

                if (a != b)
                {
                    let c = join(a, b);
                    now.push(c);
                }
            }
        }

        // Stores the primes out of the
        // numbers generated above
        let current = [];

        for(let i = 0; i < now.length; i++)
            if (prime[now[i]] == 1)
                current.push(now[i]);

        // Store the unique primes
        let cnt = new Array(1000009);
        for(let i = 0; i < 1000001; i++)
            cnt[i] = 0;

        let current_set = [];
        for(let i = 0; i < current.length; i++)
        {
            cnt[current[i]]++;
            if (cnt[current[i]] == 1)
                current_set.push(current[i]);
        }

        // Find the minimum
        let first = 1000000000;
        for(let i = 0; i < current_set.length; i++)
            first = Math.min(first, current_set[i]);

        // Find the minimum
        let second = 0;
        for(let i = 0; i < current_set.length; i++)
            second = Math.max(second, current_set[i]);

        // Find N
        let count = current_set.length - 1;
        let curr = 1;
        let c = 0;

        while(curr < count)
        {
            c = first + second;
            first = second;
            second = c;
            curr += 1;
        }

        // Print the N-th term
        // of the Fibonacci Series
        document.write(c);
    }

    let x = 2;
    let y = 40;

    fibonacciOfPrime(x, y);

</script>
```

**Output:** 

```
13158006689
```

***时间复杂度:** O(N <sup>2</sup> + log(log(maxm)))，其中需要 O(N <sup>2</sup> )生成所有对，O(1)检查一个数是否是素数，maxm 是素数的大小[]*
***辅助空间:** O(maxm)*