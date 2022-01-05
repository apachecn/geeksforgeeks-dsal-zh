# 交替打印矩阵(从左到右，然后从右到左)

> 原文:[https://www . geesforgeks . org/print-matrix-alternate-mode-left-right-right-left/](https://www.geeksforgeeks.org/print-matrix-alternate-manner-left-right-right-left/)

给定一个 2D 数组，任务是以交替的方式打印 2D(第一行从左到右，然后从右到左，依此类推)。
**例:**

```
Input : arr[][2] = {{1, 2}
                    {2, 3}}; 
Output : 1  2  3  2 

Input :arr[][3] = { { 7 , 2 , 3 },
                    { 2 , 3 , 4 },
                    { 5 , 6 ,  1 }}; 
Output : 7  2   3  4  3  2  5  6  1
```

这个问题的解决方案是运行两个循环，并以从左到右和从右到左的方式打印行。我们维护一个标志，看看当前行应该从左到右还是从右到左打印。我们在每次迭代后切换标志。

## C++

```
// C++ program to print matrix in alternate manner
#include<bits/stdc++.h>
using namespace std;
#define R 3
#define C 3

// Function for print matrix in alternate manner
void convert(int arr[R][C])
{
    bool leftToRight = true;
    for (int i=0; i<R; i++)
    {
        if (leftToRight)
        {
            for (int j=0; j<C; j++)
                printf("%d ", arr[i][j]);
        }
        else
        {
            for (int j=C-1; j>=0; j--)
                printf("%d ",arr[i][j]);
        }

        leftToRight = !leftToRight;
    }
}

// Driver code
int main()
{
    int arr[][C] =
    {
        { 1 , 2 , 3 },
        { 3 , 2 , 1 },
        { 4 , 5 , 6 },
    };

    convert(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to print matrix in alternate manner
class GFG {

    static final int R = 3;
    static final int C = 3;

// Function for print matrix in alternate manner
    static void convert(int arr[][]) {
        boolean leftToRight = true;
        for (int i = 0; i < R; i++) {
            if (leftToRight) {
                for (int j = 0; j < C; j++) {
                    System.out.printf("%d ", arr[i][j]);
                }
            } else {
                for (int j = C - 1; j >= 0; j--) {
                    System.out.printf("%d ", arr[i][j]);
                }
            }

            leftToRight = !leftToRight;
        }
    }

// Driver code
    static public void main(String[] args) {
        int arr[][]
                = {
                    {1, 2, 3},
                    {3, 2, 1},
                    {4, 5, 6},};

        convert(arr);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to print matrix
# in alternate manner
R = 3
C = 3

# Function for print matrix
# in alternate manner
def convert(arr):

    leftToRight = True
    for i in range(R):
        if (leftToRight):
            for j in range(C):
                print(arr[i][j], end = " ")

        else:
            for j in range(C - 1, -1, -1):
                print(arr[i][j], end = " ")

        leftToRight = not leftToRight

# Driver code
if __name__ == "__main__":
    arr =[[ 1 , 2 , 3 ],
          [ 3 , 2 , 1 ],
          [ 4 , 5 , 6 ]]

    convert(arr)

# This code is contributed
# by ChitraNayal
```

## C#

```

//C# program to print matrix in alternate manner
using System;
public class GFG {

    static readonly int R = 3;
    static readonly int C = 3;

// Function for print matrix in alternate manner
    static void convert(int [,]arr) {
        bool leftToRight = true;
        for (int i = 0; i < R; i++) {
            if (leftToRight) {
                for (int j = 0; j < C; j++) {
                    Console.Write(arr[i,j]+" ");
                }
            } else {
                for (int j = C - 1; j >= 0; j--) {
                    Console.Write(arr[i,j]+" ");
                }
            }

            leftToRight = !leftToRight;
        }
    }

// Driver code
    static public void Main() {
        int [,]arr
                = {
                    {1, 2, 3},
                    {3, 2, 1},
                    {4, 5, 6},};

        convert(arr);
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print matrix
// in alternate manner
$R = 3;
$C = 3;

// Function for print matrix
// in alternate manner
function convert($arr)
{
    global $R;
    global $C;
    $leftToRight = true;
    for ($i = 0; $i < $R; $i++)
    {
        if ($leftToRight)
        {
            for ($j = 0; $j < $C; $j++)
                echo $arr[$i][$j], " ";
        }
        else
        {
            for ($j = $C - 1; $j >= 0; $j--)
                echo $arr[$i][$j], " ";
        }

        $leftToRight = !$leftToRight;
    }
}

// Driver code
$arr = array(array(1 , 2 , 3 ),
             array(3 , 2 , 1 ),
             array(4 , 5 , 6 ));

convert($arr);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to print matrix in alternate manner
    let R = 3;
    let C = 3;

    // Function for print matrix in alternate manner
    function convert(arr)
    {
        let leftToRight = true;
        for (let i = 0; i < R; i++) {
            if (leftToRight) {
                for (let j = 0; j < C; j++) {
                    document.write(arr[i][j]+" ");
                }
            } else {
                for (let j = C - 1; j >= 0; j--) {
                    document.write( arr[i][j]+" ");
                }
            }

            leftToRight = !leftToRight;
        }
    }

    // Driver code
    let arr =[[ 1 , 2 , 3 ],
          [ 3 , 2 , 1 ],
          [ 4 , 5 , 6 ]]
    convert(arr)

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
1 2 3 1 2 3 4 5 6
```

**时间复杂度:**O(R * C)
T3】空间复杂度: O(1)
本文由**丹麦语 _RAZA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。