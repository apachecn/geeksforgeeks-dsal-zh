# 重新排列数组，使偶数位置大于奇数

> 原文： [https://www.geeksforgeeks.org/rearrange-array-such-that-even-positioned-are-greater-than-odd/](https://www.geeksforgeeks.org/rearrange-array-such-that-even-positioned-are-greater-than-odd/)

给定一个`n`个元素的数组`A`，请根据以下关系对数组进行排序：

![](img/b4e44739d3fc921e3bf8796ce2b4a859.png "Rendered by QuickLaTeX.com")

，如果`i`是偶数。

![](img/63dad9a4afe79564bb6534bf955fc110.png "Rendered by QuickLaTeX.com")

，如果`i`是奇数。

打印结果数组。

例子 ：

```
Input : A[] = {1, 2, 2, 1}
Output :  1 2 1 2
Explanation : 
For 1st element, 1  1, i = 2 is even.
3rd element, 1  1, i = 4 is even.

Input : A[] = {1, 3, 2}
Output : 1 3 2
Explanation : 
Here, the array is also sorted as per the conditions. 
1  1 and 2 < 3.

```



观察到该数组由[n / 2]个均匀放置的元素组成。 如果我们将最大[n / 2]个元素分配给偶数位置，而将其余元素分配给奇数位置，那么我们的问题就解决了。 因为处于奇数位置的元素将始终小于处于偶数位置的元素，因为它是最大元素，反之亦然。 对数组进行排序，并在偶数位置分配前[n / 2]个元素。

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to rearrange the elements  
// in array such that even positioned are  
// greater than odd positioned elements 
#include<bits/stdc++.h> 
using namespace std; 

void assign(int a[], int n) 
{ 
    // Sort the array 
    sort(a, a + n); 

    int ans[n];  
    int p = 0, q = n - 1; 
    for (int i = 0; i < n; i++)  
    { 
        // Assign even indexes with maximum elements 
        if ((i + 1) % 2 == 0) 
            ans[i] = a[q--]; 

        // Assign odd indexes with remaining elements 
        else
            ans[i] = a[p++]; 
    } 

    // Print result 
    for (int i = 0; i < n; i++)  
        cout << ans[i] << " "; 
} 

// Driver Code 
int main() 
{ 
    int A[] = { 1, 3, 2, 2, 5 }; 
    int n = sizeof(A) / sizeof(A[0]); 
    assign(A, n); 
    return 0; 
} 

```

## Java

```java
// Java program to rearrange the elements
// in array such that even positioned are
// greater than odd positioned elements
import java.io.*;
import java.util.*;
 
class GFG {
 
    static void assign(int a[], int n)
    {
 
        // Sort the array
        Arrays.sort(a);
 
        int ans[] = new int[n];
        int p = 0, q = n - 1;
        for (int i = 0; i < n; i++) {
 
            // Assign even indexes with maximum elements
            if ((i + 1) % 2 == 0)
                ans[i] = a[q--];
 
            // Assign odd indexes with remaining elements
            else
                ans[i] = a[p++];
        }
 
        // Print result
        for (int i = 0; i < n; i++)
            System.out.print(ans[i] + " ");
    }
 
    // Driver code
    public static void main(String args[])
    {
        int A[] = { 1, 3, 2, 2, 5 };
        int n = A.length;
        assign(A, n);
    }
}
 
// This code is contributed by Nikita Tiwari.
```

## Python3

```py
# Python3 code to rearrange the
# elements in array such that
# even positioned are greater
# than odd positioned elements
 
def assign(a, n):
     
    # Sort the array
    a.sort()
     
    ans = [0] * n
    p = 0
    q = n - 1
    for i in range(n):
         
        # Assign even indexes with
        # maximum elements
        if (i + 1) % 2 == 0:
            ans[i] = a[q]
            q = q - 1
         
        # Assign odd indexes with
        # remaining elements
        else:
            ans[i] = a[p]
            p = p + 1
             
    # Print result
    for i in range(n):
        print(ans[i], end = " ")
 
# Driver Code
A = [ 1, 3, 2, 2, 5 ]
n = len(A)
assign(A, n)
 
# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```cs
// C# program to rearrange the elements
// in array such that even positioned are
// greater than odd positioned elements
using System;
 
class GFG {
 
    static void assign(int[] a, int n)
    {
        // Sort the array
        Array.Sort(a);
 
        int[] ans = new int[n];
        int p = 0, q = n - 1;
        for (int i = 0; i < n; i++) {
 
            // Assign even indexes with maximum elements
            if ((i + 1) % 2 == 0)
                ans[i] = a[q--];
 
            // Assign odd indexes with remaining elements
            else
                ans[i] = a[p++];
        }
 
        // Print result
        for (int i = 0; i < n; i++)
            Console.Write(ans[i] + " ");
    }
 
    // Driver code
    public static void Main()
    {
        int[] A = { 1, 3, 2, 2, 5 };
        int n = A.Length;
        assign(A, n);
    }
}
 
// This code is contributed by vt_m.
```

## PHP

```php
<?php
// PHP program to rearrange
// the elements in array such 
// that even positioned are 
// greater than odd positioned 
// elements
 
function assign($a, $n)
{
     
    // Sort the array
    sort($a);
 
    $p = 0; $q = $n - 1;
    for ($i = 0; $i < $n; $i++) 
    {
         
        // Assign even indexes 
        // with maximum elements
        if (($i + 1) % 2 == 0)
            $ans[$i] = $a[$q--];
 
        // Assign odd indexes 
        // with remaining elements
        else
            $ans[$i] = $a[$p++];
    }
 
    // Print result
    for ($i = 0; $i < $n; $i++) 
        echo($ans[$i] . " ");
}
 
// Driver Code
$A = array( 1, 3, 2, 2, 5 );
$n = sizeof($A);
assign($A, $n);
 
// This code is contributed by Ajit.
?>
```

输出：

```
 1 5 2 3 2
```

方法 2：

另一种方法是遍历数组的第二个元素，如果不满足条件，则将其与前一个元素交换。 它的实现如下：

## C++

```cpp
// C++ program to rearrange the elements
// in the array such that even positioned are
// greater than odd positioned elements
#include <bits/stdc++.h>
using namespace std;
 
// swap two elements
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
 
void rearrange(int arr[], int n)
{
    for (int i = 1; i < n; i++) {
        // if index is even
        if (i % 2 == 0) {
            if (arr[i] > arr[i - 1])
                swap(&arr[i - 1], &arr[i]);
        }
        // if index is odd
        else {
            if (arr[i] < arr[i - 1])
                swap(&arr[i - 1], &arr[i]);
        }
    }
}
 
int main()
{
    int n = 5;
    int arr[] = { 1, 3, 2, 2, 5 };
    rearrange(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << "\n";
    return 0;
}
```

## Python3

```py
# Python3 program to rearrange 
# the elements in the array 
# such that even positioned are
# greater than odd positioned elements
def rearrange(arr, n):
 
    for i in range (1, n):
       
        # if index is even
        if (i % 2 == 0):
            if (arr[i] > arr[i - 1]):
                arr[i - 1], arr[i] = arr[i], arr[i - 1]
         
        # if index is odd
        else:
            if (arr[i] < arr[i - 1]):
                arr[i - 1], arr[i] = arr[i] , arr[i - 1]
 
if __name__ == "__main__":          
    n = 5
    arr = [1, 3, 2, 2, 5]
    rearrange(arr, n);
    for i in range (n):
        print (arr[i], end = " ")
    print ()
    
# This code is contributed by Chitranayal
```

输出：
 
```
  1 3 2 5 2
```
