# 数组中范围的乘积

> 原文： [https://www.geeksforgeeks.org/products-ranges-array/](https://www.geeksforgeeks.org/products-ranges-array/)

给定大小为`N`的数组`A[]`。解决`Q`个查询。 在模`P`下找到`[L, R]`范围内的乘积（`P`为质数）。

**示例**：

```
Input : A[] = {1, 2, 3, 4, 5, 6} 
          L = 2, R = 5, P = 229
Output : 120

Input : A[] = {1, 2, 3, 4, 5, 6},
         L = 2, R = 5, P = 113
Output : 7

```



**暴力**：

对于每个查询，遍历`[L, R]`范围内的每个元素并计算模`P`下的乘积。这将以`O(n)`回答每个查询。

## C++ 

```cpp

// Product in range  
// Queries in O(N) 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate  
// Product in the given range. 
int calculateProduct(int A[], int L,  
                     int R, int P) 
{ 
    // As our array is 0 based  
    // as and L and R are given 
    // as 1 based index. 
    L = L - 1; 
    R = R - 1; 

    int ans = 1; 
    for (int i = L; i <= R; i++)  
    { 
        ans = ans * A[i]; 
        ans = ans % P; 
    } 

    return ans; 
} 

// Driver code 
int main() 
{ 
    int A[] = { 1, 2, 3, 4, 5, 6 }; 
    int P = 229; 
    int L = 2, R = 5; 
    cout << calculateProduct(A, L, R, P) 
         << endl; 

    L = 1, R = 3; 
    cout << calculateProduct(A, L, R, P)  
         << endl; 

    return 0; 
} 

```

## Java

```
// Product in range Queries in O(N) 
import java.io.*; 
  
class GFG  
{ 
      
    // Function to calculate  
    // Product in the given range. 
    static int calculateProduct(int []A, int L,  
                                int R, int P) 
    { 
          
        // As our array is 0 based as  
        // and L and R are given as 1  
        // based index. 
        L = L - 1; 
        R = R - 1; 
      
        int ans = 1; 
        for (int i = L; i <= R; i++) 
        { 
            ans = ans * A[i]; 
            ans = ans % P; 
        } 
      
        return ans; 
    } 
      
    // Driver code 
    static public void main (String[] args) 
    { 
        int []A = { 1, 2, 3, 4, 5, 6 }; 
        int P = 229; 
        int L = 2, R = 5; 
        System.out.println( 
            calculateProduct(A, L, R, P)); 
      
        L = 1;  
        R = 3; 
        System.out.println( 
            calculateProduct(A, L, R, P)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## Python3

```
# Python3 program to find  
# Product in range Queries in O(N) 
  
# Function to calculate Product  
# in the given range. 
def calculateProduct (A, L, R, P): 
  
    # As our array is 0 based   
    # and L and R are given as 
    # 1 based index. 
    L = L - 1
    R = R - 1
    ans = 1
    for i in range(R + 1): 
        ans = ans * A[i] 
        ans = ans % P 
    return ans 
      
# Driver code 
A = [ 1, 2, 3, 4, 5, 6 ] 
P = 229
L = 2
R = 5
print (calculateProduct(A, L, R, P)) 
L = 1
R = 3
print (calculateProduct(A, L, R, P)) 
  
# This code is contributed  
# by "Abhishek Sharma 44"
```

## C#

```
// Product in range Queries in O(N) 
using System; 
  
class GFG  
{ 
      
    // Function to calculate  
    // Product in the given range. 
    static int calculateProduct(int []A, int L,      
                                int R, int P) 
    { 
          
        // As our array is 0 based  
        // as and L and R are given  
        // as 1 based index. 
        L = L - 1; 
        R = R - 1; 
      
        int ans = 1; 
        for (int i = L; i <= R; i++) 
        { 
            ans = ans * A[i]; 
            ans = ans % P; 
        } 
      
        return ans; 
    } 
      
    // Driver code 
    static public void Main () 
    { 
        int []A = { 1, 2, 3, 4, 5, 6 }; 
        int P = 229; 
        int L = 2, R = 5; 
        Console.WriteLine( 
            calculateProduct(A, L, R, P)); 
      
        L = 1;  
        R = 3; 
        Console.WriteLine( 
            calculateProduct(A, L, R, P)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// Product in range Queries in O(N) 
  
// Function to calculate  
// Product in the given range. 
function calculateProduct($A, $L,  
                          $R, $P) 
{ 
    // As our array is 0 based as  
    // and L and R are given as 1  
    // based index. 
    $L = $L - 1; 
    $R = $R - 1; 
  
    $ans = 1; 
    for ($i = $L; $i <= $R; $i++)  
    { 
        $ans = $ans * $A[$i]; 
        $ans = $ans % $P; 
    } 
  
    return $ans; 
} 
  
// Driver code 
$A = array( 1, 2, 3, 4, 5, 6 ); 
$P = 229; 
$L = 2; $R = 5; 
echo calculateProduct($A, $L, $R, $P),"\n" ; 
  
$L = 1; $R = 3; 
echo calculateProduct($A, $L, $R, $P),"\n" ; 
  
// This code is contributed by ajit. 
?>
```

输出：

```
120
6
```

由于`P`是质数，我们可以使用模乘逆。 使用动态编程，我们可以计算模`P`下的乘积数组，以使索引`i`处的值包含在`[0, i]`范围内的乘积。 同样，我们可以计算模`P`下的逆前积。现在，每个查询都可以在`O(1)`中回答。

逆积数组在索引`i`处包含`[0, i]`范围内的逆积。 因此对于查询`[L, R]`，答案将是`Product[R] * InverseProduct[L-1]。`

注意：我们不能将结果计算为`Product[R] / Product[L-1]`，因为乘积是在模`P`下计算的。如果我们不计算模`P`下的乘积，则总是有溢出的可能性。

## C++

```
// Product in range Queries in O(1) 
#include <bits/stdc++.h> 
using namespace std; 
#define MAX 100 
  
int pre_product[MAX]; 
int inverse_product[MAX]; 
  
// Returns modulo inverse of a 
// with respect to m using 
// extended Euclid Algorithm 
// Assumption: a and m are 
// coprimes, i.e., gcd(a, m) = 1 
int modInverse(int a, int m) 
{ 
    int m0 = m, t, q; 
    int x0 = 0, x1 = 1; 
  
    if (m == 1) 
        return 0; 
  
    while (a > 1)  
    { 
  
        // q is quotient 
        q = a / m; 
  
        t = m; 
  
        // m is remainder now,  
        // process same as 
        // Euclid's algo 
        m = a % m, a = t; 
  
        t = x0; 
  
        x0 = x1 - q * x0; 
  
        x1 = t; 
    } 
  
    // Make x1 positive 
    if (x1 < 0) 
        x1 += m0; 
  
    return x1; 
} 
  
// calculating pre_product 
// array 
void calculate_Pre_Product(int A[],  
                           int N, int P) 
{ 
    pre_product[0] = A[0]; 
  
    for (int i = 1; i < N; i++)  
    { 
        pre_product[i] = pre_product[i - 1] *  
                                        A[i]; 
        pre_product[i] = pre_product[i] % P; 
    } 
} 
  
// Cacluating inverse_product  
// array. 
void calculate_inverse_product(int A[],  
                               int N, int P) 
{ 
    inverse_product[0] = modInverse(pre_product[0], P); 
  
    for (int i = 1; i < N; i++)  
        inverse_product[i] = modInverse(pre_product[i], P);  
} 
  
// Function to calculate  
// Product in the given range. 
int calculateProduct(int A[], int L,  
                     int R, int P) 
{ 
    // As our array is 0 based as  
    // and L and R are given as 1  
    // based index. 
    L = L - 1; 
    R = R - 1; 
    int ans; 
  
    if (L == 0) 
        ans = pre_product[R]; 
    else
        ans = pre_product[R] *  
              inverse_product[L - 1]; 
  
    return ans; 
} 
  
// Driver Code 
int main() 
{ 
    // Array 
    int A[] = { 1, 2, 3, 4, 5, 6 }; 
  
    int N = sizeof(A) / sizeof(A[0]); 
  
    // Prime P 
    int P = 113; 
  
    // Calculating PreProduct 
    // and InverseProduct 
    calculate_Pre_Product(A, N, P); 
    calculate_inverse_product(A, N, P); 
  
    // Range [L, R] in 1 base index 
    int L = 2, R = 5; 
    cout << calculateProduct(A, L, R, P)  
         << endl; 
  
    L = 1, R = 3; 
    cout << calculateProduct(A, L, R, P) 
         << endl; 
    return 0; 
}
```

## Java

```
// Java program to find Product 
// in range Queries in O(1) 
class GFG 
{  
  
static int MAX = 100; 
int pre_product[] = new int[MAX]; 
int inverse_product[] = new int[MAX]; 
  
// Returns modulo inverse of a  
// with respect to m using extended  
// Euclid Algorithm Assumption: a  
// and m are coprimes,  
// i.e., gcd(a, m) = 1 
int modInverse(int a, int m) 
{ 
    int m0 = m, t, q; 
    int x0 = 0, x1 = 1; 
  
    if (m == 1) 
        return 0; 
  
    while (a > 1)  
    { 
  
        // q is quotient 
        q = a / m; 
  
        t = m; 
  
        // m is remainder now, 
        // process same as  
        // Euclid's algo 
        m = a % m; 
        a = t; 
  
        t = x0; 
  
        x0 = x1 - q * x0; 
  
        x1 = t; 
    } 
  
    // Make x1 positive 
    if (x1 < 0) 
        x1 += m0; 
  
    return x1; 
} 
  
// calculating pre_product array 
void calculate_Pre_Product(int A[],  
                           int N, int P) 
{ 
    pre_product[0] = A[0]; 
  
    for (int i = 1; i < N; i++)  
    { 
        pre_product[i] = pre_product[i - 1] * 
                                        A[i]; 
        pre_product[i] = pre_product[i] % P; 
    } 
} 
  
// Cacluating inverse_product array. 
void calculate_inverse_product(int A[],  
                               int N, int P) 
{ 
    inverse_product[0] = modInverse(pre_product[0], 
                                                P); 
  
    for (int i = 1; i < N; i++)  
        inverse_product[i] = modInverse(pre_product[i],  
                                                     P);  
} 
  
// Function to calculate Product  
// in the given range. 
int calculateProduct(int A[], int L, 
                     int R, int P) 
{ 
    // As our array is 0 based as and  
    // L and R are given as 1 based index. 
    L = L - 1; 
    R = R - 1; 
    int ans; 
  
    if (L == 0) 
        ans = pre_product[R]; 
    else
        ans = pre_product[R] *  
              inverse_product[L - 1]; 
  
    return ans; 
} 
  
// Driver code 
public static void main(String[] s) 
{ 
    GFG d = new GFG(); 
      
    // Array 
    int A[] = { 1, 2, 3, 4, 5, 6 }; 
      
    // Prime P 
    int P = 113; 
  
    // Calculating PreProduct and  
    // InverseProduct 
    d.calculate_Pre_Product(A, A.length, P); 
    d.calculate_inverse_product(A, A.length,  
                                         P); 
  
    // Range [L, R] in 1 base index 
    int L = 2, R = 5; 
    System.out.println(d.calculateProduct(A, L,  
                                          R, P)); 
    L = 1; 
    R = 3; 
    System.out.println(d.calculateProduct(A, L,  
                                          R, P)); 
          
} 
} 
  
// This code is contributed by Prerna Saini
```

## Python3

```
# Python3 implementation of the 
# above approach 
  
# Returns modulo inverse of a with  
# respect to m using extended Euclid  
# Algorithm. Assumption: a and m are  
# coprimes, i.e., gcd(a, m) = 1  
def modInverse(a, m):  
  
    m0, x0, x1 = m, 0, 1
  
    if m == 1:  
        return 0
  
    while a > 1:  
  
        # q is quotient  
        q = a // m  
        t = m  
  
        # m is remainder now, process  
        # same as Euclid's algo  
        m, a = a % m, t  
        t = x0  
        x0 = x1 - q * x0  
        x1 = t  
  
    # Make x1 positive  
    if x1 < 0:  
        x1 += m0  
  
    return x1  
  
# calculating pre_product array  
def calculate_Pre_Product(A, N, P):  
  
    pre_product[0] = A[0]  
  
    for i in range(1, N):  
      
        pre_product[i] = pre_product[i - 1] * A[i]  
        pre_product[i] = pre_product[i] % P  
  
# Cacluating inverse_product  
# array.  
def calculate_inverse_product(A, N, P):  
  
    inverse_product[0] = modInverse(pre_product[0], P)  
  
    for i in range(1, N): 
        inverse_product[i] = modInverse(pre_product[i], P)  
  
# Function to calculate  
# Product in the given range.  
def calculateProduct(A, L, R, P):  
  
    # As our array is 0 based as  
    # and L and R are given as 1  
    # based index.  
    L = L - 1
    R = R - 1
    ans = 0
  
    if L == 0:  
        ans = pre_product[R]  
    else: 
        ans = pre_product[R] * inverse_product[L - 1]  
  
    return ans  
  
# Driver Code  
if __name__ == "__main__": 
  
    # Array  
    A = [1, 2, 3, 4, 5, 6]  
    N = len(A)  
  
    # Prime P  
    P = 113
    MAX = 100
      
    pre_product = [None] * (MAX)  
    inverse_product = [None] * (MAX)  
  
    # Calculating PreProduct  
    # and InverseProduct  
    calculate_Pre_Product(A, N, P)  
    calculate_inverse_product(A, N, P)  
  
    # Range [L, R] in 1 base index  
    L, R = 2, 5
    print(calculateProduct(A, L, R, P)) 
  
    L, R = 1, 3
    print(calculateProduct(A, L, R, P)) 
      
# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find Product 
// in range Queries in O(1) 
using System; 
  
class GFG  
{ 
  
    static int MAX = 100; 
    int []pre_product = new int[MAX]; 
    int []inverse_product = new int[MAX]; 
      
    // Returns modulo inverse of  
    // a with respect to m using  
    // extended Euclid Algorithm  
    // Assumption: a and m are  
    // coprimes, i.e., gcd(a, m) = 1 
    int modInverse(int a, int m) 
    { 
        int m0 = m, t, q; 
        int x0 = 0, x1 = 1; 
      
        if (m == 1) 
            return 0; 
      
        while (a > 1) 
        { 
      
            // q is quotient 
            q = a / m; 
            t = m; 
      
            // m is remainder now, process  
            // same as Euclid's algo 
            m = a % m; 
            a = t; 
            t = x0; 
            x0 = x1 - q * x0; 
            x1 = t; 
        } 
      
        // Make x1 positive 
        if (x1 < 0) 
            x1 += m0; 
      
        return x1; 
    } 
      
    // calculating pre_product array 
    void calculate_Pre_Product(int []A,  
                               int N,  
                               int P) 
    { 
        pre_product[0] = A[0]; 
      
        for (int i = 1; i < N; i++) 
        { 
            pre_product[i] =  
                pre_product[i - 1] *  
                               A[i]; 
                                  
            pre_product[i] = 
                pre_product[i] % P; 
        } 
    } 
      
    // Cacluating inverse_product 
    // array. 
    void calculate_inverse_product(int []A,  
                                   int N,  
                                   int P) 
    { 
        inverse_product[0] =  
                modInverse(pre_product[0], P); 
      
        for (int i = 1; i < N; i++)  
            inverse_product[i] =  
                modInverse(pre_product[i], P);  
    } 
      
    // Function to calculate Product  
    // in the given range. 
    int calculateProduct(int []A, int L, 
                         int R, int P) 
    { 
          
        // As our array is 0 based as 
        // and L and R are given as 1 
        // based index. 
        L = L - 1; 
        R = R - 1; 
        int ans; 
      
        if (L == 0) 
            ans = pre_product[R]; 
        else
            ans = pre_product[R] *  
                  inverse_product[L - 1]; 
      
        return ans; 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        GFG d = new GFG(); 
          
        // Array 
        int []A = { 1, 2, 3, 4, 5, 6 }; 
          
        // Prime P 
        int P = 113; 
      
        // Calculating PreProduct and  
        // InverseProduct 
        d.calculate_Pre_Product(A,  
                        A.Length, P); 
                          
        d.calculate_inverse_product(A, 
                        A.Length, P); 
      
        // Range [L, R] in 1 base index 
        int L = 2, R = 5; 
        Console.WriteLine( 
            d.calculateProduct(A, L, R, P)); 
              
        L = 1; 
        R = 3; 
        Console.WriteLine( 
            d.calculateProduct(A, L, R, P)); 
    } 
} 
  
// This code is contributed by vt_m.
```

输出：

```
7
6
```

