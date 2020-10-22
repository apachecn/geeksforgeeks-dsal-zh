# 每个元素是其行号和列号的绝对差的矩阵总和

> 原文： [https://www.geeksforgeeks.org/sum-matrix-element-absolute-difference-row-column-numbers/](https://www.geeksforgeeks.org/sum-matrix-element-absolute-difference-row-column-numbers/)

给定正整数`n`。 考虑一个`n`行和`n`列的矩阵，其中每个元素包含其行号和数字的绝对差。 任务是计算矩阵中每个元素的和。

**示例**：

```
Input : n = 2
Output : 2
Matrix formed with n = 2 with given constraint:
0 1
1 0
Sum of matrix = 2.

Input : n = 3
Output : 8
Matrix formed with n = 3 with given constraint:
0 1 2
1 0 1
2 1 0
Sum of matrix = 8.

```



**方法 1（暴力）**：

只需构造一个`n`行`n`列的矩阵，并以其对应的行号和列号的绝对差初始化每个单元格。 现在，找到每个单元格的总和。

以下是上述想法的实现：

## C++ 

```cpp

// C++ program to find sum of matrix in which each 
// element is absolute difference of its corresponding 
// row and column number row. 
#include<bits/stdc++.h> 
using namespace std; 

// Retuen the sum of matrix in which each element 
// is absolute difference of its corresponding row 
// and column number row 
int findSum(int n) 
{ 
    // Generate matrix 
    int arr[n][n]; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            arr[i][j] = abs(i - j); 

    // Compute sum 
    int sum = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            sum += arr[i][j]; 

    return sum; 
} 

// Driven Program 
int main() 
{ 
    int n = 3; 
    cout << findSum(n) << endl; 
    return 0; 
} 

```

## Java

```java
// Java program to find sum of matrix 
// in which each element is absolute 
// difference of its corresponding 
// row and column number row. 
import java.io.*; 
  
public class GFG { 
  
// Retuen the sum of matrix in which 
// each element is absolute difference 
// of its corresponding row and column 
// number row 
static int findSum(int n) 
{ 
      
    // Generate matrix 
    int [][]arr = new int[n][n]; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            arr[i][j] = Math.abs(i - j); 
  
    // Compute sum 
    int sum = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            sum += arr[i][j]; 
  
    return sum; 
} 
  
    // Driver Code 
    static public void main (String[] args) 
    { 
        int n = 3; 
        System.out.println(findSum(n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## Python3

```py
# Python3 program to find sum of matrix  
# in which each element is absolute  
# difference of its corresponding 
# row and column number row. 
  
# Return the sum of matrix in which each  
# element is absolute difference of its  
# corresponding row and column number row 
def findSum(n): 
  
    # Generate matrix 
    arr = [[0 for x in range(n)] 
              for y in range (n)] 
    for i in range (n): 
        for j in range (n): 
            arr[i][j] = abs(i - j) 
  
    # Compute sum 
    sum = 0
    for i in range (n): 
        for j in range(n): 
            sum += arr[i][j] 
  
    return sum
  
# Driver Code 
if __name__ == "__main__": 
  
    n = 3
    print (findSum(n)) 
      
# This code is contributed by ita_c
```

## C#

```cs
// C# program to find sum of matrix 
// in which each element is absolute 
// difference of its corresponding 
// row and column number row. 
using System; 
  
public class GFG { 
  
// Retuen the sum of matrix in which 
// each element is absolute difference 
// of its corresponding row and column 
// number row 
static int findSum(int n) 
{ 
      
// Generate matrix 
    int [,]arr = new int[n, n]; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            arr[i,j ] = Math.Abs(i - j); 
   
    // Compute sum 
    int sum = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            sum += arr[i, j]; 
   
    return sum; 
} 
  
    // Driver Code 
    static public void Main(String[] args) 
    { 
        int n = 3; 
        Console.WriteLine(findSum(n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP program to find sum of  
// matrix in which each element 
// is absolute difference of  
// its corresponding row and  
// column number row. 
  
// Retuen the sum of matrix  
// in which each element 
// is absolute difference  
// of its corresponding row 
// and column number row 
function findSum( $n) 
{ 
      
    // Generate matrix 
    $arr =array(array()); 
    for($i = 0; $i < $n; $i++) 
        for($j = 0; $j < $n; $j++) 
            $arr[$i][$j] = abs($i - $j); 
  
    // Compute sum 
    $sum = 0; 
    for($i = 0; $i < $n; $i++) 
        for ($j = 0; $j < $n; $j++) 
            $sum += $arr[$i][$j]; 
  
    return $sum; 
} 
  
    // Driver Code 
    $n = 3; 
    echo findSum($n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
8
```

方法 2（`O(n)`）：

考虑`n = 3`，形成的矩阵将是：

```
0 1 2
1 0 1
2 1 0
```

注意，由于所有`i`均等于`j`，所以主对角线始终为 0。 正好在正下方的对角线将始终为 1，因为在每个像元上，`i`比`j`大 1 或`j`比`i`大于 1，依此类推。

按照该模式，我们可以看到矩阵中所有元素的总和为每个`i`从 0 到`n`的`i * (n-i) * 2`。

下面是上述想法的实现：

## C++

```cpp
// C++ program to find sum of matrix in which 
// each element is absolute difference of its 
// corresponding row and column number row. 
#include<bits/stdc++.h> 
using namespace std; 
  
// Retuen the sum of matrix in which each 
// element is absolute difference of its 
// corresponding row and column number row 
int findSum(int n) 
{ 
    int sum = 0; 
    for (int i = 0; i < n; i++) 
        sum += i*(n-i); 
    return 2*sum; 
} 
  
// Driven Program 
int main() 
{ 
    int n = 3; 
    cout << findSum(n) << endl; 
    return 0; 
}
```

## Java

```java
// Java program to find sum of matrix in which 
// each element is absolute difference of its 
// corresponding row and column number row. 
import java.io.*; 
  
class GFG { 
  
// Retuen the sum of matrix in which each 
// element is absolute difference of its 
// corresponding row and column number row 
static int findSum(int n) 
{ 
    int sum = 0; 
    for (int i = 0; i < n; i++) 
        sum += i * (n - i); 
    return 2 * sum; 
} 
  
    // Driver Code 
    static public void main(String[] args) 
    { 
        int n = 3; 
        System.out.println(findSum(n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## C#

```cs
// C# program to find sum of matrix in which 
// each element is absolute difference of its 
// corresponding row and column number row. 
using System; 
  
class GFG { 
  
// Retuen the sum of matrix in which each 
// element is absolute difference of its 
// corresponding row and column number row 
static int findSum(int n) 
{ 
    int sum = 0; 
    for (int i = 0; i < n; i++) 
        sum += i * (n - i); 
    return 2 * sum; 
} 
  
    // Driver Code 
    static public void Main(String[] args) 
    { 
        int n = 3; 
        Console.WriteLine(findSum(n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## Python3

```py
# Python 3 program to find sum  
# of matrix in which each element  
# is absolute difference of its  
# corresponding row and column  
# number row.  
  
# Return the sum of matrix in  
# which each element is absolute  
# difference of its corresponding 
# row and column number row  
def findSum(n): 
    sum = 0
    for i in range(n): 
        sum += i * (n - i) 
    return 2 * sum
  
# Driver code 
n = 3
print(findSum(n)) 
  
# This code is contributed by Shrikant13
```

## PHP

```php
<?php 
// PHP program to find sum of matrix in which 
// each element is absolute difference of its 
// corresponding row and column number row. 
  
// Return the sum of matrix in which each 
// element is absolute difference of its 
// corresponding row and column number row 
function findSum($n) 
{ 
    $sum = 0; 
    for ( $i = 0; $i < $n; $i++) 
        $sum += $i * ($n - $i); 
    return 2 * $sum; 
} 
  
    // Driver Code 
    $n = 3; 
    echo findSum($n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
8
```

方法 3（技巧）：

考虑`n = 3`，形成的矩阵将是：

```
0 1 2
1 0 1
2 1 0
```

因此，总和`= 1 + 1 + 1 + 1 + 2 + 2`。

重新排列时，`1 + 2 + 1 + 2 + 2 = 1 + 2 + 1 + 22`。

因此，在每种情况下，我们都可以重新排列矩阵总和，使答案始终是前`n-1`个自然数的和与前`n-1`个自然数的平方和。

```
Sum of first n natural number = ((n)*(n + 1))/2.
Sum of first n natural number = ((n)*(n + 1)*(2*n + 1)/6.
```

下面是上述想法的实现：

## C++

```cpp
// C++ program to find sum of matrix in which 
// each element is absolute difference of its 
// corresponding row and column number row. 
#include<bits/stdc++.h> 
using namespace std; 
  
// Retuen the sum of matrix in which each element 
// is absolute difference of its corresponding 
// row and column number row 
int findSum(int n) 
{ 
    n--; 
    int sum = 0; 
    sum += (n*(n+1))/2; 
    sum += (n*(n+1)*(2*n + 1))/6; 
    return sum; 
} 
  
// Driven Program 
int main() 
{ 
    int n = 3; 
    cout << findSum(n) << endl; 
    return 0; 
}
```

## Java

```java
// Java program to find sum of matrix in which 
// each element is absolute difference of its 
// corresponding row and column number row. 
import java.io.*; 
  
public class GFG { 
      
// Retuen the sum of matrix in which each element 
// is absolute difference of its corresponding 
// row and column number row 
static int findSum(int n) 
{ 
    n--; 
    int sum = 0; 
    sum += (n * (n + 1)) / 2; 
    sum += (n * (n + 1) * (2 * n + 1)) / 6; 
    return sum; 
} 
  
    // Driver Code 
    static public void main (String[] args) 
    { 
        int n = 3; 
        System.out.println(findSum(n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## Python3

```py
# Python 3 program to find sum of matrix  
# in which each element is absolute  
# difference of its corresponding row  
# and column number row.  
  
# Return the sum of matrix in which  
# each element is absolute difference  
# of its corresponding row and column  
# number row  
def findSum(n): 
    n -= 1
    sum = 0
    sum += (n * (n + 1)) / 2
    sum += (n * (n + 1) * (2 * n + 1)) / 6
    return int(sum)  
  
# Driver Code 
n = 3
print(findSum(n))  
  
# This code contributed by Rajput-Ji
```

## C#

```cs
// C# program to find sum of matrix in which 
// each element is absolute difference of its 
// corresponding row and column number row. 
using System; 
  
public class GFG { 
      
// Retuen the sum of matrix in which each element 
// is absolute difference of its corresponding 
// row and column number row 
static int findSum(int n) 
{ 
    n--; 
    int sum = 0; 
    sum += (n * (n + 1)) / 2; 
    sum += (n * (n + 1) * (2 * n + 1)) / 6; 
    return sum; 
} 
  
    // Driver Code 
    static public void Main(String[] args) 
    { 
        int n = 3; 
        Console.WriteLine(findSum(n)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP program to find sum of  
// matrix in which each element  
// is absolute difference of its  
// corresponding row and column  
// number row. 
  
// Retuen the sum of matrix in  
// which each element is absolute  
// difference of its corresponding 
// row and column number row 
function findSum($n) 
{ 
    $n--; 
    $sum = 0; 
    $sum += ($n * ($n + 1)) / 2; 
    $sum += ($n * ($n + 1) *  
                  (2 * $n + 1)) / 6; 
    return $sum; 
} 
  
// Driver Code 
$n = 3; 
echo findSum($n) ; 
  
// This code is contributed 
// by nitin mittal.  
?>
```

输出：

```
8
```

来源：

<https://stackoverflow.com/questions/42043708/sum-of-matrix-in-which-each-element-is-absolute-difference-of-row-and-column>