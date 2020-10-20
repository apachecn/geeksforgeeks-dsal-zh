# 矩阵元素的总和，其中每个元素是行和列的整数除法

> 原文： [https://www.geeksforgeeks.org/sum-matrix-element-element-integer-division-row-column/](https://www.geeksforgeeks.org/sum-matrix-element-element-integer-division-row-column/)

考虑一个`NXN`矩阵，其中每个元素都是行号除以列号（整数除法），即`mat[i][j] = floor((i + 1) / (j + 1))`其中`0 <= i < n`和`0 <= j < n`。 任务是找到所有矩阵元素的和。

**示例**：

```
Input  : N = 2
Output : 4
2 X 2 matrix with given constraint:
1 0
2 1
Sum of matrix element: 4

Input  : N = 3
Output : 9

```



**方法 1（暴力）**：

运行两个循环，一个循环用于行，另一个循环用于列，并找到`i / j`的整数部分，然后添加到答案中。

以下是此方法的实现：

## C++ 

```cpp

// C++ program to find sum of matrix element 
// where each element is integer division of 
// row and column. 
#include<bits/stdc++.h> 
using namespace std; 

// Return sum of matrix element where each element 
// is division of its corresponding row and column. 
int findSum(int n) 
{ 
    int ans = 0; 
    for (int i = 1; i <= n; i++)   // for rows 
        for (int j = 1; j <= n; j++) // for columns 
            ans += (i/j); 
    return ans; 
} 

// Driven Program 
int main() 
{ 
    int N = 2; 
    cout << findSum(N) << endl; 
    return 0; 
} 

```

## Java

```
// java program to find sum of matrix 
// element where each element is integer 
// division of row and column. 
  
import java.io.*; 
  
class GFG { 
      
    // Return sum of matrix element  
    // where each element is division 
    // of its corresponding row and 
    // column. 
    static int findSum(int n) 
    { 
        int ans = 0; 
          
        // for rows 
        for (int i = 1; i <= n; i++)  
          
            // for columns 
            for (int j = 1; j <= n; j++)  
                ans += (i/j); 
                  
        return ans; 
    } 
      
    // Driven Program 
    public static void main (String[] args)  
    { 
        int N = 2; 
        System.out.println( findSum(N)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## Python3

```
# Python 3 program to find sum of  
# matrix element where each element  
# is integer division of row and column.  
  
# Return sum of matrix element  
# where each element is division  
# of its corresponding row and column.  
def findSum(N): 
    ans = 0
    for i in range(1, N + 1): 
        for j in range(1, N + 1): 
            ans += i // j 
    return ans 
  
# Driver code 
N = 2
print(findSum(N)) 
  
# This code is contributed  
# by Shrikant13
```

## C#

```
// C# program to find the sum of matrix 
// element where each element is an integer 
// division of row and column. 
using System; 
  
class GFG { 
      
    // Return sum of matrix element  
    // where each element is division 
    // of its corresponding row and 
    // column. 
    static int findSum(int n) 
    { 
        int ans = 0; 
          
        // for rows 
        for (int i = 1; i <= n; i++)  
          
            // for columns 
            for (int j = 1; j <= n; j++)  
                ans += (i/j); 
                  
        return ans; 
    } 
      
    // Driven Program 
    public static void Main ()  
    { 
        int N = 2; 
        Console.WriteLine( findSum(N)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```
<?php 
// PHP program to find sum of matrix element 
// where each element is integer division of 
// row and column. 
  
// Return sum of matrix element 
// where each element is division  
// of its corresponding row and  
// column. 
function findSum( $n) 
{ 
    $ans = 0; 
      
    // for rows 
    for($i = 1; $i <= $n; $i++)  
      
        // for columns 
        for($j = 1; $j <= $n; $j++)  
            $ans += ($i / $j); 
    return floor($ans); 
} 
  
    // Driver Code 
    $N = 2; 
    echo findSum($N); 
      
// This code is contributed by anuj_67. 
?>
```

输出：

```
4
```

方法 2（高效）：

令`N = 9`，矩阵将是：

![](https://media.geeksforgeeks.org/wp-content/uploads/sumofmatrix1.png)

观察，对于第`j`列：

```
mat[i][k] = 0, for 1 <= k < j, 1 <= i <= N
mat[i][k] = 1, for j <= k < 2*j, 1 <= i <= N
mat[i][k] = 2, for 2*j <= k < 3*j, 1 <= i <= N
...
```

因此，在第`i`列中，有`i – 1`个零，然后是`i`乘以 1，然后是`i`乘以 2，依此类推。

我们逐列遍历矩阵和求和元素。

下面是这种方法的实现：

## C++

```
// C++ program to find sum of matrix element 
// where each element is integer division of 
// row and column. 
#include<bits/stdc++.h> 
using namespace std; 
  
// Return sum of matrix element where each 
// element is division of its corresponding 
// row and column. 
int findSum(int n) 
{ 
    int ans = 0, temp = 0, num; 
  
    // For each column. 
    for (int i = 1; i <= n && temp < n; i++) 
    { 
        // count the number of elements of 
        // each column. Initialize to i -1 
        // because number of zeroes are i - 1. 
        temp = i - 1; 
  
        // For multiply 
        num = 1; 
  
        while (temp < n) 
        { 
            if (temp + i <= n) 
                ans += (i * num); 
            else
                ans += ((n - temp) * num); 
  
            temp += i; 
            num ++; 
        } 
    } 
  
    return ans; 
} 
  
// Driven Program 
int main() 
{ 
    int N = 2; 
    cout << findSum(N) << endl; 
    return 0; 
}
```

## Java

```
// java program to find sum of matrix element 
// where each element is integer division of 
// row and column. 
  
import java.io.*; 
  
class GFG { 
      
    // Return sum of matrix element where each 
    // element is division of its corresponding 
    // row and column. 
    static int findSum(int n) 
    { 
        int ans = 0, temp = 0, num; 
      
        // For each column. 
        for (int i = 1; i <= n && temp < n; i++) 
        { 
              
            // count the number of elements of 
            // each column. Initialize to i -1 
            // because number of zeroes are i - 1. 
            temp = i - 1; 
      
            // For multiply 
            num = 1; 
      
            while (temp < n) 
            { 
                if (temp + i <= n) 
                    ans += (i * num); 
                else
                    ans += ((n - temp) * num); 
      
                temp += i; 
                num ++; 
            } 
        } 
      
        return ans; 
    } 
      
    // Driven Program 
    public static void main (String[] args)  
    { 
        int N = 2; 
        System.out.println(findSum(N)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## Python3

```
# Program to find sum of matrix element  
# where each element is integer division   
# of row and column.  
  
# Return sum of matrix element where each  
# element is division of its corresponding  
# row and column.  
def findSum(n): 
    ans = 0; temp = 0; 
  
    for i in range(1, n + 1): 
  
        # count the number of elements of  
        # each column. Initialize to i -1  
        # because number of zeroes are i - 1.  
        if temp < n: 
            temp = i - 1
  
            # For multiply 
            num = 1
            while temp < n: 
                if temp + i <= n: 
                    ans += i * num 
                else: 
                    ans += (n - temp) * num 
                temp += i 
                num += 1
    return ans 
  
# Driver Code 
N = 2
print(findSum(N)) 
  
# This code is contributed by Shrikant13
```

## C#

```
// C# program to find sum of matrix  
// element where each element is  
// integer division of row and column. 
using System; 
  
class GFG  
{ 
      
    // Return sum of matrix element  
    // where each element is division  
    // of its corresponding row and column. 
    static int findSum(int n) 
    { 
        int ans = 0, temp = 0, num; 
      
        // For each column. 
        for (int i = 1; i <= n && temp < n; i++) 
        { 
              
            // count the number of elements  
            // of each column. Initialize  
            // to i -1 because number of  
            // zeroes are i - 1. 
            temp = i - 1; 
      
            // For multiply 
            num = 1; 
      
            while (temp < n) 
            { 
                if (temp + i <= n) 
                    ans += (i * num); 
                else
                    ans += ((n - temp) * num); 
      
                temp += i; 
                num ++; 
            } 
        } 
      
        return ans; 
    } 
      
    // Driver Code 
    public static void Main ()  
    { 
        int N = 2; 
        Console.WriteLine(findSum(N)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```
<?php 
// PHP program to find sum of  
// matrix element where each  
// element is integer division  
// of row and column. 
  
// Return sum of matrix element  
// where each element is division  
// of its corresponding row and column. 
function findSum( $n) 
{ 
    $ans = 0; $temp = 0; $num; 
  
    // For each column. 
    for ($i = 1; $i <= $n and 
         $temp < $n; $i++) 
    { 
        // count the number of elements  
        // of each column. Initialize  
        // to i -1 because number of  
        // zeroes are i - 1. 
        $temp = $i - 1; 
  
        // For multiply 
        $num = 1; 
  
        while ($temp < $n) 
        { 
            if ($temp + $i <= $n) 
                $ans += ($i * $num); 
            else
                $ans += (($n - $temp) *      
                                $num); 
  
            $temp += $i; 
            $num ++; 
        } 
    } 
  
    return $ans; 
} 
  
// Driver Code 
$N = 2; 
echo findSum($N); 
  
// This code is contributed by anuj_67. 
?>
```

来源：

<http://stackoverflow.com/questions/41094769/sum-of-integer-division-matrix?rq=1>