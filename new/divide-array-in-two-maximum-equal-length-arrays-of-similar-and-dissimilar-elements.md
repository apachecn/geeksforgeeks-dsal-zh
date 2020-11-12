# 将相似和不相似元素的两个最大等长数组划分为数组

> 原文：[https://www.geeksforgeeks.org/divide-array-in-two-maximum-equal-length-arrays-of-similar-and-dissimilar-elements/](https://www.geeksforgeeks.org/divide-array-in-two-maximum-equal-length-arrays-of-similar-and-dissimilar-elements/)

给定一个自然数为`n`的数组`arr`，找到可以将数组`arr`划分为两个相等大小的数组的最大大小，这样 第一个数组包含所有相同的元素，而第二个数组包含所有不同的元素。

**示例**：

> **输入**：`n = 8, arr[] = {7, 3, 7, 1, 7, 7}`
>
> **输出**：
>
> ```
> 最大大小为：3
> arr1[] = {7, 7, 7}
> arr2[] = {1, 3, 7}
> ```
> 
> **说明**：
>
> 可以构造两个大小为 3 的数组 。
>
> 第一个数组为`[7, 7, 7]`，第二个数组为`[1, 3, 7]`。
> 
> **输入**：`n = 7, arr[] = {1, 2, 1, 5, 1, 6, 7, 2}`
> **输出**：
>
> ```
> 最大大小为：3
> arr1[] = {1, 1, 1}
> arr2[] = {2, 5, 6}
> ```

**方法**：

为解决上述问题，主要思想是使用散列来查找数组中每个元素的出现频率。

*   使用哈希向量`v`找到数组`arr[]`中存在频率最高的元素。

*   查找数组`arr[]`中存在的全部唯一元素。

*   对于具有最大频率的元素，有两种情况：最大频率元素将进入第一个数组，然后数组的大小分别为`diff1 – 1`和`max1`。 否则，最大频率的至少一个元素进入第二数组，并且大小最大分别为`diff1`和`max1 ? 1`。 然后找到数组可拆分的最大大小，为`max(min(diff1 ? 1, max1), min(diff1, max1 ? 1))`。

*   使用`max_size`和最大频率为`max1`的元素找到相似元素的第一个数组。

*   使用`max_size`和哈希向量`v`查找第二个唯一元素数组。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the max-size to which 
// an array can be divided into 2 equal parts 
// such that one part contains unique elements  
// while another contains similar elements 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the max-size to which an array 
// can be divided into 2 equal parts 
void Solve(int arr[], int size, int n) 
{ 

    vector<int> v(n + 1); 

    // Vector to find the frequency of 
    // each element of array 
    for (int i = 0; i < size; i++) 
        v[arr[i]]++; 

    // Find the maximum frequency 
    // element present in array arr[] 
    int max1 = (max_element(v.begin(), v.end())  
                                       - v.begin()); 
    // Find total unique elements 
    // present in array arr[] 
    int diff1 = n + 1 - count(v.begin(), v.end(), 0); 

    // Find the Max-Size to which 
    // an array arr[] can be splitted 
    int max_size = max(min(v[max1] - 1, diff1),  
                            min(v[max1], diff1 - 1)); 

    cout << "Maximum size is :" << max_size << "\n"; 

    // Find the first array 
    // containing same elements 
    cout << "The First Array Is : \n"; 
    for (int i = 0; i < max_size; i++) { 
        cout << max1 << " "; 
        v[max1] -= 1; 
    } 

    cout << "\n"; 

    // Find the second array 
    // containing unique elements 
    cout << "The Second Array Is : \n"; 
    for (int i = 0; i < (n + 1); i++) { 
        if (v[i] > 0) { 
            cout << i << " "; 
            max_size--; 
        } 
        if (max_size < 1) 
            break; 
    } 

    cout << "\n"; 
} 

// Driver code 
int main() 
{ 
    // initialise n 
    int n = 7; 

    // array declaration 
    int arr[] = { 1, 2, 1, 5, 1, 6, 7, 2 }; 

    // size of array 
    int size = sizeof(arr) / sizeof(arr[0]); 

    Solve(arr, size, n); 

    return 0; 
} 

```

## Java

```java

// Java program to find the  
// max-size to which an array  
// can be divided into 2 equal parts 
// such that one part contains unique  
// elements while another contains  
// similar elements 
import java.io.*; 
import java.lang.*; 
import java.util.*; 
class GFG{ 

  // Function to find the max-size to  
  // which an array can be divided into  
  // 2 equal parts 
  static void Solve(int arr[],  
                    int size, int n) 
  { 
    int[] v = new int[n + 1]; 

    // Array to find the frequency of 
    // each element of array 
    for (int i = 0; i < size; i++) 
      v[arr[i]]++; 

    // Find the index maximum frequency 
    // element present in array arr[] 
    int max1 = -1, mx = -1; 
    for (int i = 0; i < v.length; i++)  
    { 
      if (v[i] > mx)  
      { 
        mx = v[i]; 
        max1 = i; 
      } 
    } 
    // Find total unique elements 
    // present in array arr[] 
    int cnt = 0; 
    for (int i : v)  
    { 
      if (i == 0) 
        ++cnt; 
    } 
    int diff1 = n + 1 - cnt; 

    // Find the Max-Size to which 
    // an array arr[] can be splitted 
    int max_size = Math.max(Math.min(v[max1] - 1,  
                                     diff1), 
                            Math.min(v[max1],  
                                     diff1 - 1)); 
    System.out.println("Maximum size is: " +  
                        max_size); 

    // Find the first array 
    // containing same elements 
    System.out.println("First Array is"); 
    for (int i = 0; i < max_size; i++)  
    { 
      System.out.print(max1 + " "); 
      v[max1] -= 1; 
    } 
    System.out.println(); 

    // Find the second array 
    // containing unique elements 
    System.out.println("The Second Array Is :"); 
    for (int i = 0; i < (n + 1); i++)  
    { 
      if (v[i] > 0)  
      { 
        System.out.print(i + " "); 
        max_size--; 
      } 
      if (max_size < 1) 
        break; 
    } 
    System.out.println(); 
  } 

  // Driver Code 
  public static void main(String[] args) 
  { 
    // initialise n 
    int n = 7; 

    // array declaration 
    int arr[] = new int[] {1, 2, 1, 5,  
                           1, 6, 7, 2}; 

    // size of array 
    int size = arr.length; 

    Solve(arr, size, n); 
  } 
} 

// This code is contributed by Sri_srajit

```

## Python3

```py

# Python3 program to find the max-size to which 
# an array can be divided into 2 equal parts 
# such that one part contains unique elements  
# while another contains similar elements 

# Function to find the max-size to which an  
# array can be divided into 2 equal parts 
def Solve(arr, size, n): 

    v = [0] * (n + 1); 

    # Vector to find the frequency of 
    # each element of list 
    for i in range(size): 
        v[arr[i]] += 1

    # Find the maximum frequency 
    # element present in list arr 
    max1 = max(set(arr), key = v.count) 

    # Find total unique elements 
    # present in list arr 
    diff1 = n + 1 - v.count(0) 

    # Find the Max-Size to which 
    # an array arr[] can be splitted 
    max_size = max(min(v[max1] - 1, diff1),  
                   min(v[max1], diff1 - 1)) 

    print("Maximum size is :", max_size) 

    # Find the first array 
    # containing same elements 
    print("The First Array Is : ") 
    for i in range(max_size): 
        print(max1, end = " ") 
        v[max1] -= 1

    print() 

    # Find the second array 
    # containing unique elements 
    print("The Second Array Is : ") 
    for i in range(n + 1): 
        if (v[i] > 0): 
            print(i, end = " ") 
            max_size -= 1

        if (max_size < 1): 
            break

    print() 

# Driver code 
if __name__ == "__main__": 

    # Initialise n 
    n = 7

    # Array declaration 
    arr = [ 1, 2, 1, 5, 1, 6, 7, 2 ] 

    # Size of array 
    size = len(arr) 

    Solve(arr, size, n) 

# This code is contributed by chitranayal 

```

## C#

```cs

// C# program to find the max-size  
// to which an array can be divided 
// into 2 equal parts such that one 
// part contains unique elements 
// while another contains similar 
// elements 
using System; 

class GFG{ 

// Function to find the max-size to  
// which an array can be divided into  
// 2 equal parts 
static void Solve(int []arr,  
                  int size, int n) 
{ 
    int[] v = new int[n + 1]; 

    // Array to find the frequency of 
    // each element of array 
    for(int i = 0; i < size; i++) 
        v[arr[i]]++; 

    // Find the index maximum frequency 
    // element present in array arr[] 
    int max1 = -1, mx = -1; 
    for(int i = 0; i < v.Length; i++)  
    { 
        if (v[i] > mx)  
        { 
            mx = v[i]; 
            max1 = i; 
        } 
    } 

    // Find total unique elements 
    // present in array arr[] 
    int cnt = 0; 
    foreach(int i in v)  
    { 
        if (i == 0) 
            ++cnt; 
    } 

    int diff1 = n + 1 - cnt; 

    // Find the Max-Size to which 
    // an array arr[] can be splitted 
    int max_size = Math.Max(Math.Min(v[max1] - 1,  
                                     diff1), 
                            Math.Min(v[max1],  
                                     diff1 - 1)); 

    Console.Write("Maximum size is :" +  
                   max_size + "\n"); 

    // Find the first array 
    // containing same elements 
    Console.Write("The First Array Is :\n"); 

    for(int i = 0; i < max_size; i++)  
    { 
        Console.Write(max1 + " "); 
        v[max1] -= 1; 
    } 
    Console.Write("\n"); 

    // Find the second array 
    // containing unique elements 
    Console.Write("The Second Array Is :\n"); 
    for(int i = 0; i < (n + 1); i++)  
    { 
        if (v[i] > 0)  
        { 
            Console.Write(i + " "); 
            max_size--; 
        } 
        if (max_size < 1) 
            break; 
    } 
    Console.Write("\n"); 
} 

// Driver Code 
public static void Main(string[] args) 
{ 

    // Initialise n 
    int n = 7; 

    // Array declaration 
    int []arr = new int[] { 1, 2, 1, 5,  
                            1, 6, 7, 2 }; 

    // Size of array 
    int size = arr.Length; 

    Solve(arr, size, n); 
} 
} 

// This code is contributed by rutvik_56 

```

**输出**： 

```
Maximum size is :3
The First Array Is : 
1 1 1 
The Second Array Is : 
2 5 6

```

**时间复杂度**：`O(n)`。

