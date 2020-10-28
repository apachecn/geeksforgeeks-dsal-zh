# 在数组

> 原文：[https://www.geeksforgeeks.org/find-pairs-in-array-whose-sum-does-not-exist-in-array/](https://www.geeksforgeeks.org/find-pairs-in-array-whose-sum-does-not-exist-in-array/)

中查找总和不存在的数组对

给定由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是打印所有对的数组元素，其和在给定数组中不存在。 如果不存在这样的对，则打印**“ -1”** 。

**范例**：

> **输入**：arr [] = {2，4，2，6}
> **输出**：
> （2，6）
> （4，6）
> （2，6）
> **说明**：
> 数组中所有可能的对是（2，4），（2，2），（2，6），（4，2） ，（4，6）和（2，6）。
> 其中，对（2、6），（4、6）和（2、6）分别具有在阵列中不存在的和{8、10、8}。
> 
> **输入**：arr [] = {1、1、2、3}
> **输出**：]
> 数组中所有可能的对是（1、1），（1、2），（1、3），（1、2），（1、3）和（2、3）。
> 其中，在数组中不存在总和的唯一对是（2，3）。

**天真的方法**：

解决该问题的最简单方法是逐个生成所有可能的对，并通过遍历数组检查每个对是否存在于数组中。 如果找到任何对，且其总和存在于数组中，则打印该对。 否则，移至下一对。

 ***时间复杂度**：O（N <sup>3</sup> ）

***辅助空间**：O（N）*

**有效方法**：

可以使用 [HashSet](http://www.geeksforgeeks.org/hashset-in-java/) 解决问题。 请按照以下步骤解决问题：

*   将元素存储在 **HashSet** 中的数组中。

*   现在，遍历所有数组元素并生成所有可能的对。

*   对于每对，检查 HashSet 中是否存在该对的总和。 如果是这样，请打印该对。 否则，移至下一对。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement  
// the above approach  
#include <bits/stdc++.h>  
using namespace std;  

// Function to print all pairs  
// with sum not present in the array  
void findPair(int arr[], int n)  
{  
    int i, j;  

    // Corner Case  
    if (n < 2)  
    {  
        cout << "-1" << endl;  
    }  

    // Stores the distinct array  
    // elements  
    set <int> hashMap;  

    for(int k = 0; k < n; k++)  
    {  
        hashMap.insert(arr[k]);  
    }  

    // Generate all possible pairs  
    for(i = 0; i < n - 1; i++)  
    {  
        for(j = i + 1; j < n; j++)  
        {  

            // Calculate sum of current pair  
            int sum = arr[i] + arr[j];  

            // Check if the sum exists in  
            // the HashSet or not  
            if (hashMap.find(sum) == hashMap.end())  
            {  

                cout << "(" << arr[i] << ", "
                    << arr[j] << ")" << endl;  
            }  
        }  
    }  
}  

// Driver code  
int main()  
{  
    int arr[] = { 2, 4, 2, 6 };  
    int n = sizeof(arr) / sizeof(arr[0]);  

    findPair(arr, n);  
    return 0;  
}  

// This code is contributed by divyeshrabadiya07  

```

## Java

```java

// Java program to implement  
// the above approach  
import java.util.*;  

class GFG {  

    // Function to print all pairs  
    // with sum not present in the array  
    public static void findPair(  
        int[] arr, int n)  
    {  
        int i, j;  

        // Corner Case  
        if (n < 2) {  
            System.out.println("-1");  
        }  

        // Stores the distinct array  
        // elements  
        HashSet<Integer> hashMap  
            = new HashSet<Integer>();  

        for (Integer k : arr) {  
            hashMap.add(k);  
        }  

        // Generate all possible pairs  
        for (i = 0; i < n - 1; i++) {  

            for (j = i + 1; j < n; j++) {  

                // Calculate sum of current pair  
                int sum = arr[i] + arr[j];  

                // Check if the sum exists in  
                // the HashSet or not  
                if (!hashMap.contains(sum)) {  

                    System.out.println(  
                        "(" + arr[i] + ", "
                        + arr[j] + ")");  
                }  
            }  
        }  
    }  

    // Driver Code  
    public static void main(String[] args)  
    {  
        int[] arr = { 2, 4, 2, 6 };  
        int n = arr.length;  

        findPair(arr, n);  
    }  
}  

```

## Python3

```py

# Python3 program to implement  
# the above approach  

# Function to print all pairs  
# with sum not present in the array  
def findPair(arr, n):  

    # Corner Case  
    if (n < 2):  
        print("-1")  

    # Stores the distinct array  
    # elements  
    hashMap = []  

    for k in arr:  
        hashMap.append(k)  

    # Generate all possible pairs  
    for i in range (n - 1):  
        for j in range (i + 1, n):  
            # Calculate sum of current pair  
            sum = arr[i] + arr[j]  

            # Check if the sum exists in  
            # the HashSet or not  
            if sum not in hashMap:  
                print("(", arr[i] , ", ",  
                        arr[j] , ")")  

# Driver Code  
if __name__ == "__main__":  

    arr = [ 2, 4, 2, 6 ]  
    n = len(arr)  

    findPair(arr, n)  

# This code is contributed by ChitraNayal  

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 
using System.Collections.Generic;  

class GFG{ 

// Function to print all pairs 
// with sum not present in the array 
public static void findPair(int[] arr, int n) 
{ 
    int i, j; 

    // Corner Case 
    if (n < 2) 
    { 
        Console.Write("-1"); 
    } 

    // Stores the distinct array 
    // elements 
    HashSet<int> hashMap = new HashSet<int>(); 

    foreach(int k in arr) 
    { 
        hashMap.Add(k); 
    } 

    // Generate all possible pairs 
    for(i = 0; i < n - 1; i++) 
    { 
        for(j = i + 1; j < n; j++) 
        { 

            // Calculate sum of current pair 
            int sum = arr[i] + arr[j]; 

            // Check if the sum exists in 
            // the HashSet or not 
            if (!hashMap.Contains(sum)) 
            { 
                Console.Write("(" + arr[i] + 
                             ", " + arr[j] +  
                             ")\n"); 
            } 
        } 
    } 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    int[] arr = { 2, 4, 2, 6 }; 
    int n = arr.Length; 

    findPair(arr, n); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output:**

```
(2, 6)
(4, 6)
(2, 6)

```

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（N）*



* * *

* * *



