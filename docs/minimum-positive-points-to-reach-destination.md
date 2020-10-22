# 到达目的地的最小初始点

> 原文： [https://www.geeksforgeeks.org/minimum-positive-points-to-reach-destination/](https://www.geeksforgeeks.org/minimum-positive-points-to-reach-destination/)

给定一个网格，每个网格由正，负或无点组成，即零点。 仅当我们有正点（`> 0`）时，我们才能跨单元格移动。 每当我们经过一个单元格时，该单元格中的点都会添加到我们的总体点中。 我们需要找到从`(0, 0)`到达单元格`(m - 1, n - 1)`的最小初始点。

限制条件：

*   从一个单元`(i, j)`，我们可以移至`(i + 1, 0)`或`(i, j + 1)`。

*   如果您在`(i, j)`的总点是`<= 0`，我们将无法从`(i, j)`移开。

*   我们必须达到`(n - 1, m - 1)`的最小正数点，即`> 0`。

**示例**：

```
Input: points[m][n] = { {-2, -3,   3}, 
                        {-5, -10,  1}, 
                        {10,  30, -5} 
                      };
Output: 7
Explanation: 
7 is the minimum value to reach destination with 
positive throughout the path. Below is the path.

(0,0) -> (0,1) -> (0,2) -> (1, 2) -> (2, 2)

We start from (0, 0) with 7, we reach(0, 1) 
with 5, (0, 2) with 2, (1, 2) with 5, (2, 2)
with and finally we have 1 point (we needed 
greater than 0 points at the end). 
```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=91)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

