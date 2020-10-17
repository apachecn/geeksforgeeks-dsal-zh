# 重新排列数组，如果`arr[i]`为`j`，则`arr[j]`变为`i` | 系列 1

> 原文： [https://www.geeksforgeeks.org/rearrange-array-arrj-becomes-arri-j/](https://www.geeksforgeeks.org/rearrange-array-arrj-becomes-arri-j/)

给定大小为`n`的数组，其中所有元素都是不同的，且范围从 0 到`n-1`，请更改`arr[]`的内容，以便将`arr[i] = j`更改为`arr[j] = i`。

**示例**：

```
Example 1:
Input: arr[]  = {1, 3, 0, 2};
Output: arr[] = {2, 0, 3, 1};
Explanation for the above output.
Since arr[0] is 1, arr[1] is changed to 0
Since arr[1] is 3, arr[3] is changed to 1
Since arr[2] is 0, arr[0] is changed to 2
Since arr[3] is 2, arr[2] is changed to 3

Example 2:
Input: arr[]  = {2, 0, 1, 4, 5, 3};
Output: arr[] = {1, 2, 0, 5, 3, 4};

Example 3:
Input: arr[]  = {0, 1, 2, 3};
Output: arr[] = {0, 1, 2, 3};

Example 4:
Input: arr[]  = {3, 2, 1, 0};
Output: arr[] = {3, 2, 1, 0};

```



一种**简单解决方案**是创建一个临时数组，并逐个复制`i`到`temp[arr[i]]`，其中`i`从 0 到`n-1`不等。

以下是上述想法的实现。

## C++ 

```cpp

// A simple C++ program to rearrange contents of arr[] 
// such that arr[j] becomes j if arr[i] is j 
#include <bits/stdc++.h> 
using namespace std; 

// A simple method to rearrange 'arr[0..n-1]' so that 'arr[j]' 
// becomes 'i' if 'arr[i]' is 'j' 
void rearrangeNaive(int arr[], int n) 
{ 
    // Create an auxiliary array of same size 
    int temp[n], i; 

    // Store result in temp[] 
    for (i = 0; i < n; i++) 
        temp[arr[i]] = i; 

    // Copy temp back to arr[] 
    for (i = 0; i < n; i++) 
        arr[i] = temp[i]; 
} 

// A utility function to print contents of arr[0..n-1] 
void printArray(int arr[], int n) 
{ 
    int i; 
    for (i = 0; i < n; i++) 
        cout << ("%d ", arr[i]); 
    cout << ("\n"); 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 3, 0, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << ("Given array is \n"); 
    printArray(arr, n); 

    rearrangeNaive(arr, n); 

    cout << ("Modified array is \n"); 
    printArray(arr, n); 
    return 0; 
} 

// This code is contributed by Code_Mech 

```

## C

```c
// A simple C program to rearrange contents of arr[] 
// such that arr[j] becomes j if arr[i] is j 
#include <stdio.h> 
  
// A simple method to rearrange 'arr[0..n-1]' so that 'arr[j]' 
// becomes 'i' if 'arr[i]' is 'j' 
void rearrangeNaive(int arr[], int n) 
{ 
    // Create an auxiliary array of same size 
    int temp[n], i; 
  
    // Store result in temp[] 
    for (i = 0; i < n; i++) 
        temp[arr[i]] = i; 
  
    // Copy temp back to arr[] 
    for (i = 0; i < n; i++) 
        arr[i] = temp[i]; 
} 
  
// A utility function to print contents of arr[0..n-1] 
void printArray(int arr[], int n) 
{ 
    int i; 
    for (i = 0; i < n; i++) 
        printf("%d ", arr[i]); 
    printf("\n"); 
} 
  
// Driver program 
int main() 
{ 
    int arr[] = { 1, 3, 0, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
  
    printf("Given array is \n"); 
    printArray(arr, n); 
  
    rearrangeNaive(arr, n); 
  
    printf("Modified array is \n"); 
    printArray(arr, n); 
    return 0; 
} 
```

## Java

```java
// A simple Java program to rearrange contents of arr[] 
// such that arr[j] becomes j if arr[i] is j 
class RearrangeArray { 
    // A simple method to rearrange 'arr[0..n-1]' so that 'arr[j]' 
    // becomes 'i' if 'arr[i]' is 'j' 
    void rearrangeNaive(int arr[], int n) 
    { 
        // Create an auxiliary array of same size 
        int temp[] = new int[n]; 
        int i; 
  
        // Store result in temp[] 
        for (i = 0; i < n; i++) 
            temp[arr[i]] = i; 
  
        // Copy temp back to arr[] 
        for (i = 0; i < n; i++) 
            arr[i] = temp[i]; 
    } 
  
    // A utility function to print contents of arr[0..n-1] 
    void printArray(int arr[], int n) 
    { 
        int i; 
        for (i = 0; i < n; i++) { 
            System.out.print(arr[i] + " "); 
        } 
        System.out.println(""); 
    } 
  
    // Driver program to test above functions 
    public static void main(String[] args) 
    { 
        RearrangeArray arrange = new RearrangeArray(); 
        int arr[] = { 1, 3, 0, 2 }; 
        int n = arr.length; 
  
        System.out.println("Given array is "); 
        arrange.printArray(arr, n); 
  
        arrange.rearrangeNaive(arr, n); 
  
        System.out.println("Modified array is "); 
        arrange.printArray(arr, n); 
    } 
} 
```

## Python3

```py
# A simple Python3 program to rearrange  
# contents of arr[] such that arr[j] 
# becomes j if arr[i] is j 
  
# A simple method to rearrange  
# 'arr[0..n-1]' so that 'arr[j]' 
# becomes 'i' if 'arr[i]' is 'j' 
def rearrangeNaive(arr, n): 
  
    # Create an auxiliary array  
    # of same size 
    temp = [0] * n 
      
    # Store result in temp[] 
    for i in range(0, n): 
        temp[arr[i]] = i 
  
    # Copy temp back to arr[] 
    for i in range(0, n): 
        arr[i] = temp[i] 
  
  
    # A utility function to print 
    # contents of arr[0..n-1] 
def printArray(arr, n): 
    for i in range(0, n): 
        print(arr[i], end = " ") 
  
# Driver program 
arr = [1, 3, 0, 2] 
n = len(arr) 
print("Given array is", end = " ") 
printArray(arr, n) 
  
rearrangeNaive(arr, n) 
print("\nModified array is", end = " ") 
printArray(arr, n) 
  
# This code is contributed by Smitha Dinesh Semwal 
```

## C#

```cs
// A simple C# program to rearrange contents of arr[] 
// such that arr[j] becomes j if arr[i] is j 
  
using System; 
class RearrangeArray { 
    // A simple method to rearrange 'arr[0..n-1]' so that 'arr[j]' 
    // becomes 'i' if 'arr[i]' is 'j' 
    void rearrangeNaive(int[] arr, int n) 
    { 
        // Create an auxiliary array of same size 
        int[] temp = new int[n]; 
        int i; 
  
        // Store result in temp[] 
        for (i = 0; i < n; i++) 
            temp[arr[i]] = i; 
  
        // Copy temp back to arr[] 
        for (i = 0; i < n; i++) 
            arr[i] = temp[i]; 
    } 
  
    // A utility function to print contents of arr[0..n-1] 
    void printArray(int[] arr, int n) 
    { 
        int i; 
        for (i = 0; i < n; i++) { 
            Console.Write(arr[i] + " "); 
        } 
        Console.WriteLine(""); 
    } 
  
    // Driver program to test above functions 
    public static void Main() 
    { 
        RearrangeArray arrange = new RearrangeArray(); 
        int[] arr = { 1, 3, 0, 2 }; 
        int n = arr.Length; 
  
        Console.WriteLine("Given array is "); 
        arrange.printArray(arr, n); 
  
        arrange.rearrangeNaive(arr, n); 
  
        Console.WriteLine("Modified array is "); 
        arrange.printArray(arr, n); 
    } 
} 
```

输出：

```
Given array is
1 3 0 2
Modified array is
2 0 3 1
```

上述解决方案的时间复杂度为`O(n)`，所需的辅助空间为`O(n)`。

我们可以在`O(n)`时间和`O(n)`辅助空间中解决这个问题吗？

这个想法基于这样一个事实，即修改后的数组基本上是输入数组的排列。 我们可以通过在更新之前存储下一个项目来找到目标排列。

例如，让我们考虑数组`{1, 3, 0, 2}`。 我们从`i = 0`开始，`arr[i]`为1。因此，我们转到`arr[1]`并将其更改为 0（因为`i`为 0）。 在进行更改之前，我们存储`arr[1]`的旧值，因为旧值将成为我们的新索引`i`。 在下一次迭代中，我们有`i = 3`，`arr[3]`为2，因此我们将`arr[2]`更改为 3。在进行更改之前，我们将下一个`i`存储为`arr[2]`的旧值。

以下代码给出了有关此方法的想法。

```cpp
// This function works only when output is a permutation
// with one cycle.
void rearrangeUtil(int arr[], int n)
{
    // 'val' is the value to be stored at 'arr[i]'
    int val = 0;   // The next value is determined
                  // using current index
    int i = arr[0];  // The next index is determined
                     // using current value

    // While all elements in cycle are not processed
    while (i != 0)
    {
        // Store value at index as it is going to be
        // used as next index
        int new_i = arr[i];

        // Update arr[]
        arr[i] = val;

        // Update value and index for next iteration
        val = i;
        i = new_i;
    }

    arr[0] = val;  // Update the value at arr[0]
}
```

上述功能不适用于`{2, 0, 1, 4, 5, 3}`之类的输入； 因为有两个周期。 一个周期是`(2, 0, 1)`，另一个周期是`(4, 5, 3)`。

如何使用`O(1)`空间约束处理多个循环？

这个想法是一个接一个地处理所有循环。 为了检查某个元素是否被处理，我们将已处理项`arr[i]`的值更改为`-arr[i]`。 由于不能将 0 设为负，因此我们首先将所有`arr[i]`更改为`arr[i] + 1`。最后，我们使所有值均为正，然后减去 1 以返回旧值。

## C++

```cpp
// A space efficient C++ program to rearrange contents of  
// arr[] such that arr[j] becomes j if arr[i] is j  
#include <iostream> 
using namespace std; 
  
// A utility function to rearrange elements in the cycle  
// starting at arr[i]. This function assumes values in  
// arr[] be from 1 to n. It changes arr[j-1] to i+1  
// if arr[i-1] is j+1  
void rearrangeUtil(int arr[], int n, int i)  
{  
    // 'val' is the value to be stored at 'arr[i]'  
    int val = -(i + 1); // The next value is determined  
    // using current index  
    i = arr[i] - 1; // The next index is determined  
    // using current value  
  
    // While all elements in cycle are not processed  
    while (arr[i] > 0)  
    { 
          
        // Store value at index as it is going to be  
        // used as next index  
        int new_i = arr[i] - 1;  
  
        // Update arr[]  
        arr[i] = val;  
  
        // Update value and index for next iteration  
        val = -(i + 1);  
        i = new_i;  
    }  
}  
  
// A space efficient method to rearrange 'arr[0..n-1]'  
// so that 'arr[j]' becomes 'i' if 'arr[i]' is 'j'  
void rearrange(int arr[], int n)  
{  
    // Increment all values by 1, so that all elements  
    // can be made negative to mark them as visited  
    int i;  
    for (i = 0; i < n; i++)  
        arr[i]++;  
  
    // Process all cycles  
    for (i = 0; i < n; i++)  
    { 
          
        // Process cycle starting at arr[i] if this cycle is  
        // not already processed  
        if (arr[i] > 0)  
            rearrangeUtil(arr, n, i);  
    }  
  
    // Change sign and values of arr[] to get the original  
    // values back, i.e., values in range from 0 to n-1  
    for (i = 0; i < n; i++)  
        arr[i] = (-arr[i]) - 1;  
}  
  
// A utility function to print contents of arr[0..n-1]  
void printArray(int arr[], int n)  
{  
    int i;  
    for (i = 0; i < n; i++)  
        cout << arr[i] << " ";  
    cout << endl;  
}  
  
// Driver program  
int main()  
{  
    int arr[] = { 2, 0, 1, 4, 5, 3 };  
    int n = sizeof(arr) / sizeof(arr[0]);  
  
    cout << "Given array is " << endl;  
    printArray(arr, n);  
  
    rearrange(arr, n);  
  
    cout << "Modified array is " << endl;  
    printArray(arr, n);  
    return 0;  
}  
  
// This code is contributed by shubhamsingh10 
```

## C

```c
// A space efficient C program to rearrange contents of 
// arr[] such that arr[j] becomes j if arr[i] is j 
#include <stdio.h> 
  
// A utility function to rearrange elements in the cycle 
// starting at arr[i]. This function assumes values in 
// arr[] be from 1 to n.  It changes arr[j-1] to i+1 
// if arr[i-1] is j+1 
void rearrangeUtil(int arr[], int n, int i) 
{ 
    // 'val' is the value to be stored at 'arr[i]' 
    int val = -(i + 1); // The next value is determined 
    // using current index 
    i = arr[i] - 1; // The next index is determined 
    // using current value 
  
    // While all elements in cycle are not processed 
    while (arr[i] > 0) { 
        // Store value at index as it is going to be 
        // used as next index 
        int new_i = arr[i] - 1; 
  
        // Update arr[] 
        arr[i] = val; 
  
        // Update value and index for next iteration 
        val = -(i + 1); 
        i = new_i; 
    } 
} 
  
// A space efficient method to rearrange 'arr[0..n-1]' 
// so that 'arr[j]' becomes 'i' if 'arr[i]' is 'j' 
void rearrange(int arr[], int n) 
{ 
    // Increment all values by 1, so that all elements 
    // can be made negative to mark them as visited 
    int i; 
    for (i = 0; i < n; i++) 
        arr[i]++; 
  
    // Process all cycles 
    for (i = 0; i < n; i++) { 
        // Process cycle starting at arr[i] if this cycle is 
        // not already processed 
        if (arr[i] > 0) 
            rearrangeUtil(arr, n, i); 
    } 
  
    // Change sign and values of arr[] to get the original 
    // values back, i.e., values in range from 0 to n-1 
    for (i = 0; i < n; i++) 
        arr[i] = (-arr[i]) - 1; 
} 
  
// A utility function to print contents of arr[0..n-1] 
void printArray(int arr[], int n) 
{ 
    int i; 
    for (i = 0; i < n; i++) 
        printf("%d ", arr[i]); 
    printf("\n"); 
} 
  
// Driver program 
int main() 
{ 
    int arr[] = { 2, 0, 1, 4, 5, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
  
    printf("Given array is \n"); 
    printArray(arr, n); 
  
    rearrange(arr, n); 
  
    printf("Modified array is \n"); 
    printArray(arr, n); 
    return 0; 
} 
```

## Java

```java
// A space efficient Java program to rearrange contents of 
// arr[] such that arr[j] becomes j if arr[i] is j 
  
class RearrangeArray { 
    // A utility function to rearrange elements in the cycle 
    // starting at arr[i]. This function assumes values in 
    // arr[] be from 1 to n.  It changes arr[j-1] to i+1 
    // if arr[i-1] is j+1 
    void rearrangeUtil(int arr[], int n, int i) 
    { 
        // 'val' is the value to be stored at 'arr[i]' 
  
        // The next value is determined using current index 
        int val = -(i + 1); 
  
        // The next index is determined 
        // using current value 
        i = arr[i] - 1; 
  
        // While all elements in cycle are not processed 
        while (arr[i] > 0) { 
            // Store value at index as it is going to be 
            // used as next index 
            int new_i = arr[i] - 1; 
  
            // Update arr[] 
            arr[i] = val; 
  
            // Update value and index for next iteration 
            val = -(i + 1); 
            i = new_i; 
        } 
    } 
  
    // A space efficient method to rearrange 'arr[0..n-1]' 
    // so that 'arr[j]' becomes 'i' if 'arr[i]' is 'j' 
    void rearrange(int arr[], int n) 
    { 
        // Increment all values by 1, so that all elements 
        // can be made negative to mark them as visited 
        int i; 
        for (i = 0; i < n; i++) 
            arr[i]++; 
  
        // Process all cycles 
        for (i = 0; i < n; i++) { 
            // Process cycle starting at arr[i] if this cycle is 
            // not already processed 
            if (arr[i] > 0) 
                rearrangeUtil(arr, n, i); 
        } 
  
        // Change sign and values of arr[] to get the original 
        // values back, i.e., values in range from 0 to n-1 
        for (i = 0; i < n; i++) 
            arr[i] = (-arr[i]) - 1; 
    } 
  
    // A utility function to print contents of arr[0..n-1] 
    void printArray(int arr[], int n) 
    { 
        int i; 
        for (i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
        System.out.println(""); 
    } 
  
    // Driver program 
    public static void main(String[] args) 
    { 
        RearrangeArray arrange = new RearrangeArray(); 
        int arr[] = { 2, 0, 1, 4, 5, 3 }; 
        int n = arr.length; 
  
        System.out.println("Given array is "); 
        arrange.printArray(arr, n); 
  
        arrange.rearrange(arr, n); 
  
        System.out.println("Modified array is "); 
        arrange.printArray(arr, n); 
    } 
} 
```

## Python3

```py
# A space efficient Python3 program to  
# rearrange contents of arr such that 
# arr[j] becomes j if arr[i] is j  
  
# A utility function to rearrange elements 
# in the cycle starting at arr[i]. This  
# function assumes values in arr be from 
# 1 to n. It changes arr[j-1] to i+1 if  
# arr[i-1] is j+1  
def rearrangeUtil(arr, n, i): 
      
    # 'val' is the value to be stored at   
    # 'arr[i]' 
    # The next value is determined using  
    # current index   
    val = -(i + 1)  
      
    # The next index is determined using 
    # current index  
    i = arr[i] - 1 
   
    # While all elements in cycle are  
    # not processed  
    while (arr[i] > 0): 
          
        # Store value at index as it is  
        # going to be used as next index  
        new_i = arr[i] - 1
          
        # Update arr  
        arr[i] = val  
          
        # Update value and index for  
        # next iteration  
        val = -(i + 1)  
        i = new_i  
  
# A space efficient method to rearrange 
# 'arr[0..n-1]' so that 'arr[j]' becomes  
# 'i' if 'arr[i]' is 'j'  
def rearrange(arr, n): 
      
    # Increment all values by 1, so that  
    # all elements can be made negative to  
    # mark them as visited  
    for i in range(n): 
        arr[i] += 1
          
    # Process all cycles  
    for i in range(n): 
          
        # Process cycle starting at arr[i] if   
        # this cycle is not already processed  
        if (arr[i] > 0): 
            rearrangeUtil(arr, n, i)  
      
    # Change sign and values of arr to  
    # get the original values back, i.e.,   
    # values in range from 0 to n-1  
    for i in range(n): 
        arr[i] = (-arr[i]) - 1
  
# A utility function to prcontents o 
# f arr[0..n-1]  
def printArray(arr, n): 
      
    for i in range(n): 
        print(arr[i], end = " ") 
    print() 
  
# Driver code  
arr = [ 2, 0, 1, 4, 5, 3 ] 
n = len(arr) 
  
print("Given array is ") 
printArray(arr, n)  
  
rearrange(arr, n)  
  
print("Modified array is ") 
printArray(arr, n)  
  
# This code is contributed by shubhamsingh10 
```

## C#

```cs
// A simple C# program to 
// rearrange contents of arr[] 
// such that arr[j] becomes 
// j if arr[i] is j 
using System; 
  
class GFG { 
    // A simple method to rearrange 
    // 'arr[0..n-1]' so that 'arr[j]' 
    // becomes 'i' if 'arr[i]' is 'j' 
    void rearrangeNaive(int[] arr, 
                        int n) 
    { 
        // Create an auxiliary 
        // array of same size 
        int[] temp = new int[n]; 
        int i; 
  
        // Store result in temp[] 
        for (i = 0; i < n; i++) 
            temp[arr[i]] = i; 
  
        // Copy temp back to arr[] 
        for (i = 0; i < n; i++) 
            arr[i] = temp[i]; 
    } 
  
    // A utility function to 
    // print contents of arr[0..n-1] 
    void printArray(int[] arr, int n) 
    { 
        int i; 
        for (i = 0; i < n; i++) { 
            Console.Write(arr[i] + " "); 
        } 
        Console.WriteLine(""); 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
        GFG arrange = new GFG(); 
        int[] arr = { 2, 0, 1, 4, 5, 3 }; 
        int n = arr.Length; 
  
        Console.WriteLine("Given array is "); 
        arrange.printArray(arr, n); 
  
        arrange.rearrangeNaive(arr, n); 
  
        Console.WriteLine("Modified array is "); 
        arrange.printArray(arr, n); 
    } 
} 
  
// This code is contributed by anuj_67.
```

输出：

```
Given array is
2 0 1 4 5 3
Modified array is
1 2 0 5 3 4 
```

乍一看，此方法的时间复杂度似乎大于`O(n)`。 如果我们仔细观察，会发现没有元素的处理次数超过了固定的次数。

另一种方法：想法是将每个元素的新值和旧值分别存储为`n`的商和`n`的余数（`n`是数组的大小）。
例如，假设一个元素的新值为 2，旧值为 1，`n`为 3，则该元素的值存储为`1 + 2 * 3 = 7`。我们可以按`7 % 3 = 1`检索其旧值，以及其新值`7 / 3 = 2`。

感谢 Prateek Oraon 建议使用此方法。

## C++

```cpp
// A simple C++ program to rearrange 
// contents of arr[] such that arr[j] 
// becomes j if arr[i] is j 
#include <bits/stdc++.h> 
using namespace std; 
  
// A simple method to rearrange 
// 'arr[0..n-1]' so that 'arr[j]' 
// becomes 'i' if 'arr[i]' is 'j' 
void rearrange(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) { 
  
        // retrieving old value and 
        // storing with the new one 
        arr[arr[i] % n] += i * n; 
    } 
  
    for (int i = 0; i < n; i++) { 
  
        // retrieving new value 
        arr[i] /= n; 
    } 
} 
  
// A utility function to print 
// contents of arr[0..n-1] 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
  
    cout << endl; 
} 
  
// Driver program 
int main() 
{ 
    int arr[] = { 2, 0, 1, 4, 5, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
  
    cout << "Given array is : " << endl; 
    printArray(arr, n); 
  
    rearrange(arr, n); 
  
    cout << "Modified array is :" << endl; 
    printArray(arr, n); 
  
    return 0; 
} 
```

## Java

```java
// A simple JAVA program to rearrange 
// contents of arr[] such that arr[j] 
// becomes j if arr[i] is j 
  
class GFG { 
  
    // A simple method to rearrange 
    // 'arr[0..n-1]' so that 'arr[j]' 
    // becomes 'i' if 'arr[i]' is 'j' 
    static void rearrange(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) { 
  
            // retrieving old value and 
            // storing with the new one 
            arr[arr[i] % n] += i * n; 
        } 
  
        for (int i = 0; i < n; i++) { 
  
            // retrieving new value 
            arr[i] /= n; 
        } 
    } 
  
    // A utility function to print 
    // contents of arr[0..n-1] 
    static void printArray(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) { 
            System.out.print(arr[i] + " "); 
        } 
  
        System.out.println(); 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 2, 0, 1, 4, 5, 3 }; 
        int n = arr.length; 
  
        System.out.println("Given array is : "); 
        printArray(arr, n); 
  
        rearrange(arr, n); 
  
        System.out.println("Modified array is :"); 
        printArray(arr, n); 
    } 
} 
  
// This code has been contributed by 29AjayKumar 
```

## Python3

```py
# A simple Python3 program to rearrange 
# contents of arr[] such that arr[j] 
# becomes j if arr[i] is j 
  
# A simple method to rearrange 
# 'arr[0..n-1]' so that 'arr[j]' 
# becomes 'i' if 'arr[i]' is 'j' 
def rearrange(arr, n): 
      
    for i in range(n): 
          
        # Retrieving old value and 
        # storing with the new one 
        arr[arr[i] % n] += i * n 
      
    for i in range(n): 
          
        # Retrieving new value 
        arr[i] //= n 
      
# A utility function to pr 
# contents of arr[0..n-1] 
def prArray(arr, n): 
      
    for i in range(n): 
        print(arr[i], end = " ") 
    print() 
  
# Driver code 
arr = [2, 0, 1, 4, 5, 3] 
n = len(arr) 
  
print("Given array is : ") 
prArray(arr, n) 
  
rearrange(arr, n) 
  
print("Modified array is :") 
prArray(arr, n) 
  
# This code is contributed by shubhamsingh10 
```

## C#

```cs
// A simple C# program to rearrange 
// contents of arr[] such that arr[j] 
// becomes j if arr[i] is j 
using System; 
  
class GFG{ 
  
    // A simple method to rearrange 
    // 'arr[0..n-1]' so that 'arr[j]' 
    // becomes 'i' if 'arr[i]' is 'j' 
    static void rearrange(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) { 
      
            // retrieving old value and 
            // storing with the new one 
            arr[arr[i] % n] += i * n; 
        } 
      
        for (int i = 0; i < n; i++) { 
      
            // retrieving new value 
            arr[i] /= n; 
        } 
    } 
      
    // A utility function to print 
    // contents of arr[0..n-1] 
    static void printArray(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
      
        Console.WriteLine(); 
    } 
      
    // Driver program 
    static public void Main () 
    { 
        int[] arr = { 2, 0, 1, 4, 5, 3 }; 
        int n = arr.Length; 
      
        Console.WriteLine("Given array is : "); 
        printArray(arr, n); 
      
        rearrange(arr, n); 
      
        Console.WriteLine("Modified array is :"); 
        printArray(arr, n); 
    } 
} 
  
// This code is contributed by shubhamsingh10 
```

输出：

```
Given array is : 
2 0 1 4 5 3 
Modified array is :
1 2 0 5 3 4 
```

