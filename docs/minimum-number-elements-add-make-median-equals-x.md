# 使中位数等于`x`的要添加的最小元素数量

> 原文： [https://www.geeksforgeeks.org/minimum-number-elements-add-make-median-equals-x/](https://www.geeksforgeeks.org/minimum-number-elements-add-make-median-equals-x/)

长度为`n`的数组中的中位数是一个元素，在我们按非降序对元素进行排序（数组元素从 1 开始编号）后，它占据位置编号`(n + 1) / 2`。 数组的中位数`2, 6, 1, 2, 3`是 2，数组的中位数`0, 96, 17, 23`是数字 17。

**示例**：

```
Input : 3 10
        10 20 30
Output : 1
In the first sample we can add number 9 
to array (10, 20, 30). The resulting array
(9, 10, 20, 30) will have a median in 
position (4+1)/2 = 2, that is, 10

Input : 3 4
        1 2 3
Output : 4
In the second sample you should add numbers 
4, 5, 5, 5\. The resulting array has median
equal to 4.

```



**第一种方法**：该方法是向数组中再添加一个数字`x`，直到数组的中位数等于`x`。 下面是上述方法的实现：

## C++ 

```cpp

// CPP program to find minimum number 
// of elements needs to add to the  
// array so that its median equals x. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns count of elements to be  
// added to make median x. This function 
// assumes that a[] has enough extra space. 
int minNumber(int a[], int n, int x) 
{     
    // to sort the array in increasing order. 
    sort(a, a + n); 

    int k; 
    for (k = 0; a[(n - 1) / 2] != x; k++) { 
        a[n++] = x; 
        sort(a, a + n); 
    } 
    return k; 
} 

// Driver code 
main() 
{ 
    int x = 10; 
    int a[6] = { 10, 20, 30 }; 
    int n = 3; 
    cout << minNumber(a, n, x) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum number 
// of elements needs to add to the  
// array so that its median equals x. 
import java.util.Arrays; 

class GFG  
{ 

// Returns count of elements to be  
// added to make median x. This function 
// assumes that a[] has enough extra space. 
static int minNumber(int a[], int n, int x) 
{  
    // to sort the array in increasing order. 
    Arrays.sort(a); 

    int k; 
    for (k = 0; a[(n) / 2] != x; k++)  
    { 
        a[n++] = x; 
        Arrays.sort(a); 
    } 
    return k; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int x = 10; 
    int a[] = { 10, 20, 30 }; 
    int n = 3; 
    System.out.println(minNumber(a, n-1, x)); 
} 
} 

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Python 3 program to find minimum number 
# of elements needs to add to the  
# array so that its median equals x. 

# Returns count of elements to be added   
# to make median x. This function 
# assumes that a[] has enough extra space. 
def minNumber(a, n, x): 

    # to sort the array in increasing order. 
    a.sort(reverse = False) 
    k = 0
    while(a[int((n - 1) / 2)] != x): 
        a[n - 1] = x 
        n += 1
        a.sort(reverse = False) 
        k += 1

    return k 

# Driver code 
if __name__ == '__main__': 
    x = 10
    a = [10, 20, 30] 
    n = 3
    print(minNumber(a, n, x)) 

# This code is contributed by 
# Surendra_Gangwar 

```

## C# 

```cs

// C# program to find minimum number  
// of elements needs to add to the  
// array so that its median equals x.  
using System; 

class GFG  
{  

// Returns count of elements to be  
// added to make median x. This function  
// assumes that a[] has enough extra space.  
static int minNumber(int []a, int n, int x)  
{  
    // to sort the array in increasing order.  
    Array.Sort(a);  

    int k;  
    for (k = 0; a[(n) / 2] != x; k++)  
    {  
        a[n++] = x;  
        Array.Sort(a);  
    }  
    return k;  
}  

// Driver code  
public static void Main(String[] args)  
{  
    int x = 10;  
    int []a = { 10, 20, 30 };  
    int n = 3;  
    Console.WriteLine(minNumber(a, n-1, x));  
}  
}  

// This code contributed by Rajput-Ji 

```

## PHP

```php

<?php 
// PHP program to find minimum  
// number of elements needs to  
// add to the array so that its 
// median equals x. 

// Returns count of elements  
// to be added to make median  
// x. This function assumes  
// that a[] has enough extra space. 
function minNumber($a, $n, $x) 
{  
    // to sort the array in  
    // increasing order. 
    sort($a); 

    $k; 
    for ($k = 0;  
         $a[($n - 1) / 2] != $x; $k++)  
    { 
        $a[$n++] = $x; 
        sort($a); 
    } 
    return $k; 
} 

// Driver code 
$x = 10; 
$a = array (10, 20, 30); 
$n = 3; 
echo minNumber($a, $n, $x),"\n"; 

// This code is contributed by ajit 
?> 

```

**输出**：

```
1

```

**时间复杂度**：`O(knLogn)`。

**第二种方法**：更好的方法是对等于`x`（即`e`），大于`x`（即`h`）和小于`x`（即`l`）的所有元素进行计数。 然后，

如果`l`大于`h`，则`ans`为`(l – h) + 1 – e`；

如果`h`大于`l`，则`ans`将为`(h – l – 1) + 1 – e`；

我们可以使用 [Hoare 的分区方案](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)来计算较小，相等和较大的元素。

下面是上述方法的实现：

## C++

```cpp

// CPP program to find minimum number of  
// elements to add so that its median  
// equals x. 
#include <bits/stdc++.h> 
using namespace std; 

int minNumber(int a[], int n, int x) 
{ 
    int l = 0, h = 0, e = 0; 
    for (int i = 0; i < n; i++) { 

        // no. of elements equals to x,  
        // that is, e. 
        if (a[i] == x) 
            e++; 

        // no. of elements greater than x,  
        // that is, h. 
        else if (a[i] > x) 
            h++; 

        // no. of elements smaller than x, 
        // that is, l. 
        else if (a[i] < x) 
            l++; 
    } 

    int ans = 0; 
    if (l > h)  
        ans = l - h; 
    else if (l < h)  
        ans = h - l - 1; 

    // subtract the no. of elements  
    // that are equal to x. 
    return ans + 1 - e; 
} 

// Driver code 
int main() 
{ 
    int x = 10; 
    int a[] = { 10, 20, 30 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << minNumber(a, n, x) << endl; 
    return 0; 
} 

```

## Java

```java
// Java program to find minimum number 
// of elements to add so that its  
// median equals x. 
import java.util.*; 
import java.lang.*; 
  
class GFG { 
  
    public static int minNumber(int a[], 
                           int n, int x) 
    { 
        int l = 0, h = 0, e = 0; 
        for (int i = 0; i < n; i++) 
        { 
  
            // no. of elements equals to 
            // x, that is, e. 
            if (a[i] == x) 
                e++; 
  
            // no. of elements greater 
            // than x, that is, h. 
            else if (a[i] > x) 
                h++; 
  
            // no. of elements smaller 
            // than x, that is, l. 
            else if (a[i] < x) 
                l++; 
        } 
  
        int ans = 0; 
        if (l > h)  
            ans = l - h; 
        else if (l < h)  
            ans = h - l - 1; 
      
        // subtract the no. of elements  
        // that are equal to x. 
        return ans + 1 - e; 
    } 
  
    // Driven Program 
    public static void main(String[] args) 
    { 
        int x = 10; 
        int a[] = { 10, 20, 30 }; 
        int n = a.length; 
        System.out.println( 
                      minNumber(a, n, x)); 
    } 
} 
  
// This code is contributed by  
// Prasad Kshirsagar
```

## Python3

```py
# Python3 program to find minimum number  
# of elements to add so that its median  
# equals x. 
  
def minNumber (a, n, x): 
    l = 0
    h = 0
    e = 0
    for i in range(n): 
      
        # no. of elements equals to x, 
        # that is, e. 
        if a[i] == x: 
            e+=1
          
        # no. of elements greater than x, 
        # that is, h. 
        elif a[i] > x: 
            h+=1
          
        # no. of elements smaller than x, 
        # that is, l. 
        elif a[i] < x: 
            l+=1
      
    ans = 0; 
    if l > h: 
        ans = l - h 
    elif l < h: 
        ans = h - l - 1; 
      
    # subtract the no. of elements  
    # that are equal to x. 
    return ans + 1 - e 
  
# Driver code 
x = 10
a = [10, 20, 30] 
n = len(a) 
print(minNumber(a, n, x)) 
  
# This code is contributed 
# by "Abhishek Sharma 44"
```

## C#

```cs
// C# program to find minimum  
// number of elements to add  
// so that its median equals x. 
using System; 
  
class GFG  
{ 
public static int minNumber(int []a, 
                            int n,  
                            int x) 
{ 
    int l = 0, h = 0, e = 0; 
    for (int i = 0; i < n; i++) 
    { 
  
        // no. of elements  
        // equals to x, 
        // that is, e. 
        if (a[i] == x) 
            e++; 
  
        // no. of elements  
        // greater than x, 
        // that is, h. 
        else if (a[i] > x) 
            h++; 
  
        // no. of elements smaller 
        // than x, that is, l. 
        else if (a[i] < x) 
            l++; 
    } 
  
    int ans = 0; 
    if (l > h)  
        ans = l - h; 
    else if (l < h)  
        ans = h - l - 1; 
  
    // subtract the no.  
    // of elements that 
    // are equal to x. 
    return ans + 1 - e; 
} 
  
// Driver Code 
public static void Main() 
{ 
    int x = 10; 
    int []a = {10, 20, 30}; 
    int n = a.Length; 
    Console.WriteLine( 
                minNumber(a, n, x)); 
} 
} 
  
// This code is contributed 
// by anuj_67.
```

## PHP

```php
<?php 
// PHP program to find minimum  
// number of elements to add so   
// that its median equals x. 
  
function minNumber($a, $n, $x) 
{ 
    $l = 0; $h = 0; $e = 0; 
    for ($i = 0; $i < $n; $i++) 
    { 
  
        // no. of elements equals   
        // to x, that is, e. 
        if ($a[$i] == $x) 
            $e++; 
  
        // no. of elements greater 
        // than x, that is, h. 
        else if ($a[$i] > $x) 
            $h++; 
  
        // no. of elements smaller  
        // than x, that is, l. 
        else if ($a[$i] < $x) 
            $l++; 
    } 
  
    $ans = 0; 
    if ($l > $h)  
        $ans = $l - $h; 
    else if ($l < $h)  
        $ans = $h - $l - 1; 
      
    // subtract the no. of elements  
    // that are equal to x. 
    return $ans + 1 - $e; 
} 
  
// Driver code 
$x = 10; 
$a = array (10, 20, 30); 
$n = sizeof($a) ; 
echo minNumber($a, $n, $x), "\n"; 
  
// This code is contributed by jit_t 
?>
```

输出：

```
1
```

时间复杂度：`O(n)`。