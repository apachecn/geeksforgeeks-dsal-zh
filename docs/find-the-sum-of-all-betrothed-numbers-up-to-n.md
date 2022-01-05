# 求所有订婚号码的和，直到 N

> 原文:[https://www . geesforgeks . org/find-the-sum-of-all-fixed-numbers-up-n/](https://www.geeksforgeeks.org/find-the-sum-of-all-betrothed-numbers-up-to-n/)

给定一个数字 **N** ，任务是找出所有[订婚数字](https://www.geeksforgeeks.org/betrothed-numbers/)到 **N** 的总和。

> 假设， **A** 和 **B** 是定数对，那么 **A** 的定数之和等于 **B+1** ，而 **B** 的定数之和等于 **A+1。**

**示例:**

> **输入:** 78
> **输出:** 123
> **说明:** 48 和 75 是唯一一对**到 78 的订婚号码**。
> 
> **输入:** 5
> **输出:** 0
> **说明:**没有 50 以下的订婚号码对。

**进场:**

*   初始化数组以存储所有预定号码直到 **N**
*   使用所有适当除数的和找到预定数，并将该对存储在数组中。
*   然后求所有小于等于 **N** 的数字的**和**。
*   结果总和是所需的值。

下面的代码是上述方法的实现:

## C++

```
// C++ program to find the sum of the  
// all betrothed numbers up to N
#include<bits/stdc++.h>
using namespace std;

// Function to find the sum of
// the all betrothed numbers
int Betrothed_Sum(int n)
{
    // To store the betrothed
    // numbers
    vector<int > Set;

    for(int number_1 = 1; number_1 < n;
                            number_1++)
    {

       // Calculate sum of
       // number_1's divisors
       // 1 is always a divisor
       int sum_divisor_1 = 1;

       // i = 2 because we don't
       // want to include
       // 1 as a divisor.
       int i = 2;

       while (i * i <= number_1)
       {
           if (number_1 % i == 0)
           {
               sum_divisor_1 = sum_divisor_1 + i;

               if (i * i != number_1)
                   sum_divisor_1 += number_1 / i;
           }
           i ++;
       }
       if (sum_divisor_1 > number_1)
       {
           int number_2 = sum_divisor_1 - 1;
           int sum_divisor_2 = 1;
           int j = 2;

           while (j * j <= number_2)
           {
               if (number_2 % j == 0)
               {
                   sum_divisor_2 += j;
                   if (j * j != number_2)
                       sum_divisor_2 += number_2 / j;
               }
               j = j + 1;
           }
           if (sum_divisor_2 == number_1 + 1 and
               number_1 <= n && number_2 <= n)
           {
               Set.push_back(number_1);
               Set.push_back(number_2);
           }
       }
    }

    // Sum all betrothed
    // numbers up to N
    int Summ = 0;
    for(auto i : Set)
    {
       if(i <= n)
          Summ += i;
    }
    return Summ;
}

// Driver code
int main()
{
    int n = 78;

    cout << Betrothed_Sum(n);
    return 0;
}

// This code is contributed by ishayadav181
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum
// of the all betrothed numbers
// up to N 
import java.util.*;

class GFG{

// Function to find the sum of 
// the all betrothed numbers 
public static int Betrothed_Sum(int n)
{

    // To store the betrothed 
    // numbers 
    Vector<Integer> Set = new Vector<Integer>();

    for(int number_1 = 1;
            number_1 < n; 
            number_1++)
    {

       // Calculate sum of 
       // number_1's divisors 
       // 1 is always a divisor
       int sum_divisor_1 = 1;

       // i = 2 because we don't 
       // want to include 
       // 1 as a divisor. 
       int i = 2;

       while (i * i <= number_1)
       {
           if (number_1 % i == 0)
           {
               sum_divisor_1 = sum_divisor_1 + i;

               if (i * i != number_1)
                   sum_divisor_1 += number_1 / i; 
           }
           i ++;
       }

       if (sum_divisor_1 > number_1)
       {
           int number_2 = sum_divisor_1 - 1;
           int sum_divisor_2 = 1;
           int j = 2;

           while (j * j <= number_2) 
           {
               if (number_2 % j == 0) 
               {
                   sum_divisor_2 += j;

                   if (j * j != number_2)
                       sum_divisor_2 += number_2 / j;
               }
               j = j + 1;
           }
           if (sum_divisor_2 == number_1 + 1 && 
               number_1 <= n && number_2 <= n)
           {
               Set.add(number_1);
               Set.add(number_2);
           }
       }
    }

    // Sum all betrothed 
    // numbers up to N 
    int Summ = 0;
    for(int i = 0; i < Set.size(); i++)
    {
       if (Set.get(i) <= n) 
          Summ += Set.get(i);
    }
    return Summ;
}

// Driver code
public static void main(String[] args)
{
    int n = 78;

    System.out.println(Betrothed_Sum(n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the
# Sum of the all Betrothed
# numbers up to N

import math

# Function to find the Sum of
# the all Betrothed numbers
def Betrothed_Sum(n):

    # To store the Betrothed
    # numbers
    Set = []

    for number_1 in range(1, n):

        # Calculate sum of
        # number_1's divisors

        # 1 is always a divisor
        sum_divisor_1 = 1

        # i = 2 because we don't
        # want to include
        # 1 as a divisor.
        i = 2

        while i * i <= number_1:
            if (number_1 % i == 0):
                sum_divisor_1 = sum_divisor_1 + i

                if (i * i != number_1):
                    sum_divisor_1 += number_1 // i
            i = i + 1

        if (sum_divisor_1 > number_1):

            number_2 = sum_divisor_1 - 1
            sum_divisor_2 = 1
            j = 2
            while j * j <= number_2:
                if (number_2 % j == 0):
                    sum_divisor_2 += j
                    if (j * j != number_2):
                        sum_divisor_2 += number_2 // j
                j = j + 1

            if (sum_divisor_2 == number_1 + 1
                and number_1<= n and number_2<= n):
                Set.append(number_1)
                Set.append(number_2)

    # Sum all Betrothed
    # numbers up to N
    Summ = 0
    for i in Set:
        if i <= n:
            Summ += i
    return Summ

# Driver Code
n = 78
print(Betrothed_Sum(n))
```

## C#

```
// C# program to find the sum
// of the all betrothed numbers
// up to N 
using System;
using System.Collections;

class GFG{

// Function to find the sum of 
// the all betrothed numbers 
public static int Betrothed_Sum(int n)
{

    // To store the betrothed 
    // numbers 
    ArrayList set = new ArrayList();

    for(int number_1 = 1;
            number_1 < n; 
            number_1++)
    {

        // Calculate sum of 
        // number_1's divisors 
        // 1 is always a divisor
        int sum_divisor_1 = 1;

        // i = 2 because we don't 
        // want to include 
        // 1 as a divisor. 
        int i = 2;

        while (i * i <= number_1)
        {
            if (number_1 % i == 0)
            {
                sum_divisor_1 = sum_divisor_1 + i;

                if (i * i != number_1)
                    sum_divisor_1 += number_1 / i; 
            }
            i ++;
        }

        if (sum_divisor_1 > number_1)
        {
            int number_2 = sum_divisor_1 - 1;
            int sum_divisor_2 = 1;
            int j = 2;

            while (j * j <= number_2) 
            {
                if (number_2 % j == 0) 
                {
                    sum_divisor_2 += j;

                    if (j * j != number_2)
                        sum_divisor_2 += number_2 / j;
                }
                j = j + 1;
            }

            if (sum_divisor_2 == number_1 + 1 && 
                number_1 <= n && number_2 <= n)
            {
                set.Add(number_1);
                set.Add(number_2);
            }
        }
    }

    // Sum all betrothed 
    // numbers up to N 
    int Summ = 0;
    for(int i = 0; i < set.Count; i++)
    {
        if ((int)set[i] <= n) 
            Summ += (int)set[i];
    }
    return Summ;
}

// Driver code
static public void Main()
{
    int n = 78;

    Console.WriteLine(Betrothed_Sum(n));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
// Javascript program to find the sum of the  
// all betrothed numbers up to N

// Function to find the sum of
// the all betrothed numbers
function Betrothed_Sum(n)
{
    // To store the betrothed
    // numbers
    let Set = [];

    for(let number_1 = 1; number_1 < n;
                            number_1++)
    {

       // Calculate sum of
       // number_1's divisors
       // 1 is always a divisor
       let sum_divisor_1 = 1;

       // i = 2 because we don't
       // want to include
       // 1 as a divisor.
       let i = 2;

       while (i * i <= number_1)
       {
           if (number_1 % i == 0)
           {
               sum_divisor_1 = sum_divisor_1 + i;

               if (i * i != number_1)
                   sum_divisor_1 += parseInt(number_1 / i);
           }
           i++;
       }
       if (sum_divisor_1 > number_1)
       {
           let number_2 = sum_divisor_1 - 1;
           let sum_divisor_2 = 1;
           let j = 2;

           while (j * j <= number_2)
           {
               if (number_2 % j == 0)
               {
                   sum_divisor_2 += j;
                   if (j * j != number_2)
                       sum_divisor_2 += parseInt(number_2 / j);
               }
               j = j + 1;
           }
           if ((sum_divisor_2 == number_1 + 1) &&
               number_1 <= n && number_2 <= n)
           {
               Set.push(number_1);
               Set.push(number_2);
           }
       }
    }

    // Sum all betrothed
    // numbers up to N
    let Summ = 0;
    for(let i = 0; i < Set.length; i++)
    {
       if(Set[i] <= n)
          Summ += Set[i];
    }
    return Summ;
}

// Driver code
    let n = 78;
    document.write(Betrothed_Sum(n));

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
123
```

**时间复杂度:**T2【O(N * sqrt(N))T4】