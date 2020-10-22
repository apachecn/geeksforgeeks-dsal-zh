# 计数范围内的素数

> 原文： [https://www.geeksforgeeks.org/count-primes-ranges/](https://www.geeksforgeeks.org/count-primes-ranges/)

给定范围`[L, R]`，我们需要找到范围为`[L, R]`的素数总数，其中`0 <= L <= R < 10000`。 针对不同范围的大量查询。

**示例**：

```
Input : Query 1 : L = 1, R = 10
        Query 2 : L = 5, R = 10
Output : 4
         2
Explanation
Primes in the range L = 1 to R = 10 are 
{2, 3, 5, 7}. Therefore for query, answer 
is 4 {2, 3, 5, 7}.
For the second query, answer is 2 {5, 7}.

```



一个**简单解决方案**是为每个查询`[L, R]`执行以下操作。 从`L`遍历到`R`，[检查当前数字是否为素数](https://www.geeksforgeeks.org/prime-numbers/)。 如果是，则增加计数。 最后返回计数。

一种有效的**解决方案**是使用 [Eratosthenes 筛子](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)查找达到给定极限的所有素数。 然后，我们计算一个前缀数组来存储计数，直到每个值超出限制为止。 一旦有了前缀数组，就可以在`O(1)`时间内回答查询。 我们只需要返回`prefix[R] – prefix[L-1]`。

## C++ 

```cpp

// CPP program to answer queries for count of 
// primes in given range. 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX = 10000; 

// prefix[i] is going to store count of primes 
// till i (including i). 
int prefix[MAX + 1]; 

void buildPrefix() 
{ 
    // Create a boolean array "prime[0..n]". A  
    // value in prime[i] will finally be false  
    // if i is Not a prime, else true. 
    bool prime[MAX + 1]; 
    memset(prime, true, sizeof(prime)); 

    for (int p = 2; p * p <= MAX; p++) { 

        // If prime[p] is not changed, then  
        // it is a prime 
        if (prime[p] == true) { 

            // Update all multiples of p 
            for (int i = p * 2; i <= MAX; i += p) 
                prime[i] = false; 
        } 
    } 

    // Build prefix array 
    prefix[0] = prefix[1] = 0; 
    for (int p = 2; p <= MAX; p++) { 
        prefix[p] = prefix[p - 1]; 
        if (prime[p]) 
            prefix[p]++; 
    } 
} 

// Returns count of primes in range from L to 
// R (both inclusive). 
int query(int L, int R) 
{ 
    return prefix[R] - prefix[L - 1]; 
} 

// Driver code 
int main() 
{ 
    buildPrefix(); 

    int L = 5, R = 10; 
    cout << query(L, R) << endl; 

    L = 1, R = 10; 
    cout << query(L, R) << endl; 

    return 0; 
} 

```

## Java

```java
// Java program to answer queries for  
// count of primes in given range. 
import java.util.*; 
  
class GFG { 
      
static final int MAX = 10000; 
  
// prefix[i] is going to store count  
// of primes till i (including i). 
static int prefix[] = new int[MAX + 1]; 
  
static void buildPrefix() { 
      
    // Create a boolean array "prime[0..n]". A 
    // value in prime[i] will finally be false 
    // if i is Not a prime, else true. 
    boolean prime[] = new boolean[MAX + 1]; 
    Arrays.fill(prime, true); 
  
    for (int p = 2; p * p <= MAX; p++) { 
  
    // If prime[p] is not changed, then 
    // it is a prime 
    if (prime[p] == true) { 
  
        // Update all multiples of p 
        for (int i = p * 2; i <= MAX; i += p) 
        prime[i] = false; 
    } 
    } 
  
    // Build prefix array 
    prefix[0] = prefix[1] = 0; 
    for (int p = 2; p <= MAX; p++) { 
    prefix[p] = prefix[p - 1]; 
    if (prime[p]) 
        prefix[p]++; 
    } 
} 
  
// Returns count of primes in range  
// from L to R (both inclusive). 
static int query(int L, int R) 
{ 
    return prefix[R] - prefix[L - 1];  
} 
  
// Driver code 
public static void main(String[] args) { 
      
    buildPrefix(); 
    int L = 5, R = 10; 
    System.out.println(query(L, R)); 
  
    L = 1; R = 10; 
    System.out.println(query(L, R)); 
} 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python3 program to answer queries for  
# count of primes in given range. 
MAX = 10000
  
# prefix[i] is going to 
# store count of primes 
# till i (including i). 
prefix =[0]*(MAX + 1) 
  
def buildPrefix(): 
      
    # Create a boolean array value in 
    # prime[i] will "prime[0..n]". A  
    # finally be false if i is Not a 
    # prime, else true. 
    prime = [1]*(MAX + 1) 
  
    p = 2
    while(p * p <= MAX):  
  
        # If prime[p] is not changed,  
        # then it is a prime 
        if (prime[p] == 1): 
  
            # Update all multiples of p 
            i = p * 2
            while(i <= MAX): 
                prime[i] = 0
                i += p 
        p+=1
  
    # Build prefix array 
    # prefix[0] = prefix[1] = 0; 
    for p in range(2,MAX+1):  
        prefix[p] = prefix[p - 1] 
        if (prime[p]==1): 
            prefix[p]+=1
  
# Returns count of primes  
# in range from L to 
# R (both inclusive). 
def query(L, R): 
    return prefix[R]-prefix[L - 1] 
  
# Driver code 
if __name__=='__main__': 
    buildPrefix() 
  
    L = 5
    R = 10
    print(query(L, R)) 
  
    L = 1
    R = 10
    print(query(L, R)) 
  
# This code is contributed by mits.
```

## C#

```cs
// C# program to answer  
// queries for count of 
// primes in given range. 
using System; 
  
class GFG 
{ 
static int MAX = 10000; 
  
// prefix[i] is going  
// to store count of  
// primes till i (including i). 
static int[] prefix = new int[MAX + 1]; 
  
static void buildPrefix()  
{ 
      
    // Create a boolean array  
    // "prime[0..n]". A value  
    // in prime[i] will finally  
    // be false if i is Not a 
    // prime, else true. 
    bool[] prime = new bool[MAX + 1]; 
  
    for (int p = 2;  
             p * p <= MAX; p++)  
    { 
  
    // If prime[p] is  
    // not changed, then 
    // it is a prime 
    if (prime[p] == false) 
    { 
  
        // Update all  
        // multiples of p 
        for (int i = p * 2;  
                 i <= MAX; i += p) 
        prime[i] = true; 
    } 
    } 
  
    // Build prefix array 
    prefix[0] = prefix[1] = 0; 
    for (int p = 2; p <= MAX; p++) 
    { 
        prefix[p] = prefix[p - 1]; 
        if (prime[p] == false) 
            prefix[p]++; 
    } 
} 
  
// Returns count of primes  
// in range from L to R  
// (both inclusive). 
static int query(int L, int R) 
{ 
    return prefix[R] -  
           prefix[L - 1];  
} 
  
// Driver code 
public static void Main() 
{ 
    buildPrefix(); 
    int L = 5, R = 10; 
    Console.WriteLine(query(L, R)); 
  
    L = 1; R = 10; 
    Console.WriteLine(query(L, R)); 
} 
} 
  
// This code is contributed 
// by mits.
```

## PHP

```php
<?php 
// PHP program to answer queries for  
// count of primes in given range. 
$MAX = 10000; 
  
// prefix[i] is going to 
// store count of primes 
// till i (including i). 
$prefix = array_fill(0, ($MAX + 1), 0); 
  
function buildPrefix() 
{ 
    global $MAX, $prefix; 
      
    // Create a boolean array value in 
    // prime[i] will "prime[0..n]". A  
    // finally be false if i is Not a 
    // prime, else true. 
    $prime = array_fill(0, ($MAX + 1), true); 
  
    for ($p = 2;  
         $p * $p <= $MAX; $p++)  
    { 
  
        // If prime[p] is not changed,  
        // then it is a prime 
        if ($prime[$p] == true) 
        { 
  
            // Update all multiples of p 
            for ($i = $p * 2;  
                 $i <= $MAX; $i += $p) 
                $prime[$i] = false; 
        } 
    } 
  
    // Build prefix array 
    // $prefix[0] = $prefix[1] = 0; 
    for ($p = 2; $p <= $MAX; $p++)  
    { 
        $prefix[$p] = $prefix[$p - 1]; 
        if ($prime[$p]) 
            $prefix[$p]++; 
    } 
} 
  
// Returns count of primes  
// in range from L to 
// R (both inclusive). 
function query($L, $R) 
{ 
    global $prefix; 
    return $prefix[$R] - 
           $prefix[$L - 1]; 
} 
  
// Driver code 
buildPrefix(); 
  
$L = 5; 
$R = 10; 
echo query($L, $R) . "\n"; 
  
$L = 1; 
$R = 10; 
echo query($L, $R) . "\n"; 
  
// This code is contributed by mits. 
?>
```

输出：

```
2
4
```

