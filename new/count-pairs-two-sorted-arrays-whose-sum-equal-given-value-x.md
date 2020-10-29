# 计数两个总和等于给定值 x 的排序数组对

> 原文：[https://www.geeksforgeeks.org/count-pairs-two-sorted-arrays-whose-sum-equal-given-value-x/](https://www.geeksforgeeks.org/count-pairs-two-sorted-arrays-whose-sum-equal-given-value-x/)

给定两个大小分别为 **m** 和 **n** 的不同元素的排序数组。 给定值 **x** 。 问题是要计算两个数组的总和等于 **x** 的所有对。

**注意**：该对具有每个阵列中的一个元素。

**示例**：

```
Input : arr1[] = {1, 3, 5, 7}
        arr2[] = {2, 3, 5, 8}
        x = 10

Output : 2
The pairs are:
(5, 5) and (7, 3)

Input : arr1[] = {1, 2, 3, 4, 5, 7, 11} 
        arr2[] = {2, 3, 4, 5, 6, 8, 12} 
        x = 9

Output : 5

```

**方法 1（朴素方法）**：使用两个循环从两个数组中选取元素，并检查该对的总和是否等于 **x** 。

## C++

```cpp

// C++ implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 
#include <bits/stdc++.h> 
using namespace std; 

// function to count all pairs 
// from both the sorted arrays  
// whose sum is equal to a given 
// value 
int countPairs(int arr1[], int arr2[],  
               int m, int n, int x) 
{ 
    int count = 0; 

    // generating pairs from  
    // both the arrays 
    for (int i = 0; i < m; i++) 
        for (int j = 0; j < n; j++) 

            // if sum of pair is equal  
            // to 'x' increment count  
            if ((arr1[i] + arr2[j]) == x)  
                count++; 

    // required count of pairs      
    return count; 
} 

// Driver Code 
int main() 
{ 
    int arr1[] = {1, 3, 5, 7}; 
    int arr2[] = {2, 3, 5, 8}; 
    int m = sizeof(arr1) / sizeof(arr1[0]); 
    int n = sizeof(arr2) / sizeof(arr2[0]); 
    int x = 10; 
    cout << "Count = "
         << countPairs(arr1, arr2, m, n, x); 
    return 0;      
}  

```

## Java

```java

// Java implementation to count pairs from 
// both sorted arrays whose sum is equal 
// to a given value 
import java.io.*; 

class GFG { 

    // function to count all pairs 
    // from both the sorted arrays  
    // whose sum is equal to a given 
    // value 
    static int countPairs(int []arr1,  
             int []arr2, int m, int n, int x) 
    { 
        int count = 0; 

        // generating pairs from  
        // both the arrays 
        for (int i = 0; i < m; i++) 
            for (int j = 0; j < n; j++) 

                // if sum of pair is equal  
                // to 'x' increment count  
                if ((arr1[i] + arr2[j]) == x)  
                    count++; 

        // required count of pairs  
        return count; 
    } 

    // Driver Code 

    public static void main (String[] args) 
    { 
        int arr1[] = {1, 3, 5, 7}; 
        int arr2[] = {2, 3, 5, 8}; 
        int m = arr1.length; 
        int n = arr2.length; 
        int x = 10; 

        System.out.println( "Count = "
        + countPairs(arr1, arr2, m, n, x)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## Python3

```py

# python implementation to count 
# pairs from both sorted arrays  
# whose sum is equal to a given  
# value 

# function to count all pairs from 
# both the sorted arrays whose sum 
# is equal to a given value 
def countPairs(arr1, arr2, m, n, x): 
    count = 0

    # generating pairs from both 
    # the arrays 
    for i in range(m): 
        for j in range(n): 

            # if sum of pair is equal 
            # to 'x' increment count 
            if arr1[i] + arr2[j] == x: 
                count = count + 1

    # required count of pairs 
    return count 

# Driver Program 
arr1 = [1, 3, 5, 7] 
arr2 = [2, 3, 5, 8] 
m = len(arr1) 
n = len(arr2) 
x = 10
print("Count = ",  
        countPairs(arr1, arr2, m, n, x)) 

# This code is contributed by Shrikant13\. 

```

## C#

```cs

// C# implementation to count pairs from 
// both sorted arrays whose sum is equal 
// to a given value 
using System; 

class GFG { 

    // function to count all pairs 
    // from both the sorted arrays  
    // whose sum is equal to a given 
    // value 
    static int countPairs(int []arr1,  
            int []arr2, int m, int n, int x) 
    { 
        int count = 0; 

        // generating pairs from  
        // both the arrays 
        for (int i = 0; i < m; i++) 
            for (int j = 0; j < n; j++) 

                // if sum of pair is equal  
                // to 'x' increment count  
                if ((arr1[i] + arr2[j]) == x)  
                    count++; 

        // required count of pairs  
        return count; 
    } 

    // Driver Code 

    public static void Main () 
    { 
        int []arr1 = {1, 3, 5, 7}; 
        int []arr2 = {2, 3, 5, 8}; 
        int m = arr1.Length; 
        int n = arr2.Length; 
        int x = 10; 

        Console.WriteLine( "Count = "
        + countPairs(arr1, arr2, m, n, x)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## PHP

```php

<?php 
// PHP implementation to count 
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 

// function to count all pairs  
// from both the sorted arrays 
// whose sum is equal to a given 
// value 
function countPairs( $arr1, $arr2,  
                     $m, $n, $x) 
{ 
    $count = 0; 

    // generating pairs from 
    // both the arrays 
    for ( $i = 0; $i < $m; $i++) 
        for ( $j = 0; $j < $n; $j++) 

            // if sum of pair is equal  
            // to 'x' increment count  
            if (($arr1[$i] + $arr2[$j]) == $x)  
                $count++; 

    // required count of pairs  
    return $count; 
} 

// Driver Code 
$arr1 = array(1, 3, 5, 7); 
$arr2 = array(2, 3, 5, 8); 
$m = count($arr1); 
$n = count($arr2); 
$x = 10; 
echo "Count = ",  
      countPairs($arr1, $arr2,  
                   $m,$n, $x); 

// This code is contributed by anuj_67\. 
?> 

```

**Output :**

```
Count = 2

```

**时间复杂度**：`O(mn)`

**辅助空间**：`O(1)`

**方法 2（二进制搜索）**：对于每个元素 **arr1 [i]** ，其中 **1 < = i < = m** ，搜索值[ **arr2 []** 中的**（x – arr1 [i]）**。 如果搜索成功，则增加**计数**。

## C++

```cpp

// C++ implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given 
// value 
#include <bits/stdc++.h> 
using namespace std; 

// function to search 'value'  
// in the given array 'arr[]'  
// it uses binary search technique  
// as  'arr[]' is sorted  
bool isPresent(int arr[], int low, 
               int high, int value) 
{ 
    while (low <= high) 
    { 
        int mid = (low + high) / 2; 

        // value found 
        if (arr[mid] == value) 
            return true;      

        else if (arr[mid] > value)  
            high = mid - 1; 
        else
            low = mid + 1;  
    } 

    // value not found 
    return false; 
} 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given 
// value 
int countPairs(int arr1[], int arr2[], 
               int m, int n, int x) 
{ 
    int count = 0;      
    for (int i = 0; i < m; i++) 
    { 
        // for each arr1[i] 
        int value = x - arr1[i]; 

        // check if the 'value' 
        // is present in 'arr2[]' 
        if (isPresent(arr2, 0, n - 1, value)) 
            count++; 
    } 

    // required count of pairs      
    return count; 
} 

// Driver Code 
int main() 
{ 
    int arr1[] = {1, 3, 5, 7}; 
    int arr2[] = {2, 3, 5, 8}; 
    int m = sizeof(arr1) / sizeof(arr1[0]); 
    int n = sizeof(arr2) / sizeof(arr2[0]); 
    int x = 10; 
    cout << "Count = "
         << countPairs(arr1, arr2, m, n, x); 
    return 0;      
} 

```

## Java

```java

// Java implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given 
// value 
import java.io.*; 
class GFG { 

// function to search 'value'  
// in the given array 'arr[]'  
// it uses binary search technique  
// as 'arr[]' is sorted  
static boolean isPresent(int arr[], int low, 
                         int high, int value) 
{ 
    while (low <= high) 
    { 
        int mid = (low + high) / 2; 

        // value found 
        if (arr[mid] == value) 
            return true;      

        else if (arr[mid] > value)  
            high = mid - 1; 
        else
            low = mid + 1;  
    } 

    // value not found 
    return false; 
} 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given 
// value 
static int countPairs(int arr1[], int arr2[], 
                      int m, int n, int x) 
{ 
    int count = 0;  
    for (int i = 0; i < m; i++) 
    { 

        // for each arr1[i] 
        int value = x - arr1[i]; 

        // check if the 'value' 
        // is present in 'arr2[]' 
        if (isPresent(arr2, 0, n - 1, value)) 
            count++; 
    } 

    // required count of pairs  
    return count; 
} 

    // Driver Code 
    public static void main (String[] args)  
    { 
        int arr1[] = {1, 3, 5, 7}; 
        int arr2[] = {2, 3, 5, 8}; 
        int m = arr1.length; 
        int n = arr2.length; 
        int x = 10; 
        System.out.println("Count = "
              + countPairs(arr1, arr2, m, n, x)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## Python 3

```

# Python 3 implementation to count  
# pairs from both sorted arrays  
# whose sum is equal to a given 
# value 

# function to search 'value'  
# in the given array 'arr[]'  
# it uses binary search technique  
# as 'arr[]' is sorted  
def isPresent(arr, low, high, value): 

    while (low <= high): 

        mid = (low + high) // 2

        # value found 
        if (arr[mid] == value): 
            return True

        elif (arr[mid] > value) : 
            high = mid - 1
        else: 
            low = mid + 1

    # value not found 
    return False

# function to count all pairs  
# from both the sorted arrays  
# whose sum is equal to a given 
# value 
def countPairs(arr1, arr2, m, n, x): 
    count = 0
    for i in range(m): 
        # for each arr1[i] 
        value = x - arr1[i] 

        # check if the 'value' 
        # is present in 'arr2[]' 
        if (isPresent(arr2, 0, n - 1, value)): 
            count += 1

    # required count of pairs      
    return count 

# Driver Code 
if __name__ == "__main__": 
    arr1 = [1, 3, 5, 7] 
    arr2 = [2, 3, 5, 8] 
    m = len(arr1) 
    n = len(arr2) 
    x = 10
    print("Count = ", 
           countPairs(arr1, arr2, m, n, x)) 

# This code is contributed  
# by ChitraNayal 

```

## C#

```cs

// C# implementation to count pairs from both  
// sorted arrays whose sum is equal to a given 
// value 
using System; 

class GFG { 

    // function to search 'value' in the given 
    // array 'arr[]' it uses binary search  
    // technique as 'arr[]' is sorted  
    static bool isPresent(int []arr, int low, 
                         int high, int value) 
    { 
        while (low <= high) 
        { 
            int mid = (low + high) / 2; 

            // value found 
            if (arr[mid] == value) 
                return true;      

            else if (arr[mid] > value)  
                high = mid - 1; 
            else
                low = mid + 1;  
        } 

        // value not found 
        return false; 
    } 

    // function to count all pairs  
    // from both the sorted arrays  
    // whose sum is equal to a given 
    // value 
    static int countPairs(int []arr1, int []arr2, 
                             int m, int n, int x) 
    { 
        int count = 0;  

        for (int i = 0; i < m; i++) 
        { 

            // for each arr1[i] 
            int value = x - arr1[i]; 

            // check if the 'value' 
            // is present in 'arr2[]' 
            if (isPresent(arr2, 0, n - 1, value)) 
                count++; 
        } 

        // required count of pairs  
        return count; 
    } 

    // Driver Code 
    public static void Main ()  
    { 
        int []arr1 = {1, 3, 5, 7}; 
        int []arr2 = {2, 3, 5, 8}; 
        int m = arr1.Length; 
        int n = arr2.Length; 
        int x = 10; 
        Console.WriteLine("Count = "
            + countPairs(arr1, arr2, m, n, x)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## PHP

```php

<?php 
// PHP implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given 
// value 

// function to search 'value'  
// in the given array 'arr[]'  
// it uses binary search technique  
// as 'arr[]' is sorted  
function isPresent($arr, $low, 
                   $high, $value) 
{ 
    while ($low <= $high) 
    { 
        $mid = ($low + $high) / 2; 

        // value found 
        if ($arr[$mid] == $value) 
            return true;      

        else if ($arr[$mid] > $value)  
            $high = $mid - 1; 
        else
            $low = $mid + 1;  
    } 

    // value not found 
    return false; 
} 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given 
// value 
function countPairs($arr1, $arr2, 
                    $m, $n, $x) 
{ 
    $count = 0;  
    for ($i = 0; $i < $m; $i++) 
    { 

        // for each arr1[i] 
        $value = $x - $arr1[$i]; 

        // check if the 'value' 
        // is present in 'arr2[]' 
        if (isPresent($arr2, 0,  
                      $n - 1, $value)) 
            $count++; 
    } 

    // required count of pairs  
    return $count; 
} 

    // Driver Code 
    $arr1 = array(1, 3, 5, 7); 
    $arr2 = array(2, 3, 5, 8); 
    $m = count($arr1); 
    $n = count($arr2); 
    $x = 10; 
    echo "Count = "
        , countPairs($arr1, $arr2, $m, $n, $x); 

// This code is contributed by anuj_67\. 
?> 

```

**Output :**

```
Count = 2

```

**时间复杂度**：O（mlogn），应在更大大小的数组上进行搜索，以减少时间复杂度。

**辅助空间**：`O(1)`

**方法 3（哈希）**：哈希表是使用 C++ 中的 [unordered_set 实现的。 我们将所有第一个数组元素存储在哈希表中。 对于第二个数组的元素，我们从 **x** 中减去每个元素，然后在哈希表中检查结果。 如果结果存在，我们将增加**计数**。](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)

## C++

```cpp

// C++ implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 
#include <bits/stdc++.h> 
using namespace std; 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given 
// value 
int countPairs(int arr1[], int arr2[],  
               int m, int n, int x) 
{ 
    int count = 0; 

    unordered_set<int> us; 

    // insert all the elements  
    // of 1st array in the hash 
    // table(unordered_set 'us') 
    for (int i = 0; i < m; i++) 
        us.insert(arr1[i]); 

    // for each element of 'arr2[]  
    for (int j = 0; j < n; j++)  

        // find (x - arr2[j]) in 'us' 
        if (us.find(x - arr2[j]) != us.end()) 
            count++; 

    // required count of pairs      
    return count; 
} 

// Driver Code 
int main() 
{ 
    int arr1[] = {1, 3, 5, 7}; 
    int arr2[] = {2, 3, 5, 8}; 
    int m = sizeof(arr1) / sizeof(arr1[0]); 
    int n = sizeof(arr2) / sizeof(arr2[0]); 
    int x = 10; 
    cout << "Count = "
         << countPairs(arr1, arr2, m, n, x); 
    return 0;      
} 

```

## Java

```java

import java.util.*; 
// Java implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 

class GFG 
{ 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given  
// value  
static int countPairs(int arr1[], int arr2[],  
            int m, int n, int x)  
{  
    int count = 0;  

    HashSet<Integer> us = new HashSet<Integer>(); 

    // insert all the elements  
    // of 1st array in the hash  
    // table(unordered_set 'us')  
    for (int i = 0; i < m; i++)  
        us.add(arr1[i]);  

    // for each element of 'arr2[]  
    for (int j = 0; j < n; j++)  

        // find (x - arr2[j]) in 'us'  
        if (us.contains(x - arr2[j]))  
            count++;  

    // required count of pairs  
    return count;  
}  

// Driver Code  
public static void main(String[] args) 
{ 
    int arr1[] = {1, 3, 5, 7};  
    int arr2[] = {2, 3, 5, 8};  
    int m = arr1.length;  
    int n = arr2.length;  
    int x = 10;  
    System.out.print("Count = "
        + countPairs(arr1, arr2, m, n, x)); 
} 
} 

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation to count  
# pairs from both sorted arrays  
# whose sum is equal to a given value  

# function to count all pairs from   
# both the sorted arrays whose sum 
# is equal to a given value  
def countPairs(arr1, arr2, m, n, x): 
    count = 0
    us = set() 

    # insert all the elements  
    # of 1st array in the hash  
    # table(unordered_set 'us')  
    for i in range(m): 
        us.add(arr1[i]) 

    # or each element of 'arr2[]  
    for j in range(n): 

        # find (x - arr2[j]) in 'us'  
        if x - arr2[j] in us: 
            count += 1

    # required count of pairs 
    return count 

# Driver code 
arr1 = [1, 3, 5, 7] 
arr2 = [2, 3, 5, 8] 
m = len(arr1) 
n = len(arr2) 
x = 10
print("Count =",  
       countPairs(arr1, arr2, m, n, x)) 

# This code is contributed by Shrikant13 

```

## C#

```cs

// C# implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given  
// value  
static int countPairs(int []arr1, int []arr2,  
            int m, int n, int x)  
{  
    int count = 0;  

    HashSet<int> us = new HashSet<int>(); 

    // insert all the elements  
    // of 1st array in the hash  
    // table(unordered_set 'us')  
    for (int i = 0; i < m; i++)  
        us.Add(arr1[i]);  

    // for each element of 'arr2[]  
    for (int j = 0; j < n; j++)  

        // find (x - arr2[j]) in 'us'  
        if(us.Contains(x - arr2[j]))  
            count++;  

    // required count of pairs  
    return count;  
}  

// Driver Code  
public static void Main(String[] args) 
{ 
    int []arr1 = {1, 3, 5, 7};  
    int []arr2 = {2, 3, 5, 8};  
    int m = arr1.Length;  
    int n = arr2.Length;  
    int x = 10;  
    Console.Write("Count = "
        + countPairs(arr1, arr2, m, n, x)); 
} 
} 

// This code contributed by Rajput-Ji 

```

**Output :**

```
Count = 2

```

**时间复杂度**：`O(m + n)`

**辅助空间**：O（m），应创建具有较小大小的数组的哈希表，以降低空间复杂度 。

**方法 4（有效方法）**：此方法使用两个指针的概念，一个指针从左到右遍历第一个数组，另一个指针从右到左遍历第二个数组。

**算法**：

```
countPairs(arr1, arr2, m, n, x)

     Initialize l = 0, r = n - 1
     Initialize count = 0

     loop while l = 0
        if (arr1[l] + arr2[r]) == x
           l++, r--
           count++
        else if (arr1[l] + arr2[r]) < x
           l++
        else
           r--

     return count 

```

## C++

```cpp

// C++ implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 
#include <bits/stdc++.h> 
using namespace std; 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given  
// value 
int countPairs(int arr1[], int arr2[],  
               int m, int n, int x) 
{ 
    int count = 0;  
    int l = 0, r = n - 1; 

    // traverse 'arr1[]' from  
    // left to right 
    // traverse 'arr2[]' from  
    // right to left 
    while (l < m && r >= 0) 
    { 
        // if this sum is equal  
        // to 'x', then increment 'l',  
        // decrement 'r' and 
        // increment 'count' 
        if ((arr1[l] + arr2[r]) == x) 
        { 
            l++; r--; 
            count++;          
        } 

        // if this sum is less  
        // than x, then increment l 
        else if ((arr1[l] + arr2[r]) < x) 
            l++; 

        // else decrement 'r'  
        else
            r--;  
    } 

    // required count of pairs      
    return count; 
} 

// Driver Code 
int main() 
{ 
    int arr1[] = {1, 3, 5, 7}; 
    int arr2[] = {2, 3, 5, 8}; 
    int m = sizeof(arr1) / sizeof(arr1[0]); 
    int n = sizeof(arr2) / sizeof(arr2[0]); 
    int x = 10; 
    cout << "Count = "
          << countPairs(arr1, arr2, m, n, x); 
    return 0;      
} 

```

## Java

```java

// Java implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 
import java.io.*; 

class GFG { 

    // function to count all pairs  
    // from both the sorted arrays  
    // whose sum is equal to a given  
    // value 
    static int countPairs(int arr1[],  
         int arr2[], int m, int n, int x) 
    { 
        int count = 0;  
        int l = 0, r = n - 1; 

        // traverse 'arr1[]' from  
        // left to right 
        // traverse 'arr2[]' from  
        // right to left 
        while (l < m && r >= 0) 
        { 

            // if this sum is equal  
            // to 'x', then increment 'l',  
            // decrement 'r' and 
            // increment 'count' 
            if ((arr1[l] + arr2[r]) == x) 
            { 
                l++; r--; 
                count++;          
            } 

            // if this sum is less  
            // than x, then increment l 
            else if ((arr1[l] + arr2[r]) < x) 
                l++; 

            // else decrement 'r'  
            else
                r--;  
        } 

        // required count of pairs  
        return count; 
    } 

    // Driver Code 
    public static void main (String[] args)  
    { 
        int arr1[] = {1, 3, 5, 7}; 
        int arr2[] = {2, 3, 5, 8}; 
        int m = arr1.length; 
        int n = arr2.length; 
        int x = 10; 
        System.out.println( "Count = "
         + countPairs(arr1, arr2, m, n, x)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## Python3

```py

# Python 3 implementation to count 
# pairs from both sorted arrays 
# whose sum is equal to a given 
# value 

# function to count all pairs 
# from both the sorted arrays 
# whose sum is equal to a given 
# value 
def countPairs(arr1, arr2, m, n, x): 
    count, l, r = 0, 0, n - 1

    # traverse 'arr1[]' from 
    # left to right 
    # traverse 'arr2[]' from 
    # right to left 
    while (l < m and r >= 0): 

        # if this sum is equal 
        # to 'x', then increment 'l', 
        # decrement 'r' and 
        # increment 'count' 
        if ((arr1[l] + arr2[r]) == x): 
            l += 1
            r -= 1
            count += 1

        # if this sum is less 
        # than x, then increment l 
        elif ((arr1[l] + arr2[r]) < x): 
            l += 1

        # else decrement 'r' 
        else: 
            r -= 1

    # required count of pairs 
    return count 

# Driver Code 
if __name__ == '__main__': 
    arr1 = [1, 3, 5, 7] 
    arr2 = [2, 3, 5, 8] 
    m = len(arr1) 
    n = len(arr2) 
    x = 10
    print("Count =", 
            countPairs(arr1, arr2, 
                          m, n, x)) 

# This code is contributed  
# by PrinciRaj19992 

```

## C#

```cs

// C# implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 
using System; 

class GFG { 

    // function to count all pairs  
    // from both the sorted arrays  
    // whose sum is equal to a given  
    // value 
    static int countPairs(int []arr1,  
        int []arr2, int m, int n, int x) 
    { 
        int count = 0;  
        int l = 0, r = n - 1; 

        // traverse 'arr1[]' from  
        // left to right 
        // traverse 'arr2[]' from  
        // right to left 
        while (l < m && r >= 0) 
        { 

            // if this sum is equal  
            // to 'x', then increment 'l',  
            // decrement 'r' and 
            // increment 'count' 
            if ((arr1[l] + arr2[r]) == x) 
            { 
                l++; r--; 
                count++;          
            } 

            // if this sum is less  
            // than x, then increment l 
            else if ((arr1[l] + arr2[r]) < x) 
                l++; 

            // else decrement 'r'  
            else
                r--;  
        } 

        // required count of pairs  
        return count; 
    } 

    // Driver Code 
    public static void Main ()  
    { 
        int []arr1 = {1, 3, 5, 7}; 
        int []arr2 = {2, 3, 5, 8}; 
        int m = arr1.Length; 
        int n = arr2.Length; 
        int x = 10; 
        Console.WriteLine( "Count = "
        + countPairs(arr1, arr2, m, n, x)); 
    } 
} 

// This code is contributed by anuj_67\. 

```

## PHP

```php

<?php 
// PHP implementation to count  
// pairs from both sorted arrays  
// whose sum is equal to a given  
// value 

// function to count all pairs  
// from both the sorted arrays  
// whose sum is equal to a given  
// value 
function  countPairs( $arr1,  $arr2,  
          $m,  $n,  $x) 
{ 
     $count = 0;  
     $l = 0; $r = $n - 1; 

    // traverse 'arr1[]' from  
    // left to right 
    // traverse 'arr2[]' from  
    // right to left 
    while ($l < $m and $r >= 0) 
    { 
        // if this sum is equal  
        // to 'x', then increment 'l',  
        // decrement 'r' and 
        // increment 'count' 
        if (($arr1[$l] + $arr2[$r]) == $x) 
        { 
            $l++; $r--; 
            $count++;          
        } 

        // if this sum is less  
        // than x, then increment l 
        else if (($arr1[$l] + $arr2[$r]) < $x) 
            $l++; 

        // else decrement 'r'  
        else
            $r--;  
    } 

    // required count of pairs      
    return $count; 
} 

// Driver Code 
     $arr1 = array(1, 3, 5, 7); 
     $arr2 = array(2, 3, 5, 8); 
     $m = count($arr1); 
     $n = count($arr2); 
     $x = 10; 
     echo "Count = "
    , countPairs($arr1, $arr2, $m, $n, $x); 
// This code is contributed by anuj_67 

?> 

```

**Output :**

```
Count = 2

```

**时间复杂度**：`O(m + n)`

**辅助空间**：`O(1)`

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

