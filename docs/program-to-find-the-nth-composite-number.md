# 程序寻找第 n 个合成号码

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-composite-number/](https://www.geeksforgeeks.org/program-to-find-the-nth-composite-number/)

给定一个正整数 **N，**的任务是找到**N<sup>th</sup>T5[复合数。](https://www.geeksforgeeks.org/composite-number/)**

**示例:**

> **输入:**N = 1
> T3】输出: 4
> 
> **输入:**N = 3
> T3】输出: 8

**方法:**利用厄拉多塞的[筛的概念可以解决给定的问题。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   用厄拉多塞的[筛子在布尔数组中标记所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[质数](https://www.geeksforgeeks.org/prime-numbers/)到**10<sup>5</sup>T5【说 i **sPrime[]** 。**
*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说**复合[]** ，存储所有的复合数字。
*   使用变量 **i** 遍历数组 **isPrime[]** ，如果 **isPrime[i]** 的值为假，则在数组 **composites[]** 中插入数字 **i** 。
*   完成上述步骤后，将数值**复合[N–1]**打印为**N<sup>th</sup>T5[复合编号。](https://www.geeksforgeeks.org/composite-number/)**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define MAX_SIZE 1000005

// Function to find the Nth Composite
// Numbers using Sieve of Eratosthenes
int NthComposite(int N)
{
    // Sieve of prime numbers
    bool IsPrime[MAX_SIZE];

    // Initialize the array to true
    memset(IsPrime, true, sizeof(IsPrime));

    // Iterate over the range [2, MAX_SIZE]
    for (int p = 2;
         p * p < MAX_SIZE; p++) {

        // If IsPrime[p] is true
        if (IsPrime[p] == true) {

            // Iterate over the
            // range [p * p, MAX_SIZE]
            for (int i = p * p;
                 i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Stores the list of composite numbers
    vector<int> Composites;

    // Iterate over the range [4, MAX_SIZE]
    for (int p = 4; p < MAX_SIZE; p++)

        // If i is not prime
        if (!IsPrime[p])
            Composites.push_back(p);

    // Return Nth Composite Number
    return Composites[N - 1];
}

// Driver Code
int main()
{
    int N = 4;
    cout << NthComposite(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to find the Nth Composite
// Numbers using Sieve of Eratosthenes
public static int NthComposite(int N)
{
    int MAX_SIZE = 1000005;

    // Sieve of prime numbers
    boolean[] IsPrime = new boolean[MAX_SIZE];

    // Initialize the array to true
    Arrays.fill(IsPrime, true);

    // Iterate over the range [2, MAX_SIZE]
    for (int p = 2; p * p < MAX_SIZE; p++) {

        // If IsPrime[p] is true
        if (IsPrime[p] == true) {

            // Iterate over the
            // range [p * p, MAX_SIZE]
            for (int i = p * p;
                 i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Stores the list of composite numbers
    Vector<Integer> Composites = new Vector<Integer>();

    // Iterate over the range [4, MAX_SIZE]
    for (int p = 4; p < MAX_SIZE; p++)

        // If i is not prime
        if (!IsPrime[p])
            Composites.add(p);

    // Return Nth Composite Number
    return Composites.get(N - 1);
}

// Driver Code
   public static void main(String args[])
   {
     int N = 4;
     System.out.println(NthComposite(N));
    }
}

// This code is contributed by SoumikMondal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Nth Composite
# Numbers using Sieve of Eratosthenes
def NthComposite(N):

    # Sieve of prime numbers
    IsPrime = [True]*1000005

    # Iterate over the range [2, 1000005]
    for p in range(2, 1000005):
        if p * p > 1000005:
            break

        # If IsPrime[p] is true
        if (IsPrime[p] == True):

            # Iterate over the
            # range [p * p, 1000005]
            for i in range(p*p,1000005,p):
                IsPrime[i] = False

    # Stores the list of composite numbers
    Composites = []

    # Iterate over the range [4, 1000005]
    for p in range(4,1000005):

        # If i is not prime
        if (not IsPrime[p]):
            Composites.append(p)

    # Return Nth Composite Number
    return Composites[N - 1]

# Driver Code
if __name__ == '__main__':
    N = 4
    print (NthComposite(N))

# This code is contributed by mohit kumar 29.
```

## C#

```
using System;
using System.Collections.Generic;

public class GFG{

  // Function to find the Nth Composite
  // Numbers using Sieve of Eratosthenes
  public static int NthComposite(int N)
  {
    int MAX_SIZE = 1000005;

    // Sieve of prime numbers
    bool[] IsPrime = new bool[MAX_SIZE];

    // Initialize the array to true
    Array.Fill(IsPrime, true);

    // Iterate over the range [2, MAX_SIZE]
    for (int p = 2; p * p < MAX_SIZE; p++) {

      // If IsPrime[p] is true
      if (IsPrime[p] == true) {

        // Iterate over the
        // range [p * p, MAX_SIZE]
        for (int i = p * p;
             i < MAX_SIZE; i += p)
          IsPrime[i] = false;
      }
    }

    // Stores the list of composite numbers
    List<int> Composites = new List<int>();

    // Iterate over the range [4, MAX_SIZE]
    for (int p = 4; p < MAX_SIZE; p++)

      // If i is not prime
      if (!IsPrime[p])
        Composites.Add(p);

    // Return Nth Composite Number
    return Composites[N - 1];
  }

  // Driver Code
  static public void Main ()
  {

    int N = 4;
    Console.WriteLine(NthComposite(N));

  }
}

// This code is contributed by patel2127
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let MAX_SIZE =  1000005;

// Function to find the Nth Composite
// Numbers using Sieve of Eratosthenes
function NthComposite( N)
{
    // Sieve of prime numbers
    let IsPrime = [];

    // Initialize the array to true
    for(let i = 0;i<MAX_SIZE;i++)
        IsPrime.push(true);

    // Iterate over the range [2, MAX_SIZE]
    for (let p = 2;
         p * p < MAX_SIZE; p++) {

        // If IsPrime[p] is true
        if (IsPrime[p] == true) {

            // Iterate over the
            // range [p * p, MAX_SIZE]
            for (let i = p * p;
                 i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Stores the list of composite numbers
    let Composites = [];

    // Iterate over the range [4, MAX_SIZE]
    for (let p = 4; p < MAX_SIZE; p++)

        // If i is not prime
        if (!IsPrime[p])
            Composites.push(p);

    // Return Nth Composite Number
    return Composites[N - 1];
}

// Driver Code
let N = 4;
document.write(NthComposite(N));

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N + M * log(log(M))，其中**【2，M】**是执行厄拉多塞筛选的范围。*
***辅助空间:** O(N)*