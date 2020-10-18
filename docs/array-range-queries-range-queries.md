# 范围查询中的数组范围查询

> 原文： [https://www.geeksforgeeks.org/array-range-queries-range-queries/](https://www.geeksforgeeks.org/array-range-queries-range-queries/)

给定大小为`n`的数组和大小为`m`的给定命令集。 命令从 1 到`m`枚举。 这些命令可以是以下两种类型的命令：

1.  类型 1，`[lr(1 <= l <= r <= n)]`：将数组的所有元素加一，其索引属于范围`[l, r]`。 在这些查询中，索引包含在范围内。

2.  类型 2，`[lr(1 <= l <= r <= m)]`：执行所有索引在`[l, r]`范围内的命令。 在这些查询中，索引包含在范围内。 保证`r`严格小于当前命令的枚举/数量。

注意：根据问题说明，数组索引从 1 开始。

**示例 1**：

```
Input : 5 5
        1 1 2
        1 4 5
        2 1 2
        2 1 3
        2 3 4
Output : 7 7 0 7 7
```

**示例 1 的说明**：

我们的数组最初是大小为 5 的数组，其每个元素都已初始化为 0。

因此，现在的问题是对于上述示例，我们有 5 个查询。

1.  查询 1 的类型为 1：如上所述，在给定索引为 1 和 2 的情况下，我们将简单地将数组索引增加 1，因此在执行第一个数组后，我们的数组将变为`1 1 0 0 0`。

2.  查询 2 的类型为 1：如上所述，在给定索引为 4 和 5 的情况下，我们将简单地将数组索引增加 1

    ，因此在执行第一个数组后，我们的数组将变为`1 1 0 1 1`。

3.  查询 3 是类型 2：如此类查询的定义中所述，我们将执行范围内所述的查询，即，我们将操作查询而不是数组。 给定的范围是 1 和 2，所以我们将再次执行查询 1 和 2，即，我们将对类型 2 查询使用重复方法，因此我们将再次执行查询 1，数组将是`2 2 0 11`。现在，当执行 查询，我们将执行查询 2，结果数组将是`2 2 0 2 2`。

4.  查询 4 是类型 2：如此类查询的定义中所述，我们将执行范围内所述的查询，即，我们将操作查询而不是数组。 给定的范围是 1 和 3，因此我们将再次执行查询 1、2 和 3，即使用重复方法将执行查询 1、2 和 3。 再次执行查询 1 后，数组将为`3 3 0 2 2`。 再次执行查询 2 后，数组将为`3 3 0 3 3`。 现在由于查询 3 包含范围，我们将执行查询 3，结果数组将为`4 4 0 4 4`。 如上所述。

5.  查询 5 是类型 2：最后一个查询将执行上面已说明的第三和第四查询。 执行完第三个查询后，我们的数组将为`5 5 0 5 5`。 在执行第四个查询后，即执行查询 1、2 和 3，我们的数组将为`7 7 0 7 7`以上是所需结果。

**示例 2**：

```
Input : 1 2
        1 1 1
        1 1 1
Output : 2

```

示例 2 的说明：

我们的数组初始大小为 1，其每个元素都已初始化为 0。

因此，现在的问题表明，对于上述示例，我们有 2 个查询。

1.  查询 1 的类型为 1：如上所述，在给定索引为 1 和 1 的情况下，我们将简单地将数组索引加 1，因此在执行第一个数组后，我们的数组将变为 1。

2.  查询 2 的类型为 1：如上所述，在给定索引为 1 和 1 的情况下，我们将简单地将数组索引增加 1，因此在执行第一个数组后，我们的数组将变为 2。 这给了我们想要的结果。



**方法 1**：

此方法是暴力方法，其中对 2 类查询应用简单递归，对 1 类查询执行简单的数组索引增量。

## C++ 

```cpp

// CPP program to perform range queries over range 
// queries. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to execute type 1 query 
void type1(int arr[], int start, int limit) 
{ 
    // incrementing the array by 1 for type  
    // 1 queries 
    for (int i = start; i <= limit; i++)        
        arr[i]++; 
} 

// Function to execute type 2 query 
void type2(int arr[], int query[][3], int start, int limit) 
{ 
    for (int i = start; i <= limit; i++) { 

        // If the query is of type 1 function 
        // call to type 1 query 
        if (query[i][0] == 1)  
            type1(arr, query[i][1], query[i][2]); 

        // If the query is of type 2 recursive call  
        // to type 2 query 
        else if (query[i][0] == 2)  
            type2(arr, query, query[i][1], query[i][2]);         
    } 
} 

// Driver code 
int main() 
{ 
    // Input size of array amd number of queries 
    int n = 5, m = 5; 
    int arr[n + 1]; 
    for (int i = 1; i <= n; i++)  
        arr[i] = 0; 

    // Build query matrix 
    int temp[15] = { 1, 1, 2, 1, 4, 5, 2,  
                    1, 2, 2, 1, 3, 2, 3, 4 }; 
    int query[5][3]; 
    int j = 0; 
    for (int i = 1; i <= m; i++) { 
        query[i][0] = temp[j++]; 
        query[i][1] = temp[j++]; 
        query[i][2] = temp[j++]; 
    } 

    // Perform queries  
    for (int i = 1; i <= m; i++)  
        if (query[i][0] == 1)  
            type1(arr, query[i][1], query[i][2]); 
        else if (query[i][0] == 2)  
            type2(arr, query, query[i][1], query[i][2]);         

    // printing the result 
    for (int i = 1; i <= n; i++)  
        cout << arr[i] << " "; 

    return 0; 
} 

```

## Java

```java
// Java program to perform range queries  
// over range queries. 
import java.util.*; 
  
class GFG  
{ 
  
    // Function to execute type 1 query 
    static void type1(int[] arr, int start, int limit)  
    { 
  
        // incrementing the array by 1 for type 
        // 1 queries 
        for (int i = start; i <= limit; i++) 
            arr[i]++; 
    } 
  
    // Function to execute type 2 query 
    static void type2(int[] arr, int[][] query,  
                      int start, int limit)  
    { 
        for (int i = start; i <= limit; i++) 
        { 
  
            // If the query is of type 1 function 
            // call to type 1 query 
            if (query[i][0] == 1) 
                type1(arr, query[i][1], query[i][2]); 
  
            // If the query is of type 2 recursive call 
            // to type 2 query 
            else if (query[i][0] == 2) 
                type2(arr, query, query[i][1], 
                                  query[i][2]); 
        } 
    } 
  
    // Driver Code 
    public static void main(String[] args) 
    { 
  
        // Input size of array amd number of queries 
        int n = 5, m = 5; 
        int[] arr = new int[n + 1]; 
  
        // Build query matrix 
        int[] temp = { 1, 1, 2, 1, 4, 5, 2,  
                       1, 2, 2, 1, 3, 2, 3, 4 }; 
        int[][] query = new int[6][4]; 
        int j = 0; 
        for (int i = 1; i <= m; i++)  
        { 
            query[i][0] = temp[j++]; 
            query[i][1] = temp[j++]; 
            query[i][2] = temp[j++]; 
        } 
  
        // Perform queries 
        for (int i = 1; i <= m; i++) 
            if (query[i][0] == 1) 
                type1(arr, query[i][1], query[i][2]); 
            else if (query[i][0] == 2) 
                type2(arr, query, query[i][1], 
                                  query[i][2]); 
  
        // printing the result 
        for (int i = 1; i <= n; i++) 
            System.out.print(arr[i] + " "); 
        System.out.println(); 
    } 
} 
  
// This code is contributed by 
// sanjeev2552 
```

## Python3

```py
# Python3 program to perform range  
# queries over range queries. 
  
# Function to execute type 1 query 
def type1(arr, start, limit): 
      
    # incrementing the array by 1  
    # for type 1 queries 
    for i in range(start, limit + 1): 
        arr[i] += 1
  
# Function to execute type 2 query 
def type2(arr, query, start, limit): 
  
    for i in range(start, limit + 1): 
  
        # If the query is of type 1  
        # function call to type 1 query 
        if (query[i][0] == 1): 
            type1(arr, query[i][1], query[i][2]) 
  
        # If the query is of type 2  
        # recursive call to type 2 query 
        elif (query[i][0] == 2): 
            type2(arr, query, query[i][1],  
                              query[i][2]) 
  
# Driver code 
  
# Input size of array amd  
# number of queries 
n = 5
m = 5
arr = [0 for i in range(n + 1)] 
  
# Build query matrix 
temp = [1, 1, 2, 1, 4, 5, 2,  
        1, 2, 2, 1, 3, 2, 3, 4 ] 
  
query = [[0 for i in range(3)]  
            for j in range(6)] 
  
j = 0
for i in range(1, m + 1): 
    query[i][0] = temp[j] 
    j += 1
    query[i][1] = temp[j] 
    j += 1
    query[i][2] = temp[j] 
    j += 1
  
# Perform queries 
for i in range(1, m + 1): 
    if (query[i][0] == 1): 
        type1(arr, query[i][1], 
                   query[i][2]) 
    elif (query[i][0] == 2): 
        type2(arr, query, query[i][1],  
                          query[i][2]) 
  
# printing the result 
for i in range(1, n + 1): 
    print(arr[i], end = " ") 
  
# This code is contributed 
# by mohit kumar 
```

## C#

```cs
// C# program to perform range queries  
// over range queries. 
using System; 
  
class GFG  
{ 
  
    // Function to execute type 1 query 
    static void type1(int[] arr, int start, int limit)  
    { 
  
        // incrementing the array by 1 for type 
        // 1 queries 
        for (int i = start; i <= limit; i++) 
            arr[i]++; 
    } 
  
    // Function to execute type 2 query 
    static void type2(int[] arr, int[,] query,  
                    int start, int limit)  
    { 
        for (int i = start; i <= limit; i++) 
        { 
  
            // If the query is of type 1 function 
            // call to type 1 query 
            if (query[i, 0] == 1) 
                type1(arr, query[i,1], query[i,2]); 
  
            // If the query is of type 2 recursive call 
            // to type 2 query 
            else if (query[i, 0] == 2) 
                type2(arr, query, query[i, 1], 
                                query[i, 2]); 
        } 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
  
        // Input size of array amd number of queries 
        int n = 5, m = 5; 
        int[] arr = new int[n + 1]; 
  
        // Build query matrix 
        int[] temp = { 1, 1, 2, 1, 4, 5, 2,  
                    1, 2, 2, 1, 3, 2, 3, 4 }; 
        int[,] query = new int[6,4]; 
        int j = 0; 
        for (int i = 1; i <= m; i++)  
        { 
            query[i, 0] = temp[j++]; 
            query[i, 1] = temp[j++]; 
            query[i, 2] = temp[j++]; 
        } 
  
        // Perform queries 
        for (int i = 1; i <= m; i++) 
            if (query[i, 0] == 1) 
                type1(arr, query[i, 1], query[i, 2]); 
            else if (query[i, 0] == 2) 
                type2(arr, query, query[i, 1], 
                                query[i, 2]); 
  
        // printing the result 
        for (int i = 1; i <= n; i++) 
            Console.Write(arr[i] + " "); 
        Console.WriteLine(); 
    } 
} 
  
// This code is contributed by AbhiThakur 
```

输出：

```
7 7 0 7 7
```

上面代码的时间复杂度是`O(2 ^ m)`

方法 2：

在此方法中，我们使用一个额外的数组来创建记录数组，以查找执行特定查询的时间，并且在创建记录数组之后，我们仅执行类型1的查询，并将记录数组的包含内容简单地添加到 主数组，这将给我们结果数组。

## C++

```cpp
// CPP program to perform range queries over range 
// queries. 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to create the record array 
void record_sum(int record[], int l, int r, 
                           int n, int adder) 
{ 
    for (int i = l; i <= r; i++)  
        record[i] += adder;     
} 
  
// Driver Code 
int main() 
{ 
    int n = 5, m = 5; 
    int arr[n]; 
  
    // Build query matrix 
    memset(arr, 0, sizeof arr); 
    int query[5][3] = { { 1, 1, 2 }, { 1, 4, 5 }, 
                         { 2, 1, 2 }, { 2, 1, 3 },  
                         { 2, 3, 4 } }; 
    int record[m]; 
    memset(record, 0, sizeof record); 
  
    for (int i = m - 1; i >= 0; i--) { 
  
        // If query is of type 2 then function 
        // call to record_sum 
        if (query[i][0] == 2)  
            record_sum(record, query[i][1] - 1,  
               query[i][2] - 1, m, record[i] + 1); 
          
        // If query is of type 1 then simply add  
        // 1 to the record array 
        else 
            record_sum(record, i, i, m, 1); 
          
    } 
  
    // for type 1 queries adding the contains of  
    // record array to the main array record array 
    for (int i = 0; i < m; i++) { 
        if (query[i][0] == 1)  
            record_sum(arr, query[i][1] - 1, 
                 query[i][2] - 1, n, record[i]);         
    } 
  
    // printing the array 
    for (int i = 0; i < n; i++)  
        cout << arr[i] << ' '; 
      
    return 0; 
} 
```

## Java

```java
// Java program to perform range queries  
// over range queries. 
import java.util.Arrays; 
  
class GFG  
{ 
  
    // Function to create the record array 
    static void record_sum(int record[], int l, 
                           int r, int n, int adder) 
    { 
        for (int i = l; i <= r; i++) 
        { 
            record[i] += adder; 
        } 
    } 
  
    // Driver Code 
    public static void main(String[] args) 
    { 
        int n = 5, m = 5; 
        int arr[] = new int[n]; 
  
        // Build query matrix 
        Arrays.fill(arr, 0); 
        int query[][] = {{1, 1, 2}, {1, 4, 5}, 
                         {2, 1, 2}, {2, 1, 3}, 
                         {2, 3, 4}}; 
        int record[] = new int[m]; 
        Arrays.fill(record, 0); 
  
        for (int i = m - 1; i >= 0; i--)  
        { 
  
            // If query is of type 2 then function 
            // call to record_sum 
            if (query[i][0] == 2)  
            { 
                record_sum(record, query[i][1] - 1,  
                                   query[i][2] - 1, m,  
                                   record[i] + 1); 
            }  
              
            // If query is of type 1 then  
            // simply add 1 to the record array 
            else 
            { 
                record_sum(record, i, i, m, 1); 
            } 
  
        } 
  
        // for type 1 queries adding the contains of  
        // record array to the main array record array 
        for (int i = 0; i < m; i++)  
        { 
            if (query[i][0] == 1)  
            { 
                record_sum(arr, query[i][1] - 1,  
                                query[i][2] - 1, 
                                n, record[i]); 
            } 
        } 
  
        // printing the array 
        for (int i = 0; i < n; i++) 
        { 
            System.out.print(arr[i] + " "); 
        } 
    } 
} 
  
// This code is contributed  
// by Princi Singh 
```

## Python3

```py
# Python3 program to perform range queries over range 
# queries. 
  
# Function to create the record array 
def record_sum(record, l, r, n, adder): 
      
    for i in range(l, r + 1): 
        record[i] += adder  
  
# Driver Code 
n = 5
m = 5
arr = [0]*n 
  
# Build query matrix 
query = [[1, 1, 2 ],[ 1, 4, 5 ],[2, 1, 2 ],  
        [ 2, 1, 3 ],[ 2, 3, 4]] 
record = [0]*m 
  
for i in range(m - 1, -1, -1): 
      
    # If query is of type 2 then function 
    # call to record_sum 
    if (query[i][0] == 2): 
        record_sum(record, query[i][1] - 1,  
                query[i][2] - 1, m, record[i] + 1) 
          
    # If query is of type 1 then simply add  
    # 1 to the record array 
    else: 
        record_sum(record, i, i, m, 1) 
          
# for type 1 queries adding the contains of  
# record array to the main array record array 
for i in range(m): 
    if (query[i][0] == 1): 
        record_sum(arr, query[i][1] - 1, 
            query[i][2] - 1, n, record[i])  
  
# printing the array 
for i in range(n): 
    print(arr[i], end=' ') 
  
# This code is contributed by shubhamsingh10 
```

## C#

```cs
// C# program to perform range queries  
// over range queries. 
using System; 
      
class GFG  
{ 
  
    // Function to create the record array 
    static void record_sum(int []record, int l, 
                        int r, int n, int adder) 
    { 
        for (int i = l; i <= r; i++) 
        { 
            record[i] += adder; 
        } 
    } 
  
    // Driver Code 
    public static void Main(String[] args) 
    { 
        int n = 5, m = 5; 
        int []arr = new int[n]; 
  
        // Build query matrix 
        int [,]query = {{1, 1, 2}, {1, 4, 5}, 
                        {2, 1, 2}, {2, 1, 3}, 
                        {2, 3, 4}}; 
        int []record = new int[m]; 
  
        for (int i = m - 1; i >= 0; i--)  
        { 
  
            // If query is of type 2 then function 
            // call to record_sum 
            if (query[i,0] == 2)  
            { 
                record_sum(record, query[i,1] - 1,  
                                query[i,2] - 1, m,  
                                record[i] + 1); 
            }  
              
            // If query is of type 1 then  
            // simply add 1 to the record array 
            else
            { 
                record_sum(record, i, i, m, 1); 
            } 
  
        } 
  
        // for type 1 queries adding the contains of  
        // record array to the main array record array 
        for (int i = 0; i < m; i++)  
        { 
            if (query[i, 0] == 1)  
            { 
                record_sum(arr, query[i, 1] - 1,  
                                query[i, 2] - 1, 
                                n, record[i]); 
            } 
        } 
  
        // printing the array 
        for (int i = 0; i < n; i++) 
        { 
            Console.Write(arr[i] + " "); 
        } 
    } 
} 
  
// This code is contributed by Rajput-Ji 
```

输出：

```
7 7 0 7 7
```

上面代码的时间复杂度是`O(n ^ 2)`

方法 3：

通过对记录数组应用平方根分解，使此方法更加有效。

## C++

```cpp
// CPP program to perform range queries over range 
// queries. 
#include <bits/stdc++.h> 
#define max 10000 
using namespace std; 
  
// For prefix sum array 
void update(int arr[], int l) 
{ 
    arr[l] += arr[l - 1]; 
} 
  
// This function is used to apply square root  
// decomposition in the record array 
void record_func(int block_size, int block[],  
         int record[], int l, int r, int value) 
{ 
    // traversing first block in range 
    while (l < r && l % block_size != 0 && l != 0) { 
        record[l] += value; 
        l++; 
    } 
    // traversing completely overlapped blocks in range 
    while (l + block_size <= r + 1) { 
        block[l / block_size] += value; 
        l += block_size; 
    } 
    // traversing last block in range 
    while (l <= r) { 
        record[l] += value; 
        l++; 
    } 
} 
// Function to print the resultant array 
void print(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++)  
        cout << arr[i] << " ";     
} 
  
// Driver code 
int main() 
{ 
    int n = 5, m = 5; 
    int arr[n], record[m]; 
    int block_size = sqrt(m); 
    int block[max]; 
    int command[5][3] = { { 1, 1, 2 }, { 1, 4, 5 },  
                          { 2, 1, 2 }, { 2, 1, 3 }, 
                          { 2, 3, 4 } }; 
    memset(arr, 0, sizeof arr); 
    memset(record, 0, sizeof record); 
    memset(block, 0, sizeof block); 
  
    for (int i = m - 1; i >= 0; i--) { 
  
        // If query is of type 2 then function 
        // call to record_func 
        if (command[i][0] == 2) { 
            int x = i / (block_size); 
            record_func(block_size, block, record, 
                        command[i][1] - 1, command[i][2] - 1,  
                        (block[x] + record[i] + 1)); 
        } 
        // If query is of type 1 then simply add  
        // 1 to the record array 
        else 
            record[i]++;         
    } 
  
    // Merging the value of the block in the record array 
    for (int i = 0; i < m; i++) { 
        int check = (i / block_size); 
        record[i] += block[check]; 
    } 
  
    for (int i = 0; i < m; i++) { 
        // If query is of type 1 then the array  
        // elements are over-written by the record 
        //  array 
        if (command[i][0] == 1) { 
            arr[command[i][1] - 1] += record[i]; 
            if ((command[i][2] - 1) < n - 1)  
                arr[(command[i][2])] -= record[i];             
        } 
    } 
  
    // The prefix sum of the array 
    for (int i = 1; i < n; i++)  
        update(arr, i); 
      
    // Printing the resultant array 
    print(arr, n); 
    return 0; 
} 
```

## Java

```java
// Java program to perform range queries over range 
// queries. 
public class GFG { 
  
    static final int max = 10000; 
  
// For prefix sum array 
    static void update(int arr[], int l) { 
        arr[l] += arr[l - 1]; 
    } 
  
// This function is used to apply square root  
// decomposition in the record array 
    static void record_func(int block_size, int block[], 
            int record[], int l, int r, int value) { 
        // traversing first block in range 
        while (l < r && l % block_size != 0 && l != 0) { 
            record[l] += value; 
            l++; 
        } 
        // traversing completely overlapped blocks in range 
        while (l + block_size <= r + 1) { 
            block[l / block_size] += value; 
            l += block_size; 
        } 
        // traversing last block in range 
        while (l <= r) { 
            record[l] += value; 
            l++; 
        } 
    } 
// Function to print the resultant array 
  
    static void print(int arr[], int n) { 
        for (int i = 0; i < n; i++) { 
            System.out.print(arr[i] + " "); 
        } 
    } 
  
// Driver code 
    public static void main(String[] args) { 
  
        int n = 5, m = 5; 
        int arr[] = new int[n], record[] = new int[m]; 
        int block_size = (int) Math.sqrt(m); 
        int block[] = new int[max]; 
        int command[][] = {{1, 1, 2}, {1, 4, 5}, 
        {2, 1, 2}, {2, 1, 3}, 
        {2, 3, 4}}; 
  
        for (int i = m - 1; i >= 0; i--) { 
  
            // If query is of type 2 then function 
            // call to record_func 
            if (command[i][0] == 2) { 
                int x = i / (block_size); 
                record_func(block_size, block, record, 
                        command[i][1] - 1, command[i][2] - 1, 
                        (block[x] + record[i] + 1)); 
            } // If query is of type 1 then simply add  
            // 1 to the record array 
            else { 
                record[i]++; 
            } 
        } 
  
        // Merging the value of the block in the record array 
        for (int i = 0; i < m; i++) { 
            int check = (i / block_size); 
            record[i] += block[check]; 
        } 
  
        for (int i = 0; i < m; i++) { 
            // If query is of type 1 then the array  
            // elements are over-written by the record 
            //  array 
            if (command[i][0] == 1) { 
                arr[command[i][1] - 1] += record[i]; 
                if ((command[i][2] - 1) < n - 1) { 
                    arr[(command[i][2])] -= record[i]; 
                } 
            } 
        } 
  
        // The prefix sum of the array 
        for (int i = 1; i < n; i++) { 
            update(arr, i); 
        } 
  
        // Printing the resultant array 
        print(arr, n); 
  
    } 
  
} 
// This code is contributed by 29AjayKumar 
```

## Python3

```py
# Python3 program to perform range  
# queries over range queries. 
import math 
  
max = 10000
  
# For prefix sum array 
def update(arr, l): 
      
    arr[l] += arr[l - 1] 
  
# This function is used to apply square root 
# decomposition in the record array 
def record_func(block_size, block, 
                record, l, r, value): 
  
    # Traversing first block in range 
    while (l < r and 
           l % block_size != 0 and
           l != 0): 
        record[l] += value 
        l += 1
  
    # Traversing completely overlapped  
    # blocks in range 
    while (l + block_size <= r + 1): 
        block[l // block_size] += value 
        l += block_size 
  
    # Traversing last block in range 
    while (l <= r): 
        record[l] += value 
        l += 1
  
# Function to print the resultant array 
def print_array(arr, n): 
      
    for i in range(n): 
        print(arr[i], end = " ") 
  
# Driver code 
if __name__ == "__main__": 
  
    n = 5
    m = 5
    arr = [0] * n 
    record = [0] * m 
      
    block_size = (int)(math.sqrt(m)) 
    block = [0] * max
      
    command = [ [ 1, 1, 2 ], 
                [ 1, 4, 5 ], 
                [ 2, 1, 2 ], 
                [ 2, 1, 3 ], 
                [ 2, 3, 4 ] ] 
  
    for i in range(m - 1, -1, -1): 
  
        # If query is of type 2 then function 
        # call to record_func 
        if (command[i][0] == 2): 
            x = i // (block_size) 
              
            record_func(block_size, block, 
                        record, command[i][1] - 1, 
                                command[i][2] - 1, 
                        (block[x] + record[i] + 1)) 
  
        # If query is of type 1 then simply add 
        # 1 to the record array 
        else: 
            record[i] += 1
  
    # Merging the value of the block 
    # in the record array 
    for i in range(m): 
        check = (i // block_size) 
        record[i] += block[check] 
  
    for i in range(m): 
          
        # If query is of type 1 then the array 
        # elements are over-written by the record 
        # array 
        if (command[i][0] == 1): 
            arr[command[i][1] - 1] += record[i] 
              
            if ((command[i][2] - 1) < n - 1): 
                arr[(command[i][2])] -= record[i] 
  
    # The prefix sum of the array 
    for i in range(1, n): 
        update(arr, i) 
  
    # Printing the resultant array 
    print_array(arr, n) 
  
# This code is contributed by chitranayal 
```

## C#

```cs
// C# program to perform range queries over range 
// queries. 
using System;  
public class GFG { 
   
    static readonly int max = 10000; 
   
// For prefix sum array 
    static void update(int []arr, int l) { 
        arr[l] += arr[l - 1]; 
    } 
   
// This function is used to apply square root  
// decomposition in the record array 
    static void record_func(int block_size, int []block, 
            int []record, int l, int r, int value) { 
        // traversing first block in range 
        while (l < r && l % block_size != 0 && l != 0) { 
            record[l] += value; 
            l++; 
        } 
        // traversing completely overlapped blocks in range 
        while (l + block_size <= r + 1) { 
            block[l / block_size] += value; 
            l += block_size; 
        } 
        // traversing last block in range 
        while (l <= r) { 
            record[l] += value; 
            l++; 
        } 
    } 
// Function to print the resultant array 
   
    static void print(int []arr, int n) { 
        for (int i = 0; i < n; i++) { 
            Console.Write(arr[i] + " "); 
        } 
    } 
   
// Driver code 
    public static void Main() { 
   
        int n = 5, m = 5; 
        int []arr = new int[n]; int []record = new int[m]; 
        int block_size = (int) Math.Sqrt(m); 
        int []block = new int[max]; 
        int [,]command= {{1, 1, 2}, {1, 4, 5}, 
        {2, 1, 2}, {2, 1, 3}, 
        {2, 3, 4}}; 
   
        for (int i = m - 1; i >= 0; i--) { 
   
            // If query is of type 2 then function 
            // call to record_func 
            if (command[i,0] == 2) { 
                int x = i / (block_size); 
                record_func(block_size, block, record, 
                        command[i,1] - 1, command[i,2] - 1, 
                        (block[x] + record[i] + 1)); 
            } // If query is of type 1 then simply add  
            // 1 to the record array 
            else { 
                record[i]++; 
            } 
        } 
   
        // Merging the value of the block in the record array 
        for (int i = 0; i < m; i++) { 
            int check = (i / block_size); 
            record[i] += block[check]; 
        } 
   
        for (int i = 0; i < m; i++) { 
            // If query is of type 1 then the array  
            // elements are over-written by the record 
            //  array 
            if (command[i,0] == 1) { 
                arr[command[i,1] - 1] += record[i]; 
                if ((command[i,2] - 1) < n - 1) { 
                    arr[(command[i,2])] -= record[i]; 
                } 
            } 
        } 
   
        // The prefix sum of the array 
        for (int i = 1; i < n; i++) { 
            update(arr, i); 
        } 
   
        // Printing the resultant array 
        print(arr, n); 
   
    } 
   
} 
// This code is contributed by 29AjayKumar 
```

输出：

```
7 7 0 7 7
```

方法 4：

通过分别为查询 1 和查询 2 创建两个二进制索引树来应用[二进制索引树或 Fenwick 树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)，使该方法更加有效。

## CPP

```cpp
// CPP program to perform range queries over range 
// queries. 
#include <bits/stdc++.h> 
using namespace std; 
  
// Updates a node in Binary Index Tree (BITree) at given index 
// in BITree.  The given value 'val' is added to BITree[i] and 
// all of its ancestors in tree. 
void updateBIT(int BITree[], int n, int index, int val) 
{ 
    // index in BITree[] is 1 more than the index in arr[] 
    index = index + 1; 
  
    // Traverse all ancestors and add 'val' 
    while (index <= n) { 
  
        // Add 'val' to current node of BI Tree 
        BITree[index] = (val + BITree[index]); 
  
        // Update index to that of parent in update View 
        index = (index + (index & (-index))); 
    } 
    return; 
} 
  
// Constructs and returns a Binary Indexed Tree for given 
// array of size n. 
int* constructBITree(int n) 
{ 
    // Create and initialize BITree[] as 0 
    int* BITree = new int[n + 1]; 
    for (int i = 1; i <= n; i++)  
        BITree[i] = 0; 
      
    return BITree; 
} 
  
// Returns sum of arr[0..index]. This function assumes 
// that the array is preprocessed and partial sums of 
// array elements are stored in BITree[] 
int getSum(int BITree[], int index) 
{ 
    int sum = 0; 
    // index in BITree[] is 1 more than the index in arr[] 
    index = index + 1; 
  
    // Traverse ancestors of BITree[index] 
    while (index > 0) { 
  
        // Add element of BITree to sum 
        sum = (sum + BITree[index]); 
  
        // Move index to parent node in getSum View 
        index -= index & (-index); 
    } 
    return sum; 
} 
  
// Function to update the BITree 
void update(int BITree[], int l, int r, int n, int val) 
{ 
    updateBIT(BITree, n, l, val); 
    updateBIT(BITree, n, r + 1, -val); 
    return; 
} 
  
// Driver code 
int main() 
{ 
    int n = 5, m = 5; 
    int temp[15] = { 1, 1, 2, 1, 4, 5, 2, 1, 2, 
                            2, 1, 3, 2, 3, 4 }; 
    int q[5][3]; 
    int j = 0; 
    for (int i = 1; i <= m; i++) { 
        q[i][0] = temp[j++]; 
        q[i][1] = temp[j++]; 
        q[i][2] = temp[j++]; 
    } 
  
    // BITree for query of type 2 
    int* BITree = constructBITree(m); 
  
    // BITree for query of type 1 
    int* BITree2 = constructBITree(n); 
  
    // Input the queries in a 2D matrix 
    for (int i = 1; i <= m; i++)  
        cin >> q[i][0] >> q[i][1] >> q[i][2]; 
      
     // If query is of type 2 then function call  
     // to update with BITree 
    for (int i = m; i >= 1; i--)         
        if (q[i][0] == 2) 
            update(BITree, q[i][1] - 1, q[i][2] - 1, m, 1); 
      
    for (int i = m; i >= 1; i--) { 
        if (q[i][0] == 2) { 
            long int val = getSum(BITree, i - 1); 
            update(BITree, q[i][1] - 1, q[i][2] - 1, m, val); 
        } 
    } 
  
    // If query is of type 1 then function call  
    // to update with BITree2 
    for (int i = m; i >= 1; i--) {         
        if (q[i][0] == 1) { 
            long int val = getSum(BITree, i - 1); 
            update(BITree2, q[i][1] - 1, q[i][2] - 1, 
                    n, (val + 1)); 
        } 
    } 
  
    for (int i = 1; i <= n; i++)  
        cout << (getSum(BITree2, i - 1)) << " "; 
      
    return 0; 
} 
```

输出：

```
7 7 0 7 7
```

方法 3 和方法 4 的时间复杂度为`O(log n)`。