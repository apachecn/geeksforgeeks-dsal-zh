# 素因子出现在数组中的元素的和

> 原文:[https://www . geeksforgeeks . org/其素因子存在于数组中的元素之和/](https://www.geeksforgeeks.org/sum-of-element-whose-prime-factors-are-present-in-array/)

给定一个非负整数数组 **arr[]** ，其中**2≤arr[I]≤10<sup>6</sup>T5】。任务是从数组中找出那些素因子存在于同一个数组中的元素的和。**

**示例:**

> **输入:** arr[] = {2，3，10}
> **输出:**5
> 2 的因子是 2，存在于数组中
> 3 的因子是 3，也存在于数组中
> 10 的因子是 2 和 5，其中只有 2 存在于数组中。
> 所以，和= 2 + 3 = 5
> 
> **输入:** arr[] = {5，11，55，25，100 }
> T3】输出: 96

**方法:**思路是先用筛子用[素分解计算](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)[最小素因子](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)直到数组的最大元素。

1.  现在，迭代数组，对于元素**arr【I】**
2.  如果 **arr[i]！= 1** :
    *   如果数组中存在**最小化默认因子(arr[i])** ，则更新 **arr[i] /最小化默认因子(arr[i])** 并转到步骤 2。
    *   否则转到步骤 1。
3.  否则更新**sum = sum+original val(arr[I])**。
4.  最后打印**和**。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of the elements of an array
// whose prime factors are present in the same array
#include <bits/stdc++.h>
using namespace std;

#define MAXN 1000001

// Stores smallest prime factor for every number
int spf[MAXN];

// Function to calculate SPF (Smallest Prime Factor)
// for every number till MAXN
void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)

        // Marking smallest prime factor for every
        // number to be itself.
        spf[i] = i;

    // Separately marking spf for every even
    // number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {

        // If i is prime
        if (spf[i] == i) {

            // Marking SPF for all numbers divisible by i
            for (int j = i * i; j < MAXN; j += i)

                // Marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to return the sum of the elements of an array
// whose prime factors are present in the same array
int sumFactors(int arr[], int n)
{

    // Function call to calculate smallest prime factors of
    // all the numbers upto MAXN
    sieve();

    // Create map for each element
    std::map<int, int> map;

    for (int i = 0; i < n; ++i)
        map[arr[i]] = 1;

    int sum = 0;

    for (int i = 0; i < n; ++i) {
        int num = arr[i];

        // If smallest prime factor of num is present in array
        while (num != 1 && map[spf[num]] == 1) {
            num /= spf[num];
        }

        // Each factor of arr[i] is present in the array
        if (num == 1)
            sum += arr[i];
    }

    return sum;
}

// Driver program
int main()
{
    int arr[] = { 5, 11, 55, 25, 100 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to print required answer
    cout << sumFactors(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the elements of an array 
// whose prime factors are present in the same array 

import java.util.*;  

public class GFG{

final static int MAXN = 1000001 ;

// Stores smallest prime factor for every number 
static int spf[] = new int [MAXN]; 

    // Function to calculate SPF (Smallest Prime Factor) 
    // for every number till MAXN 
    static void sieve() 
    { 
        spf[1] = 1; 
        for (int i = 2; i < MAXN; i++) 

            // Marking smallest prime factor for every 
            // number to be itself. 
            spf[i] = i; 

        // Separately marking spf for every even 
        // number as 2 
        for (int i = 4; i < MAXN; i += 2) 
            spf[i] = 2; 

        for (int i = 3; i * i < MAXN; i++) { 

            // If i is prime 
            if (spf[i] == i) { 

                // Marking SPF for all numbers divisible by i 
                for (int j = i * i; j < MAXN; j += i) 

                    // Marking spf[j] if it is not 
                    // previously marked 
                    if (spf[j] == j) 
                        spf[j] = i; 
            } 
        } 
    } 

    // Function to return the sum of the elements of an array 
    // whose prime factors are present in the same array 
    static int sumFactors(int arr[], int n) 
    { 

        // Function call to calculate smallest prime factors of 
        // all the numbers upto MAXN 
        sieve(); 

        // Create map for each element 
        Map map=new HashMap();

        for(int i = 0 ; i < MAXN ; ++i)
            map.put(i,0) ;

        for (int i = 0; i < n; ++i) 
            map.put(arr[i],1); 

        int sum = 0; 

        for (int i = 0; i < n; ++i) { 
            int num = arr[i]; 

            // If smallest prime factor of num is present in array 
            while (num != 1 && (int)(map.get(spf[num])) == 1) { 
                num /= spf[num]; 
            } 

            // Each factor of arr[i] is present in the array 
            if (num == 1) 
                sum += arr[i]; 
        } 

        return sum; 
    } 

    // Driver program 
     public static void main(String []args)
    { 
        int arr[] = { 5, 11, 55, 25, 100 }; 
        int n = arr.length ;

        // Function call to print required answer 
         System.out.println(sumFactors(arr, n)) ;
    } 
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python program to find the sum of the 
# elements of an array whose prime factors
# are present in the same array 
from collections import defaultdict

MAXN = 1000001
MAXN_sqrt = int(MAXN ** (0.5))

# Stores smallest prime factor
# for every number 
spf = [None] * (MAXN) 

# Function to calculate SPF (Smallest 
# Prime Factor) for every number till MAXN 
def sieve():

    spf[1] = 1
    for i in range(2, MAXN): 

        # Marking smallest prime factor 
        # for every number to be itself. 
        spf[i] = i 

    # Separately marking spf for every 
    # even number as 2 
    for i in range(4, MAXN, 2): 
        spf[i] = 2

    for i in range(3, MAXN_sqrt): 

        # If i is prime 
        if spf[i] == i:

            # Marking SPF for all numbers 
            # divisible by i 
            for j in range(i * i, MAXN, i): 

                # Marking spf[j] if it is  
                # not previously marked 
                if spf[j] == j:
                    spf[j] = i 

# Function to return the sum of the elements 
# of an array whose prime factors are present 
# in the same array 
def sumFactors(arr, n): 

    # Function call to calculate smallest 
    # prime factors of all the numbers upto MAXN 
    sieve() 

    # Create map for each element 
    Map = defaultdict(lambda:0) 

    for i in range(0, n): 
        Map[arr[i]] = 1

    Sum = 0

    for i in range(0, n): 
        num = arr[i] 

        # If smallest prime factor of num
        # is present in array 
        while num != 1 and Map[spf[num]] == 1: 
            num = num // spf[num] 

        # Each factor of arr[i] is present 
        # in the array 
        if num == 1: 
            Sum += arr[i] 

    return Sum

# Driver Code
if __name__ == "__main__":

    arr = [5, 11, 55, 25, 100] 
    n = len(arr) 

    # Function call to print 
    # required answer 
    print(sumFactors(arr, n)) 

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the sum of the elements 
// of an array whose prime factors are present
// in the same array 
using System;
using System.Collections.Generic;

class GFG
{
    static int MAXN = 1000001;

    // Stores smallest prime factor for every number 
    static int []spf = new int [MAXN]; 

    // Function to calculate SPF (Smallest Prime Factor) 
    // for every number till MAXN 
    static void sieve() 
    { 
        spf[1] = 1; 
        for (int i = 2; i < MAXN; i++) 

            // Marking smallest prime factor for 
            // every number to be itself. 
            spf[i] = i; 

        // Separately marking spf for every even 
        // number as 2 
        for (int i = 4; i < MAXN; i += 2) 
            spf[i] = 2; 

        for (int i = 3; i * i < MAXN; i++) 
        { 

            // If i is prime 
            if (spf[i] == i)
            { 

                // Marking SPF for all numbers divisible by i 
                for (int j = i * i; j < MAXN; j += i) 

                    // Marking spf[j] if it is not 
                    // previously marked 
                    if (spf[j] == j) 
                        spf[j] = i; 
            } 
        } 
    } 

    // Function to return the sum of the elements 
    // of an array whose prime factors are present 
    // in the same array 
    static int sumFactors(int []arr, int n) 
    { 

        // Function call to calculate smallest 
        // prime factors of all the numbers upto MAXN 
        sieve(); 

        // Create map for each element 
        Dictionary<int, int> map = new Dictionary<int, int>();

        for(int i = 0 ; i < MAXN ; ++i)
            map.Add(i, 0);

        for (int i = 0; i < n; ++i)
        {
            if(map.ContainsKey(arr[i]))
            {
                map[arr[i]] = 1; 
            }
            else
            {
                map.Add(arr[i], 1);
            }
        }

        int sum = 0; 

        for (int i = 0; i < n; ++i) 
        { 
            int num = arr[i]; 

            // If smallest prime factor of num 
            // is present in array 
            while (num != 1 && 
             (int)(map[spf[num]]) == 1) 
            { 
                num /= spf[num]; 
            } 

            // Each factor of arr[i] is present
            // in the array 
            if (num == 1) 
                sum += arr[i]; 
        } 
        return sum; 
    } 

    // Driver Code
    public static void Main(String []args)
    { 
        int []arr = { 5, 11, 55, 25, 100 }; 
        int n = arr.Length;

        // Function call to print required answer 
        Console.WriteLine(sumFactors(arr, n));
    } 
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
96

```