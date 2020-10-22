# 打印形成 AP 的排序数组中的所有三元组

> 原文： [https://www.geeksforgeeks.org/print-triplets-sorted-array-form-ap/](https://www.geeksforgeeks.org/print-triplets-sorted-array-form-ap/)

给定不同正整数的排序数组，请打印形成 AP（或算术级数）的所有三元组。

**示例**：

```
Input : arr[] = { 2, 6, 9, 12, 17, 22, 31, 32, 35, 42 };
Output :
6 9 12
2 12 22
12 17 22
2 17 32
12 22 32
9 22 35
2 22 42
22 32 42

Input : arr[] = { 3, 5, 6, 7, 8, 10, 12};
Output :
3 5 7
5 6 7
6 7 8
6 8 10
8 10 12

```



一种简单的**解决方案**是运行三个嵌套循环以生成所有三元组，并针对每个三元组检查是否形成 AP。 该解决方案的时间复杂度为`O(n ^ 3)`。

**更好的解决方案**是使用哈希。 我们从左到右遍历数组。 我们将每个元素视为中间元素，并将其后的所有元素视为下一个元素。 要搜索上一个元素，我们使用哈希表。

## C++ 

```cpp

// C++ program to print all triplets in given 
// array that form Arithmetic Progression 
// C++ program to print all triplets in given 
// array that form Arithmetic Progression 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print all triplets in 
// given sorted array that forms AP 
void printAllAPTriplets(int arr[], int n) 
{ 
    unordered_set<int> s; 
    for (int i = 0; i < n - 1; i++) 
    { 
    for (int j = i + 1; j < n; j++) 
    { 
        // Use hash to find if there is 
        // a previous element with difference 
        // equal to arr[j] - arr[i] 
        int diff = arr[j] - arr[i]; 
        if (s.find(arr[i] - diff) != s.end()) 
            cout << arr[i] - diff << " " << arr[i] 
                 << " " << arr[j] << endl; 
    } 
    s.insert(arr[i]); 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 2, 6, 9, 12, 17,  
                 22, 31, 32, 35, 42 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printAllAPTriplets(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to print all  
// triplets in given array  
// that form Arithmetic  
// Progression 
import java.io.*; 
import java.util.*; 

class GFG 
{ 
    // Function to print 
    // all triplets in 
    // given sorted array  
    // that forms AP 
    static void printAllAPTriplets(int []arr, 
                                   int n) 
    { 
        ArrayList<Integer> s =  
                 new ArrayList<Integer>(); 
        for (int i = 0; 
                 i < n - 1; i++) 
        { 
            for (int j = i + 1; j < n; j++) 
            { 
                // Use hash to find if 
                // there is a previous  
                // element with difference 
                // equal to arr[j] - arr[i] 
                int diff = arr[j] - arr[i]; 
                boolean exists =  
                        s.contains(arr[i] - diff); 

                if (exists) 
                    System.out.println(arr[i] - diff +  
                                        " " + arr[i] +  
                                        " " + arr[j]); 
            } 

        s.add(arr[i]); 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int []arr = {2, 6, 9, 12, 17,  
                     22, 31, 32, 35, 42}; 
        int n = arr.length; 
        printAllAPTriplets(arr, n); 
    } 
} 

// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

## Python3

```py

# Python program to print all  
# triplets in given array  
# that form Arithmetic  
# Progression 

# Function to print 
# all triplets in 
# given sorted array  
# that forms AP 
def printAllAPTriplets(arr, n) : 

    s = []; 
    for i in range(0, n - 1) : 

        for j in range(i + 1, n) : 

            # Use hash to find if 
            # there is a previous  
            # element with difference 
            # equal to arr[j] - arr[i] 
            diff = arr[j] - arr[i]; 

            if ((arr[i] - diff) in arr) : 
                print ("{} {} {}" .  
                        format((arr[i] - diff), 
                                arr[i], arr[j]),  
                                    end = "\n"); 

    s.append(arr[i]); 

# Driver code 
arr = [2, 6, 9, 12, 17,  
       22, 31, 32, 35, 42]; 
n = len(arr); 
printAllAPTriplets(arr, n); 

# This code is contributed by  
# Manish Shaw(manishshaw1) 

```

## C# 

```cs

// C# program to print all  
// triplets in given array  
// that form Arithmetic  
// Progression 
using System; 
using System.Collections.Generic; 

class GFG 
{ 
    // Function to print 
    // all triplets in 
    // given sorted array  
    // that forms AP 
    static void printAllAPTriplets(int []arr, 
                                   int n) 
    { 
        List<int> s = new List<int>(); 
        for (int i = 0; 
                 i < n - 1; i++) 
        { 
            for (int j = i + 1; j < n; j++) 
            { 
                // Use hash to find if 
                // there is a previous  
                // element with difference 
                // equal to arr[j] - arr[i] 
                int diff = arr[j] - arr[i]; 
                bool exists = s.Exists(element =>  
                                       element == (arr[i] - 
                                                   diff)); 
                if (exists) 
                    Console.WriteLine(arr[i] - diff +  
                                      " " + arr[i] +  
                                      " " + arr[j]); 
            } 
        s.Add(arr[i]); 
        } 
    } 

    // Driver code 
    static void Main() 
    { 
        int []arr = new int[]{ 2, 6, 9, 12, 17,  
                                 22, 31, 32, 35, 42 }; 
        int n = arr.Length; 
        printAllAPTriplets(arr, n); 
    } 
} 
// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

## PHP

```php

<?php 
// PHP program to pr$all  
// triplets in given array  
// that form Arithmetic  
// Progression 

// Function to print 
// all triplets in 
// given sorted array  
// that forms AP 
function printAllAPTriplets($arr, $n) 
{ 
    $s = array(); 
    for ($i = 0; $i < $n - 1; $i++) 
    { 
        for ($j = $i + 1;  
             $j < $n; $j++) 
        { 
            // Use hash to find if 
            // there is a previous  
            // element with difference 
            // equal to arr[j] - arr[i] 
            $diff = $arr[$j] - $arr[$i]; 

            if (in_array($arr[$i] - 
                         $diff, $arr)) 
                echo(($arr[$i] - $diff) .  
                         " " . $arr[$i] .  
                         " " . $arr[$j] . "\n"); 
        } 
    array_push($s, $arr[$i]); 
    } 
} 

// Driver code 
$arr = array(2, 6, 9, 12, 17,  
            22, 31, 32, 35, 42); 
$n = count($arr); 
printAllAPTriplets($arr, $n); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**输出**：

```
6 9 12
2 12 22
12 17 22
2 17 32
12 22 32
9 22 35
2 22 42
22 32 42

```

**时间复杂度**：`O(n^2)`。

**辅助空间**：`O(n)`。

**有效解决方案**基于对数组进行排序的事实。 我们使用与 [GP 三元组问题](https://www.geeksforgeeks.org/find-all-triplets-in-a-sorted-array-that-forms-geometric-progression/)中讨论的相同概念。 这个想法是从第二个元素开始，将每个元素固定为中间元素，然后在一个三元组中搜索另外两个元素（一个较小一个，另一个较大一个）。

以下是上述想法的实现。

## C++

```cpp

// C++ program to print all triplets in given  
// array that form Arithmetic Progression 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print all triplets in 
// given sorted array that forms AP 
void printAllAPTriplets(int arr[], int n) 
{ 
    for (int i = 1; i < n - 1; i++)  
    { 

        // Search other two elements of  
        // AP with arr[i] as middle. 
        for (int j = i - 1, k = i + 1; j >= 0 && k < n;)  
        { 

            // if a triplet is found 
            if (arr[j] + arr[k] == 2 * arr[i])  
            { 
                cout << arr[j] << " " << arr[i] 
                     << " " << arr[k] << endl; 

                // Since elements are distinct, 
                // arr[k] and arr[j] cannot form 
                // any more triplets with arr[i] 
                k++; 
                j--; 
            } 

            // If middle element is more move to  
            // higher side, else move lower side. 
            else if (arr[j] + arr[k] < 2 * arr[i])  
                k++;          
            else
                j--;          
        } 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 2, 6, 9, 12, 17,  
                  22, 31, 32, 35, 42 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printAllAPTriplets(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java implementation to print 
// all the triplets in given array 
// that form Arithmetic Progression 
   
import java.io.*; 
   
class GFG  
{ 
       
    // Function to print all triplets in 
    // given sorted array that forms AP 
    static void findAllTriplets(int arr[], int n) 
    { 
           
        for (int i = 1; i < n - 1; i++)  
        { 
       
            // Search other two elements  
            // of AP with arr[i] as middle. 
            for (int j = i - 1, k = i + 1; j >= 0 && k < n;) 
            { 
                   
                // if a triplet is found 
                if (arr[j] + arr[k] == 2 * arr[i])  
                { 
                    System.out.println(arr[j] +" " +  
                                       arr[i]+ " " + arr[k]); 
       
                    // Since elements are distinct, 
                    // arr[k] and arr[j] cannot form 
                    // any more triplets with arr[i] 
                    k++; 
                    j--; 
                } 
       
                // If middle element is more move to  
                // higher side, else move lower side. 
                else if (arr[j] + arr[k] < 2 * arr[i])  
                    k++;          
                else
                    j--;          
            } 
        } 
    } 
   
    // Driver code 
    public static void main (String[] args)  
    { 
           
        int arr[] = { 2, 6, 9, 12, 17,  
                      22, 31, 32, 35, 42 }; 
        int n = arr.length; 
           
        findAllTriplets(arr, n); 
    } 
} 
   
// This code is contributed by vt_m.
```

## Python 3

```
# python 3 program to print all triplets in given  
# array that form Arithmetic Progression 
   
# Function to print all triplets in 
# given sorted array that forms AP 
def printAllAPTriplets(arr, n): 
   
    for i in range(1, n - 1):  
   
        # Search other two elements of 
        # AP with arr[i] as middle. 
        j = i - 1
        k = i + 1
        while(j >= 0 and k < n ):  
   
            # if a triplet is found 
            if (arr[j] + arr[k] == 2 * arr[i]):  
                print(arr[j], "", arr[i], "", arr[k]) 
   
                # Since elements are distinct, 
                # arr[k] and arr[j] cannot form 
                # any more triplets with arr[i] 
                k += 1
                j -= 1
               
   
            # If middle element is more move to  
            # higher side, else move lower side. 
            elif (arr[j] + arr[k] < 2 * arr[i]):  
                k += 1     
            else: 
                j -= 1     
           
# Driver code 
arr = [ 2, 6, 9, 12, 17,  
        22, 31, 32, 35, 42 ] 
n = len(arr)  
printAllAPTriplets(arr, n) 
   
# This article is contributed  
# by Smitha Dinesh Semwal
```

## C#

```cs
// C# implementation to print 
// all the triplets in given array 
// that form Arithmetic Progression 
   
using System; 
   
class GFG  
{ 
       
    // Function to print all triplets in 
    // given sorted array that forms AP 
    static void findAllTriplets(int []arr, int n) 
    { 
           
        for (int i = 1; i < n - 1; i++)  
        { 
       
            // Search other two elements  
            // of AP with arr[i] as middle. 
            for (int j = i - 1, k = i + 1; j >= 0 && k < n;) 
            { 
                   
                // if a triplet is found 
                if (arr[j] + arr[k] == 2 * arr[i])  
                { 
                    Console.WriteLine(arr[j] +" " +  
                                      arr[i]+ " " + arr[k]); 
       
                    // Since elements are distinct, 
                    // arr[k] and arr[j] cannot form 
                    // any more triplets with arr[i] 
                    k++; 
                    j--; 
                } 
       
                // If middle element is more move to  
                // higher side, else move lower side. 
                else if (arr[j] + arr[k] < 2 * arr[i])  
                    k++;          
                else
                    j--;          
            } 
        } 
    } 
   
    // Driver code 
    public static void Main ()  
    { 
           
        int []arr = { 2, 6, 9, 12, 17,  
                      22, 31, 32, 35, 42 }; 
        int n = arr.Length; 
           
        findAllTriplets(arr, n); 
    } 
} 
   
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP implementation to print 
// all the triplets in given array 
// that form Arithmetic Progression 
  
// Function to print all triplets in 
// given sorted array that forms AP 
function findAllTriplets($arr, $n) 
{ 
    for ($i = 1; $i < $n - 1; $i++)  
    { 
  
        // Search other two elements  
        // of AP with arr[i] as middle. 
        for ($j = $i - 1, $k = $i + 1;  
                   $j >= 0 && $k < $n😉 
        { 
              
            // if a triplet is found 
            if ($arr[$j] + $arr[$k] == 2 *  
                           $arr[$i])  
            { 
                echo $arr[$j] ." " . 
                     $arr[$i]. " " .  
                     $arr[$k] . "\n"; 
  
                // Since elements are distinct, 
                // arr[k] and arr[j] cannot form 
                // any more triplets with arr[i] 
                $k++; 
                $j--; 
            } 
  
            // If middle element is more move to  
            // higher side, else move lower side. 
            else if ($arr[$j] + $arr[$k] < 2 *  
                                     $arr[$i])  
                $k++;          
            else
                $j--;          
        } 
    } 
} 
  
// Driver code 
$arr = array(2, 6, 9, 12, 17,  
             22, 31, 32, 35, 42); 
               
$n = count($arr); 
findAllTriplets($arr, $n); 
  
// This code is contributed by Sam007 
?>
```

输出：

```
6 9 12
2 12 22
12 17 22
2 17 32
12 22 32
9 22 35
2 22 42
22 32 42
```

时间复杂度：`O(n2)`。

辅助空间：`O(1)`。