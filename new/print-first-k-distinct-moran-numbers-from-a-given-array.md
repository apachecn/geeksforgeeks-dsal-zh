# 打印给定数组中的前 K 个不同的 Moran 编号

给定[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，其中包含 **N** 个不同的正整数，任务是打印第一个 **K** 个不同的 [Moran 给定数组中的数字](https://www.geeksforgeeks.org/check-whether-given-number-n-is-a-moran-number-or-not/)。

> *数字 **N** 是 **Moran 数**，如果 **N** 除以其位数* [*的总和*](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/) *给出* [***素数***](https://www.geeksforgeeks.org/prime-numbers/) *。*
> ***范例**：18、21、27、42、45*

**示例**：

> **输入**：arr [] = {192、21、18、138、27、42、45}，K = 4
> **输出**：21、27、42、45 [
> **说明**：
> 
> *   整数 21 的位数之和为 2 +1 =3。因此，将 21 除以其位数之和= 21/3 = 7，这是质数。
> *   整数 27 的位数之和为 2 + 7 =9。因此，将 27 除以其位数之和得出 27/9 = 3，这是质数。
> *   整数 42 的位数之和为 4 + 2 =6。因此，将 42 除以其位数之和得出 42/6 = 7，这是质数。
> *   整数 45 的位数之和为 4 + 5 =9。因此，将 45 除以其位数之和得出 45/9 = 5，这是质数。
> 
> **输入**：arr [] = {127，186，198，63，27，91}，K = 3
> **输出**：27，63，198

**方法**：请按照以下步骤解决问题：

1.  [对数组进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
2.  [遍历排序后的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，[检查其是否为莫兰数](https://www.geeksforgeeks.org/check-whether-given-number-n-is-a-moran-number-or-not/)
3.  如果确定为真，则将元素插入[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，并递增**计数器**直到达到 **K** 。
4.  当组的[大小等于 **K** 时，打印**组**中的元素。](https://www.geeksforgeeks.org/setsize-c-stl/)

下面是上述方法的实现：

## C++

```cpp

#include <algorithm> 
#include <iostream> 
#include <set> 
using namespace std; 

// Function to calculate the 
// sum of digits of a number 
int digiSum(int a) 
{ 
    // Stores the sum of digits 
    int sum = 0; 
    while (a) { 

        // Add the digit to sum 
        sum += a % 10; 

        // Remove digit 
        a = a / 10; 
    } 

    // Returns the sum 
    // of digits 
    return sum; 
} 

// Function to check if a number 
// is prime or not 
bool isPrime(int r) 
{ 
    bool s = true; 

    for (int i = 2; i * i <= r; i++) { 

        // If r has any divisor 
        if (r % i == 0) { 

            // Set r as non-prime 
            s = false; 
            break; 
        } 
    } 
    return s; 
} 

// Function to check if a 
// number is moran number 
bool isMorannumber(int n) 
{ 
    int dup = n; 

    // Calculate sum of digits 
    int sum = digiSum(dup); 

    // Check if n is divisible 
    // by the sum of digits 
    if (n % sum == 0) { 

        // Calculate the quotient 
        int c = n / sum; 

        // If the quotient is prime 
        if (isPrime(c)) { 

            return true; 
        } 
    } 

    return false; 
} 

// Function to print the first K 
// Moran numbers from the array 
void FirstKMorannumber(int a[], 
                       int n, int k) 
{ 
    int X = k; 

    // Sort the given array 
    sort(a, a + n); 

    // Initialise a set 
    set<int> s; 

    // Traverse the array from the end 
    for (int i = n - 1; i >= 0 
                        && k > 0; 
         i--) { 
        // If the current array element 
        // is a Moran number 
        if (isMorannumber(a[i])) { 

            // Insert into the set 
            s.insert(a[i]); 
            k--; 
        } 
    } 

    if (k > 0) { 
        cout << X << " Moran numbers are"
             << " not present in the array" << endl; 
        return; 
    } 

    set<int>::iterator it; 
    for (it = s.begin(); it != s.end(); ++it) { 
        cout << *it << ", "; 
    } 
    cout << endl; 
} 

// Driver Code 
int main() 
{ 

    int A[] = { 34, 198, 21, 42, 
                63, 45, 22, 44, 43 }; 
    int K = 4; 

    int N = sizeof(A) / sizeof(A[0]); 

    FirstKMorannumber(A, N, K); 

    return 0; 
} 

```

## Java

```java

import java.io.*; 
import java.util.*; 

class GFG{ 

// Function to calculate the 
// sum of digits of a number 
static int digiSum(int a) 
{ 

    // Stores the sum of digits 
    int sum = 0; 
    while (a != 0) 
    { 

        // Add the digit to sum 
        sum += a % 10; 

        // Remove digit 
        a = a / 10; 
    } 

    // Returns the sum 
    // of digits 
    return sum; 
} 

// Function to check if a number 
// is prime or not 
static boolean isPrime(int r) 
{ 
    boolean s = true; 

    for(int i = 2; i * i <= r; i++) 
    { 

        // If r has any divisor 
        if (r % i == 0) 
        { 

            // Set r as non-prime 
            s = false; 
            break; 
        } 
    } 
    return s; 
} 

// Function to check if a 
// number is moran number 
static boolean isMorannumber(int n) 
{ 
    int dup = n; 

    // Calculate sum of digits 
    int sum = digiSum(dup); 

    // Check if n is divisible 
    // by the sum of digits 
    if (n % sum == 0)  
    { 

        // Calculate the quotient 
        int c = n / sum; 

        // If the quotient is prime 
        if (isPrime(c)) 
        { 
            return true; 
        } 
    } 
    return false; 
} 

// Function to print the first K 
// Moran numbers from the array 
static void FirstKMorannumber(int[] a,  
                              int n, int k) 
{ 
    int X = k; 

    // Sort the given array 
    Arrays.sort(a); 

    // Initialise a set 
    TreeSet<Integer> s = new TreeSet<Integer>(); 

    // Traverse the array from the end 
    for(int i = n - 1; i >= 0 && k > 0; i--)  
    { 

        // If the current array element 
        // is a Moran number 
        if (isMorannumber(a[i]))  
        { 

            // Insert into the set 
            s.add(a[i]); 
            k--; 
        } 
    } 

    if (k > 0)  
    { 
        System.out.println(X + " Moran numbers are" +  
                               " not present in the array"); 
        return; 
    } 

    for(int value : s) 
        System.out.print(value + ", "); 

    System.out.print("\n"); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int[] A = { 34, 198, 21, 42,  
                63, 45, 22, 44, 43 }; 
    int K = 4; 

    int N = A.length; 

    FirstKMorannumber(A, N, K); 
} 
} 

// This code is contributed by akhilsaini

```

## Python3

```py

import math 

# Function to calculate the 
# sum of digits of a number 
def digiSum(a): 

    # Stores the sum of digits 
    sums = 0
    while (a != 0): 

        # Add the digit to sum 
        sums += a % 10

        # Remove digit 
        a = a // 10

    # Returns the sum 
    # of digits 
    return sums 

# Function to check if a number 
# is prime or not 
def isPrime(r): 

    s = True

    for i in range(2, int(math.sqrt(r)) + 1): 

        # If r has any divisor 
        if (r % i == 0): 

            # Set r as non-prime 
            s = False
            break

    return s 

# Function to check if a 
# number is moran number 
def isMorannumber(n): 

    dup = n 

    # Calculate sum of digits 
    sums = digiSum(dup) 

    # Check if n is divisible 
    # by the sum of digits 
    if (n % sums == 0): 

        # Calculate the quotient 
        c = n // sums 

        # If the quotient is prime 
        if isPrime(c): 
            return True

    return False

# Function to print the first K 
# Moran numbers from the array 
def FirstKMorannumber(a, n, k): 

    X = k 

    # Sort the given array 
    a.sort() 

    # Initialise a set 
    s = set() 

    # Traverse the array from the end 
    for i in range(n - 1, -1, -1): 
        if (k <= 0): 
            break

        # If the current array element 
        # is a Moran number 
        if (isMorannumber(a[i])): 

            # Insert into the set 
            s.add(a[i]) 
            k -= 1

    if (k > 0): 
        print(X, end =' Moran numbers are not '
                       'present in the array') 
        return

    lists = sorted(s) 
    for i in lists: 
        print(i, end = ', ') 

# Driver Code 
if __name__ == '__main__': 

    A = [ 34, 198, 21, 42,  
          63, 45, 22, 44, 43 ] 
    K = 4

    N = len(A) 

    FirstKMorannumber(A, N, K) 

# This code is contributed by akhilsaini

```

## C#

```cs

using System; 
using System.Collections; 
using System.Collections.Generic; 

class GFG{ 

// Function to calculate the 
// sum of digits of a number 
static int digiSum(int a) 
{ 

    // Stores the sum of digits 
    int sum = 0; 
    while (a != 0) 
    { 

        // Add the digit to sum 
        sum += a % 10; 

        // Remove digit 
        a = a / 10; 
    } 

    // Returns the sum 
    // of digits 
    return sum; 
} 

// Function to check if a number 
// is prime or not 
static bool isPrime(int r) 
{ 
    bool s = true; 

    for(int i = 2; i * i <= r; i++) 
    { 

        // If r has any divisor 
        if (r % i == 0) 
        { 

            // Set r as non-prime 
            s = false; 
            break; 
        } 
    } 
    return s; 
} 

// Function to check if a 
// number is moran number 
static bool isMorannumber(int n) 
{ 
    int dup = n; 

    // Calculate sum of digits 
    int sum = digiSum(dup); 

    // Check if n is divisible 
    // by the sum of digits 
    if (n % sum == 0) 
    { 

        // Calculate the quotient 
        int c = n / sum; 

        // If the quotient is prime 
        if (isPrime(c))  
        { 
            return true; 
        } 
    } 
    return false; 
} 

// Function to print the first K 
// Moran numbers from the array 
static void FirstKMorannumber(int[] a, 
                              int n, int k) 
{ 
    int X = k; 

    // Sort the given array 
    Array.Sort(a); 

    // Initialise a set 
    SortedSet<int> s = new SortedSet<int>(); 

    // Traverse the array from the end 
    for(int i = n - 1; i >= 0 && k > 0; i--) 
    { 

        // If the current array element 
        // is a Moran number 
        if (isMorannumber(a[i])) 
        { 

            // Insert into the set 
            s.Add(a[i]); 
            k--; 
        } 
    } 

    if (k > 0) 
    { 
        Console.WriteLine(X + " Moran numbers are" +  
                              " not present in the array"); 
        return; 
    } 

    foreach(var val in s) 
    { 
        Console.Write(val + ", "); 
    } 
    Console.Write("\n"); 
} 

// Driver Code 
public static void Main() 
{ 
    int[] A = { 34, 198, 21, 42,  
                63, 45, 22, 44, 43 }; 
    int K = 4; 

    int N = A.Length; 

    FirstKMorannumber(A, N, K); 
} 
} 

// This code is contributed by akhilsaini

```

**Output:** 

```
42, 45, 63, 198,

```

***时间复杂度**：O（N <sup>3/2</sup> ）*
***辅助空间**：O（N）*



* * *

* * *



