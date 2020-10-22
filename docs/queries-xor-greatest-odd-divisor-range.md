# 最大奇数除数的 XOR 的范围查询

> 原文： [https://www.geeksforgeeks.org/queries-xor-greatest-odd-divisor-range/](https://www.geeksforgeeks.org/queries-xor-greatest-odd-divisor-range/)

给定`N`个正整数的数组。 有`Q`个查询，每个查询都包含一个范围`[L, R]`。 对于每个查询输出，该范围内每个数字的最大奇数除数的异或。

**示例**：

```
Input : arr[] = { 3, 4, 5 }
query 1: [0, 2]
query 2: [1, 2]
Output : 7 4
Greatest odd divisor are: { 3, 1, 5 }
XOR of 3, 1, 5 is 7
XOR of 1, 5 is 4

Input : arr[] = { 2, 1, 2 }
query 1: [0, 2]
Output : 1

```



这个想法是预先计算数组的最大奇数除数，并将其存储在数组中，例如`preXOR[]`。 现在，预先计算并存储数组`preXOR[]`的前缀 XOR。 要回答每个查询，请返回`preXOR[r] xor preXOR[l-1]`。

以下是此方法的实现：

## C++ 

```cpp

#include <bits/stdc++.h> 
using namespace std; 

// Precompute the prefix XOR of greatest  
// odd divisor 
void prefixXOR(int arr[], int preXOR[], int n) 
{ 
    // Finding the Greatest Odd divisor 
    for (int i = 0; i < n; i++) { 
        while (arr[i] % 2 != 1) 
            arr[i] /= 2; 

        preXOR[i] = arr[i]; 
    } 

    // Finding prefix XOR 
    for (int i = 1; i < n; i++) 
        preXOR[i] = preXOR[i - 1] ^ preXOR[i]; 
} 

// Return XOR of the range 
int query(int preXOR[], int l, int r) 
{ 
    if (l == 0) 
        return preXOR[r]; 
    else
        return preXOR[r] ^ preXOR[l - 1]; 
} 

// Driven Program 
int main() 
{ 
    int arr[] = { 3, 4, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int preXOR[n]; 
    prefixXOR(arr, preXOR, n); 

    cout << query(preXOR, 0, 2) << endl; 
    cout << query(preXOR, 1, 2) << endl; 

    return 0; 
} 

```

## Java

```java
// Java code Queries on XOR of  
// greatest odd divisor of the range 
import java.io.*; 
  
class GFG  
{ 
    // Precompute the prefix XOR of greatest  
    // odd divisor 
    static void prefixXOR(int arr[], int preXOR[], int n) 
    { 
        // Finding the Greatest Odd divisor 
        for (int i = 0; i < n; i++)  
        { 
            while (arr[i] % 2 != 1) 
                arr[i] /= 2; 
      
            preXOR[i] = arr[i]; 
        } 
      
        // Finding prefix XOR 
        for (int i = 1; i < n; i++) 
            preXOR[i] = preXOR[i - 1] ^ preXOR[i]; 
    } 
      
    // Return XOR of the range 
    static int query(int preXOR[], int l, int r) 
    { 
        if (l == 0) 
            return preXOR[r]; 
        else
            return preXOR[r] ^ preXOR[l - 1]; 
    } 
      
    // Driven Program 
    public static void main (String[] args)  
    { 
        int arr[] = { 3, 4, 5 }; 
        int n = arr.length; 
      
        int preXOR[] = new int[n]; 
        prefixXOR(arr, preXOR, n); 
      
        System.out.println(query(preXOR, 0, 2)) ; 
        System.out.println (query(preXOR, 1, 2)); 
      
              
    } 
} 
  
// This article is contributed by vt_m
```

## Python3

```py
# Precompute the prefix XOR of greatest  
# odd divisor 
def prefixXOR(arr, preXOR, n): 
      
    # Finding the Greatest Odd divisor 
    for i in range(0, n, 1): 
        while (arr[i] % 2 != 1): 
            arr[i] = int(arr[i] / 2)  
  
        preXOR[i] = arr[i] 
  
    # Finding prefix XOR 
    for i in range(1, n, 1): 
        preXOR[i] = preXOR[i - 1] ^ preXOR[i] 
  
# Return XOR of the range 
def query(preXOR, l, r): 
    if (l == 0): 
        return preXOR[r] 
    else: 
        return preXOR[r] ^ preXOR[l - 1] 
  
# Driver Code 
if __name__ == '__main__': 
    arr = [3, 4, 5] 
    n = len(arr) 
  
    preXOR = [0 for i in range(n)] 
    prefixXOR(arr, preXOR, n) 
  
    print(query(preXOR, 0, 2)) 
    print(query(preXOR, 1, 2)) 
      
# This code is contributed by 
# Sahil_shelangia
```

## C#

```cs
// C# code Queries on XOR of  
// greatest odd divisor of the range 
using System; 
  
class GFG  
{ 
    // Precompute the prefix XOR of greatest  
    // odd divisor 
    static void prefixXOR(int []arr,  
                    int []preXOR, int n) 
    { 
        // Finding the Greatest Odd divisor 
        for (int i = 0; i < n; i++)  
        { 
            while (arr[i] % 2 != 1) 
                arr[i] /= 2; 
      
            preXOR[i] = arr[i]; 
        } 
      
        // Finding prefix XOR 
        for (int i = 1; i < n; i++) 
            preXOR[i] = preXOR[i - 1] ^ preXOR[i]; 
    } 
      
    // Return XOR of the range 
    static int query(int [] preXOR, int l, int r) 
    { 
        if (l == 0) 
            return preXOR[r]; 
        else
            return preXOR[r] ^ preXOR[l - 1]; 
    } 
      
    // Driven Program 
    public static void Main ()  
    { 
        int []arr = { 3, 4, 5 }; 
        int n = arr.Length; 
      
        int []preXOR = new int[n]; 
        prefixXOR(arr, preXOR, n); 
      
        Console.WriteLine(query(preXOR, 0, 2)) ; 
        Console.WriteLine (query(preXOR, 1, 2)); 
    } 
} 
  
// This code is contributed by vt_m
```

输出：

```
7
4
```

