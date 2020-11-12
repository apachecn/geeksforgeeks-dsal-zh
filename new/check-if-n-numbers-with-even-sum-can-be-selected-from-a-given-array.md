# 检查是否可以从给定数组中选择`N`个具有偶数和的数字

> 原文：[https://www.geeksforgeeks.org/check-if-n-numbers-with-even-sum-can-be-selected-from-a-given-array/](https://www.geeksforgeeks.org/check-if-n-numbers-with-even-sum-can-be-selected-from-a-given-array/)

给定[数组](https://www.geeksforgeeks.org/array-data-structure/)`arr[]`和奇数`N`，任务是检查可以从数组中选择`N`个具有偶数和的数字。 如果可能，打印`Yes`。 否则打印`No`。

**示例**：

> **输入**：`arr[] = {9, 2, 3, 4, 1, 8, 7, 7, 6}, N = 5`
> **输出**：`Yes`
> **说明**：`{9, 3, 1, 7, 6}`是具有偶数和的`N`个元素。
> 
> **输入**：`arr[] = {1, 3, 7, 9, 3}, N = 3`
> **输出**：`No`

**方法**：请按照以下步骤解决问题：

1.  计算偶数和奇数整数并将其分别存储在`even_freq`和`odd_freq_`中。

2.  如果`even_freq`超过`N`，则取所有偶数，它们的和将为偶数。 因此，打印`Yes`。

3.  否则，检查`odd_freq`。

4.  如果`odd_freq`为**奇数**，则检查`odd_freq + even_freq – 1`是否`≥ N`。 如果发现是真的，则打印`Yes`。

5.  如果`odd_freq`为偶数，则检查`odd_freq + even_freq`是否`≥ N`。 如果发现是真的，则打印`Yes`。

6.  如果以上条件都不满足，请打印`No`。

下面是上述方法的实现：

## C++

```cpp

// C++ efficient program to check 
// if N numbers with Odd sum can be 
// selected from the given array 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check if an odd sum can be 
// made using N integers from the array 
bool checkEvenSum(int arr[], int N, int size) 
{ 
    // Initialize odd and even counts 
    int even_freq = 0, odd_freq = 0; 

    // Iterate over the array to count 
    // the no. of even and odd integers 
    for (int i = 0; i < size; i++) { 
        // If element is odd 
        if (arr[i] & 1) 
            odd_freq++; 

        // If element is even 
        else
            even_freq++; 
    } 

    // Check if even_freq is more than N 
    if (even_freq >= N) 
        return true; 
    else { 

        // If odd_freq is odd 
        if (odd_freq & 1) { 

            // Consider even count of odd 
            int taken = odd_freq - 1; 

            // Calculate even required 
            int req = N - taken; 

            // If even count is less 
            // than required count 
            if (even_freq < req) { 
                return false; 
            } 
            else
                return true; 
        } 
        else { 

            int taken = odd_freq; 

            // Calculate even required 
            int req = N - taken; 

            // If even count is less 
            // than required count 
            if (even_freq < req) { 
                return false; 
            } 
            else
                return true; 
        } 
    } 

    return false; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 9, 2, 3, 4, 18, 7, 7, 6 }; 
    int size = sizeof(arr) / sizeof(arr[0]); 
    int N = 5; 

    if (checkEvenSum(arr, N, size)) 
        cout << "Yes" << endl; 
    else
        cout << "No" << endl; 
} 

```

## Java

```java

// Java efficient program to check 
// if N numbers with Odd sum can be 
// selected from the given array 
import java.util.*; 

class GFG{ 

// Function to check if an odd sum can be 
// made using N integers from the array 
static boolean checkEvenSum(int arr[],  
                            int N, int size) 
{ 

    // Initialize odd and even counts 
    int even_freq = 0, odd_freq = 0; 

    // Iterate over the array to count 
    // the no. of even and odd integers 
    for(int i = 0; i < size; i++) 
    { 

        // If element is odd 
        if (arr[i] % 2 == 1) 
            odd_freq++; 

        // If element is even 
        else
            even_freq++; 
    } 

    // Check if even_freq is more than N 
    if (even_freq >= N) 
        return true; 
    else
    { 

        // If odd_freq is odd 
        if (odd_freq % 2 == 1)  
        { 

            // Consider even count of odd 
            int taken = odd_freq - 1; 

            // Calculate even required 
            int req = N - taken; 

            // If even count is less 
            // than required count 
            if (even_freq < req) 
            { 
                return false; 
            } 
            else
                return true; 
        } 
        else
        { 
            int taken = odd_freq; 

            // Calculate even required 
            int req = N - taken; 

            // If even count is less 
            // than required count 
            if (even_freq < req)  
            { 
                return false; 
            } 
            else
                return true; 
        } 
    } 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int arr[] = { 9, 2, 3, 4, 18, 7, 7, 6 }; 
    int size = arr.length; 
    int N = 5; 

    if (checkEvenSum(arr, N, size)) 
        System.out.print("Yes" + "\n"); 
    else
        System.out.print("No" + "\n"); 
} 
} 

// This code is contributed by Rohit_ranjan

```

## Python3

```py

# Python3 efficient program to check 
# if N numbers with Odd sum can be 
# selected from the given array 

# Function to check if an odd sum can be 
# made using N integers from the array 
def checkEvenSum(arr, N, size): 

    # Initialize odd and even counts 
    even_freq , odd_freq = 0 , 0

    # Iterate over the array to count 
    # the no. of even and odd integers 
    for i in range(size): 

        # If element is odd 
        if (arr[i] & 1): 
            odd_freq += 1

        # If element is even 
        else: 
            even_freq += 1

    # Check if even_freq is more than N 
    if (even_freq >= N): 
        return True
    else: 

        # If odd_freq is odd 
        if (odd_freq & 1): 

            # Consider even count of odd 
            taken = odd_freq - 1

            # Calculate even required 
            req = N - taken 

            # If even count is less 
            # than required count 
            if (even_freq < req): 
                return False
            else: 
                return True

        else: 
            taken = odd_freq 

            # Calculate even required 
            req = N - taken 

            # If even count is less 
            # than required count 
            if (even_freq < req): 
                return False
            else: 
                return True

    return False

# Driver Code 
if __name__ == "__main__": 

    arr = [ 9, 2, 3, 4, 18, 7, 7, 6 ] 
    size = len(arr) 
    N = 5

    if (checkEvenSum(arr, N, size)): 
        print("Yes") 
    else: 
        print("No") 

# This code is contributed by chitranayal 

```

## C#

```cs

// C# efficient program to check 
// if N numbers with Odd sum can be 
// selected from the given array 
using System; 

class GFG{ 

// Function to check if an odd sum can be 
// made using N integers from the array 
static bool checkEvenSum(int []arr,  
                         int N, int size) 
{ 

    // Initialize odd and even counts 
    int even_freq = 0, odd_freq = 0; 

    // Iterate over the array to count 
    // the no. of even and odd integers 
    for(int i = 0; i < size; i++) 
    { 

        // If element is odd 
        if (arr[i] % 2 == 1) 
            odd_freq++; 

        // If element is even 
        else
            even_freq++; 
    } 

    // Check if even_freq is more than N 
    if (even_freq >= N) 
        return true; 

    else
    { 

        // If odd_freq is odd 
        if (odd_freq % 2 == 1)  
        { 

            // Consider even count of odd 
            int taken = odd_freq - 1; 

            // Calculate even required 
            int req = N - taken; 

            // If even count is less 
            // than required count 
            if (even_freq < req) 
            { 
                return false; 
            } 
            else
                return true; 
        } 
        else
        { 
            int taken = odd_freq; 

            // Calculate even required 
            int req = N - taken; 

            // If even count is less 
            // than required count 
            if (even_freq < req)  
            { 
                return false; 
            } 
            else
                return true; 
        } 
    } 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { 9, 2, 3, 4, 18, 7, 7, 6 }; 
    int size = arr.Length; 
    int N = 5; 

    if (checkEvenSum(arr, N, size)) 
        Console.Write("Yes" + "\n"); 
    else
        Console.Write("No" + "\n"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**： 

```
Yes

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *



