# 求三个给定和的素数

> 原文:[https://www . geesforgeks . org/find-三素数-带给定和/](https://www.geeksforgeeks.org/find-three-prime-numbers-with-given-sum/)

给定一个整数 **N** ，任务是找出三个质数 **X** 、 **Y** 和 **Z** ，使得这三个数之和等于 **N** ，即 **X + Y + Z = N** 。

**示例:**

> **输入:**N = 20
> T3】输出: 2 5 13
> 
> **输入:**N = 34
> T3】输出: 2 3 29

**进场:**

*   使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成素数
*   从第一个素数开始。
*   从生成的列表中再取一个数字。
*   从原始数字中减去第一个数字和第二个数字，得到第三个数字。
*   检查第三个数字是否是质数。
*   如果第三个数字是质数，那么输出这三个数字。
*   否则，对第二个数字重复该过程，然后对第一个数字重复该过程
*   如果答案不存在，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

const int MAX = 100001;

// The vector primes holds
// the prime numbers
vector<int> primes;

// Function to generate prime numbers
void initialize()
{

    // Initialize the array elements to 0s
    bool numbers[MAX] = {};
    int n = MAX;
    for (int i = 2; i * i <= n; i++)
        if (!numbers[i])
            for (int j = i * i; j <= n; j += i)

                // Set the non-primes to true
                numbers[j] = true;

    // Fill the vector primes with prime
    // numbers which are marked as false
    // in the numbers array
    for (int i = 2; i <= n; i++)
        if (numbers[i] == false)
            primes.push_back(i);
}

// Function to print three prime numbers
// which sum up to the number N
void findNums(int num)
{

    bool ans = false;
    int first = -1, second = -1, third = -1;
    for (int i = 0; i < num; i++) {

        // Take the first prime number
        first = primes[i];
        for (int j = 0; j < num; j++) {

            // Take the second prime number
            second = primes[j];

            // Subtract the two prime numbers
            // from the N to obtain the third number
            third = num - first - second;

            // If the third number is prime
            if (binary_search(primes.begin(),
                              primes.end(), third)) {
                ans = true;
                break;
            }
        }
        if (ans)
            break;
    }
    // Print the three prime numbers
    // if the solution exists
    if (ans)
        cout << first << " "
             << second << " " << third << endl;
    else
        cout << -1 << endl;
}

// Driver code
int main()
{
    int n = 101;

    // Function for generating prime numbers
    // using Sieve of Eratosthenes
    initialize();

    // Function to print the three prime
    // numbers whose sum is equal to N
    findNums(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static int MAX = 100001;

// The vector primes holds
// the prime numbers
static ArrayList<Integer> primes;

// Function to generate prime numbers
static void initialize()
{

    // Initialize the array elements to 0s
    boolean[] numbers = new boolean[MAX + 1];
    int n = MAX;

    for(int i = 2; i * i <= n; i++)
        if (!numbers[i])
            for(int j = i * i; j <= n; j += i)

                // Set the non-primes to true
                numbers[j] = true;

    // Fill the vector primes with prime
    // numbers which are marked as false
    // in the numbers array
    for(int i = 2; i <= n; i++)
        if (numbers[i] == false)
            primes.add(i);
}

// Function to print three prime numbers
// which sum up to the number N
static void findNums(int num)
{
    boolean ans = false;
    int first = -1, second = -1, third = -1;

    for(int i = 0; i < num; i++)
    {

        // Take the first prime number
        first = primes.get(i);

        for(int j = 0; j < num; j++)
        {

            // Take the second prime number
            second = primes.get(j);

            // Subtract the two prime numbers
            // from the N to obtain the third number
            third = num - first - second;

            // If the third number is prime
            if (Collections.binarySearch(
                primes, third) >= 0)
            {
                ans = true;
                break;
            }
        }
        if (ans)
            break;
    }

    // Print the three prime numbers
    // if the solution exists
    if (ans)
       System.out.println(first + " " +
                          second + " " +
                          third);
    else
        System.out.println(-1 );
}

// Driver code
public static void main (String[] args)
{
    int n = 101;
    primes = new ArrayList<>();

    // Function for generating prime numbers
    // using Sieve of Eratosthenes
    initialize();

    // Function to print the three prime
    // numbers whose sum is equal to N
    findNums(n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

MAX = 100001;

# The vector primes holds
# the prime numbers
primes = [];

# Function to generate prime numbers
def initialize() :

    # Initialize the array elements to 0s
    numbers = [0]*(MAX + 1);
    n = MAX;
    for i in range(2, int(sqrt(n)) + 1) :
        if (not numbers[i]) :
            for j in range( i * i , n + 1, i) :

                # Set the non-primes to true
                numbers[j] = True;

    # Fill the vector primes with prime
    # numbers which are marked as false
    # in the numbers array
    for i in range(2, n + 1) :
        if (numbers[i] == False) :
            primes.append(i);

# Function to print three prime numbers
# which sum up to the number N
def findNums(num) :

    ans = False;
    first = -1;
    second = -1;
    third = -1;
    for i in range(num) :

        # Take the first prime number
        first = primes[i];
        for j in range(num) :

            # Take the second prime number
            second = primes[j];

            # Subtract the two prime numbers
            # from the N to obtain the third number
            third = num - first - second;

            # If the third number is prime
            if (third in primes) :
                ans = True;
                break;

        if (ans) :
            break;

    # Print the three prime numbers
    # if the solution exists
    if (ans) :
        print(first , second , third);
    else :
        print(-1);

# Driver code
if __name__ == "__main__" :

    n = 101;

    # Function for generating prime numbers
    # using Sieve of Eratosthenes
    initialize();

    # Function to print the three prime
    # numbers whose sum is equal to N
    findNums(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{  
  static int MAX = 100001;

  // The vector primes holds
  // the prime numbers
  static List<int> primes = new List<int>();

  // Function to generate prime numbers
  static void initialize()
  {

    // Initialize the array elements to 0s
    bool[] numbers = new bool[MAX + 1];
    int n = MAX;
    for (int i = 2; i * i <= n; i++)
      if (!numbers[i])
        for (int j = i * i; j <= n; j += i)

          // Set the non-primes to true
          numbers[j] = true;

    // Fill the vector primes with prime
    // numbers which are marked as false
    // in the numbers array
    for (int i = 2; i <= n; i++)
      if (numbers[i] == false)
        primes.Add(i);
  }

  // Function to print three prime numbers
  // which sum up to the number N
  static void findNums(int num)
  {

    bool ans = false;
    int first = -1, second = -1, third = -1;
    for (int i = 0; i < num; i++)
    {

      // Take the first prime number
      first = primes[i];
      for (int j = 0; j < num; j++)
      {

        // Take the second prime number
        second = primes[j];

        // Subtract the two prime numbers
        // from the N to obtain the third number
        third = num - first - second;

        // If the third number is prime
        if (Array.BinarySearch(primes.ToArray(), third) >= 0)
        {
          ans = true;
          break;
        }
      }
      if (ans)
        break;
    }

    // Print the three prime numbers
    // if the solution exists
    if (ans)
      Console.WriteLine(first + " " + second + " " + third);
    else
      Console.WriteLine(-1);
  }

  // Driver code
  static void Main()
  {
    int n = 101;

    // Function for generating prime numbers
    // using Sieve of Eratosthenes
    initialize();

    // Function to print the three prime
    // numbers whose sum is equal to N
    findNums(n);
  }
}

// This code is contributed by divyesh072019
```

**Output:** 

```
2 2 97
```