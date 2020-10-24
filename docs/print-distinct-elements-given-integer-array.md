# 打印给定整数数组的所有不同元素

> 原文： [https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)

方法：

1.  将所有输入整数放入哈希映射的键

2.  在循环外部打印键集

## Java

```java

import java.util.HashMap; 
public class UniqueInArray2 { 

    public static void main(String args[]) 

    { 
        int ar[] = { 10, 5, 3, 4, 3, 5, 6 }; 
        HashMap<Integer,Integer> hm = new HashMap<Integer,Integer>(); 
        for (int i = 0; i < ar.length; i++) { 
            hm.put(ar[i], i); 
        } 
        // Using hm.keySet() to print output reduces time complexity. - Lokesh 
        System.out.println(hm.keySet()); 

    } 

} 

```

## C#

```cs
// C# implementation of the approach 
using System; 
using System.Collections.Generic;  
  
public class UniqueInArray2  
{ 
  
    public static void Main(String []args) 
  
    { 
        int []ar = { 10, 5, 3, 4, 3, 5, 6 }; 
        Dictionary<int,int> hm = new Dictionary<int,int>(); 
        for (int i = 0; i < ar.Length; i++) 
        { 
            if(hm.ContainsKey(ar[i])) 
                hm.Remove(ar[i]); 
            hm.Add(ar[i], i); 
        } 
  
        // Using hm.Keys to print output  
        // reduces time complexity. - Lokesh 
        var v = hm.Keys; 
        foreach(int a in v) 
            Console.Write(a+" "); 
  
    } 
  
} 
  
/* This code contributed by PrinciRaj1992 */
```

给定一个整数数组，打印数组中所有不同的元素。 给定的数组可能包含重复项，并且输出应仅将每个元素打印一次。 给定的数组未排序。

示例：

```
Input: arr[] = {12, 10, 9, 45, 2, 10, 10, 45}
Output: 12, 10, 9, 45, 2

Input: arr[] = {1, 2, 3, 4, 5}
Output: 1, 2, 3, 4, 5

Input: arr[] = {1, 1, 1, 1, 1}
Output: 1
```

一个简单的解决方案是使用两个嵌套循环。 外循环从最左边的元素开始一个接一个地选择一个元素。 内部循环检查元素的左侧是否存在。 如果存在，则忽略该元素，否则打印该元素。 以下是简单算法的实现。

## C++

```cpp
// C++ program to print all distinct elements in a given array 
#include <bits/stdc++.h> 
using namespace std; 
  
void printDistinct(int arr[], int n) 
{ 
    // Pick all elements one by one 
    for (int i=0; i<n; i++) 
    { 
        // Check if the picked element is already printed 
        int j; 
        for (j=0; j<i; j++) 
           if (arr[i] == arr[j]) 
               break; 
  
        // If not printed earlier, then print it 
        if (i == j) 
          cout << arr[i] << " "; 
    } 
} 
  
// Driver program to test above function 
int main() 
{ 
    int arr[] = {6, 10, 5, 4, 9, 120, 4, 6, 10}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printDistinct(arr, n); 
    return 0; 
}
```

## Java

```java
// Java program to print all distinct 
// elements in a given array 
import java.io.*; 
  
class GFG { 
  
    static void printDistinct(int arr[], int n) 
    { 
        // Pick all elements one by one 
        for (int i = 0; i < n; i++) 
        { 
            // Check if the picked element  
            // is already printed 
            int j; 
            for (j = 0; j < i; j++) 
            if (arr[i] == arr[j]) 
                break; 
      
            // If not printed earlier,  
            // then print it 
            if (i == j) 
            System.out.print( arr[i] + " "); 
        } 
    } 
      
    // Driver program 
    public static void main (String[] args)  
    { 
        int arr[] = {6, 10, 5, 4, 9, 120, 4, 6, 10}; 
        int n = arr.length; 
        printDistinct(arr, n); 
  
    } 
} 
  
// This code is contributed by vt_m
```

## Python3

```py
# python program to print all distinct 
# elements in a given array 
  
def printDistinct(arr, n): 
  
    # Pick all elements one by one 
    for i in range(0, n): 
  
        # Check if the picked element  
        # is already printed 
        d = 0
        for j in range(0, i): 
            if (arr[i] == arr[j]): 
                d = 1
                break
  
        # If not printed earlier, 
        # then print it 
        if (d == 0): 
            print(arr[i]) 
      
# Driver program to test above function 
arr = [6, 10, 5, 4, 9, 120, 4, 6, 10] 
n = len(arr) 
printDistinct(arr, n) 
  
# This code is contributed by Sam007.
```

## C#

