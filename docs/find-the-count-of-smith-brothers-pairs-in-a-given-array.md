# 找出给定数组中史密斯兄弟对的计数

> 原文:[https://www . geeksforgeeks . org/find-the-count-of-Smith-brothers-in-a-given-array/](https://www.geeksforgeeks.org/find-the-count-of-smith-brothers-pairs-in-a-given-array/)

给定一个大小为 **N** 的数组 **A[]** ，任务是计算数组中的**史密斯兄弟对**。

> 两个数字 **X** 和 **Y** 如果都是 [**史密斯数字**](https://www.geeksforgeeks.org/smith-number/) 且连续，则称之为**史密斯兄弟对子**。

注:史密斯数是一个复合数，其位数之和等于其素分解中的位数之和。

**示例**:

> **输入** : A = {728，729，28，2964，2965}，N=5
> **输出** : 2
> **说明:**这对是(728，729)和(2964，2965)是史密斯兄弟对，因为它们是史密斯数，也是连续的。
> 
> **输入** : A = {12345，6789}，N=5
> **输出** : 0

**天真的方法**:天真的方法是使用嵌套循环迭代每个可能的对，并检查这些数字是否是史密斯兄弟对。按照以下步骤解决问题:

1.  初始化一个变量**计数**到 **0** ，该变量存储数组中史密斯兄弟对的数量。
2.  [从 **0** 到 **N-1** 遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A** 。对于每个当前指标 **i** ，执行以下操作:
    1.  [从 **i+1** 到 **N-1** 穿越](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2。对于每个当前指标 **j** ，执行以下操作:
        1.  检查**A【I】****A【j】**是否为[史密斯数。](https://www.geeksforgeeks.org/smith-number/)
        2.  如果它们是史密斯数，并且它们的差是 1，则递增计数。
3.  最后，返回**计数**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
const int MAX = 10000;

// array to store all prime less than and equal to MAX
vector<int> primes;

// utility function for sieve of sundaram
void sieveSundaram()
{
    bool marked[MAX / 2 + 100] = { 0 };

    // Main logic of Sundaram.
    for (int i = 1; i <= (sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1; j <= MAX / 2;
             j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // only primes are selected
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push_back(2 * i + 1);
}

// Function to check whether a number is a smith number.
bool isSmith(int n)
{
    int original_no = n;

    // Find sum the digits of prime factors of n
    int pDigitSum = 0;
    for (int i = 0; primes[i] <= n / 2; i++) {
        while (n % primes[i] == 0) {
            // add its digits of prime factors to pDigitSum.
            int p = primes[i];
            n = n / p;
            while (p > 0) {
                pDigitSum += (p % 10);
                p = p / 10;
            }
        }
    }

    // one prime factor is still to be summed up
    if (n != 1 && n != original_no) {
        while (n > 0) {
            pDigitSum = pDigitSum + n % 10;
            n = n / 10;
        }
    }
    // Now sum the digits of the original number
    int sumDigits = 0;
    while (original_no > 0) {
        sumDigits = sumDigits + original_no % 10;
        original_no = original_no / 10;
    }

    // return the answer
    return (pDigitSum == sumDigits);
}

// Function to check if X and Y are a
// Smith Brother Pair
bool isSmithBrotherPair(int X, int Y)
{
    return isSmith(X) && isSmith(Y) && abs(X - Y) == 1;
}

// Function to find pairs from array
int countSmithBrotherPairs(int A[], int N)
{
    int count = 0;
    // Iterate through all pairs
    for (int i = 0; i < N; i++)
        for (int j = i + 1; j < N; j++) {
            // Increment count if there is a smith brother
            // pair
            if (isSmithBrotherPair(A[i], A[j]))
                count++;
        }
    return count;
}

// Driver code
int main()
{
    // Preprocessing
    sieveSundaram();
    // Input
    int A[] = { 728, 729, 28, 2964, 2965 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << countSmithBrotherPairs(A, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG{

static int MAX = 10000;

// Array to store all prime less than and equal to MAX
static ArrayList<Integer> primes = new ArrayList<Integer>();

// Utility function for sieve of sundaram
public static void sieveSundaram()
{
    ArrayList<Boolean> marked = new ArrayList<Boolean>(
        MAX / 2 + 100);

    for(int i = 0; i < MAX / 2 + 100; i++)
    {
        marked.add(false);
    }

    // Main logic of Sundaram.
    for(int i = 1; i <= (Math.sqrt(MAX) - 1) / 2; i++)
        for(int j = (i * (i + 1)) << 1;
                j <= MAX / 2;
                j = j + 2 * i + 1)
            marked.set(j, true);

    // Since 2 is a prime number
    primes.add(2);

    // Only primes are selected
    for(int i = 1; i <= MAX / 2; i++)
        if (marked.get(i) == false)
            primes.add(2 * i + 1);
}

// Function to check whether a number is a smith number.
public static Boolean isSmith(int n)
{
    int original_no = n;

    // Find sum the digits of prime factors of n
    int pDigitSum = 0;

    for(int i = 0; primes.get(i) <= n / 2; i++)
    {
        while (n % primes.get(i) == 0)
        {

            // Add its digits of prime factors
            // to pDigitSum.
            int p = primes.get(i);
            n = n / p;

            while (p > 0)
            {
                pDigitSum += (p % 10);
                p = p / 10;
            }
        }
    }

    // One prime factor is still to be summed up
    if (n != 1 && n != original_no)
    {
        while (n > 0)
        {
            pDigitSum = pDigitSum + n % 10;
            n = n / 10;
        }
    }

    // Now sum the digits of the original number
    int sumDigits = 0;
    while (original_no > 0)
    {
        sumDigits = sumDigits + original_no % 10;
        original_no = original_no / 10;
    }

    // Return the answer
    return (pDigitSum == sumDigits);
}

// Function to check if X and Y are a
// Smith Brother Pair
public static Boolean isSmithBrotherPair(int X, int Y)
{
    return isSmith(X) && isSmith(Y) &&
           Math.abs(X - Y) == 1;
}

// Function to find pairs from array
public static Integer countSmithBrotherPairs(int A[],
                                             int N)
{
    int count = 0;

    // Iterate through all pairs
    for(int i = 0; i < N; i++)
        for(int j = i + 1; j < N; j++)
        {

            // Increment count if there is a
            // smith brother pair
            if (isSmithBrotherPair(A[i], A[j]))
                count++;
        }
    return count;
}

// Driver code
public static void main(String args[])
{

    // Preprocessing
    sieveSundaram();

    // Input
    int A[] = { 728, 729, 28, 2964, 2965 };
    int N = A.length;

    // Function call
    System.out.println(countSmithBrotherPairs(A, N));
}
}

// This code is contributed by _saurabh_jaiswal
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt
MAX = 10000

# Array to store all prime less than
# and equal to MAX
primes = []

# Utility function for sieve of sundaram
def sieveSundaram():

    marked = [0 for i in range(MAX // 2 + 100)]

    # Main logic of Sundaram.
    j = 0
    for i in range(1, int((sqrt(MAX) - 1) / 2) + 1, 1):
        for j in range((i * (i + 1)) << 1,
                      MAX // 2 + 1, j + 2 * i + 1):
            marked[j] = True

    # Since 2 is a prime number
    primes.append(2)

    # only primes are selected
    for i in range(1, MAX // 2 + 1, 1):
        if (marked[i] == False):
            primes.append(2 * i + 1)

# Function to check whether a number
# is a smith number.
def isSmith(n):

    original_no = n

    # Find sum the digits of prime
    # factors of n
    pDigitSum = 0
    i = 0

    while (primes[i] <= n // 2):
        while (n % primes[i] == 0):

            # Add its digits of prime factors
            # to pDigitSum.
            p = primes[i]
            n = n // p

            while (p > 0):
                pDigitSum += (p % 10)
                p = p // 10

        i += 1

    # One prime factor is still to be summed up
    if (n != 1 and n != original_no):
        while (n > 0):
            pDigitSum = pDigitSum + n % 10
            n = n // 10

    # Now sum the digits of the original number
    sumDigits = 0

    while (original_no > 0):
        sumDigits = sumDigits + original_no % 10
        original_no = original_no // 10

    # Return the answer
    return (pDigitSum == sumDigits)

# Function to check if X and Y are a
# Smith Brother Pair
def isSmithBrotherPair(X, Y):

    return (isSmith(X) and isSmith(Y) and
            abs(X - Y) == 1)

# Function to find pairs from array
def countSmithBrotherPairs(A, N):

    count = 0

    # Iterate through all pairs
    for i in range(N):
        for j in range(i + 1, N, 1):

            # Increment count if there is a
            # smith brother pair
            if (isSmithBrotherPair(A[i], A[j])):
                count += 1

    return count

# Driver code
if __name__ == '__main__':

    # Preprocessing
    sieveSundaram()

    # Input
    A = [ 728, 729, 28, 2964, 2965 ]
    N = len(A)

    # Function call
    print(countSmithBrotherPairs(A, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int MAX = 10000;

// array to store all prime less than and equal to MAX
static List<int> primes = new List<int>();

// utility function for sieve of sundaram
static void sieveSundaram()
{
    int []marked = new int[MAX / 2 + 100];
    Array.Clear(marked,0,MAX/2 +100);

    // Main logic of Sundaram.
    for (int i = 1; i <= (int)(Math.Sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1; j <= MAX / 2;
             j = j + 2 * i + 1)
             marked[j] = 1;

    // Since 2 is a prime number
    primes.Add(2);

    // only primes are selected
    for (int i = 1; i <= (int)MAX / 2; i++)
        if (marked[i] == 0)
            primes.Add(2 * i + 1);
}

// Function to check whether a number is a smith number.
static bool isSmith(int n)
{
    int original_no = n;

    // Find sum the digits of prime factors of n
    int pDigitSum = 0;
    for (int i = 0; primes[i] <= n / 2; i++)
    {
        while (n % primes[i] == 0)
        {

            // add its digits of prime factors to pDigitSum.
            int p = primes[i];
            n = n / p;
            while (p > 0) {
                pDigitSum += (p % 10);
                p = p / 10;
            }
        }
    }

    // one prime factor is still to be summed up
    if (n != 1 && n != original_no) {
        while (n > 0) {
            pDigitSum = pDigitSum + n % 10;
            n = n / 10;
        }
    }

    // Now sum the digits of the original number
    int sumDigits = 0;
    while (original_no > 0) {
        sumDigits = sumDigits + original_no % 10;
        original_no = original_no / 10;
    }

    // return the answer
    return (pDigitSum == sumDigits);
}

// Function to check if X and Y are a
// Smith Brother Pair
static bool isSmithBrotherPair(int X, int Y)
{
    return isSmith(X) && isSmith(Y) && Math.Abs(X - Y) == 1;
}

// Function to find pairs from array
static int countSmithBrotherPairs(int []A, int N)
{
    int count = 0;

    // Iterate through all pairs
    for (int i = 0; i < N; i++)
        for (int j = i + 1; j < N; j++)
        {

            // Increment count if there is a smith brother
            // pair
            if (isSmithBrotherPair(A[i], A[j]))
                count++;
        }
    return count;
}

// Driver code
public static void Main()
{
    // Preprocessing
    sieveSundaram();

    // Input
    int []A = { 728, 729, 28, 2964, 2965 };
    int N = A.Length;

    // Function call
    Console.Write(countSmithBrotherPairs(A, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let MAX = 10000;

// array to store all prime less than and equal to MAX
let primes = new Array();

// utility function for sieve of sundaram
function sieveSundaram()
{
    let marked = Array.from({length: MAX / 2 + 100}, (_, i) => 0);

    // Main logic of Sundaram.
    for (let i = 1; i <= (Math.floor(Math.sqrt(MAX) - 1)) / 2; i++)
        for (let j = (i * (i + 1)) << 1; j <= MAX / 2;
             j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push(2);

    // only primes are selected
    for (let i = 1; i <= Math.floor(MAX / 2); i++)
        if (marked[i] == false)
            primes.push(2 * i + 1);
}

// Function to check whether a number is a smith number.
function isSmith(n)
{
    let original_no = n;

    // Find sum the digits of prime factors of n
    let pDigitSum = 0;
    for (let i = 0; primes[i] <= Math.floor(n / 2); i++) {
        while (n % primes[i] == 0) {
            // add its digits of prime factors to pDigitSum.
            let p = primes[i];
            n = Math.floor(n / p);
            while (p > 0) {
                pDigitSum += (p % 10);
                p = Math.floor(p / 10);
            }
        }
    }

    // one prime factor is still to be summed up
    if (n != 1 && n != original_no) {
        while (n > 0) {
            pDigitSum = pDigitSum + n % 10;
            n = Math.floor(n / 10);
        }
    }
    // Now sum the digits of the original number
    let sumDigits = 0;
    while (original_no > 0) {
        sumDigits = sumDigits + original_no % 10;
        original_no = Math.floor(original_no / 10);
    }

    // return the answer
    return (pDigitSum == sumDigits);
}

// Function to check if X and Y are a
// Smith Brother Pair
function isSmithBrotherPair(X, Y)
{
    return isSmith(X) && isSmith(Y) && Math.abs(X - Y) == 1;
}

// Function to find pairs from array
function countSmithBrotherPairs(A, N)
{
    let count = 0;
    // Iterate through all pairs
    for (let i = 0; i < N; i++)
        for (let j = i + 1; j < N; j++) {
            // Increment count if there is a smith brother
            // pair
            if (isSmithBrotherPair(A[i], A[j]))
                count++;
        }
    return count;
}

// Driver Code

    // Preprocessing
    sieveSundaram();
    // Input
    let A = [ 728, 729, 28, 2964, 2965 ];
    let N = A.length;

    // Function call
    document.write(countSmithBrotherPairs(A, N));

</script>
```

**Output**

```
2
```

***时间复杂度:**O(M+N<sup>2</sup>)*
***辅助空间:** O(M)*

**有效方法:**由于只有连续的史密斯数才能形成史密斯兄弟对，最佳解决方案是[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)**进行排序，然后，只检查连续的元素。
按照以下步骤解决问题。**

1.  **将变量**计数**初始化为 **0** 。**
2.  **[整理](https://www.geeksforgeeks.org/sort-c-stl/)阵列，**一**。**
3.  **[从 0 到 **N-2** 遍历](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A** ，对于每个当前索引 **i** ，执行以下操作:

    1.  检查 **A[i]** 和 **A[i+1]** 是否都是[史密斯数。](https://www.geeksforgeeks.org/smith-number/)
    2.  如果都是史密斯数，递增**计数**。** 
4.  **最后，返回**计数**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
const int MAX = 10000;

// array to store all prime
// less than and equal to MAX
vector<int> primes;

// utility function for sieve of sundaram
void sieveSundaram()
{
    bool marked[MAX / 2 + 100] = { 0 };

    // Main logic of Sundaram.
    for (int i = 1; i <= (sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1; j <= MAX / 2;
             j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // only primes are selected
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push_back(2 * i + 1);
}

// Function to check whether
// a number is a smith number.
bool isSmith(int n)
{
    int original_no = n;

    // Find sum the digits of prime factors of n
    int pDigitSum = 0;
    for (int i = 0; primes[i] <= n / 2; i++) {
        while (n % primes[i] == 0) {
            // add its digits of
            // prime factors to pDigitSum.
            int p = primes[i];
            n = n / p;
            while (p > 0) {
                pDigitSum += (p % 10);
                p = p / 10;
            }
        }
    }

    // one prime factor is still to be summed up
    if (n != 1 && n != original_no) {
        while (n > 0) {
            pDigitSum = pDigitSum + n % 10;
            n = n / 10;
        }
    }
    // Now sum the digits of the original number
    int sumDigits = 0;
    while (original_no > 0) {
        sumDigits = sumDigits + original_no % 10;
        original_no = original_no / 10;
    }

    // return the answer
    return (pDigitSum == sumDigits);
}

// Function to check if X and Y are a
// Smith Brother Pair
bool isSmithBrotherPair(int X, int Y)
{
    return isSmith(X) && isSmith(Y);
}

// Function to find pairs from array
int countSmithBrotherPairs(int A[], int N)
{
    // Variable to store number
    // of Smith Brothers Pairs
    int count = 0;
    // sort A
    sort(A, A + N);
    // check for consecutive numbers only
    for (int i = 0; i < N - 2; i++)
        if (isSmithBrotherPair(A[i], A[i + 1]))
            count++;
    return count;
}

// Driver code
int main()
{
    // Preprocessing sieve of sundaram
    sieveSundaram();
    // Input
    int A[] = { 728, 729, 28, 2964, 2965 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << countSmithBrotherPairs(A, N) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG {

static int MAX = 10000;

// array to store all prime
// less than and equal to MAX
static ArrayList<Integer> primes = new ArrayList<Integer>();

// utility function for sieve of sundaram
static void sieveSundaram()
{
     ArrayList<Boolean> marked = new ArrayList<Boolean>(
        MAX / 2 + 100);

    for(int i = 0; i < MAX / 2 + 100; i++)
    {
        marked.add(false);
    }

    // Main logic of Sundaram.
    for (int i = 1; i <= (Math.sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1; j <= MAX / 2;
             j = j + 2 * i + 1)
            marked.set(j, true);

    // Since 2 is a prime number
    primes.add(2);

    // only primes are selected
    for (int i = 1; i <= MAX / 2; i++)
        if (marked.get(i) == false)
            primes.add(2 * i + 1);
}

// Function to check whether
// a number is a smith number.
static Boolean isSmith(int n)
{
    int original_no = n;

    // Find sum the digits of prime factors of n
    int pDigitSum = 0;
    for (int i = 0; primes.get(i) <= n / 2; i++) {
        while (n % primes.get(i) == 0) {
            // add its digits of
            // prime factors to pDigitSum.
            int p = primes.get(i);
            n = n / p;
            while (p > 0) {
                pDigitSum += (p % 10);
                p = p / 10;
            }
        }
    }

    // one prime factor is still to be summed up
    if (n != 1 && n != original_no) {
        while (n > 0) {
            pDigitSum = pDigitSum + n % 10;
            n = n / 10;
        }
    }
    // Now sum the digits of the original number
    int sumDigits = 0;
    while (original_no > 0) {
        sumDigits = sumDigits + original_no % 10;
        original_no = original_no / 10;
    }

    // return the answer
    return (pDigitSum == sumDigits);
}

// Function to check if X and Y are a
// Smith Brother Pair
static Boolean isSmithBrotherPair(int X, int Y)
{
    return isSmith(X) && isSmith(Y);
}

// Function to find pairs from array
static Integer countSmithBrotherPairs(int A[], int N)
{
    // Variable to store number
    // of Smith Brothers Pairs
    int count = 0;

    // sort A
    Arrays.sort(A);

    // check for consecutive numbers only
    for (int i = 0; i < N - 2; i++)
        if (isSmithBrotherPair(A[i], A[i + 1]))
            count++;
    return count;
}

// Driver Code
public static void main(String[] args)
{
    // Preprocessing sieve of sundaram
    sieveSundaram();
    // Input
    int A[] = { 728, 729, 28, 2964, 2965 };
    int N = A.length;

    // Function call
    System.out.print(countSmithBrotherPairs(A, N));
}
}

// This code is contributed by avijitmondal1998.
```

## **java 描述语言**

```
<script>
       // JavaScript Program for the above approach

       const MAX = 10000;

       // array to store all prime
       // less than and equal to MAX
       var primes = [];

       // utility function for sieve of sundaram
       function sieveSundaram() {
           let marked = new Array(MAX / 2 + 100).fill(false);

           // Main logic of Sundaram.
           for (let i = 1; i <= (Math.sqrt(MAX) - 1) / 2; i++)
               for (let j = (i * (i + 1)) << 1; j <= MAX / 2;
                   j = j + 2 * i + 1)
                   marked[j] = true;

           // Since 2 is a prime number
           primes.push(2);

           // only primes are selected
           for (let i = 1; i <= MAX / 2; i++)
               if (marked[i] == false)
                   primes.push(2 * i + 1);
       }

       // Function to check whether
       // a number is a smith number.
       function isSmith(n) {
           let original_no = n;

           // Find sum the digits of prime factors of n
           let pDigitSum = 0;
           for (let i = 0; primes[i] <= Math.floor(n / 2); i++) {
               while (n % primes[i] == 0) {
                   // add its digits of
                   // prime factors to pDigitSum.
                   let p = primes[i];
                   n = Math.floor(n / p);
                   while (p > 0) {
                       pDigitSum += (p % 10);
                       p = Math.floor(p / 10);
                   }
               }
           }

           // one prime factor is still to be summed up
           if (n != 1 && n != original_no) {
               while (n > 0) {
                   pDigitSum = pDigitSum + n % 10;
                   n = Math.floor(n / 10);
               }
           }
           // Now sum the digits of the original number
           let sumDigits = 0;
           while (original_no > 0) {
               sumDigits = sumDigits + original_no % 10;
               original_no = Math.floor(original_no / 10);
           }

           // return the answer
           return (pDigitSum == sumDigits);
       }

       // Function to check if X and Y are a
       // Smith Brother Pair
       function isSmithBrotherPair(X, Y) {
           return isSmith(X) && isSmith(Y);
       }

       // Function to find pairs from array
       function countSmithBrotherPairs(A, N) {
           // Variable to store number
           // of Smith Brothers Pairs
           let count = 0;
           // sort A
           A.sort(function (a, b) { return a - b });
           // check for consecutive numbers only
           for (let i = 0; i < N - 2; i++)
               if (isSmithBrotherPair(A[i], A[i + 1]))
                   count++;
           return count;
       }

       // Driver code

       // Preprocessing sieve of sundaram
       sieveSundaram();
       // Input
       let A = [728, 729, 28, 2964, 2965];
       let N = A.length;

       // Function call
       document.write(countSmithBrotherPairs(A, N));

   // This code is contributed by Potta Lokesh
   </script>
```

****Output**

```
2
```** 

*****时间复杂度:**O(M+NLogN)*
T5**辅助空间:** O(M)**

**参考:[https://mathworld.wolfram.com/SmithBrothers.html](https://mathworld.wolfram.com/SmithBrothers.html)**