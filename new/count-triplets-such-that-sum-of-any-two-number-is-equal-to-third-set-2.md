# 对三元组进行计数，以使任何两个数的和等于三| 设置 2

给定*个不同的正整数* **arr []** 长度为 **N** 的数组，任务是对所有三元组进行计数，以使两个元素的总和等于第三个元素 。

**示例**：

> **输入**：arr [] = {1、5、3、2}
> **输出**：2
> **说明**：
> 数组中有两个这样的三元组，使得两个数字的和等于第三个数字，它们是–
> （1、2、3），（3、2、5）
> 
> **输入**：arr [] = {3，2，7}
> **输出**：0
> **说明**：
> 在给定数组中 没有这样的三元组，使得两个数字的和等于第三个数字。

**方法**：这个想法是创建一个存在于数组中的数字的频率数组，然后在帮助下检查每对元素对是否存在该对元素在数组中 在 O（1）时间中的频率数组。

**算法**：

*   声明**频率**数组以存储数字的频率。

*   遍历数组的元素并增加频率数组中该数字的计数。

*   运行两个循环以选择矩阵的两个不同索引，并检查这些索引处的元素之和是否在频率数组中具有大于 0 的频率。

    ```
    If frequency of the sum is greater than 0:
        Increment the count of the triplets.

    ```

**注意**：我们在程序中假定数组元素的值在[1，100]范围内。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to count the 
// triplets such that the sum of the 
// two numbers is equal to third number 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the count of the  
// triplets such that sum of two  
// numbers is equal to the third number  
int countTriplets(int arr[], int n){ 
    int freq[100] = {0}; 

    // Loop to count the frequency 
    for (int i=0; i < n; i++){ 
        freq[arr[i]]++; 
    } 
    int count = 0; 

    // Loop to count for triplets 
    for(int i = 0;i < n; i++){ 
        for(int j = i+1; j < n; j++){ 
            if(freq[arr[i] + arr[j]]){ 
                count++; 
            } 
        } 
    } 
    return count; 
} 

// Driver Code 
int main() 
{ 
    int n = 4; 
    int arr[] = {1, 5, 3, 2}; 

    // Function Call 
    cout << countTriplets(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count the 
// triplets such that the sum of the 
// two numbers is equal to third number 
class GFG{ 

// Function to find the count of the  
// triplets such that sum of two  
// numbers is equal to the third number  
static int countTriplets(int arr[], int n){ 
    int []freq = new int[100]; 

    // Loop to count the frequency 
    for (int i = 0; i < n; i++){ 
        freq[arr[i]]++; 
    } 
    int count = 0; 

    // Loop to count for triplets 
    for(int i = 0; i < n; i++){ 
        for(int j = i + 1; j < n; j++){ 
            if(freq[arr[i] + arr[j]] > 0){ 
                count++; 
            } 
        } 
    } 
    return count; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int n = 4; 
    int arr[] = {1, 5, 3, 2}; 

    // Function Call 
    System.out.print(countTriplets(arr, n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python 3

```

# Python 3 implementation to count the 
# triplets such that the sum of the 
# two numbers is equal to third number 

# Function to find the count of the  
# triplets such that sum of two  
# numbers is equal to the third number  
def countTriplets(arr, n): 
    freq = [0 for i in range(100)] 

    # Loop to count the frequency 
    for i in range(n): 
        freq[arr[i]] += 1
    count = 0

    # Loop to count for triplets 
    for i in range(n): 
        for j in range(i + 1, n, 1): 
            if(freq[arr[i] + arr[j]]): 
                count += 1
    return count 

# Driver Code 
if __name__ == '__main__': 
    n = 4
    arr = [1, 5, 3, 2] 

    # Function Call 
    print(countTriplets(arr, n)) 

# This code is contributed by Surendra_Gangwar 

```

## C#

```cs

// C# implementation to count the  
// triplets such that the sum of the  
// two numbers is equal to third number  
using System; 

class GFG{  

// Function to find the count of the  
// triplets such that sum of two  
// numbers is equal to the third number  
static int countTriplets(int []arr, int n){  
    int []freq = new int[100];  

    // Loop to count the frequency  
    for (int i = 0; i < n; i++){  
        freq[arr[i]]++;  
    }  
    int count = 0;  

    // Loop to count for triplets  
    for(int i = 0; i < n; i++){  
        for(int j = i + 1; j < n; j++){  
            if(freq[arr[i] + arr[j]] > 0){  
                count++;  
            }  
        }  
    }  
    return count;  
}  

// Driver Code  
public static void Main(string[] args)  
{  
    int n = 4;  
    int []arr = {1, 5, 3, 2};  

    // Function Call  
    Console.WriteLine(countTriplets(arr, n));  
}  
}  

// This code is contributed by Yahs_R 

```

**Output:**

```
2

```

**效果分析**：

*   **时间复杂度**：O（N <sup>2</sup> ）。

*   **辅助空间**：O（N）。



* * *

* * *



