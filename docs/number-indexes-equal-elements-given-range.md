# 给定范围内具有相等元素的索引数

> 原文： [https://www.geeksforgeeks.org/number-indexes-equal-elements-given-range/](https://www.geeksforgeeks.org/number-indexes-equal-elements-given-range/)

给定`N`个数字和`Q`个查询，每个查询都由`L`和`R`组成，任务是找到这样的整数`i`（`L <= i < R`）的数量，以使`A[i] = A[i+1]`。 考虑基于 0 的索引。

**示例**：

```
Input : A = [1, 2, 2, 2, 3, 3, 4, 4, 4] 
        Q = 2 
        L = 1 R = 8 
        L = 0 R = 4 
Output : 5 
         2
Explanation: We have 5 index i which has 
Ai=Ai+1 in range [1, 8). We have 
2 indexes i which have Ai=Ai+1
in range [0, 4). 

Input :A = [3, 3, 4, 4] 
       Q = 2
       L = 0 R = 3
       L = 2 R = 3 
Output : 2 
         1

```



**朴素的方法**是从`L`遍历到`R`（不包括`R`）并分别针对每个查询，计算满足条件`A[i] = A[i+1]`的索引`i`的数量。

以下是朴素方法的实现：

## C++ 

```cpp

// CPP program to count the number of indexes 
// in range L R such that Ai = Ai+1 
#include <bits/stdc++.h> 
using namespace std; 

// function that answers every query in O(r-l) 
int answer_query(int a[], int n, int l, int r) 
{ 
    // traverse from l to r and count 
    // the required indexes 
    int count = 0; 
    for (int i = l; i < r; i++) 
        if (a[i] == a[i + 1]) 
            count += 1; 

    return count; 
} 

// Driver Code 
int main() 
{ 
    int a[] = { 1, 2, 2, 2, 3, 3, 4, 4, 4 }; 
    int n = sizeof(a) / sizeof(a[0]); 

    // 1-st query 
    int L, R; 
    L = 1; 
    R = 8; 

    cout << answer_query(a, n, L, R) << endl; 

    // 2nd query 
    L = 0; 
    R = 4; 
    cout << answer_query(a, n, L, R) << endl; 
    return 0; 
} 

```

## Java

```
// Java program to count the number of  
// indexes in range L R such that  
// Ai = Ai+1 
class GFG { 
      
    // function that answers every query  
    // in O(r-l) 
    static int answer_query(int a[], int n, 
                              int l, int r) 
    { 
          
        // traverse from l to r and count 
        // the required indexes 
        int count = 0; 
        for (int i = l; i < r; i++) 
            if (a[i] == a[i + 1]) 
                count += 1; 
  
        return count; 
    } 
  
    // Driver Code 
    public static void main(String[] args) 
    { 
        int a[] = {1, 2, 2, 2, 3, 3, 4, 4, 4}; 
        int n = a.length; 
  
        // 1-st query 
        int L, R; 
        L = 1; 
        R = 8; 
  
        System.out.println( 
                   answer_query(a, n, L, R)); 
  
        // 2nd query 
        L = 0; 
        R = 4; 
        System.out.println( 
                  answer_query(a, n, L, R)); 
    } 
} 
  
// This code is contribute by 
// Smitha Dinesh Semwal
```

## Python 3

```
# Python 3 program to count the  
# number of indexes in range L R  
# such that Ai = Ai + 1 
  
# function that answers every  
# query in O(r-l) 
def answer_query(a, n, l, r): 
  
    # traverse from l to r and 
    # count the required indexes 
    count = 0
    for i in range(l, r): 
        if (a[i] == a[i + 1]): 
            count += 1
  
    return count 
  
# Driver Code 
a = [1, 2, 2, 2, 3, 3, 4, 4, 4]  
n = len(a) 
  
# 1-st query 
L = 1
R = 8
print(answer_query(a, n, L, R)) 
  
# 2nd query 
L = 0
R = 4
print(answer_query(a, n, L, R)) 
  
# This code is contributed by 
# Smitha Dinesh Semwal
```

## C#

```
// C# program to count the number of  
// indexes in range L R such that  
// Ai = Ai+1 
using System; 
  
class GFG { 
      
    // function that answers every query  
    // in O(r-l) 
    static int answer_query(int []a, int n, 
                            int l, int r) 
    { 
          
        // traverse from l to r and count 
        // the required indexes 
        int count = 0; 
        for (int i = l; i < r; i++) 
            if (a[i] == a[i + 1]) 
                count += 1; 
  
        return count; 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
        int []a = {1, 2, 2, 2, 3, 3, 
                                4, 4, 4}; 
        int n = a.Length; 
  
        // 1-st query 
        int L, R; 
        L = 1; 
        R = 8; 
  
        Console.WriteLine( 
               answer_query(a, n, L, R)); 
  
        // 2nd query 
        L = 0; 
        R = 4; 
        Console.WriteLine( 
               answer_query(a, n, L, R)); 
    } 
} 
  
// This code is contribute by anuj_67.
```

## PHP

```
<?php 
// PHP program to count the  
// number of indexes in  
// range L R such that 
// Ai = Ai+1 
  
// function that answers  
// every query in O(r-l) 
function answer_query($a, $n,  
                      $l, $r) 
{ 
    // traverse from l to r and  
    // count the required indexes 
    $count = 0; 
    for ($i = $l; $i < $r; $i++) 
        if ($a[$i] == $a[$i + 1]) 
            $count += 1; 
  
    return $count; 
} 
  
// Driver Code 
$a = array(1, 2, 2, 2, 3,  
           3, 4, 4, 4 ); 
$n = count($a); 
  
// 1-st query 
$L = 1; 
$R = 8; 
  
echo (answer_query($a, $n,  
                   $L, $R). "\n"); 
  
// 2nd query 
$L = 0; 
$R = 4; 
echo (answer_query($a, $n,  
                   $L, $R). "\n"); 
                     
// This code is contributed by  
// Manish Shaw(manishshaw1) 
?>
```

输出：

```
5
2
```

时间复杂度：每个查询为`O(R – L)`。

高效的方法：我们可以在`O(1)`时间内回答查询。 这个想法是预先计算一个前缀数组`prefixans`，以便`prefixans[i]`存储从 0 到`i`的索引的总数，该总数符合给定条件。 `prefixans[R-1] - prefix[L-1]`返回`[L, r)`中每个查询的索引总数。

下面是有效方法的实现：

## C++

```
// CPP program to count the number of indexes 
// in range L R such that Ai=Ai+1 
#include <bits/stdc++.h> 
using namespace std; 
const int N = 1000; 
  
// array to store count of index from 0 to 
// i that obey condition 
int prefixans[N]; 
  
// precomputing prefixans[] array 
int countIndex(int a[], int n) 
{ 
    // traverse to compute the prefixans[] array 
    for (int i = 0; i < n; i++) { 
        if (a[i] == a[i + 1]) 
            prefixans[i] = 1; 
  
        if (i != 0) 
            prefixans[i] += prefixans[i - 1]; 
    } 
} 
  
// function that answers every query in O(1) 
int answer_query(int l, int r) 
{ 
    if (l == 0) 
        return prefixans[r - 1]; 
    else
        return prefixans[r - 1] - prefixans[l - 1]; 
} 
  
// Driver Code 
int main() 
{ 
    int a[] = { 1, 2, 2, 2, 3, 3, 4, 4, 4 }; 
    int n = sizeof(a) / sizeof(a[0]); 
  
    // pre-computation 
    countIndex(a, n); 
  
    int L, R; 
  
    // 1-st query 
    L = 1; 
    R = 8; 
  
    cout << answer_query(L, R) << endl; 
  
    // 2nd query 
    L = 0; 
    R = 4; 
    cout << answer_query(L, R) << endl; 
    return 0; 
}
```

## Java

```
// Java program to count 
// the number of indexes 
// in range L R such that 
// Ai=Ai+1 
  
class GFG { 
      
public static int N = 1000; 
  
// Array to store count 
// of index from 0 to 
// i that obey condition 
static int prefixans[] = new int[1000]; 
  
// precomputing prefixans[] array 
public static void countIndex(int a[], int n) 
{ 
      
    // traverse to compute 
    // the prefixans[] array 
    for (int i = 0; i < n; i++) { 
        if (i + 1 < n && a[i] == a[i + 1]) 
            prefixans[i] = 1; 
  
        if (i != 0) 
            prefixans[i] += prefixans[i - 1]; 
    } 
} 
  
// function that answers  
// every query in O(1) 
public static int answer_query(int l, int r) 
{ 
    if (l == 0) 
        return prefixans[r - 1]; 
    else
        return prefixans[r - 1] -  
               prefixans[l - 1]; 
} 
  
// Driver Code 
public static void main(String args[]) 
{ 
    int a[] = {1, 2, 2, 2, 3, 3, 4, 4, 4}; 
    int n = 9; 
  
    // pre-computation 
    countIndex(a, n); 
  
    int L, R; 
  
    // 1-st query 
    L = 1; 
    R = 8; 
  
    System.out.println(answer_query(L, R)); 
  
    // 2nd query 
    L = 0; 
    R = 4; 
    System.out.println(answer_query(L, R)); 
} 
} 
  
// This code is contributed by Jaideep Pyne
```

## Python3

```
# Python program to count  
# the number of indexes in  
# range L R such that Ai=Ai+1 
N = 1000
  
# array to store count  
# of index from 0 to 
# i that obey condition 
prefixans = [0] * N; 
  
# precomputing 
# prefixans[] array 
def countIndex(a, n) : 
  
    global N, prefixans 
      
    # traverse to compute  
    # the prefixans[] array 
    for i in range(0, n - 1) : 
  
        if (a[i] == a[i + 1]) : 
            prefixans[i] = 1
  
        if (i != 0) : 
            prefixans[i] = (prefixans[i] + 
                            prefixans[i - 1]) 
  
# def that answers  
# every query in O(1) 
def answer_query(l, r) :  
  
    global N, prefixans 
    if (l == 0) : 
        return prefixans[r - 1] 
    else : 
        return (prefixans[r - 1] -
                prefixans[l - 1]) 
  
# Driver Code 
a = [1, 2, 2, 2,  
     3, 3, 4, 4, 4] 
n = len(a) 
  
# pre-computation 
countIndex(a, n) 
  
# 1-st query 
L = 1
R = 8
  
print (answer_query(L, R)) 
  
# 2nd query 
L = 0
R = 4
print (answer_query(L, R)) 
  
# This code is contributed by  
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to count the  
// number of indexes in  
// range L R such that Ai=Ai+1 
using System; 
  
class GFG 
{ 
    static int N = 1000; 
      
    // array to store count  
    // of index from 0 to 
    // i that obey condition 
    static int []prefixans = new int[N]; 
      
    // precomputing prefixans[] array 
    static void countIndex(int []a,  
                           int n) 
    { 
        // traverse to compute 
        // the prefixans[] array 
        for (int i = 0; i < n - 1; i++) 
        { 
            if (a[i] == a[i + 1]) 
                prefixans[i] = 1; 
      
            if (i != 0) 
                prefixans[i] += prefixans[i - 1]; 
        } 
    } 
      
    // function that answers  
    // every query in O(1) 
    static int answer_query(int l, int r) 
    { 
        if (l == 0) 
            return prefixans[r - 1]; 
        else
            return prefixans[r - 1] -  
                   prefixans[l - 1]; 
    } 
      
    // Driver Code 
    static void Main() 
    { 
        int []a = new int[]{1, 2, 2, 2,  
                            3, 3, 4, 4, 4}; 
        int n = a.Length; 
          
        // pre-computation 
        countIndex(a, n); 
          
        int L, R; 
      
        // 1-st query 
        L = 1; 
        R = 8; 
      
        Console.WriteLine(answer_query(L, R)); 
      
        // 2nd query 
        L = 0; 
        R = 4; 
        Console.WriteLine(answer_query(L, R)); 
    } 
} 
// This code is contributed by  
// Manish Shaw(manishshaw1)
```

## PHP

```
<?php 
// PHP program to count the  
// number of indexes in  
// range L R such that Ai=Ai+1 
$N = 1000; 
  
// array to store count  
// of index from 0 to 
// i that obey condition 
$prefixans = array_fill(0, $N, 0); 
  
// precomputing 
// prefixans[] array 
function countIndex($a, $n) 
{ 
    global $N, $prefixans; 
      
    // traverse to compute  
    // the prefixans[] array 
    for ($i = 0; $i < $n - 1; $i++)  
    { 
        if ($a[$i] == $a[$i + 1]) 
            $prefixans[$i] = 1; 
  
        if ($i != 0) 
            $prefixans[$i] +=  
                  $prefixans[$i - 1]; 
    } 
} 
  
// function that answers  
// every query in O(1) 
function answer_query($l, $r) 
{ 
    global $N, $prefixans; 
    if ($l == 0) 
        return $prefixans[$r - 1]; 
    else
        return ($prefixans[$r - 1] -  
                $prefixans[$l - 1]); 
} 
  
// Driver Code 
$a = array(1, 2, 2, 2,  
           3, 3, 4, 4, 4); 
$n = count($a); 
  
// pre-computation 
countIndex($a, $n); 
  
// 1-st query 
$L = 1; 
$R = 8; 
  
echo (answer_query($L, $R) . "\n"); 
  
// 2nd query 
$L = 0; 
$R = 4; 
echo(answer_query($L, $R)."\n"); 
  
// This code is contributed by  
// Manish Shaw(manishshaw1) 
?>
```

输出：

```
5
2
```

时间复杂度：每个查询为`O(1)`，预计算为`O(n)`。