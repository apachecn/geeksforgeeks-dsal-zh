# 在死胡同之前收集最多硬币

> 原文： [https://www.geeksforgeeks.org/collect-maximum-coins-before-hitting-a-dead-end/](https://www.geeksforgeeks.org/collect-maximum-coins-before-hitting-a-dead-end/)

给定一个字符矩阵，其中每个单元格都具有以下值之一。

```
'C' -->  This cell has coin

'#' -->  This cell is a blocking cell. 
         We can not go anywhere from this.

'E' -->  This cell is empty. We don't get
         a coin, but we can move from here.  
```

初始位置是单元格`(0, 0)`，初始方向是正确的。

以下是跨单元移动的规则。

如果`face`是`Right`，那么我们可以移到下面的单元格：

1.  向前移动一步，即单元格`(0, j + 1)`，方向保持正确。

2.  向下移动一步，然后向左移动，即单元格`(i + 1, j)`，方向变为左。

如果脸是左，那么我们可以移动到下面的单元格：

1.  向前移动一步，即单元格`(i, j - 1)`，方向保持不变。

2.  向下移动一步并面向右，即单元格`(i + 1, j)`，方向变为正确。

最终位置可以在任何地方，最终方向也可以是任何东西。 目标是收集最多的硬币。

**示例**：

![example](img/e9221a02274b3cad4af9c80b7d9a9227.png)

**我们强烈建议您最小化浏览器，然后自己尝试。**

可以递归定义上述问题，如下所示：

```
maxCoins(i, j, d):  Maximum number of coins that can be 
                    collected if we begin at cell (i, j)
                    and direction d.
                    d can be either 0 (left) or 1 (right)

   // If this is a blocking cell, return 0\. isValid() checks
   // if i and j are valid row and column indexes.
   If (arr[i][j] == '#' or isValid(i, j) == false)
       return 0

   // Initialize result
   If (arr[i][j] == 'C')
       result = 1;
   Else 
       result = 0;

   If (d == 0) // Left direction 
       return result +  max(maxCoins(i+1, j, 1),  // Down
                            maxCoins(i, j-1, 0)); // Ahead in left

   If (d == 1) // Right direction 
       return result +  max(maxCoins(i+1, j, 1),  // Down
                            maxCoins(i, j+1, 0)); // Ahead in right

```

下面是上述递归算法的 C++ 实现。

## C++ 

```cpp

// A Naive Recursive C++ program to find maximum number of coins 
// that can be collected before hitting a dead end 
#include<bits/stdc++.h> 
using namespace std; 
#define R 5 
#define C 5 

// to check whether current cell is out of the grid or not 
bool isValid(int i, int j) 
{ 
    return (i >=0 && i < R && j >=0 && j < C); 
} 

// dir = 0 for left, dir = 1 for facing right.  This function returns 
// number of maximum coins that can be collected starting from (i, j). 
int maxCoinsRec(char arr[R][C],  int i, int j, int dir) 
{ 
    // If this is a invalid cell or if cell is a blocking cell 
    if (isValid(i,j) == false || arr[i][j] == '#') 
        return 0; 

    // Check if this cell contains the coin 'C' or if its empty 'E'. 
    int result = (arr[i][j] == 'C')? 1: 0; 

    // Get the maximum of two cases when you are facing right in this cell 
    if (dir == 1) // Direction is right 
       return result + max(maxCoinsRec(arr, i+1, j, 0),     // Down 
                             maxCoinsRec(arr, i, j+1, 1));  // Ahead in right 

    // Direction is left 
    // Get the maximum of two cases when you are facing left in this cell 
     return  result + max(maxCoinsRec(arr, i+1, j, 1),    // Down 
                           maxCoinsRec(arr, i, j-1, 0));  // Ahead in left 
} 

// Driver program to test above function 
int main() 
{ 
    char arr[R][C] = { {'E', 'C', 'C', 'C', 'C'}, 
                       {'C', '#', 'C', '#', 'E'}, 
                       {'#', 'C', 'C', '#', 'C'}, 
                       {'C', 'E', 'E', 'C', 'E'}, 
                       {'C', 'E', '#', 'C', 'E'} 
                     }; 

   // As per the question initial cell is (0, 0) and direction is 
    // right 
    cout << "Maximum number of collected coins is "
         << maxCoinsRec(arr, 0, 0, 1); 

    return 0; 
} 

```

## Python3

```py
# A Naive Recursive Python 3 program to  
# find maximum number of coins  
# that can be collected before hitting a dead end  
R= 5
C= 5
  
# to check whether current cell is out of the grid or not  
def isValid( i, j):  
  
    return (i >=0 and i < R and j >=0 and j < C)  
  
  
# dir = 0 for left, dir = 1 for facing right.  
# This function returns  
# number of maximum coins that can be collected 
# starting from (i, j).  
def maxCoinsRec(arr, i, j, dir):  
  
    # If this is a invalid cell or if cell is a blocking cell  
    if (isValid(i,j) == False or arr[i][j] == '#'):  
        return 0
  
    # Check if this cell contains the coin 'C' or if its empty 'E'.  
    if (arr[i][j] == 'C'): 
        result=1
    else: 
        result=0
  
    # Get the maximum of two cases when you are facing right in this cell  
    if (dir == 1): 
          
     # Direction is right  
        return (result + max(maxCoinsRec(arr, i+1, j, 0), 
               maxCoinsRec(arr, i, j+1, 1)))  
  
    # Direction is left  
    # Get the maximum of two cases when you are facing left in this cell  
    return (result + max(maxCoinsRec(arr, i+1, j, 1), 
           maxCoinsRec(arr, i, j-1, 0)))  
  
  
# Driver program to test above function  
if __name__=='__main__': 
    arr = [ ['E', 'C', 'C', 'C', 'C'], 
          ['C', '#', 'C', '#', 'E'], 
          ['#', 'C', 'C', '#', 'C'], 
          ['C', 'E', 'E', 'C', 'E'], 
          ['C', 'E', '#', 'C', 'E'] ]  
  
    # As per the question initial cell is (0, 0) and direction is  
    # right  
    print("Maximum number of collected coins is ", maxCoinsRec(arr, 0, 0, 1))  
  
# this code is contributed by ash264
```

输出：

```
Maximum number of collected coins is 8
```

上述解决方案递归的时间复杂度是指数的。 我们可以使用动态规划在多项式时间内解决此问题。 这个想法是使用 3 维表`dp[R][C][k]`，其中`R`是行数，`C`是列数，`d`是方向。 下面是基于动态编程的 C++ 实现。

## C++

```cpp
// A Dynamic Programming based C++ program to find maximum 
// number of coins that can be collected before hitting a 
// dead end 
#include<bits/stdc++.h> 
using namespace std; 
#define R 5 
#define C 5 
  
// to check whether current cell is out of the grid or not 
bool isValid(int i, int j) 
{ 
    return (i >=0 && i < R && j >=0 && j < C); 
} 
  
// dir = 0 for left, dir = 1 for right.  This function returns 
// number of maximum coins that can be collected starting from 
// (i, j). 
int maxCoinsUtil(char arr[R][C],  int i, int j, int dir, 
                 int dp[R][C][2]) 
{ 
    // If this is a invalid cell or if cell is a blocking cell 
    if (isValid(i,j) == false || arr[i][j] == '#') 
        return 0; 
  
    // If this subproblem is already solved than return the 
    // already evaluated answer. 
    if (dp[i][j][dir] != -1) 
       return dp[i][j][dir]; 
  
    // Check if this cell contains the coin 'C' or if its 'E'. 
    dp[i][j][dir] = (arr[i][j] == 'C')? 1: 0; 
  
    // Get the maximum of two cases when you are facing right 
    // in this cell 
    if (dir == 1) // Direction is right 
       dp[i][j][dir] += max(maxCoinsUtil(arr, i+1, j, 0, dp), // Down 
                            maxCoinsUtil(arr, i, j+1, 1, dp)); // Ahead in rught 
  
    // Get the maximum of two cases when you are facing left 
    // in this cell 
    if (dir == 0) // Direction is left 
       dp[i][j][dir] += max(maxCoinsUtil(arr, i+1, j, 1, dp),  // Down 
                            maxCoinsUtil(arr, i, j-1, 0, dp)); // Ahead in left 
  
    // return the answer 
    return dp[i][j][dir]; 
} 
  
// This function mainly creates a lookup table and calls 
// maxCoinsUtil() 
int maxCoins(char arr[R][C]) 
{ 
    // Create lookup table and initialize all values as -1 
    int dp[R][C][2]; 
    memset(dp, -1, sizeof dp); 
  
    // As per the question initial cell is (0, 0) and direction 
    // is right 
    return maxCoinsUtil(arr, 0, 0, 1, dp); 
} 
  
// Driver program to test above function 
int main() 
{ 
    char arr[R][C] = { {'E', 'C', 'C', 'C', 'C'}, 
                       {'C', '#', 'C', '#', 'E'}, 
                       {'#', 'C', 'C', '#', 'C'}, 
                       {'C', 'E', 'E', 'C', 'E'}, 
                       {'C', 'E', '#', 'C', 'E'} 
                     }; 
  
  
    cout << "Maximum number of collected coins is "
         << maxCoins(arr); 
  
    return 0; 
} 
```

输出：

```
Maximum number of collected coins is 8
```

上述解决方案的时间复杂度为`O(R x C x d)`。 由于`d`为 2，因此时间复杂度可以写为`O(R x C)`。

感谢 Gaurav Ahirwar 提出上述解决方案。