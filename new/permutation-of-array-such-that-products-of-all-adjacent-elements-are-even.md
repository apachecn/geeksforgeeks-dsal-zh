# 数组的排列，其中所有相邻元素的乘积是偶数

> 原文：[https://www.geeksforgeeks.org/permutation-of-array-such-that-products-of-all-adjacent-elements-are-even/](https://www.geeksforgeeks.org/permutation-of-array-such-that-products-of-all-adjacent-elements-are-even/)

给定由`N`个正整数组成的数组`arr[]`，任务是找到给定数组的任何排列，以使相邻元素的乘积为偶数。 打印任何这样的排列，如果不可能，则打印 -1。

**示例**：

> **输入**：`arr[] = {6,7,9,8,10,11}`
>
> **输出**：`8 9 10 7 6 11`
>
> **说明**：
>
> 相邻元素的乘积：
>
> `8 x 9 = 72`（偶数）
>
> `9 x 10 = 90`（偶数）
>
> `10 x 7 = 70`（偶数）
>
> `7 x 6 = 42`（偶数）
>
> `6 x 11 = 66`（偶数）
> 
> **输入**：`arr[] = {3,2,5,7,1,4,9}`
>
> **输出**：-1
>
> **说明**：没有元素的可能布置使得相邻元素的乘积相等。

**朴素的方法**：解决此问题的最简单方法是尝试元素的所有可能排列并检查条件是否为真。

**时间复杂度**：`O(N * N!)`其中`N`是数组中元素的数量。 `O(N!)`是创建给定数组的所有排列所花费的时间，而`O(n)`是检查当前排列是否为必需排列所需要的时间。

**辅助空间**：`O(n)`每次存储置换。

**高效方法**：可以使用简单的观察方法找到解决方案。 如果数组中有多个奇数和偶数元素，则任何相邻元素的最佳排列可以是以下两种情况之一，以使乘积为偶数：

```
{奇数, 偶数}
{偶数, 奇数}
{偶数, 偶数}
```

> 请注意，任何相邻元素的`{奇数, 奇数}`排列将给出奇数乘积。 因此，这种布置是不可能的。

以上安排仅在以下情况下可行：

> `number_of_odd_elements <= number_of_even_elements + 1`

请按照以下步骤解决问题。

1.  取两个向量`even`和`odd`，分别存储数组的偶数和奇数元素。

2.  如果`odd`矢量的大小大于`even`矢量的大小加 1（如上所述），则不可能求解。 因此，打印`-1`。

3.  否则，首先打印`odd`向量中的一个元素，然后打印`even`向量中的一个元素，直到两个向量都为空。

下面是上述方法的实现。

## C++

```cpp

// C++ program to Permutation of Array  
// such that product of all  
// adjacent elements is even  

#include <bits/stdc++.h>  
using namespace std;  

// Function to print  
// the required permutation  

void printPermutation(int arr[], int n)  
{  
    vector<int> odd, even;  

    // push odd elements in 'odd'  
    // and even elements in 'even'  
    for (int i = 0; i < n; i++) {  

        if (arr[i] % 2 == 0)  
            even.push_back(arr[i]);  
        else
            odd.push_back(arr[i]);  
    }  

    int size_odd = odd.size();  
    int size_even = even.size();  

    // Check if it possible to  
    // arrange the elements  
    if (size_odd > size_even + 1)  
        cout << -1 << endl;  

    // else print the permutation  
    else {  

        int i = 0;  
        int j = 0;  

        while (i < size_odd && j < size_even) {  

            cout << odd[i] << " ";  
            ++i;  
            cout << even[j] << " ";  
            ++j;  
        }  

        // Print remaining odds are even.  
        // and even elements  
        while (i < size_odd) {  
            cout << odd[i] << " ";  
            ++i;  
        }  

        while (j < size_even) {  
            cout << even[j] << " ";  
        }  
    }  
}  

// Driver code  
int main()  
{  
    int arr[] = { 6, 7, 9, 8, 10, 11 };  
    int N = sizeof(arr) / sizeof(arr[0]);  

    printPermutation(arr, N);  
    return 0;  
} 

```

## Java

```java

// Java program to permutation of array  
// such that product of all adjacent  
// elements is even  
import java.io.*; 
import java.util.*; 

class GFG{ 

// Function to print  
// the required permutation  
static void printPermutation(int arr[], int n)  
{  
    ArrayList<Integer> odd = new ArrayList<Integer>(); 
    ArrayList<Integer> even = new ArrayList<Integer>(); 

    // push odd elements in 'odd'  
    // and even elements in 'even'  
    for(int i = 0; i < n; i++) 
    {  
         if (arr[i] % 2 == 0)  
              even.add(arr[i]);  
           else
              odd.add(arr[i]);  
    }  

    int size_odd = odd.size();  
    int size_even = even.size();  

    // Check if it possible to  
    // arrange the elements  
    if (size_odd > size_even + 1)  
        System.out.println("-1");  

    // Else print the permutation  
    else 
    {  
        int i = 0;  
        int j = 0;  

        while (i < size_odd && j < size_even)  
        {  
            System.out.print(odd.get(i) + " ");  
            ++i;  
            System.out.print(even.get(j) + " ");  
            ++j;  
        }  

        // Print remaining odds are even.  
        // and even elements  
        while (i < size_odd)  
        {  
            System.out.print(odd.get(i) + " ");  
            ++i;  
        }  
        while (j < size_even)  
        {  
            System.out.print(even.get(j) + " ");  
        }  
    }  
} 

// Driver Code 
public static void main (String[] args) 
{ 
    int arr[] = { 6, 7, 9, 8, 10, 11 };  
    int N = arr.length;  

    printPermutation(arr, N);  
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program to Permutation of Array  
# such that product of all  
# adjacent elements is even  

# Function to print  
# the required permutation  
def printPermutation(arr, n):  

    odd, even = [], []  

    # push odd elements in 'odd'  
    # and even elements in 'even'  
    for i in range(n):  
        if(arr[i] % 2 == 0):  
            even.append(arr[i])  
        else:  
            odd.append(arr[i])  

    size_odd = len(odd)  
    size_even = len(even)  

    # Check if it possible to  
    # arrange the elements  
    if(size_odd > size_even + 1):  
        print(-1)  

    # else print the permutation  
    else:  
        i, j = 0, 0

        while(i < size_odd and j < size_even):  

            print(odd[i], end = " ")  
            i += 1
            print(even[j], end = " ")  
            j += 1

    # Print remaining odds are even.  
    # and even elements  
    while(i < size_odd):  
        print(odd[i], end = " ")  
        i += 1

    while(j < size_even):  
        print(even[j], end = " ")  
        j += 1

# Driver Code  
arr = [ 6, 7, 9, 8, 10, 11 ]  

N = len(arr)  

# Function call  
printPermutation(arr, N)  

# This code is contributed by Shivam Singh  

```

## C#

```cs

// C# program to permutation of array  
// such that product of all adjacent  
// elements is even  
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to print  
// the required permutation  
static void printPermutation(int []arr, int n)  
{  
    List<int> odd = new List<int>(); 
    List<int> even = new List<int>(); 

    // push odd elements in 'odd'  
    // and even elements in 'even'  
    for(int i = 0; i < n; i++) 
    {  
        if (arr[i] % 2 == 0)  
            even.Add(arr[i]);  
        else
            odd.Add(arr[i]);  
    }  

    int size_odd = odd.Count;  
    int size_even = even.Count;  

    // Check if it possible to  
    // arrange the elements  
    if (size_odd > size_even + 1)  
        Console.WriteLine("-1");  

    // Else print the permutation  
    else
    {  
        int i = 0;  
        int j = 0;  

        while (i < size_odd && j < size_even)  
        {  
            Console.Write(odd[i] + " ");  
            ++i;  
            Console.Write(even[j] + " ");  
            ++j;  
        }  

        // Print remaining odds are even.  
        // and even elements  
        while (i < size_odd)  
        {  
            Console.Write(odd[i] + " ");  
            ++i;  
        }  
        while (j < size_even)  
        {  
            Console.Write(even[j] + " ");  
        }  
    }  
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { 6, 7, 9, 8, 10, 11 };  
    int N = arr.Length;  

    printPermutation(arr, N);  
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
7 6 9 8 11 10 

```

**时间复杂度**：`O(n)`，其中`N`为元素数。 遍历给定数组并形成奇数&偶数向量需要`O(n)`时间，而打印排列需要`O(n)`。

**辅助空间**：`O(n)`，因为给定的数组元素分布在两个向量之间。



* * *

* * *



