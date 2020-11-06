# 最小数组元素更改以使其元素 1 到 N

> 原文：[https://www.geeksforgeeks.org/minimum-array-element-changes-to-make-its-elements-1-to-n/](https://www.geeksforgeeks.org/minimum-array-element-changes-to-make-its-elements-1-to-n/)

假设给定一个数组，该数组包含 N 个具有任何整数值的元素。 您需要找到必须更改的最小元质数，以便数组具有 1 到 N（包括 1，N）之间的所有整数值。

**示例**：

```
Input : arr[] = {1 4 5 3 7}
Output : 1
We need to replace 7 with 2 to satisfy
condition hence minimum changes is 1.

Input : arr[] = {8 55 22 1 3 22 4 5}
Output :3

```

我们将所有元素插入哈希表中。 然后，我们从 1 迭代到 N，并检查哈希表中是否存在该元素。 如果不存在，则增加计数。 count 的最终值将是所需的最小更改。

## C++

```cpp

// Count minimum changes to make array 
// from 1 to n 
#include <bits/stdc++.h> 
using namespace std; 

int countChanges(int arr[], int n) 
{ 
    // it will contain all initial elements  
    // of array for log(n) complexity searching 
    unordered_set<int> s; 

    // Inserting all elements in a hash table 
    for (int i = 0; i < n; i++)  
        s.insert(arr[i]); 

    // Finding elements to be changed 
    int count = 0; 
    for (int i = 1; i <= n; i++)  
        if (s.find(i) == s.end()) 
            count++; 

    return count; 
} 

int main() 
{ 
    int arr[] = {8, 55, 22, 1, 3, 22, 4, 5}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << countChanges(arr, n); 
    return 0; 
} 

```

## Java

```java

// Count minimum changes to  
// make array from 1 to n  
import java.util.Set; 
import java.util.HashSet; 

class GfG 
{ 

    static int countChanges(int arr[], int n)  
    {  
        // It will contain all initial elements  
        // of array for log(n) complexity searching  
        Set<Integer> s = new HashSet<>();  

        // Inserting all elements in a hash table  
        for (int i = 0; i < n; i++)  
            s.add(arr[i]);  

        // Finding elements to be changed  
        int count = 0;  
        for (int i = 1; i <= n; i++)  
            if (!s.contains(i))  
                count++;  

        return count;  
    }  

    // Driver code 
    public static void main(String []args) 
    { 

        int arr[] = {8, 55, 22, 1, 3, 22, 4, 5};  
        int n = arr.length;  

        System.out.println(countChanges(arr, n)); 
    } 
} 

// This code is contributed by Rituraj Jain 

```

## Python 3

```

# Count minimum changes to  
# make array from 1 to n 

def countChanges(arr, n): 

    # it will contain all initial  
    # elements of array for log(n) 
    # complexity searching 
    s = [] 

    # Inserting all elements in a list 
    for i in range(n):  
        s.append(arr[i]) 

    # Finding elements to be changed 
    count = 0
    for i in range(1, n + 1) : 
        if i not in s: 
            count += 1

    return count 

# Driver Code 
if __name__ == "__main__": 
    arr = [8, 55, 22, 1, 3, 22, 4, 5] 
    n = len(arr) 
    print(countChanges(arr, n)) 

# This code is contributed  
# by ChitraNayal 

```

## C#

```cs

// C# program to Count minimum changes to  
// make array from 1 to n  
using System; 
using System.Collections.Generic; 

class GfG 
{ 

    static int countChanges(int []arr, int n)  
    {  
        // It will contain all initial elements  
        // of array for log(n) complexity searching  
        HashSet<int> s = new HashSet<int>();  

        // Inserting all elements in a hash table  
        for (int i = 0; i < n; i++)  
            s.Add(arr[i]);  

        // Finding elements to be changed  
        int count = 0;  
        for (int i = 1; i <= n; i++)  
            if (!s.Contains(i))  
                count++;  

        return count;  
    }  

    // Driver code 
    public static void Main(String []args) 
    { 
        int []arr = {8, 55, 22, 1, 3, 22, 4, 5};  
        int n = arr.Length;  
        Console.WriteLine(countChanges(arr, n)); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

## PHP

```php

<?php  
// Count minimum changes to  
// make array from 1 to n 

function countChanges(&$arr, $n) 
{ 
    // it will contain all initial  
    // elements of array for log(n)  
    // complexity searching 
    $s = array(); 

    // Inserting all elements  
    // in an array 
    for ($i = 0; $i < $n; $i++)  
        array_push($s, $arr[$i]); 

    // Finding elements to be changed 
    $count = 0; 
    for ($i = 1; $i <= $n; $i++)  
        if (!in_array($i, $s)) 
            $count++; 

    return $count; 
} 

// Driver Code 
$arr = array(8, 55, 22, 1, 3, 22, 4, 5); 
$n = sizeof($arr); 
echo countChanges($arr, $n); 

// This code is contributed  
// by ChitraNayal 
?> 

```

**Output:**

```
3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



