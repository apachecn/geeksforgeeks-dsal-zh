# 打印数组中排序的不同元素

> 原文： [https://www.geeksforgeeks.org/print-sorted-distinct-elements-array-c/](https://www.geeksforgeeks.org/print-sorted-distinct-elements-array-c/)

给定一个可能包含重复项的数组，请按排序顺序打印所有不同的元素。

例子：

```
Input  : 1, 3, 2, 2, 1
Output : 1 2 3

Input  : 1, 1, 1, 2, 2, 3
Output : 1 2 3

```



**简单解决方案**首先对数组进行排序，然后遍历数组并仅打印元素的第一个匹配项。

**另一种方法**是使用 C++ STL 中的[集合](http://www.geeksforgeeks.org/set-in-cpp-stl/) 。

## C++ 

```cpp

// CPP program to print sorted distinct 
// elements. 
#include <bits/stdc++.h> 
using namespace std; 

void printRepeating(int arr[], int size) 
{ 
    // Create a set using array elements 
    set<int> s(arr, arr + size); 

    // Print contents of the set. 
    for (auto x : s)  
        cout << x << " "; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 3, 2, 2, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printRepeating(arr, n); 
    return 0; 
} 

```

## Java

```
// Java program to print sorted distinct 
// elements. 
import java.io.*; 
import java.util.*; 
  
public class GFG { 
       
    static void printRepeating(Integer []arr, int size) 
    { 
        // Create a set using array elements 
        SortedSet<Integer> s = new TreeSet<>(); 
        Collections.addAll(s, arr); 
          
        // Print contents of the set. 
        System.out.print(s); 
    } 
       
    // Driver code 
    public static void main(String args[]) 
    { 
        Integer []arr = {1, 3, 2, 2, 1}; 
        int n = arr.length; 
        printRepeating(arr, n); 
    } 
} 
   
// This code is contributed by 
// Manish Shaw (manishshaw1)
```

## Python3

```
# Python3 program to print  
# sorted distinct elements. 
  
def printRepeating(arr,size): 
  
    # Create a set using array elements  
    s = set() 
    for i in range(size): 
        if arr[i] not in s: 
            s.add(arr[i]) 
  
    # Print contents of the set. 
    for i in s: 
        print(i,end=" ") 
  
# Driver code 
if __name__=='__main__': 
    arr = [1,3,2,2,1] 
    size = len(arr) 
    printRepeating(arr,size) 
  
# This code is contributed by  
# Shrikant13
```

## C#

```
// C# program to print sorted distinct 
// elements. 
using System; 
using System.Collections.Generic; 
using System.Linq; 
  
class GFG { 
      
    static void printRepeating(int []arr, int size) 
    { 
        // Create a set using array elements 
        SortedSet<int> s = new SortedSet<int>(arr); 
      
        // Print contents of the set. 
        foreach (var n in s) 
        { 
            Console.Write(n + " "); 
        }  
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int []arr = {1, 3, 2, 2, 1}; 
        int n = arr.Length; 
        printRepeating(arr, n); 
    } 
} 
  
// This code is contributed by 
// Manish Shaw (manishshaw1)
```

输出：

```
1 2 3
```

