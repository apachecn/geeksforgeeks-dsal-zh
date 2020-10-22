# 在给定范围内偶数或奇数的查询概率

> 原文： [https://www.geeksforgeeks.org/queries-probability-even-odd-number-given-ranges/](https://www.geeksforgeeks.org/queries-probability-even-odd-number-given-ranges/)

给定大小为`N`的数组`A`，其中包含整数。 我们必须回答`Q`个查询，其中每个查询的形式为：

*   **`K L R`**：如果`K = 0`，则必须找到从数组`A`的段`[L, R]`（均包括）中选择**偶数**编号的可能性。

*   **`K L R`**：如果`K = 1`，则必须找到从数组`A`的线段`[L, R]`（包括两端）中选择**奇数**数字的可能性。

对于每个查询，打印两个整数`p`和`q`，它们表示概率`p / q`。 `p`和`q`都简化为最小形式。

如果`p`为 0，则打印 0；或者如果`p`等于`q`，则打印 1；否则，仅打印`p`和`q`。

**示例**：

```
Input : N = 5, arr[] = { 6, 5, 2, 1, 7 }
        query 1: 0 2 2
        query 2: 1 2 5 
        query 3: 0 1 4  
Output : 0
         3 4
         1 2
Explanation : 
First query is to find probability of even 
element in range [2, 2]. Since range contains 
a single element 5 which is odd, the answer 
is 0\. Second query is to find probability of
odd element in range [2, 5]. There are 3
odd elements in range probability is 3/4.
Third query is for even elements in range
from 1 to 4\. Since there are equal even
and odd elements, probability is 2/4
which is 1/2.

```



这个想法是要维护两个数组，即`even[]`和`odd[]`，以保持偶数或奇数元素的数目直到索引`i`。 现在，为了回答每个查询，我们可以通过查找给定查询范围内的元素数来计算结果分母`q`。 为了找到结果分子，我们从直到`r`的元素中删除了直到`l – 1`的元素数。

要以最小形式输出答案，我们找到`p`和`q`的 GCD 并输出`p / gcd`和`q / gcd`。 对于答案 0 和 1，我们将明确指定条件。

以下是此方法的实现：

## C++

```cpp
// CPP program to find probability of even 
// or odd elements in a given range. 
#include <bits/stdc++.h> 
using namespace std; 
  
// Number of tuples in a query 
#define C 3 
  
// Solve each query of K L R form 
void solveQuery(int arr[], int n, int Q,  
                           int query[][C]) 
{ 
    // To count number of odd and even  
    // number upto i-th index. 
    int even[n + 1]; 
    int odd[n + 1]; 
    even[0] = odd[0] = 0; 
  
    // Counting number of odd and even  
    // integer upto index i 
    for (int i = 0; i < n; i++) { 
  
        // If number is odd, increment the  
        // count of odd frequency leave 
        // even frequency same. 
        if (arr[i] & 1) { 
            odd[i + 1] = odd[i] + 1; 
            even[i + 1] = even[i]; 
        } 
  
        // If number is even, increment the 
        // count of even frequency leave odd 
        // frequency same. 
        else { 
            even[i + 1] = even[i] + 1; 
            odd[i + 1] = odd[i]; 
        } 
    } 
  
    // To solve each query 
    for (int i = 0; i < Q; i++) { 
        int r = query[i][2]; 
        int l = query[i][1]; 
        int k = query[i][0]; 
  
        // Counting total number of element in  
        // current query 
        int q = r - l + 1; 
        int p; 
  
        // Counting number of odd or even element  
        // in current query range 
        if (k) 
            p = odd[r] - odd[l - 1]; 
        else
            p = even[r] - even[l - 1]; 
  
        // If frequency is 0, output 0 
        if (!p) 
            cout << "0" << endl; 
  
        // If frequency is equal to number of   
        // element in current range output 1. 
        else if (p == q) 
            cout << "1" << endl; 
  
        // Else find the GCD of both. If yes,  
        // output by dividing both number by gcd 
        // to output the answer in reduced form. 
        else { 
            int g = __gcd(p, q); 
            cout << p / g << " " << q / g << endl; 
        } 
    } 
} 
// Driven Program 
int main() 
{ 
    int arr[] = { 6, 5, 2, 1, 7 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int Q = 2; 
    int query[Q][C] = { 
        { 0, 2, 2 }, 
        { 1, 2, 5 } 
    }; 
  
    solveQuery(arr, n, Q, query); 
    return 0; 
}
```

## Java

```java
// java program to find probability 
// of even or odd elements in a 
// given range. 
import java.io.*; 
  
public class GFG { 
          
    // Number of tuples in a query 
    //static int C = 3; 
    // Recursive function to return 
    // gcd of a and b 
    static int __gcd(int a, int b) 
    { 
        // Everything divides 0  
        if (a == 0 || b == 0) 
            return 0; 
      
        // base case 
        if (a == b) 
            return a; 
      
        // a is greater 
        if (a > b) 
            return __gcd(a - b, b); 
              
        return __gcd(a, b - a); 
    } 
      
    // Solve each query of K L R form 
    static void solveQuery(int []arr, 
             int n, int Q, int [][]query) 
    { 
          
        // To count number of odd and even  
        // number upto i-th index. 
        int []even = new int[n + 1]; 
        int []odd = new int[n + 1]; 
        even[0] = odd[0] = 0; 
      
        // Counting number of odd and even  
        // integer upto index i 
        for (int i = 0; i < n; i++) 
        { 
      
            // If number is odd, increment 
            // the count of odd frequency 
            // leave even frequency same. 
            if ((arr[i] & 1) > 0) 
            { 
                odd[i + 1] = odd[i] + 1; 
                even[i + 1] = even[i]; 
            } 
      
            // If number is even, increment 
            // the count of even frequency 
            // leave odd frequency same. 
            else 
            { 
                even[i + 1] = even[i] + 1; 
                odd[i + 1] = odd[i]; 
            } 
        } 
      
        // To solve each query 
        for (int i = 0; i < Q; i++) 
        { 
            int r = query[i][2]; 
            int l = query[i][1]; 
            int k = query[i][0]; 
      
            // Counting total number of 
            // element in current query 
            int q = r - l + 1; 
            int p; 
      
            // Counting number of odd or 
            // even element in current  
            // query range 
            if (k > 0) 
                p = odd[r] - odd[l - 1]; 
            else
                p = even[r] - even[l - 1]; 
      
            // If frequency is 0, output 0 
            if (p <= 0) 
                System.out.println("0"); 
      
            // If frequency is equal to 
            // number of element in current 
            // range output 1. 
            else if (p == q) 
                System.out.println("1"); 
      
            // Else find the GCD of both. 
            // If yes, output by dividing 
            // both number by gcd to output 
            // the answer in reduced form. 
            else
            { 
                int g = __gcd(p, q); 
                System.out.println(p / g  
                          + " " + q / g); 
            } 
        } 
    } 
      
    // Driven Program 
    static public void main (String[] args) 
    { 
        int []arr = { 6, 5, 2, 1, 7 }; 
        int n = arr.length; 
        int Q = 2; 
        int [][]query = { { 0, 2, 2 }, 
                          { 1, 2, 5 } }; 
  
        solveQuery(arr, n, Q, query); 
    } 
} 
  
// This code is contributed by vt_m.
```

## Python 3

```
# Python 3 program to find probability 
# of even or odd elements in a given range. 
import math 
  
# Number of tuples in a query 
C = 3
  
# Solve each query of K L R form 
def solveQuery(arr, n, Q, query): 
  
    # To count number of odd and even  
    # number upto i-th index. 
    even = [0] * (n + 1) 
    odd = [0] * (n + 1) 
    even[0] = 0
    odd[0] = 0
  
    # Counting number of odd and even  
    # integer upto index i 
    for i in range( n) : 
  
        # If number is odd, increment the  
        # count of odd frequency leave 
        # even frequency same. 
        if (arr[i] & 1) : 
            odd[i + 1] = odd[i] + 1
            even[i + 1] = even[i] 
  
        # If number is even, increment the 
        # count of even frequency leave odd 
        # frequency same. 
        else : 
            even[i + 1] = even[i] + 1
            odd[i + 1] = odd[i] 
  
    # To solve each query 
    for i in range( Q) : 
        r = query[i][2] 
        l = query[i][1] 
        k = query[i][0] 
  
        # Counting total number of element   
        # in current query 
        q = r - l + 1
  
        # Counting number of odd or even   
        # element in current query range 
        if (k): 
            p = odd[r] - odd[l - 1] 
        else: 
            p = even[r] - even[l - 1] 
  
        # If frequency is 0, output 0 
        if (not p): 
            print("0") 
  
        # If frequency is equal to number of  
        # element in current range output 1. 
        elif (p == q): 
            print("1") 
  
        # Else find the GCD of both. If yes,  
        # output by dividing both number by gcd 
        # to output the answer in reduced form. 
        else : 
            g = math.gcd(p, q) 
            print((p // g), (q // g)) 
  
# Driver Code 
if __name__ =="__main__": 
      
    arr = [ 6, 5, 2, 1, 7 ] 
    n = len(arr) 
    Q = 2
    query = [[0, 2, 2], 
             [1, 2, 5]] 
  
    solveQuery(arr, n, Q, query) 
  
# This code is contributed by ita_c
```

## C#

```cs
// C# program to find probability 
// of even or odd elements in a 
// given range. 
using System; 
  
public class GFG { 
      
    // Number of tuples in a query 
    //static int C = 3; 
    // Recursive function to return 
    // gcd of a and b 
    static int __gcd(int a, int b) 
    { 
          
        // Everything divides 0  
        if (a == 0 || b == 0) 
            return 0; 
      
        // base case 
        if (a == b) 
            return a; 
      
        // a is greater 
        if (a > b) 
            return __gcd(a - b, b); 
              
        return __gcd(a, b - a); 
    } 
      
    // Solve each query of K L R form 
    static void solveQuery(int []arr, 
           int n, int Q, int [,]query) 
    { 
          
        // To count number of odd and 
        // even number upto i-th index. 
        int []even = new int[n + 1]; 
        int []odd = new int[n + 1]; 
        even[0] = odd[0] = 0; 
      
        // Counting number of odd and 
        // even integer upto index i 
        for (int i = 0; i < n; i++) 
        { 
      
            // If number is odd, 
            // increment the count of 
            // odd frequency leave 
            // even frequency same. 
            if ((arr[i] & 1) > 0) 
            { 
                odd[i + 1] = odd[i] + 1; 
                even[i + 1] = even[i]; 
            } 
      
            // If number is even,  
            // increment the count of 
            // even frequency leave 
            // odd frequency same. 
            else
            { 
                even[i + 1] = even[i] + 1; 
                odd[i + 1] = odd[i]; 
            } 
        } 
      
        // To solve each query 
        for (int i = 0; i < Q; i++) 
        { 
            int r = query[i,2]; 
            int l = query[i,1]; 
            int k = query[i,0]; 
      
            // Counting total number of 
            // element in current query 
            int q = r - l + 1; 
            int p; 
      
            // Counting number of odd 
            // or even element in current 
            // query range 
            if (k > 0) 
                p = odd[r] - odd[l - 1]; 
            else
                p = even[r] - even[l - 1]; 
      
            // If frequency is 0, output 0 
            if (p <= 0) 
                Console.WriteLine("0"); 
      
            // If frequency is equal to 
            // number of element in 
            // current range output 1. 
            else if (p == q) 
                Console.WriteLine("1"); 
      
            // Else find the GCD of both. 
            // If yes, output by dividing 
            // both number by gcd to output 
            // the answer in reduced form. 
            else 
            { 
                int g = __gcd(p, q); 
                Console.WriteLine(p / g  
                           + " " + q / g); 
            } 
        } 
    } 
      
    // Driven Program 
    static public void Main () 
    { 
        int []arr = { 6, 5, 2, 1, 7 }; 
        int n = arr.Length; 
        int Q = 2; 
        int [,]query = { { 0, 2, 2 }, 
                         { 1, 2, 5 } }; 
      
        solveQuery(arr, n, Q, query); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP program to find probability 
// of even or odd elements in a 
// given range. 
  
// Number of tuples in a query 
//static int C = 3; 
// Recursive function to return 
// gcd of a and b 
function __gcd($a, $b) 
{ 
    // Everything divides 0  
    if ($a == 0 || $b == 0) 
        return 0; 
  
    // base case 
    if ($a == $b) 
        return $a; 
  
    // a is greater 
    if ($a > $b) 
        return __gcd($a - $b, $b); 
          
    return __gcd($a, $b - $a); 
} 
  
// Solve each query of K L R form 
function solveQuery($arr, $n, $Q, $query) 
{ 
      
    // To count number of odd and even  
    // number upto i-th index. 
    // $even = new int[n + 1]; 
    // int []odd = new int[n + 1]; 
    $even[0] = $odd[0] = 0; 
  
    // Counting number of odd and even  
    // integer upto index i 
    for ($i = 0; $i < $n; $i++) 
    { 
  
        // If number is odd, increment 
        // the count of odd frequency 
        // leave even frequency same. 
        if (($arr[$i] & 1) > 0) 
        { 
            $odd[$i + 1] = $odd[$i] + 1; 
            $even[$i + 1] = $even[$i]; 
        } 
  
        // If number is even, increment 
        // the count of even frequency 
        // leave odd frequency same. 
        else
        { 
            $even[$i + 1] = $even[$i] + 1; 
            $odd[$i + 1] = $odd[$i]; 
        } 
    } 
  
    // To solve each query 
    for ($i = 0; $i < $Q; $i++) 
    { 
        $r = $query[$i][2]; 
        $l = $query[$i][1]; 
        $k = $query[$i][0]; 
  
        // Counting total number of 
        // element in current query 
        $q = $r - $l + 1; 
        $p; 
  
        // Counting number of odd or 
        // even element in current  
        // query range 
        if ($k > 0) 
            $p = $odd[$r] - $odd[$l - 1]; 
        else
            $p = $even[$r] - $even[$l - 1]; 
  
        // If frequency is 0, output 0 
        if ($p <= 0) 
            echo "0" . "\n"; 
  
        // If frequency is equal to 
        // number of element in current 
        // range output 1. 
        else if ($p == $q) 
            echo "1" . "\n"; 
  
        // Else find the GCD of both. 
        // If yes, output by dividing 
        // both number by gcd to output 
        // the answer in reduced form. 
        else
        { 
            $g = __gcd($p, $q); 
            echo (int)($p / $g) . " " . (int)($q / $g); 
        } 
    } 
} 
  
// Driven Program 
$arr = array(6, 5, 2, 1, 7); 
$n = sizeof($arr); 
$Q = 2; 
$query = array(array(0, 2, 2), 
               array(1, 2, 5)); 
  
solveQuery($arr, $n, $Q, $query); 
  
// This code is contributed  
// by Akanksha Rai
```

输出：

```
0
3 4
```

