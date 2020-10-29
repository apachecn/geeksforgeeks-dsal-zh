# 将数组转换为简化形式| 设置 1（简单和哈希）

> 原文：[https://www.geeksforgeeks.org/convert-an-array-to-reduced-form-set-1-simple-and-hashing/](https://www.geeksforgeeks.org/convert-an-array-to-reduced-form-set-1-simple-and-hashing/)

给定具有 n 个不同元素的数组，请将给定数组转换为所有元素都在 0 到 n-1 范围内的形式。 元素的顺序相同，即，0 代替最小元素，1 代表第二个最小元素，…n-1 代表最大元素。

```
Input:  arr[] = {10, 40, 20}
Output: arr[] = {0, 2, 1}

Input:  arr[] = {5, 10, 40, 30, 20}
Output: arr[] = {0, 1, 4, 3, 2}

```

预期时间复杂度为 O（n Log n）。

## [我们强烈建议您单击此处并进行实践，然后再继续解决方案。](https://practice.geeksforgeeks.org/problem-page.php?pid=608)

**方法 1（简单）**

一个简单的解决方案是首先找到最小元素，将其替换为 0，考虑剩余数组，在剩余数组中找到最小值，然后将其替换为 1，依此类推。 该解决方案的时间复杂度为`O(N ^ 2)`

**方法 2（高效）**

这个想法是使用哈希和排序。 以下是步骤。

1.  创建一个临时数组并将给定数组的内容复制到 temp []。 这需要`O(n)`时间。

2.  以升序对 temp []进行排序。 这需要 O（n Log n）时间。

3.  创建一个空的哈希表。 这需要`O(1)`时间。

4.  从左到右遍历 temp []并将数字及其值的映射（在转换后的数组中）存储在哈希表中。 这平均需要`O(n)`时间。

5.  遍历给定的数组，并使用哈希表将元素更改为其位置。 这平均需要`O(n)`时间。

该解决方案的总时间复杂度为 O（n Log n）。

以下是上述想法的实现。

## C++

```cpp

// C++ program to convert an array in reduced 
// form 
#include <bits/stdc++.h> 
using namespace std; 

void convert(int arr[], int n) 
{ 
    // Create a temp array and copy contents 
    // of arr[] to temp 
    int temp[n]; 
    memcpy(temp, arr, n*sizeof(int)); 

    // Sort temp array 
    sort(temp, temp + n); 

    // Create a hash table. Refer  
    // http://tinyurl.com/zp5wgef  
    unordered_map<int, int> umap; 

    // One by one insert elements of sorted 
    // temp[] and assign them values from 0 
    // to n-1 
    int val = 0; 
    for (int i = 0; i < n; i++) 
        umap[temp[i]] = val++; 

    // Convert array by taking positions from 
    // umap 
    for (int i = 0; i < n; i++) 
        arr[i] = umap[arr[i]]; 
} 

void printArr(int arr[], int n) 
{ 
    for (int i=0; i<n; i++) 
        cout << arr[i] << " "; 
} 

// Driver program to test above method 
int main() 
{ 
    int arr[] = {10, 20, 15, 12, 11, 50}; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    cout << "Given Array is \n"; 
    printArr(arr, n); 

    convert(arr , n); 

    cout << "\n\nConverted Array is \n"; 
    printArr(arr, n); 

    return 0; 
} 

```

## Java

```java

// Java Program to convert an Array 
// to reduced form 
import java.util.*; 

class GFG  
{ 
    public static void convert(int arr[], int n) 
    { 
        // Create a temp array and copy contents 
        // of arr[] to temp 
        int temp[] = arr.clone(); 

        // Sort temp array 
        Arrays.sort(temp); 

        // Create a hash table. 
        HashMap<Integer, Integer> umap = new HashMap<>(); 

        // One by one insert elements of sorted 
        // temp[] and assign them values from 0 
        // to n-1 
        int val = 0; 
        for (int i = 0; i < n; i++) 
            umap.put(temp[i], val++); 

        // Convert array by taking positions from 
        // umap 
        for (int i = 0; i < n; i++) 
            arr[i] = umap.get(arr[i]); 
    } 

    public static void printArr(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 

        int arr[] = {10, 20, 15, 12, 11, 50}; 
        int n = arr.length; 

        System.out.println("Given Array is "); 
        printArr(arr, n); 

        convert(arr , n); 

        System.out.println("\n\nConverted Array is "); 
        printArr(arr, n); 

    } 
} 

// This code is contributed by Abhishek Panwar 

```

## Python3

```py

# Python3 program to convert an array  
# in reduced form 
def convert(arr, n): 
    # Create a temp array and copy contents 
    # of arr[] to temp 
    temp = [arr[i] for i in range (n) ] 

    # Sort temp array 
    temp.sort() 

    # create a map 
    umap = {} 

    # One by one insert elements of sorted 
    # temp[] and assign them values from 0 
    # to n-1 
    val = 0
    for i in range (n): 
        umap[temp[i]] = val 
        val += 1

    # Convert array by taking positions from umap 
    for i in range (n): 
        arr[i] = umap[arr[i]] 

def printArr(arr, n): 
    for i in range(n): 
        print(arr[i], end = " ") 

# Driver Code 
if __name__ == "__main__": 
    arr = [10, 20, 15, 12, 11, 50] 
    n = len(arr) 
    print("Given Array is ") 
    printArr(arr, n) 
    convert(arr , n) 
    print("\n\nConverted Array is ") 
    printArr(arr, n) 

# This code is contributed by Abhishek Gupta 

```

## C#

```cs

// C# Program to convert an Array 
// to reduced form 
using System; 
using System.Collections.Generic; 
using System.Linq; 

class GFG  
{ 
    public static void convert(int []arr, int n) 
    { 
        // Create a temp array and copy contents 
        // of []arr to temp 
        int []temp = new int[arr.Length]; 
        Array.Copy(arr, 0, temp, 0, arr.Length); 

        // Sort temp array 
        Array.Sort(temp); 

        // Create a hash table. 
        Dictionary<int, int> umap =  
            new Dictionary<int, int>(); 

        // One by one insert elements of sorted 
        // []temp and assign them values from 0 
        // to n - 1 
        int val = 0; 
        for (int i = 0; i < n; i++) 
            if(umap.ContainsKey(temp[i])) 
                umap[temp[i]] = val++; 
            else
                umap.Add(temp[i], val++); 

        // Convert array by taking positions from 
        // umap 
        for (int i = 0; i < n; i++) 
            arr[i] = umap[arr[i]]; 
    } 

    public static void printArr(int []arr, int n) 
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 

        int []arr = {10, 20, 15, 12, 11, 50}; 
        int n = arr.Length; 

        Console.WriteLine("Given Array is "); 
        printArr(arr, n); 

        convert(arr , n); 

        Console.WriteLine("\n\nConverted Array is "); 
        printArr(arr, n); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output :**

```
Given Array is 
10 20 15 12 11 50 

Converted Array is 
0 4 3 2 1 5 

```

[**将数组转换为简化形式| 集 2（使用向量对）**](https://www.geeksforgeeks.org/convert-array-reduced-form-set-2-using-vector-pairs/)

本文由 **Dheeraj Gupta** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

