# 不大于 N 的最大数字，重新排列数字后可以变成素数

> 原文:[https://www . geeksforgeeks . org/最大数字-不大于-n-重新排列其数字后可成为质数/](https://www.geeksforgeeks.org/largest-number-not-greater-than-n-which-can-become-prime-after-rearranging-its-digits/)

给定一个数 N，任务是找到小于或等于给定数 N 的最大数，这样在重新排列它的数字时，它可以变成素数。
**例:**

```
Input : N = 99 
Output : 98
Explanation : We can rearrange the digits of 
98 to 89 and 89 is a prime number. 

Input : N = 84896
Output : 84896
Explanation : We can rearrange the digits of 
84896 to 46889 which is a prime number.
```

下面是寻找这样一个最大数字 **num < = N** 的算法，这样 num 的数字可以重新排列得到一个质数:
**预处理步骤**:生成一个小于或等于给定数字 N 的所有质数的列表，这可以使用厄拉多塞的[筛高效地完成。
**主要步骤**:主要思路是检查从 N 到 1 的所有数字，如果有任何一个数字可以重新洗牌形成质数。找到的第一个这样的数字将是答案。
为此，对每个数字运行一个从 N 到 1 的循环:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

1.  提取给定数字的位数并将其存储在向量中。
2.  对这个向量进行排序，得到可以用这些数字组成的最小数。
3.  对于这个向量的每个排列，我们将形成一个数，并检查形成的数是否是质数。这里我们利用预处理步骤。
4.  如果它是质数，那么我们停止循环，这就是我们的答案。

以下是上述方法的实现:

## C++

```
// C++ Program to find a number less than
// or equal to N such that rearranging
// the digits gets a prime number

#include <bits/stdc++.h>
using namespace std;

// Preprocessed vector to store primes
vector<bool> prime(1000001, true);

// Function to generate primes using
// sieve of eratosthenese
void sieve()
{
    // Applying sieve of Eratosthenes
    prime[0] = prime[1] = false;

    for (long long i = 2; i * i <= 1000000; i++) {

        if (prime[i]) {
            for (long long j = i * i; j <= 1000000; j += i)
                prime[j] = false;
        }
    }
}

// Function to find a number less than
// or equal to N such that rearranging
// the digits gets a prime number
int findNumber(int n)
{
    vector<int> v;
    bool flag = false;

    int num;

    // Run loop from n to 1
    for (num = n; num >= 1; num--) {

        int x = num;

        // Clearing the vector
        v.clear();

        // Extracting the digits
        while (x != 0) {
            v.push_back(x % 10);

            x /= 10;
        }

        // Sorting the vector to make smallest
        // number using digits
        sort(v.begin(), v.end());

        // Check all permutation of current number
        // for primality
        while (1) {
            long long w = 0;

            // Traverse vector to for number
            for (auto u : v)
                w = w * 10 + u;

            // If prime exists
            if (prime[w]) {

                flag = true;
                break;
            }

            if (flag)
                break;

            // generating next permutation of vector
            if (!next_permutation(v.begin(), v.end()))
                break;
        }

        if (flag)
            break;
    }

    // Required number
    return num;
}

// Driver Code
int main()
{
    sieve();

    int n = 99;
    cout << findNumber(n) << endl;

    n = 84896;
    cout << findNumber(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find a number less than
// or equal to N such that rearranging
// the digits gets a prime number
import java.util.*;

class GFG{

// Preprocessed vector to store primes
static boolean[] prime = new boolean[1000001];
static boolean next_permutation(Vector<Integer> v) {
    int p[] = new int[v.size()];
    for(int l = 0; l< p.length;l++) {
        p[l] = v.elementAt(l);
    }
      for (int a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
          for (int b = p.length - 1;; --b)
            if (p[b] > p[a]) {
              int t = p[a];
              p[a] = p[b];
              p[b] = t;
              for (++a, b = p.length - 1; a < b; ++a, --b) {
                t = p[a];
                p[a] = p[b];
                p[b] = t;
              }
              return true;
            }
      return false;
    }

// Function to generate primes using
// sieve of eratosthenese
static void sieve()
{
    Arrays.fill(prime, true);
    // Applying sieve of Eratosthenes
    prime[0] = prime[1] = false;

    for (int i = 2; i * i <= 1000000; i++) {

        if (prime[i]==true) {
            for (int j = i * i; j <= 1000000; j += i)
                prime[j] = false;
        }
    }
}

// Function to find a number less than
// or equal to N such that rearranging
// the digits gets a prime number
static int findNumber(int n)
{
    Vector<Integer> v = new Vector<>();
    boolean flag = false;

    int num;

    // Run loop from n to 1
    for (num = n; num >= 1; num--) {

        int x = num;

        // Clearing the vector
        v.clear();

        // Extracting the digits
        while (x != 0) {
            v.add(x % 10);

            x /= 10;
        }

        // Sorting the vector to make smallest
        // number using digits

        Collections.sort(v);

        // Check all permutation of current number
        // for primality
        while (true) {
            int w = 0;

            // Traverse vector to for number
            for (int u : v)
                w = w * 10 + u;

            // If prime exists
            if (prime[w]==true) {

                flag = true;
                break;
            }

            if (flag)
                break;

            // generating next permutation of vector
            if (!next_permutation(v))
                break;
        }

        if (flag)
            break;
    }

    // Required number
    return num;
}

// Driver Code
public static void main(String[] args)
{
    sieve();

    int n = 99;
    System.out.print(findNumber(n) +"\n");

    n = 84896;
    System.out.print(findNumber(n) +"\n");

}
}

// This code contributed by umadevi9616
```

## 蟒蛇 3

```
# Python 3 Program to find a number less than
# or equal to N such that rearranging
# the digits gets a prime number
from math import sqrt

def next_permutation(a):

    # Generate the lexicographically
    # next permutation inplace.

    # https://en.wikipedia.org/wiki/Permutation
    # Generation_in_lexicographic_order
    # Return false if there is no next permutation.

    # Find the largest index i such that
    # a[i] < a[i + 1]. If no such index exists,
    # the permutation is the last permutation
    for i in reversed(range(len(a) - 1)):
        if a[i] < a[i + 1]:
            break # found
    else: # no break: not found
        return False # no next permutation

    # Find the largest index j greater than i
    # such that a[i] < a[j]
    j = next(j for j in reversed(range(i + 1, len(a)))
                                      if a[i] < a[j])

    # Swap the value of a[i] with that of a[j]
    a[i], a[j] = a[j], a[i]

    # Reverse sequence from a[i + 1] up to and
    # including the final element a[n]
    a[i + 1:] = reversed(a[i + 1:])
    return True

# Preprocessed vector to store primes
prime = [True for i in range(1000001)]

# Function to generate primes using
# sieve of eratosthenese
def sieve():

    # Applying sieve of Eratosthenes
    prime[0] = False
    prime[1] = False

    for i in range(2,int(sqrt(1000000)) + 1, 1):
        if (prime[i]):
            for j in range(i * i, 1000001, i):
                prime[j] = False

# Function to find a number less than
# or equal to N such that rearranging
# the digits gets a prime number
def findNumber(n):
    v = []
    flag = False

    # Run loop from n to 1
    num = n
    while(num >= 1):
        x = num

        v.clear()

        # Extracting the digits
        while (x != 0):
            v.append(x % 10)

            x = int(x / 10)

        # Sorting the vector to make smallest
        # number using digits
        v.sort(reverse = False)

        # Check all permutation of current number
        # for primality
        while (1):
            w = 0

            # Traverse vector to for number
            for u in v:
                w = w * 10 + u

            # If prime exists
            if (prime[w]):
                flag = True
                break

            if (flag):
                break

            # generating next permutation of vector
            if (next_permutation(v) == False):
                break

        if (flag):
            break

        num -= 1

    # Required number
    return num

# Driver Code
if __name__ == '__main__':
    sieve()

    n = 99
    print(findNumber(n))

    n = 84896
    print(findNumber(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to find a number less than
// or equal to N such that rearranging
// the digits gets a prime number
using System;
using System.Collections.Generic;

public class GFG {

    // Preprocessed vector to store primes
    static bool[] prime = new bool[1000001];

    static bool next_permutation(List<int> v) {
        int []p = new int[v.Count];
        for (int l = 0; l < p.Length; l++) {
            p[l] = v[l];
        }
        for (int a = p.Length - 2; a >= 0; --a)
            if (p[a] < p[a + 1])
                for (int b = p.Length - 1;; --b)
                    if (p[b] > p[a]) {
                        int t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.Length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
        return false;
    }

    // Function to generate primes using
    // sieve of eratosthenese
    static void sieve() {
        for (int j = 0; j < prime.GetLength(0); j++)
                    prime[j] = true;
        // Applying sieve of Eratosthenes
        prime[0] = prime[1] = false;

        for (int i = 2; i * i <= 1000000; i++) {

            if (prime[i] == true) {
                for (int j = i * i; j <= 1000000; j += i)
                    prime[j] = false;
            }
        }
    }

    // Function to find a number less than
    // or equal to N such that rearranging
    // the digits gets a prime number
    static int findNumber(int n) {
        List<int> v = new List<int>();
        bool flag = false;

        int num;

        // Run loop from n to 1
        for (num = n; num >= 1; num--) {

            int x = num;

            // Clearing the vector
            v.Clear();

            // Extracting the digits
            while (x != 0) {
                v.Add(x % 10);

                x /= 10;
            }

            // Sorting the vector to make smallest
            // number using digits

            v.Sort();

            // Check all permutation of current number
            // for primality
            while (true) {
                int w = 0;

                // Traverse vector to for number
                foreach (int u in v)
                    w = w * 10 + u;

                // If prime exists
                if (prime[w] == true) {

                    flag = true;
                    break;
                }

                if (flag)
                    break;

                // generating next permutation of vector
                if (!next_permutation(v))
                    break;
            }

            if (flag)
                break;
        }

        // Required number
        return num;
    }

    // Driver Code
    public static void Main(String[] args) {
        sieve();

        int n = 99;
        Console.Write(findNumber(n) + "\n");

        n = 84896;
        Console.Write(findNumber(n) + "\n");

    }
}

// This code is contributed by umadevi9616 -
```

## java 描述语言

```
<script>
// javascript Program to find a number less than
// or equal to N such that rearranging
// the digits gets a prime number

    // Preprocessed vector to store primes
    var prime = Array(1000001).fill(true);

    function next_permutation(v)
    {
        var p = Array(v.length).fill(0);
        for (l = 0; l < p.length; l++) {
            p[l] = v[l];
        }
        for (a = p.length - 2; a >= 0; --a)
            if (p[a] < p[a + 1])
                for (b = p.length - 1;; --b)
                    if (p[b] > p[a]) {
                        var t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
        return false;
    }

    // Function to generate primes using
    // sieve of eratosthenese
    function sieve() {

        // Applying sieve of Eratosthenes
        prime[0] = prime[1] = false;

        for (i = 2; i * i <= 1000000; i++) {

            if (prime[i] == true) {
                for (j = i * i; j <= 1000000; j += i)
                    prime[j] = false;
            }
        }
    }

    // Function to find a number less than
    // or equal to N such that rearranging
    // the digits gets a prime number
    function findNumber(n) {
        var v = new Array();
        var flag = false;

        var num;

        // Run loop from n to 1
        for (num = n; num >= 1; num--) {

            var x = num;

            // Clearing the vector
            v = new Array();

            // Extracting the digits
            while (x != 0) {
                v.push(x % 10);

                x = parseInt(x/10);
            }

            // Sorting the vector to make smallest
            // number using digits

            v.sort();

            // Check all permutation of current number
            // for primality
            while (true) {
                var w = 0;

                // Traverse vector to for number
                v.forEach(function (item) {
                    w = w * 10 + item;
});
                // If prime exists
                if (prime[w] == true) {

                    flag = true;
                    break;
                }

                if (flag)
                    break;

                // generating next permutation of vector
                if (!next_permutation(v))
                    break;
            }

            if (flag)
                break;
        }

        // Required number
        return num;
    }

    // Driver Code
        sieve();
        var n = 99;
        document.write(findNumber(n) + "<br/>");
        n = 84896;
        document.write(findNumber(n) + "<br/>");

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
98
84896
```