```cs
// C# program to print all distinct 
// elements in a given array 
using System; 
  
class GFG { 
  
    static void printDistinct(int []arr, int n) 
    { 
          
        // Pick all elements one by one 
        for (int i = 0; i < n; i++) 
        { 
              
            // Check if the picked element  
            // is already printed 
            int j; 
            for (j = 0; j < i; j++) 
                if (arr[i] == arr[j]) 
                     break; 
      
            // If not printed earlier,  
            // then print it 
            if (i == j) 
            Console.Write(arr[i] + " "); 
        } 
    } 
      
    // Driver program 
    public static void Main ()  
    { 
        int []arr = {6, 10, 5, 4, 9, 120, 
                                  4, 6, 10}; 
        int n = arr.Length; 
          
        printDistinct(arr, n); 
  
    } 
} 
  
// This code is contributed by Sam007.
```

## PHP

```php
<?php 
// PHP program to print all distinct 
// elements in a given array 
  
function printDistinct($arr, $n) 
{ 
    // Pick all elements one by one 
    for($i = 0; $i < $n; $i++) 
    { 
          
        // Check if the picked element 
        // is already printed 
        $j; 
        for($j = 0; $j < $i; $j++) 
        if ($arr[$i] == $arr[$j]) 
            break; 
  
        // If not printed  
        // earlier, then print it 
        if ($i == $j) 
        echo $arr[$i] , " "; 
    } 
} 
  
    // Driver Code 
    $arr = array(6, 10, 5, 4, 9, 120, 4, 6, 10); 
    $n = sizeof($arr); 
    printDistinct($arr, $n); 
      
// This code is contributed by nitin mittal 
?>
```

输出：

```
6 10 5 4 9 120
```

上述解决方案的时间复杂度为`O(n ^ 2)`。 我们可以使用排序来解决`O(nLogn)`时间中的问题。 这个想法很简单，首先对数组进行排序，以便每个元素的所有出现变为连续。 一旦出现连续，我们就可以遍历排序后的数组并在`O(n)`时间内打印出不同的元素。 以下是该想法的实现。

## C++

```cpp
// C++ program to print all distinct elements in a given array 
#include <bits/stdc++.h> 
using namespace std; 
  
void printDistinct(int arr[], int n) 
{ 
    // First sort the array so that all occurrences become consecutive 
    sort(arr, arr + n); 
  
    // Traverse the sorted array 
    for (int i=0; i<n; i++) 
    { 
       // Move the index ahead while there are duplicates 
       while (i < n-1 && arr[i] == arr[i+1]) 
          i++; 
  
       // print last occurrence of the current element 
       cout << arr[i] << " "; 
    } 
} 
  
// Driver program to test above function 
int main() 
{ 
    int arr[] = {6, 10, 5, 4, 9, 120, 4, 6, 10}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    printDistinct(arr, n); 
    return 0; 
}
```

## Java

```java
// Java program to print all distinct  
// elements in a given array 
import java.io.*; 
import java .util.*; 
  
class GFG  
{ 
    static void printDistinct(int arr[], int n) 
    { 
        // First sort the array so that  
        // all occurrences become consecutive 
        Arrays.sort(arr); 
      
        // Traverse the sorted array 
        for (int i = 0; i < n; i++) 
        { 
            // Move the index ahead while  
            // there are duplicates 
            while (i < n - 1 && arr[i] == arr[i + 1]) 
                i++; 
      
            // print last occurrence of  
            // the current element 
            System.out.print(arr[i] +" "); 
        } 
    } 
      
    // Driver program  
    public static void main (String[] args)  
    { 
        int arr[] = {6, 10, 5, 4, 9, 120, 4, 6, 10}; 
        int n = arr.length; 
        printDistinct(arr, n); 
  
    } 
} 
  
// This code is contributed by vt_m
```

## Python3

```py
# Python program to print all distinct  
# elements in a given array 
  
def printDistinct(arr, n): 
      
    # First sort the array so that  
    # all occurrences become consecutive 
    arr.sort(); 
  
    # Traverse the sorted array 
    for i in range(n): 
          
        # Move the index ahead while there are duplicates 
        if(i < n-1 and arr[i] == arr[i+1]): 
            while (i < n-1 and (arr[i] == arr[i+1])): 
                i+=1; 
              
  
        # prlast occurrence of the current element 
        else: 
            print(arr[i], end=" "); 
  
# Driver code 
arr = [6, 10, 5, 4, 9, 120, 4, 6, 10]; 
n = len(arr); 
printDistinct(arr, n); 
  
# This code has been contributed by 29AjayKumar
```

## C#

