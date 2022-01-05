# 在二维矩阵中打印角元素及其总和

> 原文:[https://www . geeksforgeeks . org/print-the-corner-elements-and-sum-in-a-2-d-matrix/](https://www.geeksforgeeks.org/print-the-corner-elements-and-their-sum-in-a-2-d-matrix/)

给定一个二维矩阵。任务是打印它的角元素和角元素的总和。
**例:**即

```
Input:  2   7   5   5   5   8   2
        2   4   4   8   8   3   5
        6   9   3   4   5   4   3
        7   1   3   7   4   2   8
        6   9   6   5   6   8   9
        8   6   9   9   8   3   6
Output:  Corner elements: 2 8 2 6, Corner_Sum = 18

Input:    6   4   6   9
          2   6   1   8
          5   5   2   2
          4   4   1   3
Output:   Corner elements: 6 4 9 3, Corner_Sum = 22
```

**方法:**二维矩阵中角元素的索引为:

*   左上角:arr[0][0]
*   右上角:arr[0][m-1]
*   左下角:arr[n-1][0]
*   右下角:arr[n-1][m-1]

下面是上述方法的实现。

## C++

```
// C++ program to print the corner
// elements and their sum
#include <iostream>
using namespace std;
const int n = 3;
const int m = 3;

// function to print corner elements
// their sum
void printCornerElements(int arr[][m])
{

    // print the corner elements
    cout << "left top corner: " << arr[0][0];
    cout << "\nright top corner: " << arr[0][m - 1];
    cout << "\nleft bottom corner: " << arr[n - 1][0];
    cout << "\nright bottom corner: " << arr[n - 1][m - 1];

    // print the sum of corner elements
    cout << "\n\nCorner elements Sum = "
         << arr[0][0] + arr[0][m - 1]
                + arr[n - 1][0] + arr[n - 1][m - 1];
}

// Driver Code
int main()
{

    int arr[][3] = {
        { 1, 2, 4 },
        { 5, 6, 8 },
        { 8, 3, 1 }
    };

    // Function to print the corner
    // elements and their sum
    printCornerElements(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// corner elements and their sum

class GFG
{
static final int n = 3;
static final int m = 3;

// function to print corner
// elements their sum
static void printCornerElements(int arr[][])
{

// print the corner elements
System.out.println("left top corner: " +
                             arr[0][0]);
System.out.println("right top corner: " +
                          arr[0][m - 1]);
System.out.println("left bottom corner: " +
                            arr[n - 1][0]);
System.out.println("right bottom corner: " +
                         arr[n - 1][m - 1]);

// print the sum of corner elements
System.out.print("\nCorner elements Sum = ");
System.out.println(arr[0][0] + arr[0][m - 1] +
                               arr[n - 1][0] +
                               arr[n - 1][m - 1]);
}

// Driver Code
public static void main(String args[])
{
    int arr[][] ={{1, 2, 4},
                  {5, 6, 8},
                  {8, 3, 1}};

    // Function to print the corner
    // elements and their sum
    printCornerElements(arr);
}
}

// This code is contributed
// by Ankita_Saini
```

## 蟒蛇 3

```
# Python3 program to print the corner
# elements and their sum

# function to print the
# corner element and their sum .
def printCornerElement(arr) :

    # no. of rows
    n = len(arr)

    # no. of columns
    m = len(arr[0])

    # print the corner elements
    print("left top corner :",arr[0][0])
    print("right top corner :",arr[0][m - 1])
    print("left bottom corner :",arr[n - 1][0])
    print("right bottom corner :",arr[n - 1][m - 1])

    # sum of corner elements
    corner_sum = (arr[0][0] + arr[0][m - 1] +
           arr[n - 1][0] + arr[n - 1][m - 1])

    print("\ncorner elements Sum :",corner_sum)

# driver code
if __name__ == "__main__" :

    # 2d array
    arr = [
        [1,2,4],
        [5,6,8],
        [8,3,1],
        ]
    # function calling
    printCornerElement(arr)
```

## C#

```
// C# program to print
// the corner elements
// and their sum
using System;

class GFG
{
static int n = 3;
static int m = 3;

// function to print corner
// elements their sum
static void printCornerElements(int[,] arr)
{

// print the corner elements
Console.WriteLine("left top corner: " +
                            arr[0, 0]);
Console.WriteLine("right top corner: " +
                         arr[0, m - 1]);
Console.WriteLine("left bottom corner: " +
                           arr[n - 1, 0]);
Console.WriteLine("right bottom corner: " +
                        arr[n - 1, m - 1]);

// print the sum of corner elements
Console.Write("\nCorner elements Sum = ");
Console.Write(arr[0, 0] + arr[0, m - 1] +
              arr[n - 1, 0] +
              arr[n - 1, m - 1]);
}

// Driver Code
public static void Main()
{
    int[,] arr ={{1, 2, 4},
                 {5, 6, 8},
                 {8, 3, 1}};

    // Function to print the corner
    // elements and their sum
    printCornerElements(arr);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the corner
// elements and their sum
$n = 3;
$m = 3;

// function to print corner
// elements their sum
function printCornerElements(&$arr)
{
    global $n, $m;

    // print the corner elements
    echo "left top corner: " .
                   $arr[0][0];
    echo "\nright top corner: " .
                 $arr[0][$m - 1];
    echo "\nleft bottom corner: " .
                   $arr[$n - 1][0];
    echo "\nright bottom corner: " .
               $arr[$n - 1][$m - 1];

    // print the sum of corner elements
    echo "\n\nCorner elements Sum = ".
        ($arr[0][0] + $arr[0][$m - 1] +
                      $arr[$n - 1][0] +
                 $arr[$n - 1][$m - 1]);
}

// Driver Code
$arr = array(array( 1, 2, 4 ),
             array( 5, 6, 8 ),
             array( 8, 3, 1 ));

// Function to print the corner
// elements and their sum
printCornerElements($arr);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to print the
// corner elements and their sum   
 var n = 3;
 var m = 3;

    // function to print corner
    // elements their sum
    function printCornerElements(arr)
    {

        // print the corner elements
        document.write("left top corner: " +
        arr[0][0] + "<br/>");
        document.write("right top corner: " +
        arr[0][m - 1] + "<br/>");
        document.write("left bottom corner: " +
        arr[n - 1][0] + "<br/>");
        document.write("right bottom corner: " +
        arr[n - 1][m - 1] + "<br/>");

        // print the sum of corner elements
        document.write("<br/>Corner elements Sum = ");
        document.write(arr[0][0] + arr[0][m - 1] +
        arr[n - 1][0]
        + arr[n - 1][m - 1]);
    }

    // Driver Code

        var arr = [ [ 1, 2, 4 ],
                    [ 5, 6, 8 ],
                    [ 8, 3, 1 ] ];

        // Function to print the corner
        // elements and their sum
        printCornerElements(arr);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
left top corner: 1
right top corner: 4
left bottom corner: 8
right bottom corner: 1

Corner elements Sum = 14
```