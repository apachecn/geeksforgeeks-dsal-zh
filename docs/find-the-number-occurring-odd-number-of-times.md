# 查找出现次数的奇数

> 原文： [https://www.geeksforgeeks.org/find-the-number-occurring-odd-number-of-times/](https://www.geeksforgeeks.org/find-the-number-occurring-odd-number-of-times/)

给定一个正整数数组。 除一个数字为奇数次外，所有数字均出现偶数次。 在`O(n)`时间&恒定空间中找到数字。

**示例**：

```
Input : arr = {1, 2, 3, 2, 3, 1, 3}
Output : 3

Input : arr = {5, 7, 2, 7, 5, 2, 5}
Output : 5

```



**简单解决方案**是运行两个嵌套循环。 外循环一一拾取所有元素，内循环计数外循环拾取的元素的出现次数。 该解决方案的时间复杂度为 `O(n^2)`。

以下是暴力方法的实现：

## C++ 

```cpp

// C++ program to find the element  
// occurring odd number of times 
#include<bits/stdc++.h> 
using namespace std; 

// Function to find the element  
// occurring odd number of times 
int getOddOccurrence(int arr[], int arr_size) 
{ 
    for (int i = 0; i < arr_size; i++) { 

        int count = 0; 

        for (int j = 0; j < arr_size; j++) 
        { 
            if (arr[i] == arr[j]) 
                count++; 
        } 
        if (count % 2 != 0) 
            return arr[i]; 
    } 
    return -1; 
} 

// driver code 
int main() 
    { 
        int arr[] = { 2, 3, 5, 4, 5, 2, 
                      4, 3, 5, 2, 4, 4, 2 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 

        // Function calling 
        cout << getOddOccurrence(arr, n); 

        return 0; 
    } 

```

## Java

```java
// Java program to find the element occurring 
// odd number of times 
class OddOccurrence { 
      
    // function to find the element occurring odd 
    // number of times 
    static int getOddOccurrence(int arr[], int arr_size) 
    { 
        int i; 
        for (i = 0; i < arr_size; i++) { 
            int count = 0; 
            for (int j = 0; j < arr_size; j++) { 
                if (arr[i] == arr[j]) 
                    count++; 
            } 
            if (count % 2 != 0) 
                return arr[i]; 
        } 
        return -1; 
    } 
      
    // driver code  
    public static void main(String[] args) 
    { 
        int arr[] = new int[]{ 2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2 }; 
        int n = arr.length; 
        System.out.println(getOddOccurrence(arr, n)); 
    } 
} 
// This code has been contributed by Kamal Rawal
```

## Python3

```py
# Python program to find the element occurring 
# odd number of times 
      
# function to find the element occurring odd 
# number of times 
def getOddOccurrence(arr, arr_size): 
      
    for i in range(0,arr_size): 
        count = 0
        for j in range(0, arr_size): 
            if arr[i] == arr[j]: 
                count+=1
              
        if (count % 2 != 0): 
            return arr[i] 
          
    return -1
      
      
# driver code  
arr = [2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2 ] 
n = len(arr) 
print(getOddOccurrence(arr, n)) 
  
# This code has been contributed by  
# Smitha Dinesh Semwal
```

## C#

```cs
// C# program to find the element  
// occurring odd number of times 
using System; 
  
class GFG 
{ 
    // Function to find the element  
    // occurring odd number of times 
    static int getOddOccurrence(int []arr, int arr_size) 
    { 
        for (int i = 0; i < arr_size; i++) { 
            int count = 0; 
              
            for (int j = 0; j < arr_size; j++) { 
                if (arr[i] == arr[j]) 
                    count++; 
            } 
            if (count % 2 != 0) 
                return arr[i]; 
        } 
        return -1; 
    } 
      
    // Driver code  
    public static void Main() 
    { 
        int []arr = { 2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2 }; 
        int n = arr.Length; 
        Console.Write(getOddOccurrence(arr, n)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to find the  
// element occurring odd 
// number of times 
  
// Function to find the element  
// occurring odd number of times 
function getOddOccurrence(&$arr, $arr_size) 
{ 
    $count = 0; 
    for ($i = 0;  
         $i < $arr_size; $i++)  
    { 
          
        for ($j = 0; 
             $j < $arr_size; $j++) 
        { 
            if ($arr[$i] == $arr[$j]) 
                $count++; 
        } 
        if ($count % 2 != 0) 
            return $arr[$i]; 
    } 
    return -1; 
} 
  
// Driver code 
$arr = array(2, 3, 5, 4, 5, 2,  
             4, 3, 5, 2, 4, 4, 2); 
$n = sizeof($arr); 
  
// Function calling 
echo(getOddOccurrence($arr, $n)); 
  
// This code is contributed 
// by Shivi_Aggarwal 
?>
```

输出：

```
5
```

更好的解决方案是使用哈希。 使用数组元素作为键，并将其计数作为值。 创建一个空的哈希表。 一对一遍历给定的数组元素并存储计数。 该解决方案的时间复杂度为`O(n)`。 但是它需要额外的空间来进行哈希处理。

## C++

```cpp
// C++ program to find the element   
// occurring odd number of times  
#include <bits/stdc++.h> 
using namespace std; 
  
// function to find the element  
// occurring odd number of times  
int getOddOccurrence(int arr[],int size) 
{ 
      
    // Defining HashMap in C++ 
    unordered_map<int, int> hash; 
  
    // Putting all elements into the HashMap  
    for(int i = 0; i < size; i++) 
    { 
        hash[arr[i]]++; 
    } 
    // Iterate through HashMap to check an element 
    // occurring odd number of times and return it 
    for(auto i : hash) 
    { 
        if(i.second % 2 != 0) 
        { 
            return i.first; 
        } 
    } 
    return -1; 
} 
  
// Driver code 
int main()  
{  
    int arr[] = { 2, 3, 5, 4, 5, 2, 4, 
                    3, 5, 2, 4, 4, 2 };  
    int n = sizeof(arr) / sizeof(arr[0]);  
      
    // Function calling  
    cout << getOddOccurrence(arr, n);  
  
    return 0;  
}  
  
// This code is contributed by codeMan_d.
```

## Java

```java
// Java program to find the element occurring odd  
// number of times 
import java.io.*; 
import java.util.HashMap; 
  
class OddOccurrence  
{ 
    // function to find the element occurring odd 
    // number of times 
    static int getOddOccurrence(int arr[], int n) 
    { 
        HashMap<Integer,Integer> hmap = new HashMap<>(); 
          
        // Putting all elements into the HashMap 
        for(int i = 0; i < n; i++) 
        { 
            if(hmap.containsKey(arr[i])) 
            { 
                int val = hmap.get(arr[i]); 
                          
                // If array element is already present then 
                // increase the count of that element. 
                hmap.put(arr[i], val + 1);  
            } 
            else
                  
                // if array element is not present then put 
                // element into the HashMap and initialize  
                // the count to one. 
                hmap.put(arr[i], 1);  
        } 
  
        // Checking for odd occurrence of each element present 
        // in the HashMap  
        for(Integer a:hmap.keySet()) 
        { 
            if(hmap.get(a) % 2 != 0) 
                return a; 
        } 
        return -1; 
    } 
          
    // driver code     
    public static void main(String[] args)  
    { 
        int arr[] = new int[]{2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2}; 
        int n = arr.length; 
        System.out.println(getOddOccurrence(arr, n)); 
    } 
} 
// This code is contributed by Kamal Rawal
```

## Python3

```py
# Python3 program to find the element   
# occurring odd number of times  
   
# function to find the element  
# occurring odd number of times  
def getOddOccurrence(arr,size): 
       
    # Defining HashMap in C++ 
    Hash=dict() 
   
    # Putting all elements into the HashMap  
    for i in range(size): 
        Hash[arr[i]]=Hash.get(arr[i],0) + 1; 
      
    # Iterate through HashMap to check an element 
    # occurring odd number of times and return it 
    for i in Hash: 
  
        if(Hash[i]% 2 != 0): 
            return i 
    return -1
  
   
# Driver code 
arr=[2, 3, 5, 4, 5, 2, 4,3, 5, 2, 4, 4, 2] 
n = len(arr) 
   
# Function calling  
print(getOddOccurrence(arr, n))  
  
# This code is contributed by mohit kumar
```

## C#

```cs
// C# program to find the element occurring odd  
// number of times 
using System; 
using System.Collections.Generic;  
  
public class OddOccurrence  
{ 
    // function to find the element occurring odd 
    // number of times 
    static int getOddOccurrence(int []arr, int n) 
    { 
        Dictionary<int,int> hmap = new Dictionary<int,int>(); 
          
        // Putting all elements into the HashMap 
        for(int i = 0; i < n; i++) 
        { 
            if(hmap.ContainsKey(arr[i])) 
            { 
                int val = hmap[arr[i]]; 
                          
                // If array element is already present then 
                // increase the count of that element. 
                hmap.Remove(arr[i]); 
                hmap.Add(arr[i], val + 1);  
            } 
            else
                  
                // if array element is not present then put 
                // element into the HashMap and initialize  
                // the count to one. 
                hmap.Add(arr[i], 1);  
        } 
  
        // Checking for odd occurrence of each element present 
        // in the HashMap  
        foreach(KeyValuePair<int, int> entry in hmap) 
        { 
            if(entry.Value % 2 != 0) 
            { 
                return entry.Key; 
            } 
        } 
        return -1; 
    } 
          
    // Driver code  
    public static void Main(String[] args)  
    { 
        int []arr = new int[]{2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2}; 
        int n = arr.Length; 
        Console.WriteLine(getOddOccurrence(arr, n)); 
    } 
} 
  
// This code is contributed by Princi Singh
```

输出：

```
5
```

最佳解决方案是对所有元素进行按位 XOR。 所有元素的 XOR 给我们奇数出现的元素。 请注意，如果两个元素相同，则两个元素的 XOR 为 0，且数字`x`与 0 的 XOR 为`x`。

下面是上述方法的实现。

## C++

```cpp
// C++ program to find the element 
// occurring odd number of times 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to find element occurring 
// odd number of times 
int getOddOccurrence(int ar[], int ar_size) 
{ 
    int res = 0;  
    for (int i = 0; i < ar_size; i++)      
        res = res ^ ar[i]; 
      
    return res; 
} 
  
/* Driver function to test above function */
int main() 
{ 
    int ar[] = {2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2}; 
    int n = sizeof(ar)/sizeof(ar[0]); 
      
    // Function calling 
    cout << getOddOccurrence(ar, n); 
      
    return 0; 
}
```

## C

```c
// C program to find the element 
// occurring odd number of times 
#include <stdio.h> 
  
// Function to find element occurring 
// odd number of times 
int getOddOccurrence(int ar[], int ar_size) 
{ 
    int res = 0;  
    for (int i = 0; i < ar_size; i++)      
        res = res ^ ar[i]; 
      
    return res; 
} 
  
/* Driver function to test above function */
int main() 
{ 
    int ar[] = {2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2}; 
    int n = sizeof(ar) / sizeof(ar[0]); 
      
    // Function calling 
    printf("%d", getOddOccurrence(ar, n)); 
    return 0; 
}
```

## Java

```java
//Java program to find the element occurring odd number of times 
  
class OddOccurance  
{ 
    int getOddOccurrence(int ar[], int ar_size)  
    { 
        int i; 
        int res = 0; 
        for (i = 0; i < ar_size; i++)  
        { 
            res = res ^ ar[i]; 
        } 
        return res; 
    } 
  
    public static void main(String[] args)  
    { 
        OddOccurance occur = new OddOccurance(); 
        int ar[] = new int[]{2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2}; 
        int n = ar.length; 
        System.out.println(occur.getOddOccurrence(ar, n)); 
    } 
} 
// This code has been contributed by Mayank Jaiswal
```

## Python3

```py
# Python program to find the element occurring odd number of times 
  
def getOddOccurrence(arr): 
  
    # Initialize result 
    res = 0
      
    # Traverse the array 
    for element in arr: 
        # XOR with the result 
        res = res ^ element 
  
    return res 
  
# Test array 
arr = [ 2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2] 
  
print("%d" % getOddOccurrence(arr))
```

## C#

```cs
// C# program to find the element 
// occurring odd number of times 
using System; 
  
class GFG 
{ 
    // Function to find the element  
    // occurring odd number of times 
    static int getOddOccurrence(int []arr, int arr_size) 
    { 
        int res = 0; 
        for (int i = 0; i < arr_size; i++)  
        { 
            res = res ^ arr[i]; 
        } 
        return res; 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int []arr = { 2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2 }; 
        int n = arr.Length; 
        Console.Write(getOddOccurrence(arr, n)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to find the  
// element occurring odd  
// number of times 
  
// Function to find element  
// occurring odd number of times 
function getOddOccurrence(&$ar, $ar_size) 
{ 
    $res = 0;  
    for ($i = 0; $i < $ar_size; $i++)      
        $res = $res ^ $ar[$i]; 
      
    return $res; 
} 
  
// Driver Code 
$ar = array(2, 3, 5, 4, 5, 2, 
            4, 3, 5, 2, 4, 4, 2); 
$n = sizeof($ar); 
  
// Function calling 
echo(getOddOccurrence($ar, $n)); 
      
// This code is contributed  
// by Shivi_Aggarwal 
?>
```


输出：

```
5
```

时间复杂度：`O(n)`。