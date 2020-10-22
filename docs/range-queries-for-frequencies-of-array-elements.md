# 数组元素的频率范围查询

> 原文： [https://www.geeksforgeeks.org/range-queries-for-frequencies-of-array-elements/](https://www.geeksforgeeks.org/range-queries-for-frequencies-of-array-elements/)

给定`n`个非负整数的数组。 任务是在`array[]`的任意范围内查找特定元素的频率。 范围以数组中的位置（不是基于 0 的索引）的形式给出。 可以有多个给定类型的查询。

**示例**：

```
Input  : arr[] = {2, 8, 6, 9, 8, 6, 8, 2, 11};
         left = 2, right = 8, element = 8
         left = 2, right = 5, element = 6      
Output : 3
         1
The element 8 appears 3 times in arr[left-1..right-1]
The element 6 appears 1 time in arr[left-1..right-1]

```

**朴素的方法**：是从左到右遍历并在找到元素时更新计数变量。

以下是朴素方法的代码：-

## C++ 

```cpp

// C++ program to find total count of an element 
// in a range 
#include<bits/stdc++.h> 
using namespace std; 

// Returns count of element in arr[left-1..right-1] 
int findFrequency(int arr[], int n, int left, 
                         int right, int element) 
{ 
    int count = 0; 
    for (int i=left-1; i<=right; ++i) 
        if (arr[i] == element) 
            ++count; 
    return count; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {2, 8, 6, 9, 8, 6, 8, 2, 11}; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // Print frequency of 2 from position 1 to 6 
    cout << "Frequency of 2 from 1 to 6 = "
         << findFrequency(arr, n, 1, 6, 2) << endl; 

    // Print frequency of 8 from position 4 to 9 
    cout << "Frequency of 8 from 4 to 9 = "
         << findFrequency(arr, n, 4, 9, 8); 

    return 0; 
} 

```

## Java

```java
// JAVA Code to find total count of an element 
// in a range 
  
class GFG { 
      
    // Returns count of element in arr[left-1..right-1] 
    public static int findFrequency(int arr[], int n,  
                                int left, int right, 
                                      int element) 
    { 
        int count = 0; 
        for (int i = left - 1; i < right; ++i) 
            if (arr[i] == element) 
                ++count; 
        return count; 
    } 
      
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int arr[] = {2, 8, 6, 9, 8, 6, 8, 2, 11}; 
        int n = arr.length; 
       
        // Print frequency of 2 from position 1 to 6 
        System.out.println("Frequency of 2 from 1 to 6 = " + 
             findFrequency(arr, n, 1, 6, 2)); 
       
        // Print frequency of 8 from position 4 to 9 
        System.out.println("Frequency of 8 from 4 to 9 = " + 
             findFrequency(arr, n, 4, 9, 8)); 
          
    } 
  }  
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python program to find total   
# count of an element in a range 
  
# Returns count of element 
# in arr[left-1..right-1] 
def findFrequency(arr, n, left, right, element): 
  
    count = 0
    for i in range(left - 1, right): 
        if (arr[i] == element): 
            count += 1
    return count 
  
  
# Driver Code 
arr = [2, 8, 6, 9, 8, 6, 8, 2, 11] 
n = len(arr) 
  
# Print frequency of 2 from position 1 to 6 
print("Frequency of 2 from 1 to 6 = ", 
        findFrequency(arr, n, 1, 6, 2)) 
  
# Print frequency of 8 from position 4 to 9 
print("Frequency of 8 from 4 to 9 = ", 
        findFrequency(arr, n, 4, 9, 8)) 
          
      
# This code is contributed by Anant Agarwal.
```

## C#

```cs
// C# Code to find total count  
// of an element in a range 
using System; 
  
class GFG { 
      
    // Returns count of element  
    // in arr[left-1..right-1] 
    public static int findFrequency(int []arr, int n,  
                                    int left, int right, 
                                    int element) 
    { 
        int count = 0; 
        for (int i = left - 1; i < right; ++i) 
            if (arr[i] == element) 
                ++count; 
        return count; 
    } 
      
    // Driver Code 
    public static void Main()  
    { 
        int []arr = {2, 8, 6, 9, 8, 6, 8, 2, 11}; 
        int n = arr.Length; 
      
        // Print frequency of 2  
        // from position 1 to 6 
        Console.WriteLine("Frequency of 2 from 1 to 6 = " + 
                            findFrequency(arr, n, 1, 6, 2)); 
      
        // Print frequency of 8  
        // from position 4 to 9 
        Console.Write("Frequency of 8 from 4 to 9 = " + 
                       findFrequency(arr, n, 4, 9, 8)); 
          
    } 
}  
  
// This code is contributed by Nitin Mittal.
```

## PHP

```php
<?php 
// PHP program to find total count of  
// an element in a range 
  
// Returns count of element in  
// arr[left-1..right-1] 
function findFrequency(&$arr, $n, $left, 
                        $right, $element) 
{ 
    $count = 0; 
    for ($i = $left - 1; $i <= $right; ++$i) 
        if ($arr[$i] == $element) 
            ++$count; 
    return $count; 
} 
  
// Driver Code 
$arr = array(2, 8, 6, 9, 8, 6, 8, 2, 11); 
$n = sizeof($arr); 
  
// Print frequency of 2 from position 1 to 6 
echo "Frequency of 2 from 1 to 6 = ".  
      findFrequency($arr, $n, 1, 6, 2) ."\n"; 
  
// Print frequency of 8 from position 4 to 9 
echo "Frequency of 8 from 4 to 9 = ".  
      findFrequency($arr, $n, 4, 9, 8); 
  
// This code is contributed by ita_c 
?>
```

输出：

```
 Frequency of 2 from 1 to 6 = 1
 Frequency of 8 from 4 to 9 = 2
```

这种方法的时间复杂度是`O(right - left + 1)`或`O(n)`。

辅助空间：`O(1)`。

一种有效的方法是使用哈希。 在 C 语言中，我们可以使用`unordered_map`

1.  首先，我们将位置存储在每个不同元素的`map[]`中，作为向量：

    ```
    int arr[] = {2, 8, 6, 9, 8, 6, 8, 2, 11};
    map[2] = {1, 8}
    map[8] = {2, 5, 7}
    map[6] = {3, 6} 
    ans so on...
    ```

2.  如我们所见，`map[]`中的元素已经按顺序排序（因为我们从左到右插入了元素），答案归结为使用类似二进制搜索的方法在该`map[]`中找到总数。
3.  在 C++ 中，我们可以使用`Lower_bound`，它会返回一个迭代器，该迭代器指向`[first, last]`范围内的第一个元素，该元素的值不少于`left`。 和`upper_bound`返回一个迭代器，该迭代器指向`[first, last)`范围内的第一个元素，该元素的值大于`right`。
4.  之后，我们只需要减去`upper_bound()`和`lower_bound()`结果即可得到最终答案。 例如，假设我们要在`[1, 6]`的范围内找到8的总数，那么`lower_bound()`函数的`map[8]`将返回结果 0（指向 2），而`upper_bound()`将返回 2（指向 7），因此我们需要将两个结果相减，例如`2 – 0 = 2`。

下面是上述方法的代码：

## C++

```cpp
// C++ program to find total count of an element 
#include<bits/stdc++.h> 
using namespace std; 
  
unordered_map< int, vector<int> > store; 
  
// Returns frequency of element in arr[left-1..right-1] 
int findFrequency(int arr[], int n, int left, 
                      int right, int element) 
{ 
    // Find the position of first occurrence of element 
    int a = lower_bound(store[element].begin(), 
                        store[element].end(), 
                        left) 
            - store[element].begin(); 
  
    // Find the position of last occurrence of element 
    int b = upper_bound(store[element].begin(), 
                        store[element].end(), 
                        right) 
            - store[element].begin(); 
  
    return b-a; 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = {2, 8, 6, 9, 8, 6, 8, 2, 11}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
  
    // Storing the indexes of an element in the map 
    for (int i=0; i<n; ++i) 
        store[arr[i]].push_back(i+1); //starting index from 1 
  
    // Print frequency of 2 from position 1 to 6 
    cout << "Frequency of 2 from 1 to 6 = "
         << findFrequency(arr, n, 1, 6, 2) <<endl; 
  
    // Print frequency of 8 from position 4 to 9 
    cout << "Frequency of 8 from 4 to 9 = "
         << findFrequency(arr, n, 4, 9, 8); 
  
    return 0; 
}
```

## Python3

```py
# Python3 program to find total count of an element 
from collections import defaultdict as dict
from bisect import bisect_left as lower_bound 
from bisect import bisect_right as upper_bound 
  
store = dict(list) 
  
# Returns frequency of element  
# in arr[left-1..right-1] 
def findFrequency(arr, n, left, right, element): 
      
    # Find the position of  
    # first occurrence of element 
    a = lower_bound(store[element], left) 
  
    # Find the position of 
    # last occurrence of element 
    b = upper_bound(store[element], right) 
  
    return b - a 
  
# Driver code 
arr = [2, 8, 6, 9, 8, 6, 8, 2, 11] 
n = len(arr) 
  
# Storing the indexes of 
# an element in the map 
for i in range(n): 
    store[arr[i]].append(i + 1) 
  
# Prfrequency of 2 from position 1 to 6 
print("Frequency of 2 from 1 to 6 = ",  
       findFrequency(arr, n, 1, 6, 2)) 
  
# Prfrequency of 8 from position 4 to 9 
print("Frequency of 8 from 4 to 9 = ", 
       findFrequency(arr, n, 4, 9, 8)) 
  
# This code is contributed by Mohit Kumar
```

输出：

```
Frequency of 2 from 1 to 6 = 1
Frequency of 8 from 4 to 9 = 2
```

如果我们有大量任意范围的查询，询问特定元素的总频率，则此方法将是有益的。

时间复杂度：单个查询为`O(log N)`。