```cs
// C# program to print all distinct  
// elements in a given array 
using System; 
  
class GFG { 
  
    static void printDistinct(int []arr, int n) 
    { 
          
        // First sort the array so that  
        // all occurrences become consecutive 
        Array.Sort(arr); 
      
        // Traverse the sorted array 
        for (int i = 0; i < n; i++) 
        { 
              
            // Move the index ahead while  
            // there are duplicates 
            while (i < n - 1 && arr[i] == arr[i + 1]) 
                i++; 
      
            // print last occurrence of  
            // the current element 
            Console.Write(arr[i] + " "); 
        } 
    } 
      
    // Driver program  
    public static void Main ()  
    { 
        int []arr = {6, 10, 5, 4, 9, 120, 4, 6, 10}; 
        int n = arr.Length; 
          
        printDistinct(arr, n); 
    } 
} 
  
// This code is contributed by Sam007.
```

## PHP

```php
<?php 
// PHP program to print all distinct 
// elements in a given array 
  
function printDistinct( $arr, $n) 
{ 
      
    // First sort the array so 
    // that all occurrences  
    // become consecutive 
    sort($arr); 
  
    // Traverse the sorted array 
    for ($i = 0; $i < $n; $i++) 
    { 
          
        // Move the index ahead  
        // while there are duplicates 
        while ($i < $n - 1 and 
               $arr[$i] == $arr[$i + 1]) 
            $i++; 
      
        // print last occurrence 
        // of the current element 
        echo $arr[$i] , " "; 
    } 
} 
  
    // Driver Code 
    $arr = array(6, 10, 5, 4, 9, 120, 4, 6, 10); 
    $n = count($arr); 
    printDistinct($arr, $n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
4 5 6 9 10 120
```

我们可以使用散列来平均解决`O(n)`时间。 这个想法是从左到右遍历给定的数组，并在哈希表中跟踪访问的元素。 以下是该想法的实现。

## C++

```cpp
/* CPP program to print all distinct elements  
   of a given array */
#include<bits/stdc++.h> 
using namespace std; 
  
// This function prints all distinct elements 
void printDistinct(int arr[],int n) 
{ 
    // Creates an empty hashset 
    unordered_set<int> s; 
  
    // Traverse the input array 
    for (int i=0; i<n; i++) 
    { 
        // If not present, then put it in 
        // hashtable and print it 
        if (s.find(arr[i])==s.end()) 
        { 
            s.insert(arr[i]); 
            cout << arr[i] << " "; 
        } 
    } 
} 
  
// Driver method to test above method 
int main () 
{ 
    int arr[] = {10, 5, 3, 4, 3, 5, 6}; 
    int n=7; 
    printDistinct(arr,n); 
    return 0; 
}
```

## Java

```java
/* Java program to print all distinct elements of a given array */
import java.util.*; 
  
class Main 
{ 
    // This function prints all distinct elements 
    static void printDistinct(int arr[]) 
    { 
        // Creates an empty hashset 
        HashSet<Integer> set = new HashSet<>(); 
  
        // Traverse the input array 
        for (int i=0; i<arr.length; i++) 
        { 
            // If not present, then put it in hashtable and print it 
            if (!set.contains(arr[i])) 
            { 
                set.add(arr[i]); 
                System.out.print(arr[i] + " "); 
            } 
        } 
    } 
  
    // Driver method to test above method 
    public static void main (String[] args) 
    { 
        int arr[] = {10, 5, 3, 4, 3, 5, 6}; 
        printDistinct(arr); 
    } 
}
```

## Python3

```py
# Python3 program to print all distinct elements  
# of a given array  
  
# This function prints all distinct elements 
def printDistinct(arr, n): 
      
    # Creates an empty hashset 
    s = dict(); 
  
    # Traverse the input array 
    for i in range(n): 
          
        # If not present, then put it in 
        # hashtable and print it 
        if (arr[i] not in s.keys()): 
            s[arr[i]] = arr[i]; 
            print(arr[i], end = " "); 
   
# Driver Code 
arr = [10, 5, 3, 4, 3, 5, 6]; 
n = 7; 
printDistinct(arr, n); 
  
# This code is contributed by Princi Singh
```

## C#

```cs
// C# program to print all distinct 
// elements of a given array  
using System; 
using System.Collections.Generic; 
  
class GFG 
{ 
// This function prints all  
// distinct elements  
public static void printDistinct(int[] arr) 
{ 
    // Creates an empty hashset  
    HashSet<int> set = new HashSet<int>(); 
  
    // Traverse the input array  
    for (int i = 0; i < arr.Length; i++) 
    { 
        // If not present, then put it  
        // in hashtable and print it  
        if (!set.Contains(arr[i])) 
        { 
            set.Add(arr[i]); 
            Console.Write(arr[i] + " "); 
        } 
    } 
} 
  
// Driver Code 
public static void Main(string[] args) 
{ 
    int[] arr = new int[] {10, 5, 3, 4, 3, 5, 6}; 
    printDistinct(arr); 
} 
} 
  
// This code is contributed by Shrikant13
```

输出：

```
10 5 3 4 6 
```

哈希优于排序的另一个优点是，元素的打印顺序与输入数组中的顺序相同。

