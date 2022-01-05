# 脉象号

> 原文:[https://www.geeksforgeeks.org/sphenic-number/](https://www.geeksforgeeks.org/sphenic-number/)

一个[素数](https://en.wikipedia.org/wiki/Sphenic_number)是一个正整数 **n** ，它正好是三个不同素数的乘积。前几个脉冲数是 30、42、66、70、78、102、105、110、114、……
给定一个数 **n** ，判断它是否为脉冲数。

**示例:**

```
Input : 30
Output : Yes
Explanation : 30 is the smallest Sphenic number, 
           30 = 2 × 3 × 5 
           the product of the smallest three primes

Input : 60
Output : No
Explanation : 60 = 22 x 3 x 5
              has exactly 3 prime factors but
              is not a sphenic number
```

每一个自然数都有正好 8 个除数[自然数](https://en.wikipedia.org/wiki/Sphenic_number)
所以首先我们要试着找出这个数是否有正好 8 个除数，如果没有，那么简单的回答是否定的如果正好有 8 个除数，那么我们将确认 1 后的前 3 位数字是否是质数。
例如 30(蝶数)
30=p*q*r(即 p，q 和 r 是三个不同的素数，它们的乘积是 30)
除数的集合是(1，2，3，5，6，10，15，30)。

下面是这个想法的实现。

## C++

```
// C++ program to check whether a number is a
// Sphenic number or not
#include<bits/stdc++.h>
using namespace std;
//create a global array of size 10001;
bool arr[1001];
// This functions finds all primes smaller than 'limit'
// using simple sieve of eratosthenes.
void simpleSieve()
{
    // initialize all entries of it as true. A value
    // in mark[p] will finally be false if 'p' is Not
    // a prime, else true.
    memset(arr,true,sizeof(arr));

    // One by one traverse all numbers so that their
    // multiples can be marked as composite.
    for(int p=2;p*p<1001;p++)
    { 
        // If p is not changed, then it is a prime
        if(arr[p])
        {// Update all multiples of p
            for(int i=p*2;i<1001;i=i+p)
            arr[i]=false;
        }
    }
}
int find_sphene(int N)
{
    int arr1[8]={0};   //to store the 8 divisors
    int count=0;        //to count the number of divisor
    int j=0;
    for(int i=1;i<=N;i++)    
    {
        if(N%i==0 &&count<9)       
        {
            count++;
            arr1[j++]=i;
        }
    }
    //finally check if there re 8 divisor and all the numbers are distinct prime no return 1
    //else return 0
    if(count==8 && (arr[arr1[1]] && arr[arr1[2]] && arr[arr1[3]]))
    return 1;
    return 0;
}

// Driver program to test above function
int main()
{
    int n = 60;
    simpleSieve();
    int ans=find_sphene(n);
    if(ans)
    cout<<"Yes";
    else
    cout<<"NO";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a number is a
// Sphenic number or not
import java.util.*;

class GFG
{

// create a global array of size 10001;
static boolean []arr = new boolean[1001];

// This functions finds all primes smaller than 'limit'
// using simple sieve of eratosthenes.
static void simpleSieve()
{
    // initialize all entries of it as true. A value
    // in mark[p] will finally be false if 'p' is Not
    // a prime, else true.
    Arrays.fill(arr, true);

    // One by one traverse all numbers so that their
    // multiples can be marked as composite.
    for(int p = 2; p * p < 1001; p++)
    {

        // If p is not changed, then it is a prime
        if(arr[p])
        {

          // Update all multiples of p
            for(int i = p * 2; i < 1001; i = i + p)
            arr[i] = false;
        }
    }
}
static int find_sphene(int N)
{
    int []arr1 = new int[8];   // to store the 8 divisors
    int count = 0;        // to count the number of divisor
    int j = 0;
    for(int i = 1; i <= N; i++)    
    {
        if(N % i == 0 && count < 8)       
        {
            count++;
            arr1[j++] = i;

        }
    }

    // finally check if there re 8 divisor and
    // all the numbers are distinct prime no return 1
    // else return 0);
    if(count == 8 && (arr[arr1[1]] && arr[arr1[2]] && arr[arr1[3]]))
      return 1;

    return 0;
}

// Driver code
public static void main(String[] args)
{
    int n = 60;
    simpleSieve();
    int ans = find_sphene(n);
    if(ans == 1)
      System.out.print("Yes");
    else
      System.out.print("NO");
}
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program to check whether a number
# is a Sphenic number or not

# Create a global array of size 1001;
arr = [True] * (1001)

# This functions finds all primes smaller
# than 'limit' using simple sieve of
# eratosthenes.
def simpleSieve():

    # Initialize all entries of it as
    # True. A value in mark[p] will
    # finally be False if 'p' is Not
    # a prime, else True.
    k = 0

    # One by one traverse all numbers so
    # that their multiples can be marked
    # as composite.
    for p in range(2, 1001):
        if (p * p > 1001):
            break

        # If p is not changed, then it is a prime
        if (arr[p]):

            # Update all multiples of p
            for k in range(p, 1001, k + p):
                arr[k] = False

def find_sphene(N):

    # To store the 8 divisors
    arr1 = [0] * (8)

    # To count the number of divisor
    count = 0
    j = 0

    for i in range(1, N + 1):
        if (N % i == 0 and count < 8):
            count += 1
            arr1[j] = i
            j += 1

    # Finally check if there re 8 divisor and
    # all the numbers are distinct prime no return 1
    # else return 0);
    if (count == 8 and (arr[arr1[1]] and
       arr[arr1[2]] and arr[arr1[3]])):
        return 1;

    return 0;

# Driver code
if __name__ == '__main__':

    n = 60
    simpleSieve()
    ans = find_sphene(n)

    if (ans == 1):
        print("Yes")
    else:
        print("NO")

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to check whether a number
// is a Sphenic number or not
using System;

class GFG{

// Create a global array of size 10001;
static bool []arr = new bool[1001];

// This functions finds all primes smaller than
// 'limit'. Using simple sieve of eratosthenes.
static void simpleSieve()
{

    // Initialize all entries of it as true.
    // A value in mark[p] will finally be
    // false if 'p' is Not a prime, else true.
    for(int i = 0;i<1001;i++)
        arr[i] = true;

    // One by one traverse all numbers so
    // that their multiples can be marked
    // as composite.
    for(int p = 2; p * p < 1001; p++)
    {

        // If p is not changed, then it
        // is a prime
        if (arr[p])
        {

            // Update all multiples of p
            for(int i = p * 2; i < 1001; i = i + p)
                arr[i] = false;
        }
    }
}

static int find_sphene(int N)
{

    // To store the 8 divisors
    int []arr1 = new int[8];  

    // To count the number of divisor
    int count = 0;       
    int j = 0;

    for(int i = 1; i <= N; i++)    
    {
        if (N % i == 0 && count < 8)       
        {
            count++;
            arr1[j++] = i;
        }
    }

    // Finally check if there re 8 divisor
    // and all the numbers are distinct prime
    // no return 1 else return 0);
    if (count == 8 && (arr[arr1[1]] &&
      arr[arr1[2]] && arr[arr1[3]]))
        return 1;

    return 0;
}

// Driver code
public static void Main(String[] args)
{
    int n = 60;
    simpleSieve();
    int ans = find_sphene(n);

    if (ans == 1)
        Console.Write("Yes");
    else
        Console.Write("NO");
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>
// javascript program to check whether a number is a
// Sphenic number or not

    // create a global array of size 10001;
    // initialize all entries of it as true. A value
        // in mark[p] will finally be false if 'p' is Not
        // a prime, else true.
    let arr = Array(1001).fill(true);

    // This functions finds all primes smaller than 'limit'
    // using simple sieve of eratosthenes.
    function simpleSieve()
    {

        // One by one traverse all numbers so that their
        // multiples can be marked as composite.
        for (let p = 2; p * p < 1001; p++) {

            // If p is not changed, then it is a prime
            if (arr[p]) {

                // Update all multiples of p
                for (let i = p * 2; i < 1001; i = i + p)
                    arr[i] = false;
            }
        }
    }

    function find_sphene(N) {
        var arr1 = Array(8).fill(0); // to store the 8 divisors
        var count = 0; // to count the number of divisor
        var j = 0;
        for (let i = 1; i <= N; i++) {
            if (N % i == 0 && count < 8) {
                count++;
                arr1[j++] = i;

            }
        }

        // finally check if there re 8 divisor and
        // all the numbers are distinct prime no return 1
        // else return 0);
        if (count == 8 && (arr[arr1[1]] && arr[arr1[2]] && arr[arr1[3]]))
            return 1;

        return 0;
    }

    // Driver code

    var n = 60;
    simpleSieve();
    var ans = find_sphene(n);
    if (ans == 1)
        document.write("Yes");
    else
        document.write("NO");

// This code is contributed by aashish1995
</script>
```

**输出:**

```
NO
```

**参考资料:**
1。 [OEIS](https://oeis.org/A007304)
2 .[https://en . Wikipedia . org/wiki/spenic _ number](https://en.wikipedia.org/wiki/Sphenic_number)

本文由 [**mra11145**](https://auth.geeksforgeeks.org/user/Mohammedansari1111145/profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。