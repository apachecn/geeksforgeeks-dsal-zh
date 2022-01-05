# 具有给定元素集的矩形和正方形的可能数量

> 原文:[https://www . geeksforgeeks . org/给定元素集的可能矩形和正方形数/](https://www.geeksforgeeks.org/possible-number-of-rectangle-and-squares-with-the-given-set-of-elements/)

给定长度为**的木棒数量 **a <sub>1</sub> ，a <sub>2</sub> ，a <sub>3</sub> …a <sub>n</sub>** 。任务是计算可能的正方形和长方形的数量。
**注意:**一根棍子只能使用一次，即在任何正方形或长方形中使用。
**举例:**** 

```
**Input:** arr[] = {1, 2, 1, 2}
**Output:** 1
Rectangle with sides 1 1 2 2

**Input:** arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9}
**Output:** 0
No square or rectangle is possible
```

****方法:**下面是解决这个问题的分步算法:** 

1.  **初始化棒的数量。**
2.  **用数组中的长度初始化所有的棒。**
3.  **按递增顺序对数组进行排序。**
4.  **计算相同长度的木棒对的数量。**
5.  **将总对数除以 2，这将是可能的矩形和正方形的总数。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the possible
// rectangles and squares
int rectangleSquare(int arr[], int n)
{

    // sort all the sticks
    sort(arr, arr + n);
    int count = 0;

    // calculate all the pair of
    // sticks with same length
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] == arr[i + 1]) {
            count++;
            i++;
        }
    }

    // divide the total number of pair
    // which will be the number of possible
    // rectangle and square
    return count / 2;
}

// Driver code
int main()
{

    // initialize all the stick lengths
    int arr[] = { 2, 2, 4, 4, 4, 4, 6, 6, 6, 7, 7, 9, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << rectangleSquare(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of above approach
import java.util.Arrays;

class GFG
{

    // Function to find the possible
    // rectangles and squares
    static int rectangleSquare(int arr[], int n)
    {

        // sort all the sticks
        Arrays.sort(arr);
        int count = 0;

        // calculate all the pair of
        // sticks with same length
        for (int i = 0; i < n - 1; i++)
        {
            if (arr[i] == arr[i + 1])
            {
                count++;
                i++;
            }
        }

        // divide the total number of pair
        // which will be the number of possible
        // rectangle and square
        return count / 2;
    }

    // Driver code
    public static void main(String[] args)
    {
        // initialize all the stick lengths
        int arr[] = {2, 2, 4, 4, 4, 4, 6, 6, 6, 7, 7, 9, 9};
        int n = arr.length;
        System.out.println(rectangleSquare(arr, n));
    }
}

// This code is contributed
// by PrinciRaj1992
```

## **蟒蛇 3**

```
# Python3 implementation of above approach

# Function to find the possible
# rectangles and squares
def rectangleSquare( arr, n):

    # sort all the sticks
    arr.sort()
    count = 0
    #print(" xx",arr[6])
    # calculate all the pair of
    # sticks with same length
    k=0
    for i in range(n-1):
        if(k==1):
            k=0
            continue

        if (arr[i] == arr[i + 1]):

            count=count+1

            k=1

    # divide the total number of pair
    # which will be the number of possible
    # rectangle and square
    return count/2

# Driver code

if __name__=='__main__':

# initialize all the stick lengths
    arr = [2, 2, 4, 4, 4, 4, 6, 6, 6, 7, 7, 9, 9]
    n = len(arr)

    print(rectangleSquare(arr, n))

# this code is written by ash264
```

## **C#**

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to find the possible
    // rectangles and squares
    static int rectangleSquare(int []arr, int n)
    {

        // sort all the sticks
        Array.Sort(arr);
        int count = 0;

        // calculate all the pair of
        // sticks with same length
        for (int i = 0; i < n - 1; i++)
        {
            if (arr[i] == arr[i + 1])
            {
                count++;
                i++;
            }
        }

        // divide the total number of pair
        // which will be the number of possible
        // rectangle and square
        return count / 2;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // initialize all the stick lengths
        int []arr = {2, 2, 4, 4, 4, 4, 6,
                        6, 6, 7, 7, 9, 9};
        int n = arr.Length;
        Console.WriteLine(rectangleSquare(arr, n));
    }
}

// This code has been contributed
// by Rajput-Ji
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of above approach

// Function to find the possible
// rectangles and squares
function rectangleSquare($arr, $n)
{

    // sort all the sticks
    sort($arr);
    $count = 0;

    // calculate all the pair of
    // sticks with same length
    for ($i = 0; $i < $n - 1; $i++)
    {
        if ($arr[$i] == $arr[$i + 1])
        {
            $count++;
            $i++;
        }
    }

    // divide the total number of pair
    // which will be the number of possible
    // rectangle and square
    return ($count / 2);
}

// Driver code

// initialize all the stick lengths
$arr = array(2, 2, 4, 4, 4, 4, 6,
                6, 6, 7, 7, 9, 9 );
$n = sizeof($arr);

echo rectangleSquare($arr, $n);

// This code is contributed by Sachin.
?>
```

## **java 描述语言**

```
<script>

// javascript implementation of above approach

// Function to find the possible
// rectangles and squares
function rectangleSquare(arr , n)
{

    // sort all the sticks
    arr.sort();
    var count = 0;

    // calculate all the pair of
    // sticks with same length
    for (i = 0; i < n - 1; i++)
    {
        if (arr[i] == arr[i + 1])
        {
            count++;
            i++;
        }
    }

    // divide the total number of pair
    // which will be the number of possible
    // rectangle and square
    return count / 2;
}

// Driver code
// initialize all the stick lengths
var arr = [2, 2, 4, 4, 4, 4, 6, 6, 6, 7, 7, 9, 9];
var n = arr.length;
document.write(rectangleSquare(arr, n));

// This code is contributed by 29AjayKumar

</script>
```

****Output:** 

```
3
```**