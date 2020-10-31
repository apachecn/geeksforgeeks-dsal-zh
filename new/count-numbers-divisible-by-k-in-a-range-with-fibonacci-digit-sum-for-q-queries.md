# 对`Q`个查询用斐波那契数字总和的范围内的`K`可整除的计数

> 原文：[https://www.geeksforgeeks.org/count-numbers-divisible-by-k-in-a-range-with-fibonacci-digit-sum-for-q-queries/](https://www.geeksforgeeks.org/count-numbers-divisible-by-k-in-a-range-with-fibonacci-digit-sum-for-q-queries/)

给定包含`Q`个查询和整数`K`的数组`arr[][]`，其中每个查询由范围`[L, R]`，任务是找到给定范围内的整数，该整数的[数字总和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)是[斐波那契数](http://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)并且可以被`K`整除。

**示例**：

> **输入**：`arr[][] = {{1, 11}, {5, 15}, {2, 24}}, K = 2`
>
> **输出**：`3 2 5`
>
> **说明**：
>
> 对于查询 1：1、2、8 和 11 是给定范围内的数字，其位数之和为斐波那契，并且可以被`K`整除。 11 是给定范围内的数字，其数字总和是斐波那契并可以被`K`整除。
>
> 查询 3：2、8、11、17 和 20 是给定范围内的数字，其数字总和是斐波那契，并且可以被`K`整除。
> 
> **输入**：`arr[][] = {{2, 17}, {3, 24}}, K = 3`
>
> **输出**：`4 4`
>
> **说明**：
>
> 对于查询 1：1、2、8、11 和 17 是给定范围内的数字，其数字总和为斐波那契并被`K`整除。
>
> 对于查询 2：8、11、17 和 20 是给定范围内的数字，其数字总和为斐波那契并被`K`整除。

**方法**：的想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)预先计算并存储[斐波纳契结点](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，直到给定范围内的最大值，从而使检查变得容易和高效 （在`O(1)`时间内）。

*   预计算后，标记从 **1** 到 **maxVal** 的所有整数，这些整数可以被 **K** 整除并且是斐波那契。

*   查找标记数组的[前缀总和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

*   通过 **prefix [right] – prefix [left – 1]** 回答给定的查询。

下面是上述方法的实现：

## C / C++

```cpp

// C++ program to count the integers 
// in a range [L, R] such that 
// their digit sum is Fibonacci 
// and divisible by K 

#include <bits/stdc++.h> 
using namespace std; 

const int maxSize = 1e5 + 5; 
bool isFib[maxSize]; 
int prefix[maxSize]; 

// Function to return the 
// digit sum of a number 
int digitSum(int num) 
{ 
    int s = 0; 
    while (num != 0) { 
        s = s + num % 10; 
        num = num / 10; 
    } 
    return s; 
} 

// Function to generate all the Fibonacci 
// numbers upto maxSize 
void generateFibonacci() 
{ 
    memset(isFib, false, sizeof(isFib)); 

    // Adding the first two Fibonacci 
    // numbers in the set 
    int prev = 0, curr = 1; 
    isFib[prev] = isFib[curr] = true; 

    // Computing the remaining Fibonacci 
    // numbers based on the previous 
    // two Fibonacci numbers 
    while (curr < maxSize) { 
        int temp = curr + prev; 
        isFib[temp] = true; 
        prev = curr; 
        curr = temp; 
    } 
} 

// Pre-Computation till maxSize 
// and for a given K 
void precompute(int k) 
{ 
    generateFibonacci(); 

    for (int i = 1; i < maxSize; i++) { 

        // Getting the digit sum 
        int sum = digitSum(i); 

        // Check if the digit sum 
        // is Fibonacci and divisible by k 
        if (isFib[sum] == true
            && sum % k == 0) { 
            prefix[i]++; 
        } 
    } 

    // Taking Prefix Sum 
    for (int i = 1; i < maxSize; i++) { 
        prefix[i] = prefix[i] 
                    + prefix[i - 1]; 
    } 
} 

// Function to perform the queries 
void performQueries( 
    int k, int q, 
    vector<vector<int> >& query) 
{ 
    // Precompute the results 
    precompute(k); 

    vector<int> ans; 

    // Iterating through the queries 
    for (int i = 0; i < q; i++) { 

        int l = query[i][0], 
            r = query[i][1]; 

        // Getting count of range 
        // in range [L, R] 
        int cnt = prefix[r] 
                  - prefix[l - 1]; 
        cout << cnt << endl; 
    } 
} 

// Driver code 
int main() 
{ 
    vector<vector<int> > query 
        = { { 1, 11 }, 
            { 5, 15 }, 
            { 2, 24 } }; 
    int k = 2, q = query.size(); 

    performQueries(k, q, query); 

    return 0; 
} 

```

## Java

```java

// Java program to count the integers 
// in a range [L, R] such that 
// their digit sum is Fibonacci 
// and divisible by K 
import java.util.*; 

class GFG{ 

static int maxSize = (int) (1e5 + 5); 
static boolean []isFib  = new boolean[maxSize]; 
static int []prefix = new int[maxSize]; 

// Function to return the 
// digit sum of a number 
static int digitSum(int num) 
{ 
    int s = 0; 
    while (num != 0) { 
        s = s + num % 10; 
        num = num / 10; 
    } 
    return s; 
} 

// Function to generate all the Fibonacci 
// numbers upto maxSize 
static void generateFibonacci() 
{ 
    Arrays.fill(isFib, false); 

    // Adding the first two Fibonacci 
    // numbers in the set 
    int prev = 0, curr = 1; 
    isFib[prev] = isFib[curr] = true; 

    // Computing the remaining Fibonacci 
    // numbers based on the previous 
    // two Fibonacci numbers 
    while (curr < maxSize) { 
        int temp = curr + prev; 
        if(temp < maxSize) 
            isFib[temp] = true; 
        prev = curr; 
        curr = temp; 
    } 
} 

// Pre-Computation till maxSize 
// and for a given K 
static void precompute(int k) 
{ 
    generateFibonacci(); 

    for (int i = 1; i < maxSize; i++) { 

        // Getting the digit sum 
        int sum = digitSum(i); 

        // Check if the digit sum 
        // is Fibonacci and divisible by k 
        if (isFib[sum] == true
            && sum % k == 0) { 
            prefix[i]++; 
        } 
    } 

    // Taking Prefix Sum 
    for (int i = 1; i < maxSize; i++) { 
        prefix[i] = prefix[i] 
                    + prefix[i - 1]; 
    } 
} 

// Function to perform the queries 
static void performQueries( 
    int k, int q, 
    int[][] query) 
{ 
    // Precompute the results 
    precompute(k); 

    // Iterating through the queries 
    for (int i = 0; i < q; i++) { 

        int l = query[i][0], 
            r = query[i][1]; 

        // Getting count of range 
        // in range [L, R] 
        int cnt = prefix[r] 
                  - prefix[l - 1]; 
        System.out.print(cnt +"\n"); 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 

    int [][]query 
        = { { 1, 11 }, 
            { 5, 15 }, 
            { 2, 24 } }; 
    int k = 2, q = query.length; 

    performQueries(k, q, query); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python 3 program to count the integers 
# in a range [L, R] such that 
# their digit sum is Fibonacci 
# and divisible by K 
maxSize = 100005
isFib = [False]*(maxSize) 
prefix = [0]*maxSize 

# Function to return the 
# digit sum of a number 
def digitSum(num): 
    s = 0
    while (num != 0): 
        s = s + num % 10
        num = num // 10

    return s 

# Function to generate all the Fibonacci 
# numbers upto maxSize 
def generateFibonacci(): 

    global isFib 

    # Adding the first two Fibonacci 
    # numbers in the set 
    prev = 0
    curr = 1
    isFib[prev] = True
    isFib[curr] = True

    # Computing the remaining Fibonacci 
    # numbers based on the previous 
    # two Fibonacci numbers 
    while (curr < maxSize): 
        temp = curr + prev 
        if temp < maxSize: 
            isFib[temp] = True
        prev = curr 
        curr = temp 

# Pre-Computation till maxSize 
# and for a given K 
def precompute(k): 

    generateFibonacci() 
    global prefix 

    for i in range(1, maxSize): 

        # Getting the digit sum 
        sum = digitSum(i) 

        # Check if the digit sum 
        # is Fibonacci and divisible by k 
        if (isFib[sum] == True
            and sum % k == 0): 
            prefix[i] += 1

    # Taking Prefix Sum 
    for i in range(1, maxSize): 
        prefix[i] = prefix[i]+ prefix[i - 1] 

# Function to perform the queries 
def performQueries(k, q,query): 

    # Precompute the results 
    precompute(k) 

    # Iterating through the queries 
    for i in range(q): 

        l = query[i][0] 
        r = query[i][1] 

        # Getting count of range 
        # in range [L, R] 
        cnt = prefix[r]- prefix[l - 1] 
        print(cnt) 

# Driver code 
if __name__ == "__main__": 
    query = [ [ 1, 11 ], 
            [ 5, 15 ], 
            [ 2, 24 ] ] 
    k = 2
    q = len(query) 

    performQueries(k, q, query) 

# This code is contributed by chitranayal 

```

## C#

```cs

// C# program to count the integers 
// in a range [L, R] such that 
// their digit sum is Fibonacci 
// and divisible by K 
using System; 

class GFG{ 

static int maxSize = (int) (1e5 + 5); 
static bool []isFib  = new bool[maxSize]; 
static int []prefix = new int[maxSize]; 

// Function to return the 
// digit sum of a number 
static int digitSum(int num) 
{ 
    int s = 0; 
    while (num != 0) { 
        s = s + num % 10; 
        num = num / 10; 
    } 
    return s; 
} 

// Function to generate all the Fibonacci 
// numbers upto maxSize 
static void generateFibonacci() 
{ 

    // Adding the first two Fibonacci 
    // numbers in the set 
    int prev = 0, curr = 1; 
    isFib[prev] = isFib[curr] = true; 

    // Computing the remaining Fibonacci 
    // numbers based on the previous 
    // two Fibonacci numbers 
    while (curr < maxSize) { 
        int temp = curr + prev; 
        if(temp < maxSize) 
            isFib[temp] = true; 
        prev = curr; 
        curr = temp; 
    } 
} 

// Pre-Computation till maxSize 
// and for a given K 
static void precompute(int k) 
{ 
    generateFibonacci(); 

    for (int i = 1; i < maxSize; i++) { 

        // Getting the digit sum 
        int sum = digitSum(i); 

        // Check if the digit sum 
        // is Fibonacci and divisible by k 
        if (isFib[sum] == true
            && sum % k == 0) { 
            prefix[i]++; 
        } 
    } 

    // Taking Prefix Sum 
    for (int i = 1; i < maxSize; i++) { 
        prefix[i] = prefix[i] 
                    + prefix[i - 1]; 
    } 
} 

// Function to perform the queries 
static void performQueries( 
    int k, int q, 
    int[,] query) 
{ 
    // Precompute the results 
    precompute(k); 

    // Iterating through the queries 
    for (int i = 0; i < q; i++) { 

        int l = query[i, 0], 
            r = query[i, 1]; 

        // Getting count of range 
        // in range [L, R] 
        int cnt = prefix[r] 
                  - prefix[l - 1]; 
        Console.Write(cnt +"\n"); 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 

    int [,]query 
        = { { 1, 11 }, 
            { 5, 15 }, 
            { 2, 24 } }; 
    int k = 2, q = query.GetLength(0); 

    performQueries(k, q, query); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
3
2
5

```



* * *

* * *



