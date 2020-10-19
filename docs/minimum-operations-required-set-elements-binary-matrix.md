# 设置二进制矩阵的所有元素所需的最少操作

> 原文： [https://www.geeksforgeeks.org/minimum-operations-required-set-elements-binary-matrix/](https://www.geeksforgeeks.org/minimum-operations-required-set-elements-binary-matrix/)

给定`N`行和`M`列的二进制矩阵。 矩阵上允许的操作是选择任何索引`(x, y)`并在左上角为`(0, 0)`和右下角为`(x-1, y-1)`的矩形之间切换所有元素。 切换元素意味着将 1 更改为 0，将 0 更改为 1。任务是找到对矩阵的所有元素进行置位（即，使所有元素均为 1）所需的最小操作。

**示例**：

```
Input : mat[][] =  0 0 0 1 1
                   0 0 0 1 1
                   0 0 0 1 1
                   1 1 1 1 1
                   1 1 1 1 1
Output : 1
In one move, choose (3, 3) to make the
whole matrix consisting of only 1s.

Input : mat[][] =  0 0 1 1 1
                   0 0 0 1 1
                   0 0 0 1 1
                   1 1 1 1 1
                   1 1 1 1 1
Output : 3

```



这个想法是从端点`(N – 1, M – 1)`开始，然后以相反的顺序遍历矩阵。 每当我们遇到一个值为 0 的单元格时，请将其翻转。

**为什么要从终点穿过？**

假设在`(x, y)`和`(x + 1, y + 1)`单元中有 0。 您不应该在单元格`(x, y)`之后翻转单元格`(x + 1, y + 1)`，因为在将`(x, y)`翻转为 1 之后，下一步是翻转`(x + 1, y + 1)`单元格 ，您将再次将`(x, y)`翻转为 0。因此，从第一步开始翻转`(x, y)`单元格没有任何好处。

以下是此方法的实现：

## C++ 

```cpp

// C++ program to find minimum operations required 
// to set all the element of binary matrix 
#include <bits/stdc++.h> 
#define N 5 
#define M 5 
using namespace std; 

// Return minimum operation required to make all 1s. 
int minOperation(bool arr[N][M]) 
{ 
    int ans = 0; 
    for (int i = N - 1; i >= 0; i--) 
    { 
        for (int j = M - 1; j >= 0; j--) 
        { 
            // check if this cell equals 0 
            if(arr[i][j] == 0) 
            { 
                // increase the number of moves 
                ans++; 

                // flip from this cell to the start point 
                for (int k = 0; k <= i; k++) 
                { 
                    for (int h = 0; h <= j; h++) 
                    { 
                        // flip the cell 
                        if (arr[k][h] == 1) 
                            arr[k][h] = 0; 
                        else
                            arr[k][h] = 1; 
                    } 
                } 
            } 
        } 
    } 
    return ans; 
} 

// Driven Program 
int main() 
{ 
    bool mat[N][M] = 
    { 
        0, 0, 1, 1, 1, 
        0, 0, 0, 1, 1, 
        0, 0, 0, 1, 1, 
        1, 1, 1, 1, 1, 
        1, 1, 1, 1, 1 
    }; 

    cout << minOperation(mat) << endl; 

    return 0; 
} 

```

## Java

```
// Java program to find minimum operations required  
// to set all the element of binary matrix  
  
class GFG { 
  
    static final int N = 5; 
    static final int M = 5; 
  
// Return minimum operation required to make all 1s.  
    static int minOperation(boolean arr[][])  
    { 
        int ans = 0; 
        for (int i = N - 1; i >= 0; i--)  
        { 
            for (int j = M - 1; j >= 0; j--) 
            { 
                // check if this cell equals 0  
                if (arr[i][j] == false)  
                { 
                    // increase the number of moves  
                    ans++; 
  
                    // flip from this cell to the start point  
                    for (int k = 0; k <= i; k++) 
                    { 
                        for (int h = 0; h <= j; h++)  
                        { 
                            // flip the cell  
                            if (arr[k][h] == true)  
                            { 
                                arr[k][h] = false; 
                            } else { 
                                arr[k][h] = true; 
                            } 
                        } 
                    } 
                } 
            } 
        } 
        return ans; 
    } 
  
// Driven Program  
    public static void main(String[] args) { 
  
        boolean mat[][] 
                = { 
                    {false, false, true, true, true}, 
                    {false, false, false, true, true}, 
                    {false, false, false, true, true}, 
                    {true, true, true, true, true}, 
                    {true, true, true, true, true} 
                }; 
  
        System.out.println(minOperation(mat)); 
    } 
} 
  
// This code is contributed  
// by PrinciRaj1992
```

## Python 3

```
# Python 3 program to find 
# minimum operations required 
# to set all the element of 
# binary matrix 
  
# Return minimum operation  
# required to make all 1s. 
def minOperation(arr): 
    ans = 0
    for i in range(N - 1, -1, -1): 
        for j in range(M - 1, -1, -1): 
              
            # check if this  
            # cell equals 0 
            if(arr[i][j] == 0): 
      
                # increase the 
                # number of moves 
                ans += 1
  
                # flip from this cell  
                # to the start point 
                for k in range(i + 1): 
                    for h in range(j + 1): 
                      
                        # flip the cell 
                        if (arr[k][h] == 1): 
                            arr[k][h] = 0
                        else: 
                            arr[k][h] = 1
                      
    return ans 
  
# Driver Code 
mat = [[ 0, 0, 1, 1, 1], 
       [0, 0, 0, 1, 1], 
       [0, 0, 0, 1, 1], 
       [1, 1, 1, 1, 1], 
       [1, 1, 1, 1, 1]] 
M = 5
N = 5
  
print(minOperation(mat)) 
  
# This code is contributed 
# by ChitraNayal
```

## C#

```
using System; 
  
// C# program to find minimum operations required   
// to set all the element of binary matrix   
  
public class GFG 
{ 
  
    public const int N = 5; 
    public const int M = 5; 
  
// Return minimum operation required to make all 1s.   
    public static int minOperation(bool[][] arr) 
    { 
        int ans = 0; 
        for (int i = N - 1; i >= 0; i--) 
        { 
            for (int j = M - 1; j >= 0; j--) 
            { 
                // check if this cell equals 0   
                if (arr[i][j] == false) 
                { 
                    // increase the number of moves   
                    ans++; 
  
                    // flip from this cell to the start point   
                    for (int k = 0; k <= i; k++) 
                    { 
                        for (int h = 0; h <= j; h++) 
                        { 
                            // flip the cell   
                            if (arr[k][h] == true) 
                            { 
                                arr[k][h] = false; 
                            } 
                            else
                            { 
                                arr[k][h] = true; 
                            } 
                        } 
                    } 
                } 
            } 
        } 
        return ans; 
    } 
  
// Driven Program   
    public static void Main(string[] args) 
    { 
  
        bool[][] mat = new bool[][] 
        { 
            new bool[] {false, false, true, true, true}, 
            new bool[] {false, false, false, true, true}, 
            new bool[] {false, false, false, true, true}, 
            new bool[] {true, true, true, true, true}, 
            new bool[] {true, true, true, true, true} 
        }; 
  
        Console.WriteLine(minOperation(mat)); 
    } 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```
<?php  
// PHP program to find minimum  
// operations required to set  
// all the element of binary matrix 
  
$N = 5; 
$M = 5; 
  
// Return minimum operation  
// required to make all 1s. 
function minOperation(&$arr) 
{ 
    global $N, $M; 
    $ans = 0; 
    for ($i = $N - 1; 
         $i >= 0; $i--) 
    { 
        for ($j = $M - 1; 
             $j >= 0; $j--) 
        { 
            // check if this 
            // cell equals 0 
            if($arr[$i][$j] == 0) 
            { 
                // increase the 
                // number of moves 
                $ans++; 
  
                // flip from this cell  
                // to the start point 
                for ($k = 0;  
                     $k <= $i; $k++) 
                { 
                    for ($h = 0; 
                         $h <= $j; $h++) 
                    { 
                        // flip the cell 
                        if ($arr[$k][$h] == 1) 
                            $arr[$k][$h] = 0; 
                        else
                            $arr[$k][$h] = 1; 
                    } 
                } 
            } 
        } 
    } 
    return $ans; 
} 
  
// Driver Code 
$mat = array(array(0, 0, 1, 1, 1), 
             array(0, 0, 0, 1, 1), 
             array(0, 0, 0, 1, 1), 
             array(1, 1, 1, 1, 1), 
             array(1, 1, 1, 1, 1)); 
  
echo minOperation($mat); 
  
// This code is contributed  
// by ChitraNayal 
?>
```

输出：

```
3
```

时间复杂度：`O(N ^ 2 * M ^ 2)`。

空间复杂度：`O(N * M)`。