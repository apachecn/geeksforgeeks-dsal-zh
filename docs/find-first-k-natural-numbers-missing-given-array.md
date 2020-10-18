# 查找给定数组中缺少的前`k`个自然数

> 原文： [https://www.geeksforgeeks.org/find-first-k-natural-numbers-missing-given-array/](https://www.geeksforgeeks.org/find-first-k-natural-numbers-missing-given-array/)

给定大小为`n`且数字为`k`的数组，我们需要打印给定数组中不存在的前`k`个自然数。

**示例**：

```
Input : [2 3 4] 
         k = 3
Output : [1 5 6]

Input  : [-2 -3 4] 
          k = 2
Output : [1 2]

```



1.  对给定的数组进行排序。

2.  排序后，我们找到数组中第一个正数的位置。

3.  现在，我们遍历数组并将打印元素保持在两个连续的数组元素之间的间隙中。

4.  如果空格不能覆盖`k`个缺失的数字，我们将打印大于最大数组元素的数字。

## C++ 

```cpp

// C++ program to find missing k numbers 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

// Prints first k natural numbers in 
// arr[0..n-1] 
void printKMissing(int arr[], int n, int k) 
{ 
    sort(arr, arr + n); 

    // Find first positive number 
    int i = 0; 
    while (i < n && arr[i] <= 0) 
        i++; 

    // Now find missing numbers 
    // between array elements 
    int count = 0, curr = 1; 
    while (count < k && i < n) { 
        if (arr[i] != curr) { 
            cout << curr << " "; 
            count++; 
        } 
        else
            i++; 

        curr++; 
    } 

    // Find missing numbers after 
    // maximum. 
    while (count < k) { 
        cout << curr << " "; 
        curr++; 
        count++; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 2, 3, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 
    printKMissing(arr, n, k); 
    return 0; 
}

```

## Java

```
// Java program to find missing k numbers
// in an array.
import java.util.Arrays;
 
class GFG {
    // Prints first k natural numbers in
    // arr[0..n-1]
    static void printKMissing(int[] arr, int n, int k)
    {
        Arrays.sort(arr);
 
        // Find first positive number
        int i = 0;
        while (i < n && arr[i] <= 0)
            i++;
 
        // Now find missing numbers
        // between array elements
        int count = 0, curr = 1;
        while (count < k && i < n) {
            if (arr[i] != curr) {
                System.out.print(curr + " ");
                count++;
            }
            else
                i++;
            curr++;
        }
 
        // Find missing numbers after
        // maximum.
        while (count < k) {
            System.out.print(curr + " ");
            curr++;
            count++;
        }
    }
 
    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 2, 3, 4 };
        int n = arr.length;
        int k = 3;
        printKMissing(arr, n, k);
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## Python3

```
# Python3 program to find missing 
# k numbers in an array. 
 
# Prints first k natural numbers 
# in arr[0..n-1] 
def printKMissing(arr, n, k) :
     
    arr.sort() 
 
    # Find first positive number 
    i = 0
    while (i < n and arr[i] <= 0) :
        i = i + 1
 
    # Now find missing numbers 
    # between array elements 
    count = 0
    curr = 1
    while (count < k and i < n) : 
        if (arr[i] != curr) :
            print(str(curr) + " ", end = '')
            count = count + 1
        else:
            i = i + 1
         
        curr = curr + 1
         
    # Find missing numbers after 
    # maximum. 
    while (count < k) :
        print(str(curr) + " ", end = '') 
        curr = curr + 1
        count = count + 1
         
# Driver code 
arr = [ 2, 3, 4 ] 
n = len(arr) 
k = 3
printKMissing(arr, n, k); 
 
# This code is contributed 
# by Yatin Gupta
```

## C#

```
// C# program to find missing 
// k numbers in an array.
using System;
 
class GFG {
    // Prints first k natural numbers
    // in arr[0..n-1]
    static void printKMissing(int[] arr, 
                              int n, 
                              int k)
    {
        Array.Sort(arr);
 
        // Find first positive number
        int i = 0;
        while (i < n && arr[i] <= 0)
            i++;
 
        // Now find missing numbers
        // between array elements
        int count = 0, curr = 1;
        while (count < k && i < n) {
            if (arr[i] != curr) {
                Console.Write(curr + " ");
                count++;
            }
            else
                i++;
            curr++;
        }
 
        // Find missing numbers 
        // after maximum.
        while (count < k) {
            Console.Write(curr + " ");
            curr++;
            count++;
        }
    }
 
    // Driver code
    public static void Main()
    {
        int[] arr = {2, 3, 4};
        int n = arr.Length;
        int k = 3;
        printKMissing(arr, n, k);
    }
}
 
// This code is contributed by Nitin Mittal
```

## PHP

```
<?php
// PHP program to find missing k numbers
// in an array.
 
// Prints first k natural numbers in
// arr[0..n-1]
function printKMissing($arr, $n, $k)
{
    sort($arr); sort($arr , $n);
 
    // Find first positive number
    $i = 0;
    while ($i < $n && $arr[$i] <= 0)
        $i++;
 
    // Now find missing numbers
    // between array elements
    $count = 0; $curr = 1;
    while ($count < $k && $i < $n) {
        if ($arr[$i] != $curr) {
            echo $curr , " ";
            $count++;
        }
        else
            $i++;
 
        $curr++;
    }
 
    // Find missing numbers after
    // maximum.
    while ($count < $k) {
        echo $curr , " ";
        $curr++;
        $count++;
    }
}
 
    // Driver code
    $arr =array ( 2, 3, 4 );
    $n = sizeof($arr);
    $k = 3;
    printKMissing($arr, $n, $k);
 
// This code is contributed by Nitin Mittal.
?>
```

输出：

```
1 5 6 
```

时间复杂度：`O(n Log n)`。

替代方法：

1.  我们可以使用哈希图在`O(1)`时间中进行搜索。
2.  使用字典将值存储在数组中。
3.  我们运行从 1 到`n + k`的循环，并检查它们是否在哈希图中。
4.  如果不存在，请打印号码。
5.  如果找到所有k个元素，则打破循环。

## C++

```
// C++ code for 
// the above approach
#include <bits/stdc++.h>
using namespace std;
 
// Program to print first k
// missing number
void printmissingk(int arr[], 
                   int n, int k)
{
  // Creating a hashmap
  map<int, int> d;
 
  // Iterate over array
  for (int i = 0; i < n; i++)
    d[arr[i]] = arr[i];
 
  int cnt = 1;
  int fl = 0;
 
  // Iterate to find missing
  // element
  for (int i = 0; i < (n + k); i++) 
  {
    if (d.find(cnt) == d.end()) 
    {
      fl += 1;
      cout << cnt << " ";
      if (fl == k)
        break;
    }
    cnt += 1;
  }
}
 
// Driver Code
int main()
{
  int arr[] = {1, 4, 3};
  int n = sizeof(arr) / 
          sizeof(arr[0]);
  int k = 3;;
  printmissingk(arr, n, k);
}
 
// This code is contributed by Chitranayal
```

## Python3

```
# Python3 code for above approach
 
# Program to print first k
# missing number
def printmissingk(arr,n,k):
   
    #creating a hashmap
    d={}
     
    # Iterate over array
    for i in range(len(arr)):
        d[arr[i]]=arr[i]
         
    cnt=1
    fl=0
     
    # Iterate to find missing
    # element
    for i in range(n+k):
        if cnt not in d:
            fl+=1
            print(cnt,end=" ")
            if fl==k:
                break
        cnt+=1
    print()
 
# Driver Code
arr=[1,4,3]
n=len(arr)
k=3
printmissingk(arr,n,k)
 
#This code is contributed by Thirumalai Srinivasan
```

输出：

```
2 5 6
```

时间复杂度：`O(n+k)`。

