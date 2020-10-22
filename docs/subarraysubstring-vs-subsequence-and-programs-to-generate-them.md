# 子数组/子字符串与子序列以及生成它们的程序

> 原文： [https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)

**子数组/子字符串**：

子数组是数组的**连续**部分。 一个在另一个数组内的数组。 例如，考虑数组`[1, 2, 3, 4]`，有 10 个非空子数组。 子栏位是`(1), (2), (3), (4), (1,2), (2,3), (3,4), (1,2,3), (2,3,  4)`和`(1,2,3,4)`。 通常，对于大小为`n`的数组/字符串，有`n * (n + 1) / 2`个非空子数组/子字符串。

![subseq-vs-subarray](img/47f0bfa4f49024229591b348fb3d6d3f.png)

**如何生成所有子数组？**

我们可以运行两个嵌套循环，外部循环选择开始元素，内部循环将被选择元素右边的所有元素视为子数组的结束元素。

## C++ 

```cpp

/*  C++ code to generate all possible subarrays/subArrays 
    Complexity- O(n^3) */
#include<bits/stdc++.h> 
using namespace std; 

// Prints all subarrays in arr[0..n-1] 
void subArray(int arr[], int n) 
{ 
    // Pick starting point 
    for (int i=0; i <n; i++) 
    { 
        // Pick ending point 
        for (int j=i; j<n; j++) 
        { 
            // Print subarray between current starting 
            // and ending points 
            for (int k=i; k<=j; k++) 
                cout << arr[k] << " "; 

            cout << endl; 
        } 
    } 
} 

// Driver program 
int main() 
{ 
    int arr[] = {1, 2, 3, 4}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "All Non-empty Subarrays\n"; 
    subArray(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program toto generate all possible subarrays/subArrays 
//  Complexity- O(n^3) */ 
  
class Test 
{ 
    static int arr[] = new int[]{1, 2, 3, 4}; 
      
    // Prints all subarrays in arr[0..n-1] 
    static void subArray( int n) 
    { 
        // Pick starting point 
        for (int i=0; i <n; i++) 
        { 
            // Pick ending point 
            for (int j=i; j<n; j++) 
            { 
                // Print subarray between current starting 
                // and ending points 
                for (int k=i; k<=j; k++) 
                    System.out.print(arr[k]+" "); 
            } 
        } 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        System.out.println("All Non-empty Subarrays"); 
        subArray(arr.length); 
          
    } 
}
```

## Python3

```py
# Python3 code to generate all possible 
# subarrays/subArrays 
# Complexity- O(n^3)  
  
# Prints all subarrays in arr[0..n-1] 
def subArray(arr, n): 
  
    # Pick starting point 
    for i in range(0,n): 
  
        # Pick ending point 
        for j in range(i,n): 
  
            # Print subarray between 
            # current starting 
            # and ending points 
            for k in range(i,j+1): 
                print (arr[k],end=" ") 
  
            print ("\n",end="") 
  
              
# Driver program 
arr = [1, 2, 3, 4] 
n = len(arr) 
print ("All Non-empty Subarrays") 
  
subArray(arr, n); 
  
# This code is contributed by Shreyanshi.
```

## C#

```cs
// C# program toto generate all 
// possible subarrays/subArrays 
// Complexity- O(n^3) 
using System; 
  
class GFG 
{  
    static int []arr = new int[]{1, 2, 3, 4}; 
      
    // Prints all subarrays in arr[0..n-1] 
    static void subArray( int n) 
    { 
          
        // Pick starting point 
        for (int i = 0; i < n; i++) 
        { 
              
            // Pick ending point 
            for (int j = i; j < n; j++) 
            { 
                  
                // Print subarray between current  
                // starting and ending points 
                for (int k = i; k <= j; k++) 
                    Console.Write(arr[k]+" "); 
                    Console.WriteLine(""); 
            } 
        } 
    } 
      
    // Driver Code 
    public static void Main()  
    { 
        Console.WriteLine("All Non-empty Subarrays"); 
        subArray(arr.Length); 
          
    } 
  
} 
  
// This code is contributed by Sam007.
```

## PHP

```php
<?php 
// PHP code to generate all possible 
// subarrays/subArrays Complexity- O(n^3)  
  
// Prints all subarrays  
// in arr[0..n-1] 
function subArray($arr, $n) 
{ 
      
    // Pick starting point 
    for ($i = 0; $i < $n; $i++) 
    { 
          
        // Pick ending point 
        for ($j = $i; $j < $n; $j++) 
        { 
              
            // Print subarray between  
            // current starting 
            // and ending points 
            for ($k = $i; $k <= $j; $k++) 
                echo $arr[$k] , " "; 
  
            echo "\n"; 
        } 
    } 
} 
  
    // Driver Code 
    $arr= array(1, 2, 3, 4); 
    $n = sizeof($arr); 
    echo "All Non-empty Subarrays\n"; 
    subArray($arr, $n); 
      
// This ocde is contributed by m_kit 
?>
```

输出：