乍一看，这个问题看起来与[最大/最小成本路径](https://www.geeksforgeeks.org/dynamic-programming-set-6-min-cost-path/)类似，但获得的最大总积分将不能保证最低的初始积分。 另外，在当前问题中必须强制这些点永远不会降至零或以下。 例如，假设存在从源到目标单元格的两条路径。

我们可以通过自下而上的表格填充动态规划技术来解决此问题。

*   首先，我们应维护一个与网格大小相同的 2D 数组`dp`，其中`dp[i][j]`代表最小点，可确保进入单元格`(i, j)`之前继续到达目的地的旅程。 但很明显`dp[0][0]`是我们的最终解决方案。 因此，对于此问题，我们需要从右下角到左上角填充表格。

*   现在，让我们确定离开单元格`(i, j)`所需的最低点（记住，我们正在从底部向上移动）。 只有两条路径可供选择：`(i + 1, j)`和`(i, j + 1)`。 当然，我们将选择玩家可以以较小的初始点完成其余旅程的单元。 因此，我们有：`min_Points_on_exit = min(dp[i + 1][j], dp[i][j + 1])`。

现在我们知道了如何计算`min_Points_on_exit`，但是我们需要填充表`dp[][]`以获得`dp[0][0]`中的解。

**如何计算`dp[i][j]`？**

`dp[i][j]`的值可以写成如下形式。

```
dp[i][j] = max(min_Points_on_exit – points[i][j], 1)
```

让我们看看上面的表达式如何涵盖所有情况。

*   如果`points[i][j] == 0`，则在该单元格中什么也不会获得； 玩家离开房间时的点数与进入房间时相同，即`dp[i][j] = min_Points_on_exit`。

*   如果`points[i][j] < 0`，则玩家必须在进入`(i, j)`之前获得大于`min_Points_on_exit`的积分，以补偿该单元格中丢失的积分。 最小补偿量为`–points[i][j]`，因此我们有`dp[i][j] = min_Points_on_exit – points[i][j]`。

*   如果`points[i][j] > 0`，则玩家可以进入`(i, j)`的点数最少为`min_Points_on_exit – points[i][j]`。 因为他可以在该单元格中获得`points[i][j]`点。 但是，在这种情况下，`min_Points_on_exit – points[i][j]`的值可能会降至 0 或以下。 发生这种情况时，我们必须将值裁剪为 1，以确保`dp[i][j]`保持正值：`dp [i] [j] = max(min_minsPoints_on_exit – points[i][j], 1)`。

最后返回`dp[0][0]`，这就是我们的答案。

下面是上述算法的实现。

## C++ 

```cpp

// C++ program to find minimum initial points to reach destination 
#include<bits/stdc++.h> 
#define R 3 
#define C 3 

using namespace std; 

int minInitialPoints(int points[][C]) 
{ 
    // dp[i][j] represents the minimum initial points player 
    // should have so that when starts with cell(i, j) successfully 
    // reaches the destination cell(m-1, n-1) 
    int dp[R][C]; 
    int m = R, n = C; 

    // Base case 
    dp[m-1][n-1] = points[m-1][n-1] > 0? 1: 
                   abs(points[m-1][n-1]) + 1; 

    // Fill last row and last column as base to fill 
    // entire table 
    for (int i = m-2; i >= 0; i--) 
         dp[i][n-1] = max(dp[i+1][n-1] - points[i][n-1], 1); 
    for (int j = n-2; j >= 0; j--) 
         dp[m-1][j] = max(dp[m-1][j+1] - points[m-1][j], 1); 

    // fill the table in bottom-up fashion 
    for (int i=m-2; i>=0; i--) 
    { 
        for (int j=n-2; j>=0; j--) 
        { 
            int min_points_on_exit = min(dp[i+1][j], dp[i][j+1]); 
            dp[i][j] = max(min_points_on_exit - points[i][j], 1); 
        } 
     } 

     return dp[0][0]; 
} 

// Driver Program 
int main() 
{ 

    int points[R][C] = { {-2,-3,3}, 
                      {-5,-10,1}, 
                      {10,30,-5} 
                    }; 
    cout << "Minimum Initial Points Required: "
         << minInitialPoints(points); 
    return 0; 
} 

```

## Java

```java
class min_steps 
{ 
    static int minInitialPoints(int points[][],int R,int C) 
    { 
        // dp[i][j] represents the minimum initial points player 
        // should have so that when starts with cell(i, j) successfully 
        // reaches the destination cell(m-1, n-1) 
        int dp[][] = new int[R][C]; 
        int m = R, n = C; 
       
        // Base case 
        dp[m-1][n-1] = points[m-1][n-1] > 0? 1: 
                       Math.abs(points[m-1][n-1]) + 1; 
       
        // Fill last row and last column as base to fill 
        // entire table 
        for (int i = m-2; i >= 0; i--) 
             dp[i][n-1] = Math.max(dp[i+1][n-1] - points[i][n-1], 1); 
        for (int j = n-2; j >= 0; j--) 
             dp[m-1][j] = Math.max(dp[m-1][j+1] - points[m-1][j], 1); 
       
        // fill the table in bottom-up fashion 
        for (int i=m-2; i>=0; i--) 
        { 
            for (int j=n-2; j>=0; j--) 
            { 
                int min_points_on_exit = Math.min(dp[i+1][j], dp[i][j+1]); 
                dp[i][j] = Math.max(min_points_on_exit - points[i][j], 1); 
            } 
         } 
       
         return dp[0][0]; 
    } 
  
    /* Driver program to test above function */ 
    public static void main (String args[]) 
    { 
          int points[][] = { {-2,-3,3}, 
                      {-5,-10,1}, 
                      {10,30,-5} 
                    }; 
          int R = 3,C = 3; 
          System.out.println("Minimum Initial Points Required: "+ 
                                            minInitialPoints(points,R,C) ); 
    } 
}/* This code is contributed by Rajat Mishra */
```

## Python3

```py
# Python3 program to find minimum initial 
# points to reach destination 
import math as mt 
R = 3
C = 3
  
def minInitialPoints(points): 
    ''' 
    dp[i][j] represents the minimum initial 
    points player should have so that when  
    starts with cell(i, j) successfully 
    reaches the destination cell(m-1, n-1) 
    '''
    dp = [[0 for x in range(C + 1)]  
             for y in range(R + 1)] 
    m, n = R, C 
      
    if points[m - 1][n - 1] > 0: 
        dp[m - 1][n - 1] = 1
    else: 
        dp[m - 1][n - 1] = abs(points[m - 1][n - 1]) + 1
    ''' 
    Fill last row and last column as base 
    to fill entire table 
    '''
    for i in range (m - 2, -1, -1): 
        dp[i][n - 1] = max(dp[i + 1][n - 1] -
                           points[i][n - 1], 1) 
    for i in range (2, -1, -1): 
        dp[m - 1][i] = max(dp[m - 1][i + 1] -
                           points[m - 1][i], 1) 
    ''' 
    fill the table in bottom-up fashion 
    '''
    for i in range(m - 2, -1, -1): 
        for j in range(n - 2, -1, -1): 
            min_points_on_exit = min(dp[i + 1][j], 
                                     dp[i][j + 1]) 
            dp[i][j] = max(min_points_on_exit -
                               points[i][j], 1) 
              
    return dp[0][0]  
      
# Driver code 
points = [[-2, -3, 3], 
          [-5, -10, 1], 
          [10, 30, -5]] 
  
print("Minimum Initial Points Required:",  
                minInitialPoints(points)) 
  
  
# This code is contributed by  
# Mohit kumar 29 (IIIT gwalior)
```

## C#

```cs
// C# program Minimum Initial Points 
// to Reach Destination 
using System; 
class GFG { 
      
    static int minInitialPoints(int [,]points,  
                                 int R, int C) 
    { 
          
        // dp[i][j] represents the  
        // minimum initial points  
        // player should have so  
        // that when starts with  
        // cell(i, j) successfully 
        // reaches the destination 
        // cell(m-1, n-1) 
        int [,]dp = new int[R,C]; 
        int m = R, n = C; 
      
        // Base case 
        dp[m - 1,n - 1] = points[m - 1, n - 1] > 0 ? 1: 
                     Math.Abs(points[m - 1,n - 1]) + 1; 
      
        // Fill last row and last  
        // column as base to fill 
        // entire table 
        for (int i = m-2; i >= 0; i--) 
            dp[i, n - 1] = Math.Max(dp[i + 1, n - 1] -  
                                points[i, n - 1], 1); 
        for (int j = n - 2; j >= 0; j--) 
            dp[m - 1, j] = Math.Max(dp[m - 1, j + 1] -  
                                points[m - 1, j], 1); 
      
        // fill the table in  
        // bottom-up fashion 
        for(int i = m - 2; i >= 0; i--) 
        { 
            for (int j = n - 2; j >= 0; j--) 
            { 
                int min_points_on_exit = Math.Min(dp[i + 1, j],  
                                                  dp[i, j + 1]); 
                dp[i, j] = Math.Max(min_points_on_exit -  
                                      points[i, j], 1); 
            } 
        } 
      
        return dp[0, 0]; 
    } 
  
    // Driver Code 
    public static void Main () 
    { 
        int [,]points = {{-2,-3,3}, 
                         {-5,-10,1}, 
                           {10,30,-5}}; 
        int R = 3,C = 3; 
        Console.Write("Minimum Initial Points Required: "+ 
                           minInitialPoints(points, R, C)); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// PHP program to find minimum initial 
// points to reach destination 
$R = 3; 
$C = 3; 
  
function minInitialPoints($points) 
{ 
    // dp[i][j] represents the minimum  
    // initial points player should have  
    // so that when starts with cell(i, j)  
    // successfully reaches the destination 
    // cell(m-1, n-1) 
    global $R; 
    global $C; 
    $dp[$R][$C] = array(); 
    $m = $R; 
    $n = $C; 
  
    // Base case 
    $dp[$m - 1][$n - 1] = $points[$m - 1][$n - 1] > 0 ? 1 :  
                      abs($points[$m - 1][$n - 1]) + 1; 
  
    // Fill last row and last column as  
    // base to fill entire table 
    for ($i = $m - 2; $i >= 0; $i--) 
        $dp[$i][$n - 1] = max($dp[$i + 1][$n - 1] -  
                              $points[$i][$n - 1], 1); 
    for ($j = $n - 2; $j >= 0; $j--) 
        $dp[$m - 1][$j] = max($dp[$m - 1][$j + 1] -  
                              $points[$m - 1][$j], 1); 
  
    // fill the table in bottom-up fashion 
    for ($i = $m - 2; $i >= 0; $i--) 
    { 
        for ($j = $n - 2; $j >= 0; $j--) 
        { 
            $min_points_on_exit = min($dp[$i + 1][$j],  
                                      $dp[$i][$j + 1]); 
            $dp[$i][$j] = max($min_points_on_exit -  
                              $points[$i][$j], 1); 
        } 
    } 
  
    return $dp[0][0]; 
} 
  
// Driver Code 
$points = array(array(-2, -3, 3), 
                array(-5, -10, 1), 
                array(10, 30, -5)); 
              
echo "Minimum Initial Points Required: ", 
               minInitialPoints($points); 
  
// This code is contributed by akt_mit 
?>
```

输出：

```
Minimum Initial Points Required: 7
```

