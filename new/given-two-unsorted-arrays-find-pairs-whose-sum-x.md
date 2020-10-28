# 给定两个未排序的数组，找到总和为 x 的所有对。

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)

给定两个不同元素的未排序数组，任务是从两个数组中找到总和等于 **X** 的所有对。

**示例**：

```
Input :  arr1[] = {-1, -2, 4, -6, 5, 7}
         arr2[] = {6, 3, 4, 0}  
         x = 8
Output : 4 4
         5 3

Input : arr1[] = {1, 2, 4, 5, 7} 
        arr2[] = {5, 6, 3, 4, 8}  
        x = 9
Output : 1 8
         4 5
         5 4

```

**在**中问：[亚马逊](https://www.geeksforgeeks.org/tag/amazon/)

**天真的方法**是简单地运行两个循环并从两个数组中选择元素。 逐一检查两个元素的总和是否等于给定值 x。

## C++

```cpp

// C++ program to find all pairs in both arrays 
// whose sum is equal to given value x 
#include <bits/stdc++.h> 

using namespace std; 

// Function to print all pairs in both arrays 
// whose sum is equal to given value x 
void findPairs(int arr1[], int arr2[], int n, 
               int m, int x) 
{ 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < m; j++) 
            if (arr1[i] + arr2[j] == x) 
                cout << arr1[i] << " "
                     << arr2[j] << endl; 
} 

// Driver code 
int main() 
{ 
    int arr1[] = { 1, 2, 3, 7, 5, 4 }; 
    int arr2[] = { 0, 7, 4, 3, 2, 1 }; 
    int n = sizeof(arr1) / sizeof(int); 
    int m = sizeof(arr2) / sizeof(int); 
    int x = 8; 
    findPairs(arr1, arr2, n, m, x); 
    return 0; 
} 

```

## Java

```java

// Java program to find all pairs in both arrays 
// whose sum is equal to given value x 
import java.io.*; 

class GFG { 

    // Function to print all pairs in both arrays 
    // whose sum is equal to given value x 
    static void findPairs(int arr1[], int arr2[], int n, 
                          int m, int x) 
    { 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < m; j++) 
                if (arr1[i] + arr2[j] == x) 
                    System.out.println(arr1[i] + " "
                                       + arr2[j]); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr1[] = { 1, 2, 3, 7, 5, 4 }; 
        int arr2[] = { 0, 7, 4, 3, 2, 1 }; 
        int x = 8; 
        findPairs(arr1, arr2, arr1.length, arr2.length, x); 
    } 
} 

// This code is contributed 
// by sunnysingh 

```

## Python3

```py

# Python 3 program to find all  

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# pairs in both arrays whose  

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# sum is equal to given value x 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)

# Function to print all pairs  

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# in both arrays whose sum is 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# equal to given value x 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
def findPairs(arr1, arr2, n, m, x): 

    for i in range(0, n): 
        for j in range(0, m): 
            if (arr1[i] + arr2[j] == x): 
                print(arr1[i], arr2[j]) 

# Driver code 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
arr1 = [1, 2, 3, 7, 5, 4] 
arr2 = [0, 7, 4, 3, 2, 1] 
n = len(arr1) 
m = len(arr2) 
x = 8
findPairs(arr1, arr2, n, m, x) 

# This code is contributed by Smitha Dinesh Semwal 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)

```

## C#

```cs

// C# program to find all 
// pairs in both arrays 
// whose sum is equal to 
// given value x 
using System; 

class GFG { 

    // Function to print all 
    // pairs in both arrays 
    // whose sum is equal to 
    // given value x 
    static void findPairs(int[] arr1, int[] arr2, 
                          int n, int m, int x) 
    { 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < m; j++) 
                if (arr1[i] + arr2[j] == x) 
                    Console.WriteLine(arr1[i] + " " + arr2[j]); 
    } 

    // Driver code 
    static void Main() 
    { 
        int[] arr1 = { 1, 2, 3, 7, 5, 4 }; 
        int[] arr2 = { 0, 7, 4, 3, 2, 1 }; 
        int x = 8; 
        findPairs(arr1, arr2, 
                  arr1.Length, 
                  arr2.Length, x); 
    } 
} 

// This code is contributed 
// by Sam007 

```

## PHP

```php

<?php 
// PHP program to find all pairs  
// in both arrays whose sum is  
// equal to given value x 

// Function to print all pairs  
// in both arrays whose sum is 
// equal to given value x 
function findPairs($arr1, $arr2,  
                   $n, $m, $x) 
{ 
    for ($i = 0; $i < $n; $i++) 
        for ($j = 0; $j < $m; $j++) 
            if ($arr1[$i] + $arr2[$j] == $x) 
                echo $arr1[$i] . " " .  
                     $arr2[$j] . "\n"; 
}  

// Driver code 
$arr1 = array(1, 2, 3, 7, 5, 4); 
$arr2 = array(0, 7, 4, 3, 2, 1); 
$n = count($arr1); 
$m = count($arr2); 
$x = 8; 
findPairs($arr1, $arr2,  
          $n, $m, $x); 

// This code is contributed  
// by Sam007 
?> 

```

**Output:**

```
1 7
7 1
5 3
4 4

```

**时间复杂度**：O（n ^ 2）

**辅助空间**：O（1）

此问题的**有效解决方案**是[哈希处理](http://www.geeksforgeeks.org/hashing-data-structure/)。 哈希表是使用 C++ 中的 [unordered_set 实现的。](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)

*   我们将所有第一个数组元素存储在哈希表中。

*   对于第二个数组的元素，我们从 x 中减去每个元素，然后在哈希表中检查结果。

*   如果存在结果，则将元素和键打印在哈希（这是第一个数组的元素）中。

## C++

```cpp

// C++ program to find all pair in both arrays 
// whose sum is equal to given value x 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find all pairs in both arrays 
// whose sum is equal to given value x 
void findPairs(int arr1[], int arr2[], int n, 
               int m, int x) 
{ 
    // Insert all elements of first array in a hash 
    unordered_set<int> s; 
    for (int i = 0; i < n; i++) 
        s.insert(arr1[i]); 

    // Subtract sum from second array elements one 
    // by one and check it's present in array first 
    // or not 
    for (int j = 0; j < m; j++) 
        if (s.find(x - arr2[j]) != s.end()) 
            cout << x - arr2[j] << " "
                 << arr2[j] << endl; 
} 

// Driver code 
int main() 
{ 
    int arr1[] = { 1, 0, -4, 7, 6, 4 }; 
    int arr2[] = { 0, 2, 4, -3, 2, 1 }; 
    int x = 8; 
    int n = sizeof(arr1) / sizeof(int); 
    int m = sizeof(arr2) / sizeof(int); 
    findPairs(arr1, arr2, n, m, x); 
    return 0; 
} 

```

## Java

```java

// JAVA Code for Given two unsorted arrays, 
// find all pairs whose sum is x 
import java.util.*; 

class GFG { 

    // Function to find all pairs in both arrays 
    // whose sum is equal to given value x 
    public static void findPairs(int arr1[], int arr2[], 
                                 int n, int m, int x) 
    { 
        // Insert all elements of first array in a hash 
        HashMap<Integer, Integer> s = new HashMap<Integer, Integer>(); 

        for (int i = 0; i < n; i++) 
            s.put(arr1[i], 0); 

        // Subtract sum from second array elements one 
        // by one and check it's present in array first 
        // or not 
        for (int j = 0; j < m; j++) 
            if (s.containsKey(x - arr2[j])) 
                System.out.println(x - arr2[j] + " " + arr2[j]); 
    } 

    /* Driver program to test above function */
    public static void main(String[] args) 
    { 
        int arr1[] = { 1, 0, -4, 7, 6, 4 }; 
        int arr2[] = { 0, 2, 4, -3, 2, 1 }; 
        int x = 8; 

        findPairs(arr1, arr2, arr1.length, arr2.length, x); 
    } 
} 
// This code is contributed by Arnav Kr. Mandal. 

```

## Python3

```py

# Python3 program to find all  

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# pair in both arrays whose  

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# sum is equal to given value x 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)

# Function to find all pairs  

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# in both arrays whose sum is 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# equal to given value x 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
def findPairs(arr1, arr2, n, m, x): 

    # Insert all elements of  
    # first array in a hash 
    s = set() 
    for i in range (0, n): 
        s.add(arr1[i]) 

    # Subtract sum from second  
    # array elements one by one  
    # and check it's present in 
    # array first or not 
    for j in range(0, m): 
        if ((x - arr2[j]) in s): 
            print((x - arr2[j]), '', arr2[j]) 

# Driver code 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
arr1 = [1, 0, -4, 7, 6, 4] 
arr2 = [0, 2, 4, -3, 2, 1] 
x = 8

n = len(arr1) 
m = len(arr2) 
findPairs(arr1, arr2, n, m, x) 

# This code is contributed  

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)
# by ihritik 

> 原文：[https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)

```

## C#

```cs

// C# Code for Given two unsorted arrays, 
// find all pairs whose sum is x 
using System; 
using System.Collections.Generic; 

class GFG { 

    // Function to find all pairs in 
    // both arrays whose sum is equal 
    // to given value x 
    public static void findPairs(int[] arr1, int[] arr2, 
                                 int n, int m, int x) 
    { 
        // Insert all elements of first 
        // array in a hash 
        Dictionary<int, 
                   int> 
            s = new Dictionary<int, 
                               int>(); 

        for (int i = 0; i < n; i++) { 
            s[arr1[i]] = 0; 
        } 

        // Subtract sum from second array 
        // elements one by one and check 
        // it's present in array first 
        // or not 
        for (int j = 0; j < m; j++) { 
            if (s.ContainsKey(x - arr2[j])) { 
                Console.WriteLine(x - arr2[j] + " " + arr2[j]); 
            } 
        } 
    } 

    // Driver Code 
    public static void Main(string[] args) 
    { 
        int[] arr1 = new int[] { 1, 0, -4, 7, 6, 4 }; 
        int[] arr2 = new int[] { 0, 2, 4, -3, 2, 1 }; 
        int x = 8; 

        findPairs(arr1, arr2, arr1.Length, 
                  arr2.Length, x); 
    } 
} 

// This code is contributed by Shrikant13 

```

**Output:**

```
6 2
4 4
6 2
7 1

```

**时间复杂度**：O（max（n，m））

**辅助空间**：O（n）

本文由 [DANISH_RAZA](https://www.facebook.com/danish.raza.98096721) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