```
All Non-empty Subarrays
1 
1 2 
1 2 3 
1 2 3 4 
2 
2 3 
2 3 4 
3 
3 4 
4 
```

子序列：

子序列是可以通过零个或多个元素从另一个序列派生的序列，而无需更改其余元素的顺序。

对于同一示例，有 15 个子序列。 它们是`(1), (2), (3), (4), (1, 2), (1, 3), (1, 4), (2, 3), (2, 4), (3, 4), (1, 2, 3), (1, 2, 4), (1, 3, 4), (2, 3, 4), (1, 2, 3, 4)`。 更笼统地说，对于一个大小为n的序列，我们总共可以有`2n - 1`个非空子序列。

区分字符串的示例：考虑字符串`"geeksforgeeks`和`"gks"`。 `"gks"`是`"geeksforgeeks`的子序列，但不是子字符串。 `"geeks"`既是子序列又是子阵列。 每个子数组都是一个子序列。 更具体地说，子序列是子字符串的概括。

如何生成所有子序列？

我们可以使用[幂集生成算法](https://www.geeksforgeeks.org/power-set/)来生成所有子序列。

## C++

```cpp
/*  C++ code to generate all possible subsequences. 
    Time Complexity O(n * 2^n) */
#include<bits/stdc++.h> 
using namespace std; 
  
void printSubsequences(int arr[], int n) 
{ 
    /* Number of subsequences is (2**n -1)*/
    unsigned int opsize = pow(2, n); 
  
    /* Run from counter 000..1 to 111..1*/
    for (int counter = 1; counter < opsize; counter++) 
    { 
        for (int j = 0; j < n; j++) 
        { 
            /* Check if jth bit in the counter is set 
                If set then print jth element from arr[] */
            if (counter & (1<<j)) 
                cout << arr[j] << " "; 
        } 
        cout << endl; 
    } 
} 
  
// Driver program 
int main() 
{ 
    int arr[] = {1, 2, 3, 4}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "All Non-empty Subsequences\n"; 
    printSubsequences(arr, n); 
    return 0; 
}
```

## Java

```java
/*  Java code to generate all possible subsequences. 
    Time Complexity O(n * 2^n) */
  
import java.math.BigInteger; 
  
class Test 
{ 
    static int arr[] = new int[]{1, 2, 3, 4}; 
      
    static void printSubsequences(int n) 
    { 
        /* Number of subsequences is (2**n -1)*/
        int opsize = (int)Math.pow(2, n); 
       
        /* Run from counter 000..1 to 111..1*/
        for (int counter = 1; counter < opsize; counter++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                /* Check if jth bit in the counter is set 
                    If set then print jth element from arr[] */
        
                if (BigInteger.valueOf(counter).testBit(j)) 
                    System.out.print(arr[j]+" "); 
            } 
            System.out.println(); 
        } 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        System.out.println("All Non-empty Subsequences"); 
        printSubsequences(arr.length); 
    } 
}
```

## Python3

```py
# Python 3 code to generate all 
# possible subsequences. 
# Time Complexity O(n * 2 ^ n)  
import math 
  
def printSubsequences(arr, n) : 
  
    # Number of subsequences is (2**n -1) 
    opsize = math.pow(2, n) 
  
    # Run from counter 000..1 to 111..1 
    for counter in range( 1, (int)(opsize)) : 
        for j in range(0, n) : 
              
            # Check if jth bit in the counter 
            # is set If set then print jth  
            # element from arr[]  
            if (counter & (1<<j)) : 
                print( arr[j], end =" ") 
          
        print() 
  
# Driver program 
arr = [1, 2, 3, 4] 
n = len(arr) 
print( "All Non-empty Subsequences") 
  
printSubsequences(arr, n) 
  
# This code is contributed by Nikita Tiwari.
```

## PHP

```php
<?php 
// PHP code to generate all  
// possible subsequences. 
// Time Complexity O(n * 2^n)  
  
function printSubsequences($arr, $n) 
{ 
    // Number of subsequences  
    // is (2**n -1) 
    $opsize = pow(2, $n); 
  
    /* Run from counter 
    000..1 to 111..1*/
    for ($counter = 1;  
         $counter < $opsize;  
         $counter++) 
    { 
        for ( $j = 0; $j < $n; $j++) 
        { 
             /* Check if jth bit in  
                the counter is set 
                If set then print jth 
                element from arr[] */
            if ($counter & (1 << $j)) 
                echo $arr[$j], " "; 
        } 
        echo "\n"; 
    } 
} 
  
// Driver Code 
$arr = array (1, 2, 3, 4); 
$n = sizeof($arr); 
  
echo "All Non-empty Subsequences\n"; 
  
printSubsequences($arr, $n); 
      
// This code is contributed by ajit 
?>
```

输出：

```
All Non-empty Subsequences
1 
2 
1 2 
3 
1 3 
2 3 
1 2 3 
4 
1 4 
2 4 
1 2 4 
3 4 
1 3 4 
2 3 4 
1 2 3 4
```

