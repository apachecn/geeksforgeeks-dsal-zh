# 执行加减命令后打印修改后的数组

> 原文： [https://www.geeksforgeeks.org/print-modified-array-executing-commands-addition-subtraction/](https://www.geeksforgeeks.org/print-modified-array-executing-commands-addition-subtraction/)

给定大小为`n`的数组和给定的大小为`m`的命令集。 每个命令由四个整数`q, l, r, k`组成。 这些命令具有以下类型：

*   如果`q = 0`，则将`k`添加到范围`a`至`b`的所有整数中（`1 <= a <= b <= n`）。

*   如果`q = 1`，则将`a`到`b`范围内的所有整数减去`k`（`1 <= a <= b <= n`）。

**注意**：最初，所有数组元素都设置为 0，而数组索引从 1 开始。

```
Input : n = 5
        commands[] = {{0 1 3 2}, {1 3 5 3}, 
                      {0 2 5 1}}
Output : 0 2 -1 -1 -3
Explanation
First command: Add 2 from index 1 to 3
>=  2 2 2 0 0
Second command: Subtract 3 from index 3 to 5 
>= 2 2 -1 -3 -3
Third command: Add 1 from index 2 to 5
>= 2 3 0 -2 -2

```



**简单方法**是通过从左索引（`l`）到右索引（`r`）进行迭代来执行每个命令，并根据给定命令更新每个索引。 该方法的时间复杂度为`O(n * m)`。

**更好的方法**是使用分域树（BIT）或段树。 但这只会最优化`log(n)`时间，即整体复杂度将变为`O(m * log(n))`。

**高效方法**是使用简单的数学方法。 由于所有命令都可以离线处理，因此我们可以将所有更新存储在临时数组中，然后最后执行它。

*   对于命令 **0**，在第`l`个第`r + 1`个索引元素中添加`+k`和`-k`。

*   对于命令 **1**，在第`l`个第`r + 1`个索引元素中添加`+k`和`-k`。

之后，对每个索引`i`的所有元素求和，从第一个索引开始，即`a[i]`将包含索引从 1 到`i`的所有元素的和。 这可以通过动态规划轻松实现。

## C++ 

```cpp

// C++ program to find modified array 
// after executing m commands/queries 
#include<bits/stdc++.h> 
using namespace std; 

// Update function for every command 
void updateQuery(int arr[], int n, int q, int l, 
                 int r, int k) 
{ 
    // If q == 0, add 'k' and '-k' 
    // to 'l-1' and 'r' index 
    if (q == 0){ 
        arr[l-1] += k; 
        arr[r] += -k; 
    } 

    // If q == 1, add '-k' and 'k' 
    // to 'l-1' and 'r' index 
    else{ 
        arr[l-1] += -k; 
        arr[r] += k; 
    } 
    return; 
} 

// Function to generate the final 
// array after executing all  
// commands 
void generateArray(int arr[], int n) 
{ 
    // Generate final array with the  
    // help of DP concept 
    for (int i = 1; i < n; ++i) 
        arr[i] += arr[i-1]; 

    return; 
} 

// Driver program 
int main() 
{ 
    int n = 5; 
    int arr[n+1]; 
    //Set all array elements to '0' 
    memset(arr, 0, sizeof(arr)); 

    int q = 0, l = 1, r = 3, k = 2; 
    updateQuery(arr, n, q, l, r, k); 

    q = 1 , l = 3, r = 5, k = 3; 
    updateQuery(arr, n, q, l, r, k); 

    q = 0 , l = 2, r = 5, k = 1; 
    updateQuery(arr, n, q, l, r, k); 

    // Generate final array 
    generateArray(arr, n); 

    // Printing the final modified array 
    for (int i = 0; i < n; ++i) 
        cout << arr[i] << " "; 
    return 0; 
} 

```

## Java

```
// Java program to find modified array 
// after executing m commands/queries 
import java.util.Arrays; 
  
class GFG { 
      
    // Update function for every command 
    static void updateQuery(int arr[], int n,  
                  int q, int l, int r, int k) 
    { 
          
        // If q == 0, add 'k' and '-k' 
        // to 'l-1' and 'r' index 
        if (q == 0){ 
            arr[l-1] += k; 
            arr[r] += -k; 
        } 
       
        // If q == 1, add '-k' and 'k' 
        // to 'l-1' and 'r' index 
        else{ 
            arr[l-1] += -k; 
            arr[r] += k; 
        } 
          
        return; 
    } 
       
    // Function to generate the final 
    // array after executing all  
    // commands 
    static void generateArray(int arr[], int n) 
    { 
        // Generate final array with the  
        // help of DP concept 
        for (int i = 1; i < n; ++i) 
            arr[i] += arr[i-1]; 
           
    } 
    //driver code 
    public static void main(String arg[]) 
    { 
        int n = 5; 
        int arr[] = new int[n+1]; 
          
        //Set all array elements to '0' 
        Arrays.fill(arr, 0); 
          
        int q = 0, l = 1, r = 3, k = 2; 
        updateQuery(arr, n, q, l, r, k); 
       
        q = 1 ; l = 3; r = 5; k = 3; 
        updateQuery(arr, n, q, l, r, k); 
       
        q = 0 ; l = 2; r = 5; k = 1; 
        updateQuery(arr, n, q, l, r, k); 
       
        // Generate final array 
        generateArray(arr, n); 
       
        // Printing the final modified array 
        for (int i = 0; i < n; ++i) 
            System.out.print(arr[i]+" "); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```
# Python3 program to find modified array 
# after executing m commands/queries 
  
# Update function for every command 
def updateQuery(arr, n, q, l, r, k): 
  
    # If q == 0, add 'k' and '-k' 
    # to 'l-1' and 'r' index 
    if (q == 0): 
        arr[l - 1] += k 
        arr[r] += -k 
  
    # If q == 1, add '-k' and 'k' 
    # to 'l-1' and 'r' index 
    else: 
        arr[l - 1] += -k 
        arr[r] += k 
      
    return
  
# Function to generate the final 
# array after executing all commands 
def generateArray(arr, n): 
  
    # Generate final array with the  
    # help of DP concept 
    for i in range(1, n): 
        arr[i] += arr[i - 1] 
      
    return
  
# Driver Code 
n = 5
arr = [0 for i in range(n + 1)] 
  
# Set all array elements to '0' 
q = 0; l = 1; r = 3; k = 2
updateQuery(arr, n, q, l, r, k) 
  
q, l, r, k = 1, 3, 5, 3
updateQuery(arr, n, q, l, r, k); 
  
q, l, r, k = 0, 2, 5, 1
updateQuery(arr, n, q, l, r, k) 
  
# Generate final array 
generateArray(arr, n) 
  
# Printing the final modified array 
for i in range(n): 
    print(arr[i], end = " ") 
      
      
# This code is contributed by Anant Agarwal.
```

## C#

```
// Program to find modified 
// array after executing 
// m commands/queries 
using System; 
  
class GFG { 
  
    // Update function for every command 
    static void updateQuery(int[] arr, int n, int q, 
                            int l, int r, int k) 
    { 
  
        // If q == 0, add 'k' and '-k' 
        // to 'l-1' and 'r' index 
        if (q == 0) { 
            arr[l - 1] += k; 
            arr[r] += -k; 
        } 
  
        // If q == 1, add '-k' and 'k' 
        // to 'l-1' and 'r' index 
        else { 
            arr[l - 1] += -k; 
            arr[r] += k; 
        } 
        return; 
    } 
  
    // Function to generate final 
    // array after executing all 
    // commands 
    static void generateArray(int[] arr, int n) 
    { 
        // Generate final array with 
        // the help of DP concept 
        for (int i = 1; i < n; ++i) 
            arr[i] += arr[i - 1]; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int n = 5; 
        int[] arr = new int[n + 1]; 
  
        // Set all array elements to '0' 
        for (int i = 0; i < arr.Length; i++) 
            arr[i] = 0; 
  
        int q = 0, l = 1, r = 3, k = 2; 
        updateQuery(arr, n, q, l, r, k); 
  
        q = 1; 
        l = 3; 
        r = 5; 
        k = 3; 
        updateQuery(arr, n, q, l, r, k); 
  
        q = 0; 
        l = 2; 
        r = 5; 
        k = 1; 
        updateQuery(arr, n, q, l, r, k); 
  
        // Generate final array 
        generateArray(arr, n); 
  
        // Printing the final modified array 
        for (int i = 0; i < n; ++i) 
            Console.Write(arr[i] + " "); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

输出：

```
Output: 2 3 0 -2 -2 
```

时间复杂度：`O(Max(m, n))`。

辅助空间：`O(n)`。