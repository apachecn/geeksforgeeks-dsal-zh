# 重新排列数组，使`arr[i] = i`

> 原文： [https://www.geeksforgeeks.org/rearrange-array-arri/](https://www.geeksforgeeks.org/rearrange-array-arri/)

给定一个长度为`N`的元素数组，范围从 0 到`N – 1`。所有元素可能不存在于数组中。 如果不存在`element`，则数组中将存在 -1。 重新排列数组，使`A[i] = i`，如果`i`不存在，则在该位置显示 -1。

**示例**：

```
Input : arr = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1}
Output : [-1, 1, 2, 3, 4, -1, 6, -1, -1, 9]

Input : arr = {19, 7, 0, 3, 18, 15, 12, 6, 1, 8,
              11, 10, 9, 5, 13, 16, 2, 14, 17, 4}
Output : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 
         11, 12, 13, 14, 15, 16, 17, 18, 19]

```

方式（朴素方式）：

+   将数字从 0 导航到`n-1`。
+   现在遍历数组。
+   如果（`i == a[j]`），则将i位置的元素替换为`a[j]`位置。
+   如果存在任何使用 -1 而不是数字的元素，那么它将被自动替换。
+   现在，遍历数组并检查（`a[i] != i`）是否为`true`，然后用 -1 替换`a[i]`。

下面是上述方法的实现：

## C++ 

```cpp
// CPP program for above approach
#include<iostream>
using namespace std;
 
// Function to tranform the array
void fix(int ar[], int n)
{
    int i,j,temp;
     
    // Iterate over the array
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < n; j++)
        {
             
            // Checf is any ar[j]
            // exists such that 
            // ar[j] is equal to i
            if(ar[j] == i)
            {
                temp = ar[j];
                ar[j] = ar[i];
                ar[i] = temp;
                break;
            }            
        }
    }
   
    // Iterate over array
    for(i = 0; i < n; i++)
    {
        // If not present
        if(ar[i] != i)
        {
            ar[i] =- 1;
        }            
    }
   
    // Print the output
    cout << "Array after Rearranging" << endl;
    for(i = 0; i < n; i++)
    {
        cout << ar[i] << " ";
    }
}
 
// Driver Code
int main()
{
    int n, ar[]={-1, -1, 6, 1, 9, 
                          3, 2, -1, 4, -1};
       n = sizeof(ar) / sizeof(ar[0]);
     
    // Function Call
    fix(ar, n);
}
 
// Code BY Tanmay Anand
```

输出：

```
Array after Rearranging
-1 1 2 3 4 -1 6 -1 -1 9 
```

时间复杂度：`O(n ^ 2)`。

另一种方法：

1.  浏览数组。
2.  检查`a[i] = -1`，如果是，则忽略它。
3.  如果`a[i] != -1`，则检查元素`a[i]`是否在其正确位置（`i = A[i]`）。 如果是，则忽略它。
4.  如果`a[i] != -1`且元素`a[i]`不在其正确位置（`i != A [i]`），则将其放置在其正确位置，但是有两个条件：
    +   `A[i]`是空的，意味着`A[i] = -1`，然后将`A[i] = i`放进去。
    +   或`A[i]`不空，表示`A[i] = x`，然后将`y = x`放入`A[i] = i`。 现在，我们需要将y放置到正确的位置，因此从第3步开始重复。

下面是上述方法的实现：

## C++

```cpp
// CPP program for rearrange an
// array such that arr[i] = i.
#include <bits/stdc++.h>
 
using namespace std;
 
// Function to rearrange an array
// such that arr[i] = i.
int fix(int A[], int len)
{
    for (int i = 0; i < len; i++) 
    {
        if (A[i] != -1 && A[i] != i) 
        {
            int x = A[i];
 
            // check if desired place
            // is not vacate
            while (A[x] != -1 && A[x] != x)
            {
                // store the value from
                // desired place
                int y = A[x];
 
                // place the x to its correct
                // position
                A[x] = x;
 
                // now y will become x, now
                // search the place for x
                x = y;
            }
 
            // place the x to its correct
            // position
            A[x] = x;
 
            // check if while loop hasn't
            // set the correct value at A[i]
            if (A[i] != i) 
            {
 
                // if not then put -1 at
                // the vacated place
                A[i] = -1;
            }
        }
    }
}
 
// Driver function.
int main()
{
    int A[] = { -1, -1, 6, 1, 9,
                3, 2, -1, 4, -1 };
 
    int len = sizeof(A) / sizeof(A[0]);
    fix(A, len);
 
    for (int i = 0; i < len; i++)
        cout << A[i] << " ";
}
 
// This code is contributed by Smitha Dinesh Semwal
```

## Java

```java
// Java program for rearrange an 
// array such that arr[i] = i.
import java.util.*;
import java.lang.*;
 
public class GfG {
 
    // Function to rearrange an array
    // such that arr[i] = i.
    public static int[] fix(int[] A)
    {
        for (int i = 0; i < A.length; i++) 
        {
            if (A[i] != -1 && A[i] != i)
            {
                int x = A[i];
 
                // check if desired place
                // is not vacate
                while (A[x] != -1 && A[x] != x) 
                {
 
                    // store the value from
                    // desired place
                    int y = A[x];
 
                    // place the x to its correct
                    // position
                    A[x] = x;
 
                    // now y will become x, now
                    // search the place for x
                    x = y;
                }
 
                // place the x to its correct
                // position
                A[x] = x;
 
                // check if while loop hasn't 
                // set the correct value at A[i]
                if (A[i] != i)
                {
 
                    // if not then put -1 at
                    // the vacated place
                    A[i] = -1;
                }
            }
        }
        return A;
    }
 
    // Driver function.
    public static void main(String[] args)
    {
        int A[] = {-1, -1, 6, 1, 
                    9, 3, 2, -1, 4,-1};
        System.out.println(Arrays.toString(fix(A)));
    }
}
```

## Python3

```py
# Python3 program for rearrange an
# array such that arr[i] = i.
 
# Function to rearrange an array
# such that arr[i] = i.
def fix( A, len):
     
    for i in range(0, len): 
         
        if (A[i] != -1 and A[i] != i):
            x = A[i];
 
            # check if desired place
            # is not vacate
            while (A[x] != -1 and A[x] != x):
                #store the value from
                # desired place
                y = A[x]
 
                # place the x to its correct
                # position
                A[x] = x
 
                # now y will become x, now
                # search the place for x
                x = y
             
            # place the x to its correct
            # position
            A[x] = x;
 
            # check if while loop hasn't
            # set the correct value at A[i]
            if (A[i] != i) :
                 
                # if not then put -1 at
                # the vacated place
                A[i] = -1;
 
# Driver function.
A = [ -1, -1, 6, 1, 9, 3, 2, -1, 4, -1 ]
 
fix(A, len(A))
 
for i in range(0, len(A)):
    print (A[i],end = ' ')
     
# This code is contributed by Saloni1297
```

## C#

```cs
// C# program for rearrange 
// an array such that 
// arr[i] = i.
using System;
 
class GfG 
{
// Function to rearrange an 
// array such that arr[i] = i.
public static int[] fix(int[] A)
{
    for (int i = 0; 
             i < A.Length; i++) 
    {
        if (A[i] != -1 && 
            A[i] != i)
        {
            int x = A[i];
 
            // check if desired 
            // place is not vacate
            while (A[x] != -1 && 
                   A[x] != x) 
            {
 
                // store the value 
                // from desired place
                int y = A[x];
 
                // place the x to its
                // correct position
                A[x] = x;
 
                // now y will become x, 
                // now search the place 
                // for x
                x = y;
            }
 
            // place the x to its 
            // correct position
            A[x] = x;
 
            // check if while loop 
            // hasn't set the correct 
            // value at A[i]
            if (A[i] != i)
            {
 
                // if not then put -1 
                // at the vacated place
                A[i] = -1;
            }
        }
    }
    return A;
}
 
// Driver Code
static void Main()
{
    int []A = new int[]{-1, -1, 6, 1, 9, 
                         3, 2, -1, 4,-1};
    Console.WriteLine(string.Join(",",
                                 fix(A)));
}
}
 
// This code is contributed by 
// Manish Shaw(manishshaw1)
```

## PHP

```php
<?php
// PHP program for rearrange an
// array such that arr[i] = i.
 
// Function to rearrange an 
// array such that arr[i] = i.
function fix(&$A, $len)
{
    for ($i = 0; $i < $len; $i++) 
    {
        if ($A[$i] != -1 && 
            $A[$i] != $i) 
        {
            $x = $A[$i];
 
            // check if desired 
            // place is not vacate
            while ($A[$x] != -1 && 
                   $A[$x] != $x)
            {
                // store the value 
                // from desired place
                $y = $A[$x];
 
                // place the x to its 
                // correct position
                $A[$x] = $x;
 
                // now y will become x, 
                // now search the place 
                // for x
                $x = $y;
            }
 
            // place the x to its 
            // correct position
            $A[$x] = $x;
 
            // check if while loop hasn't
            // set the correct value at A[i]
            if ($A[$i] != $i) 
            {
                // if not then put -1 
                // at the vacated place
                $A[$i] = -1;
            }
        }
    }
}
 
// Driver Code
$A = array(-1, -1, 6, 1, 9,
            3, 2, -1, 4, -1);
 
$len = count($A);
fix($A, $len);
 
for ($i = 0; $i < $len; $i++)
    echo ($A[$i]." ");
     
// This code is contributed by 
// Manish Shaw(manishshaw1)
?>
```

另一种方法（使用`HashSet`）：

+   将数组中存在的所有数字存储到`HashSet`中
+   遍历数组的长度，如果`HashSet`中存在相应的位置元素，则设置`A [i] = i`，否则设置`A[i] = -1`

下面是上述方法的实现。

## Java

```java
// Java program for rearrange an 
// array such that arr[i] = i.
import java.util.*;
import java.lang.*;
 
class GfG {
 
    // Function to rearrange an array
    // such that arr[i] = i.
    public static int[] fix(int[] A)
    {
        Set<Integer> s = new HashSet<Integer>();
 
        // Storing all the values in the HashSet
        for(int i = 0; i < A.length; i++)
        {
           s.add(A[i]);
        }
 
        for(int i = 0; i < A.length; i++)
        {
           if(s.contains(i))
             A[i] = i;
           else
             A[i] = -1;
        }
 
      return A;
}
 
    // Driver function.
    public static void main(String[] args)
    {
        int A[] = {-1, -1, 6, 1, 9,
                    3, 2, -1, 4,-1};
                     
        // Function calling
        System.out.println(Arrays.toString(fix(A)));
    }
}
```

## Python3

```py
# Python3 program for rearrange an 
# array such that arr[i] = i.
 
# Function to rearrange an array
# such that arr[i] = i.
def fix(A):
    s = set()
     
    # Storing all the values in the Set
    for i in range(len(A)):
        s.add(A[i])
 
    for i in range(len(A)):
       
        # check for item if present in set
        if i in s:
            A[i] = i
        else:
            A[i] = -1
    return A
     
# Driver code
if __name__ == "__main__":
    A = [-1, -1, 6, 1, 9,
          3, 2, -1, 4,-1]
    print(fix(A))
 
# This code is contributed by Chitranayal
```

## C#

```cs
// C# program for rearrange an 
// array such that arr[i] = i.
using System;
 
class GfG
{
 
    // Function to rearrange 
    // an array such that
    // arr[i] = i.
    static int[] fix(int []A)
    {
        for (int i = 0; 
                 i < A.Length; i++) 
        {
            if (A[i] != -1 && 
                A[i] != i)
            {
                int x = A[i];
 
                // check if desired place
                // is not vacate
                while (A[x] != -1 && 
                       A[x] != x) 
                {
 
                    // store the value from
                    // desired place
                    int y = A[x];
 
                    // place the x to its 
                    // correct position
                    A[x] = x;
 
                    // now y will become x, now
                    // search the place for x
                    x = y;
                }
 
                // place the x to its 
                // correct position
                A[x] = x;
 
                // check if while loop hasn't 
                // set the correct value at A[i]
                if (A[i] != i)
                { 
                    // if not then put -1 at
                    // the vacated place
                    A[i] = -1;
                }
            }
        }
        return A;
    } 
     
    // Driver Code
    static void Main()
    {
        int []A = new int[]{-1, -1, 6, 1, 9, 
                             3, 2, -1, 4,-1};
        Console.Write(string.Join(",", fix(A)));
    }
}
 
// This code is contributed by 
// Manish Shaw(manishshaw1)
```

输出：

```
[-1, 1, 2, 3, 4, -1, 6, -1, -1, 9]
```

另一种方法（交换数组中的元素）：

+   遍历数组中的元素
+   如果`arr[i] >= 0 && arr[i] != i`，则将`arr[i]`放在`i`处（用`arr[arr[i]]`交换`arr[i]`）

下面是上述方法的实现。

## C++

```cpp
// C++ program for rearrange an 
// array such that arr[i] = i.
#include<stdio.h>
 
int main() 
{
    int arr[] = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1};
    int n = sizeof(arr)/sizeof(arr[0]);
    for (int i = 0; i < n;) 
    {
        if (arr[i] >= 0 && arr[i] != i) 
        arr[arr[i]] = (arr[arr[i]] + arr[i]) - 
                        (arr[i] = arr[arr[i]]);
        else
            i++;
    }
    for(int i = 0; i < n; i++)
        printf("%d ",arr[i]);
        return 0;
}
 
// This Code is Contributed by Adarsh_Verma 
```

## Java

```java
// Java program for rearrange an 
// array such that arr[i] = i.
import java.util.Arrays;
 
class Program {
 
    public static void main(String[] args) {
        int[] arr = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1};
        for (int i = 0; i < arr.length;) {
            if (arr[i] >= 0 && arr[i] != i) {
                int ele = arr[arr[i]];
                arr[arr[i]] = arr[i];
                arr[i] = ele;
            } else {
                i++;
            }
        }
        System.out.println(Arrays.toString(arr));
    }
}
 
  
/* This Java code is contributed by PrinciRaj1992*/
```

## Python3

```py
# Python3 program for rearrange an 
# array such that arr[i] = i.
if __name__ == "__main__":
   
    arr = [-1, -1, 6, 1, 9, 
            3, 2, -1, 4, -1]
    n = len(arr)
    i = 0
    while i < n:
    
        if (arr[i] >= 0 and arr[i] != i):
            (arr[arr[i]] , 
             arr[i]) = (arr[i] , 
                        arr[arr[i]])
        else:
            i += 1
     
    for i in range (n):
        print(arr[i], end= " ")
        
# This code is contributed by Chitranayal
```

## C#

```cs
// C# program for rearrange an 
// array such that arr[i] = i.
using System;
 
namespace GFG
{
    class Program
    {
        static void Main(string[] args)
        {
            int[] arr = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1};
            for(int i = 0; i <arr.Length;)
            {
                if(arr[i] >= 0 && arr[i] != i)
                {
                    int ele = arr[arr[i]];
                    arr[arr[i]] = arr[i];
                    arr[i] = ele;
                } else {
                    i++;
                }
            }
            Console.WriteLine(String.Join(",", arr));
        }
    }
}
// This code is contributed by 
// Venkata VardhiReddy(venkata)
```

时间复杂度：`O(n)`