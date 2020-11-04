# 查找所有划分最大数组元素的数字

> 原文：[https://www.geeksforgeeks.org/find-all-numbers-that-divide-maximum-array-elements/](https://www.geeksforgeeks.org/find-all-numbers-that-divide-maximum-array-elements/)

给定一个由`N`个数字组成的数组，任务是打印所有大于 1 的数字，这些数字除以数组元素的最大值。

**范例**：

> **输入**：`a[] = {6, 6, 12, 12, 18, 13}`
>
> **输出**：`2 3 6`
>
> 所有数字均除以数组元素的最大值，即 4
> 
> **输入**：`a[] = {12, 15, 27, 20, 40}`
>
> **输出**：`2 3 4 5`

**方法**：

*   使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)存储每个数组元素的所有因子的计数。 我们可以[在`O(sqrt N)`中找出](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)的所有因子。

*   遍历所有因素，并找到除以数字的最大数组元素的数量。

*   再次重新遍历所有因子，并打印出现次数最多的因子。

下面是上述方法的实现。

## C++

```cpp

// C++ program to print all the numbers 
// that divides maximum of array elements 
#include <bits/stdc++.h> 
using namespace std; 

// Function that prints all the numbers 
// which divides maximum of array elements 
void printNumbers(int a[], int n) 
{ 

    // hash to store the number of times 
    // a factor is there 
    unordered_map<int, int> mpp; 

    for (int i = 0; i < n; i++) { 
        int num = a[i]; 

        // find all the factors 
        for (int j = 1; j * j <= num; j++) { 

            // if j is factor of num 
            if (num % j == 0) { 
                if (j != 1) 
                    mpp[j]++; 

                if ((num / j) != j) 
                    mpp[num / j]++; 
            } 
        } 
    } 

    // find the maximum times 
    // it can divide 
    int maxi = 0; 
    for (auto it : mpp) { 
        maxi = max(it.second, maxi); 
    } 

    // print all the factors of 
    // numbers which divides the 
    // maximum array elements 
    for (auto it : mpp) { 
        if (it.second == maxi) 
            cout << it.first << " "; 
    } 
} 

// Driver Code 
int main() 
{ 

    int a[] = { 12, 15, 27, 20, 40 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    printNumbers(a, n); 
} 

```

## Java

```java

// Java program to print all the numbers 
// that divides maximum of array elements 
import java.util.*; 

class GFG 
{ 

// Function that prints all the numbers 
// which divides maximum of array elements 
static void printNumbers(int a[], int n) 
{ 

    // hash to store the number of times 
    // a factor is there 
    Map<Integer,  
        Integer> mpp = new HashMap<>(); 

    for (int i = 0; i < n; i++)  
    { 
        int num = a[i]; 

        // find all the factors 
        for (int j = 1; j * j <= num; j++)  
        { 

            // if j is factor of num 
            if (num % j == 0)  
            { 
                if (j != 1) 
                { 
                    if(mpp.containsKey(j)) 
                    { 
                        mpp.put(j, mpp.get(j) + 1); 
                    } 
                    else
                    { 
                        mpp.put(j, 1); 
                    } 
                } 

                if ((num / j) != j) 
                { 
                    if(mpp.containsKey(num / j)) 
                    { 
                        mpp.put(num / j, mpp.get(num / j) + 1); 
                    } 
                    else
                    { 
                        mpp.put(num / j, 1); 
                    } 
                } 
            } 
        } 
    } 

    // find the maximum times 
    // it can divide 
    int maxi = 0; 
    for (Map.Entry<Integer, 
                   Integer> it : mpp.entrySet()) 
    { 
        maxi = Math.max(it.getValue(), maxi); 
    } 

    // print all the factors of 
    // numbers which divides the 
    // maximum array elements 
    for (Map.Entry<Integer, 
                   Integer> it : mpp.entrySet()) 
    { 
        if (it.getValue() == maxi) 
            System.out.print(it.getKey() + " "); 
    } 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    int a[] = { 12, 15, 27, 20, 40 }; 
    int n = a.length; 
    printNumbers(a, n); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python3 program to print all the numbers 
# that divides maximum of array elements 

# Function that prints all the numbers 
# which divides maximum of array elements 
def printNumbers(a, n): 

    # hash to store the number of times 
    # a factor is there 
    mpp = dict() 

    for i in range(n): 
        num = a[i] 

        # find all the factors 
        for j in range(1, num + 1): 

            if j * j > num: 
                break

            # if j is factor of num 
            if (num % j == 0): 
                if (j != 1): 
                    mpp[j]=mpp.get(j, 0) + 1

                if ((num // j) != j): 
                    mpp[num // j]=mpp.get(num//j, 0) + 1

    # find the maximum times 
    # it can divide 
    maxi = 0
    for it in mpp: 
        maxi = max(mpp[it], maxi) 

    # print all the factors of 
    # numbers which divides the 
    # maximum array elements 
    for it in mpp: 
        if (mpp[it] == maxi): 
            print(it,end=" ") 

# Driver Code 
a = [12, 15, 27, 20, 40 ] 
n = len(a) 
printNumbers(a, n) 

# This code is contributed by mohit kumar 

```

## C#

```cs

// C# program to print all the numbers 
// that divides maximum of array elements 
using System; 
using System.Collections.Generic;  

class GFG 
{ 

// Function that prints all the numbers 
// which divides maximum of array elements 
static void printNumbers(int []a, int n) 
{ 

    // hash to store the number of times 
    // a factor is there 
    Dictionary<int,int> mpp = new Dictionary<int,int>(); 

    for (int i = 0; i < n; i++)  
    { 
        int num = a[i]; 

        // find all the factors 
        for (int j = 1; j * j <= num; j++)  
        { 

            // if j is factor of num 
            if (num % j == 0)  
            { 
                if (j != 1) 
                { 
                    if(mpp.ContainsKey(j)) 
                    { 
                        var v = mpp[j]; 
                        mpp.Remove(j); 
                        mpp.Add(j, v + 1); 
                    } 
                    else
                    { 
                        mpp.Add(j, 1); 
                    } 
                } 

                if ((num / j) != j) 
                { 
                    if(mpp.ContainsKey(num / j)) 
                    { 
                        var v = mpp[num/j]; 
                        mpp.Remove(num/j); 
                        mpp.Add(num / j, v + 1); 
                    } 
                    else
                    { 
                        mpp.Add(num / j, 1); 
                    } 
                } 
            } 
        } 
    } 

    // find the maximum times 
    // it can divide 
    int maxi = 0; 
    foreach(KeyValuePair<int, int> it in mpp) 
    { 
        maxi = Math.Max(it.Value, maxi); 
    } 

    // print all the factors of 
    // numbers which divides the 
    // maximum array elements 
    foreach(KeyValuePair<int, int> it in mpp) 
    { 
        if (it.Value == maxi) 
            Console.Write(it.Key + " "); 
    } 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    int []a = { 12, 15, 27, 20, 40 }; 
    int n = a.Length; 
    printNumbers(a, n); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
5 2 3 4

```

**时间复杂度**：`O(N * sqrt(max(arr)))`



* * *

* * *



