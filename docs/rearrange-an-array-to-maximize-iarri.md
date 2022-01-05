# 重新排列一个数组，使 i*arr[i]

最大化

> 原文:[https://www . geeksforgeeks . org/重排数组以最大化-iarri/](https://www.geeksforgeeks.org/rearrange-an-array-to-maximize-iarri/)

给定一个 N 个整数的数组，你必须以任何顺序选择所有这些整数。对于您选择的每个整数，您得到的点数等于:**所选整数*当前整数之前所选整数的数量。**你的任务就是将这些点最大化。
**注意:**可以选择每一个整数正好 1 次。
**例:**

> **输入** : a = {1，4，2，3，9}
> **输出** : 56
> 这个数组的最优解是选择顺序为 1，2，3，4，9 的数字，这些数字分别给出 0，2，6，12，36 点，总的最大点数为 56 点。
> **输入** : a = {1，2，2，4，9}
> **输出** : 54
> 这个数组的最优解是选择顺序为 1，2，2，4，9 的数字，分别给出 0，2，4，12，36 点，总的最大点数为 54 点。

想法是使用贪婪方法，即最大化最大元素的乘数。
我们对给定的数组进行排序，并以这种排序方式开始挑选元素，从第一个元素开始。
以下是上述方法的实施:

## C++

```
// C++ program for the Optimal Solution
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

    // Function to calculate the maximum points
    // earned by making an optimal selection on
    // the given array
    static int findOptimalSolution(int a[], int N)
    {
        // Sorting the array
        sort(a, a+N);
        // Variable to store the total points earned
        int points = 0;

        for (int i = 0; i < N; i++) {
            points += a[i] * i;
        }
        return points;
    }

    // Driver code
int main() {
    int a[] = { 1, 4, 2, 3, 9 };
    int N = sizeof(a)/sizeof(a[0]);
        cout<<(findOptimalSolution(a, N));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the Optimal Solution
import java.io.*;
import java.util.*;

class GFG {

    // Function to calculate the maximum points
    // earned by making an optimal selection on
    // the given array
    static int findOptimalSolution(int[] a, int N)
    {
        // Sorting the array
        Arrays.sort(a);

        // Variable to store the total points earned
        int points = 0;

        for (int i = 0; i < N; i++) {
            points += a[i] * i;
        }
        return points;
    }

    // Driver code
    public static void main(String args[])
    {
        int[] a = { 1, 4, 2, 3, 9 };
        int N = a.length;
        System.out.println(findOptimalSolution(a, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the Optimal Solution

# Function to calculate the maximum points
# earned by making an optimal selection on
# the given array
def findOptimalSolution(a, N) :

    # Sorting the array
    a.sort() 

    # Variable to store the total points earned
    points = 0

    for i in range(0, N):
        points += a[i] * i

    return points

if __name__ == "__main__":

    a = [1, 4, 2, 3, 9]
    N = len(a)
    print(findOptimalSolution(a, N))
```

## C#

```
//C# program for the Optimal Solution
using System;

public class GFG{

        // Function to calculate the maximum points
    // earned by making an optimal selection on
    // the given array
    static int findOptimalSolution(int[]a, int N)
    {
        // Sorting the array
        Array.Sort(a);

        // Variable to store the total points earned
        int points = 0;

        for (int i = 0; i < N; i++) {
            points += a[i] * i;
        }
        return points;
    }

    // Driver code
    static public void Main (){
        int[] a = { 1, 4, 2, 3, 9 };
        int N = a.Length;
        Console.WriteLine(findOptimalSolution(a, N));
    }
//This code is contributed by ajit   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for the Optimal Solution

// Function to calculate the maximum
// points earned by making an optimal
// selection on the given array
function findOptimalSolution($a, $N)
{
    // Sorting the array
    sort($a);

    // Variable to store the
    // total points earned
    $points = 0;

    for ($i = 0; $i < $N; $i++)
    {
        $points += $a[$i] * $i;
    }
    return $points;
}

// Driver code
$a = array( 1, 4, 2, 3, 9 );
$N = sizeof($a);

echo (findOptimalSolution($a, $N));

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program for the Optimal Solution

    // Function to calculate the maximum points
    // earned by making an optimal selection on
    // the given array
    function findOptimalSolution(a, N)
    {
        // Sorting the array
        a.sort(function(a, b){return a - b});

        // Variable to store the total points earned
        let points = 0;

        for (let i = 0; i < N; i++) {
            points += a[i] * i;
        }
        return points;
    }

    let a = [ 1, 4, 2, 3, 9 ];
    let N = a.length;
    document.write(findOptimalSolution(a, N));

</script>
```

**Output:** 

```
56
```