# 查找数组中非重复（不同）元素的总和

> 原文： [https://www.geeksforgeeks.org/find-sum-non-repeating-distinct-elements-array/](https://www.geeksforgeeks.org/find-sum-non-repeating-distinct-elements-array/)

给定一个具有重复元素的整数数组，任务是查找数组中所有不同元素的总和。

**示例**：

```
Input  : arr[] = {12, 10, 9, 45, 2, 10, 10, 45,10};
Output : 78
Here we take 12, 10, 9, 45, 2 for sum
because it's distinct elements 

Input : arr[] = {1, 10, 9, 4, 2, 10, 10, 45 , 4};
Output : 71

```



**简单解决方案**是使用两个嵌套循环。 外循环从最左边的元素开始一个接一个地选择一个元素。 内部循环检查元素的左侧是否存在。 如果存在，则忽略该元素。

**时间复杂度**：`O(n^2)`。

**辅助空间**：`O(1)`。

这个问题的**更好的解决方案**是，使用排序技术，我们首先按升序对数组的所有元素进行排序，然后在数组中逐个查找不同的元素。

## C++ 

```cpp

// C++ Find the sum of all non-repeated 
// elements in an array 
#include<bits/stdc++.h> 
using namespace std; 

// Find the sum of all non-repeated elements 
// in an array 
int findSum(int arr[], int n) 
{ 
    // sort all elements of array 
    sort(arr, arr + n); 

    int sum = 0; 
    for (int i=0; i<n; i++) 
    { 
        if (arr[i] != arr[i+1]) 
            sum = sum + arr[i]; 
    } 

    return sum; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {1, 2, 3, 1, 1, 4, 5, 6}; 
    int n = sizeof(arr)/sizeof(int); 
    cout << findSum(arr, n); 
    return 0; 
} 

```

## Java

```java
import java.util.Arrays; 
  
// Java Find the sum of all non-repeated  
// elements in an array  
public class GFG { 
  
// Find the sum of all non-repeated elements  
// in an array  
    static int findSum(int arr[], int n) { 
        // sort all elements of array  
  
        Arrays.sort(arr); 
         
        int sum = arr[0]; 
        for (int i = 0; i < n-1; i++) { 
            if (arr[i] != arr[i + 1]) { 
                sum = sum + arr[i+1]; 
            } 
        } 
  
        return sum; 
    } 
  
// Driver code  
    public static void main(String[] args) { 
        int arr[] = {1, 2, 3, 1, 1, 4, 5, 6}; 
        int n = arr.length; 
        System.out.println(findSum(arr, n)); 
  
    } 
}
```

## Python3

```py
# Python3 Find the sum of all non-repeated 
# elements in an array 
  
   
# Find the sum of all non-repeated elements 
# in an array 
def findSum(arr,  n): 
    # sort all elements of array 
    arr.sort() 
   
    sum = arr[0] 
    for i in range(0,n-1): 
        if (arr[i] != arr[i+1]): 
            sum = sum + arr[i+1] 
      
    return sum
   
# Driver code 
def main(): 
    arr= [1, 2, 3, 1, 1, 4, 5, 6] 
    n = len(arr) 
    print(findSum(arr, n)) 
  
if __name__ == '__main__': 
    main() 
# This code is contributed by 29AjayKumar
```

## C#

```cs
// C# Find the sum of all non-repeated  
// elements in an array  
using System; 
class GFG  
{  
  
    // Find the sum of all non-repeated elements  
    // in an array  
    static int findSum(int []arr, int n) 
    {  
        // sort all elements of array  
        Array.Sort(arr);  
          
        int sum = arr[0];  
        for (int i = 0; i < n - 1; i++)  
        {  
            if (arr[i] != arr[i + 1])  
            {  
                sum = sum + arr[i + 1];  
            }  
        }  
        return sum;  
    }  
  
    // Driver code  
    public static void Main() 
    {  
        int []arr = {1, 2, 3, 1, 1, 4, 5, 6};  
        int n = arr.Length;  
        Console.WriteLine(findSum(arr, n));  
    }  
}  
  
// This code is contributed by 29AjayKumar
```

输出：

```
21
```

时间复杂度：`O(n log n)`。

空间复杂度：`O(1)`。

此问题的有效解决方案是，使用`unordered_set`我们运行一个`for`循环，并且该值首次出现在其`add sum`变量中，并存储在哈希表中，下一次我们不使用该值。

## C++

```cpp
// C++ Find the sum of all non- repeated 
// elements in an array 
#include<bits/stdc++.h> 
using namespace std; 
  
// Find the sum of all non-repeated elements 
// in an array 
int findSum(int arr[],int n) 
{ 
    int sum = 0; 
  
    // Hash to store all element of array 
    unordered_set< int > s; 
    for (int i=0; i<n; i++) 
    { 
        if (s.find(arr[i]) == s.end()) 
        { 
            sum += arr[i]; 
            s.insert(arr[i]); 
        } 
    } 
  
    return sum; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = {1, 2, 3, 1, 1, 4, 5, 6}; 
    int n = sizeof(arr)/sizeof(int); 
    cout << findSum(arr, n); 
    return 0; 
}
```

## Java

```java
// Java Find the sum of all non- repeated  
// elements in an array  
import java.util.*; 
  
class GFG 
{ 
      
    // Find the sum of all non-repeated elements  
    // in an array  
    static int findSum(int arr[], int n) 
    { 
        int sum = 0; 
  
        // Hash to store all element of array  
        HashSet<Integer> s = new HashSet<Integer>(); 
        for (int i = 0; i < n; i++) 
        { 
            if (!s.contains(arr[i])) 
            { 
                sum += arr[i]; 
                s.add(arr[i]); 
            } 
        } 
        return sum; 
    } 
  
    // Driver code  
    public static void main(String[] args)  
    { 
        int arr[] = {1, 2, 3, 1, 1, 4, 5, 6}; 
        int n = arr.length; 
        System.out.println(findSum(arr, n)); 
    } 
}  
  
// This code is contributed by Rajput-Ji
```

## Python3

```py
# Python3 Find the sum of all  
# non- repeated elements in an array  
  
# Find the sum of all non-repeated 
# elements in an array 
def findSum(arr, n): 
    s = set() 
    sum = 0
  
    # Hash to store all element  
    # of array 
    for i in range(n): 
        if arr[i] not in s: 
            s.add(arr[i]) 
    for i in s: 
        sum = sum + i 
  
    return sum
  
# Driver code 
arr = [1, 2, 3, 1, 1, 4, 5, 6] 
n = len(arr) 
print(findSum(arr, n)) 
  
# This code is contributed by Shrikant13
```

## C#

```cs
// C# Find the sum of all non- repeated  
// elements in an array  
using System; 
using System.Collections.Generic; 
  
class GFG 
{ 
      
    // Find the sum of all non-repeated elements  
    // in an array  
    static int findSum(int []arr, int n) 
    { 
        int sum = 0; 
  
        // Hash to store all element of array  
        HashSet<int> s = new HashSet<int>(); 
        for (int i = 0; i < n; i++) 
        { 
            if (!s.Contains(arr[i])) 
            { 
                sum += arr[i]; 
                s.Add(arr[i]); 
            } 
        } 
        return sum; 
    } 
  
    // Driver code  
    public static void Main(String[] args)  
    { 
        int []arr = {1, 2, 3, 1, 1, 4, 5, 6}; 
        int n = arr.Length; 
        Console.WriteLine(findSum(arr, n)); 
    } 
} 
  
// This code is contributed by Rajput-Ji
```

输出：

```
21
```

时间复杂度：`O(n)`。

辅助空间：`O(n)`。