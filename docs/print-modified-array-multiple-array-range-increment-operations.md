# 在多次数组范围递增操作后打印修改后的数组

> 原文： [https://www.geeksforgeeks.org/print-modified-array-multiple-array-range-increment-operations/](https://www.geeksforgeeks.org/print-modified-array-multiple-array-range-increment-operations/)

给定一个包含`n`整数和值`d`的数组。 给出`m`个查询。 每个查询具有两个值`start`和`end`。 对于每个查询，问题是将给定数组中从`start`到`end`索引的值增加给定值`d`。 需要线性省时的解决方案来处理此类多个查询。

**示例**：

```
Input : arr[] = {3, 5, 4, 8, 6, 1}
        Query list: {0, 3}, {4, 5}, {1, 4}, 
                           {0, 1}, {2, 5}
        d = 2
Output : 7 11 10 14 12 5

Executing 1st query {0, 3}
arr = {5, 7, 6, 10, 6, 1}

Executing 2nd query {4, 5}
arr = {5, 7, 6, 10, 8, 3}

Executing 3rd query {1, 4}
arr = {5, 9, 8, 12, 10, 3}

Executing 4th query {0, 1}
arr = {7, 11, 8, 12, 10, 3}

Executing 5th query {2, 5}
arr = {7, 11, 10, 14, 12, 5}

Note: Each query is executed on the 
previously modified array.

```



**朴素的方法**：对于每个查询，遍历`start`到`end`范围内的数组，并将该范围内的值增加给定值`d`。

**有效方法**：创建大小为`n`的数组`sum[]`并将其所有索引初始化为 0。现在，对于每个`start, end`索引对在`sum[]`数组上应用给定的运算。 仅当存在索引`end + 1`时，操作才是`sum[start] += d`和`sum[end + 1] -= d`。 现在，从索引`i = 1`到`n-1`，将`sum[]`数组中的值累加为：`sum[i] += sum[i-1]`。 最后，对于索引`i = 0`到`n-1`，执行以下操作：`arr[i] += sum[i]`。

## C++ 

```cpp

// C++ implementation to increment values in the 
// given range by a value d for multiple queries 
#include <bits/stdc++.h> 

using namespace std; 

// structure to store the (start, end) index pair for 
// each query 
struct query { 
    int start, end; 
}; 

// function to increment values in the given range 
// by a value d for multiple queries 
void incrementByD(int arr[], struct query q_arr[], 
                  int n, int m, int d) 
{ 
    int sum[n]; 
    memset(sum, 0, sizeof(sum)); 

    // for each (start, end) index pair perform the 
    // following operations on 'sum[]' 
    for (int i = 0; i < m; i++) { 

        // increment the value at index 'start' by 
        // the given value 'd' in 'sum[]' 
        sum[q_arr[i].start] += d; 

        // if the index '(end+1)' exists then decrement  
        // the value at index '(end+1)' by the given  
        // value 'd' in 'sum[]' 
        if ((q_arr[i].end + 1) < n) 
            sum[q_arr[i].end + 1] -= d; 
    } 

    // Now, perform the following operations: 
    // accumulate values in the 'sum[]' array and  
    // then add them to the corresponding indexes 
    // in 'arr[]' 
    arr[0] += sum[0]; 
    for (int i = 1; i < n; i++) { 
        sum[i] += sum[i - 1]; 
        arr[i] += sum[i]; 
    } 
} 

// function to print the elements of the given array 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = { 3, 5, 4, 8, 6, 1 }; 
    struct query q_arr[] = { { 0, 3 }, { 4, 5 }, { 1, 4 },  
                                       { 0, 1 }, { 2, 5 } }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int m = sizeof(q_arr) / sizeof(q_arr[0]); 
    int d = 2; 

    cout << "Original Array:\n"; 
    printArray(arr, n); 

    // modifying the array for multiple queries 
    incrementByD(arr, q_arr, n, m, d); 

    cout << "\nModified Array:\n"; 
    printArray(arr, n); 

    return 0; 
} 

```

## Java

```java

// Java implementation to increment values in the  
// given range by a value d for multiple queries 
class GFG  
{ 

    // structure to store the (start, end)  
    // index pair for each query 
    static class query 
    { 
        int start, end; 

        query(int start, int end)  
        { 
            this.start = start; 
            this.end = end; 
        } 
    } 

    // function to increment values in the given range 
    // by a value d for multiple queries 
    public static void incrementByD(int[] arr, query[] q_arr, 
                                    int n, int m, int d)  
    { 
        int[] sum = new int[n]; 

        // for each (start, end) index pair, perform  
        // the following operations on 'sum[]' 
        for (int i = 0; i < m; i++) 
        { 

            // increment the value at index 'start'  
            // by the given value 'd' in 'sum[]' 
            sum[q_arr[i].start] += d; 

            // if the index '(end+1)' exists then  
            // decrement the value at index '(end+1)'  
            // by the given value 'd' in 'sum[]' 
            if ((q_arr[i].end + 1) < n) 
                sum[q_arr[i].end + 1] -= d; 
        } 

        // Now, perform the following operations: 
        // accumulate values in the 'sum[]' array and 
        // then add them to the corresponding indexes 
        // in 'arr[]' 
        arr[0] += sum[0]; 
        for (int i = 1; i < n; i++) 
        { 
            sum[i] += sum[i - 1]; 
            arr[i] += sum[i]; 
        } 
    } 

    // function to print the elements of the given array 
    public static void printArray(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int[] arr = { 3, 5, 4, 8, 6, 1 }; 
        query[] q_arr = new query[5]; 
        q_arr[0] = new query(0, 3); 
        q_arr[1] = new query(4, 5); 
        q_arr[2] = new query(1, 4); 
        q_arr[3] = new query(0, 1); 
        q_arr[4] = new query(2, 5); 
        int n = arr.length; 
        int m = q_arr.length; 
        int d = 2; 
        System.out.println("Original Array:"); 
        printArray(arr, n); 

        // modifying the array for multiple queries 
        incrementByD(arr, q_arr, n, m, d); 
        System.out.println("\nModified Array:"); 
        printArray(arr, n); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python3 implementation to increment  
# values in the given range by a value d  
# for multiple queries 

# structure to store the (start, end)  
# index pair for each query 

# function to increment values in the given range 
# by a value d for multiple queries 
def incrementByD(arr, q_arr, n, m, d): 

    sum = [0 for i in range(n)] 

    # for each (start, end) index pair perform  
    # the following operations on 'sum[]' 
    for i in range(m): 

        # increment the value at index 'start'  
        # by the given value 'd' in 'sum[]' 
        sum[q_arr[i][0]] += d 

        # if the index '(end+1)' exists then decrement 
        # the value at index '(end+1)' by the given 
        # value 'd' in 'sum[]' 
        if ((q_arr[i][1] + 1) < n): 
            sum[q_arr[i][1] + 1] -= d 

    # Now, perform the following operations: 
    # accumulate values in the 'sum[]' array and 
    # then add them to the corresponding indexes 
    # in 'arr[]' 
    arr[0] += sum[0] 
    for i in range(1, n): 
        sum[i] += sum[i - 1] 
        arr[i] += sum[i] 

# function to print the elements  
# of the given array 
def printArray(arr, n): 

    for i in arr: 
        print(i, end = " ") 

# Driver Code 
arr = [ 3, 5, 4, 8, 6, 1] 

q_arr = [[0, 3], [4, 5], [1, 4], 
         [0, 1], [2, 5]] 

n = len(arr) 
m = len(q_arr) 

d = 2

print("Original Array:") 
printArray(arr, n) 

# modifying the array for multiple queries 
incrementByD(arr, q_arr, n, m, d) 

print("\nModified Array:") 
printArray(arr, n) 

# This code is contributed 
# by Mohit Kumar 

```

## C# 

```cs

// C# implementation to increment values in the  
// given range by a value d for multiple queries 
using System; 

class GFG  
{ 

    // structure to store the (start, end)  
    // index pair for each query 
    public class query 
    { 
        public int start, end; 

        public query(int start, int end)  
        { 
            this.start = start; 
            this.end = end; 
        } 
    } 

    // function to increment values in the given range 
    // by a value d for multiple queries 
    public static void incrementByD(int[] arr, query[] q_arr, 
                                    int n, int m, int d)  
    { 
        int[] sum = new int[n]; 

        // for each (start, end) index pair, perform  
        // the following operations on 'sum[]' 
        for (int i = 0; i < m; i++) 
        { 

            // increment the value at index 'start'  
            // by the given value 'd' in 'sum[]' 
            sum[q_arr[i].start] += d; 

            // if the index '(end+1)' exists then  
            // decrement the value at index '(end+1)'  
            // by the given value 'd' in 'sum[]' 
            if ((q_arr[i].end + 1) < n) 
                sum[q_arr[i].end + 1] -= d; 
        } 

        // Now, perform the following operations: 
        // accumulate values in the 'sum[]' array and 
        // then add them to the corresponding indexes 
        // in 'arr[]' 
        arr[0] += sum[0]; 
        for (int i = 1; i < n; i++) 
        { 
            sum[i] += sum[i - 1]; 
            arr[i] += sum[i]; 
        } 
    } 

    // function to print the elements of the given array 
    public static void printArray(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 3, 5, 4, 8, 6, 1 }; 
        query[] q_arr = new query[5]; 
        q_arr[0] = new query(0, 3); 
        q_arr[1] = new query(4, 5); 
        q_arr[2] = new query(1, 4); 
        q_arr[3] = new query(0, 1); 
        q_arr[4] = new query(2, 5); 
        int n = arr.Length; 
        int m = q_arr.Length; 
        int d = 2; 
        Console.WriteLine("Original Array:"); 
        printArray(arr, n); 

        // modifying the array for multiple queries 
        incrementByD(arr, q_arr, n, m, d); 
        Console.WriteLine("\nModified Array:"); 
        printArray(arr, n); 
    } 
} 

// This code is contributed by Princi Singh 

```

**输出**：

```
Original Array:
3 5 4 8 6 1
Modified Array:
7 11 10 14 12 5

```

**时间复杂度**：`O(m + n)`。

**辅助空间**：`O(n)`。

