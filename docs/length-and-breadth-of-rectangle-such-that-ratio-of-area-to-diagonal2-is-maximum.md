# 矩形的长度和宽度，使得面积与 diagonal^2 的比率最大

> 原文:[https://www . geeksforgeeks . org/矩形的长度和宽度使得面积与对角线的比率最大化/](https://www.geeksforgeeks.org/length-and-breadth-of-rectangle-such-that-ratio-of-area-to-diagonal2-is-maximum/)

给定一个正整数数组。任务是从给定的数组中选择一对元素，使它们代表矩形的长度和宽度，并且其面积与其对角线的比率 <sup>2</sup> 最大。
**注**:数组必须包含矩形的所有边。也就是说，你可以从数组中选择至少出现两次的元素，因为矩形有两个相同长度的边和两个相同宽度的边。
**例:**

> **输入:** arr[] = {4，3，5，4，3，5，7}
> **输出:** 5，4
> 在所有长度和宽度对 5 中，4 将生成最大面积直径比 <sup>2</sup> 。
> **输入:** arr[] = {2，2，2，2，2}
> **输出:** 2，2
> 只有一对可能的长宽 2，2 会产生最大的面积直径比 <sup>2</sup> 。

下面给出了矩形的一些性质，这些性质是形成矩形所必须满足的。

*   只有当我们至少有一对相等的整数时，才能形成矩形。出现一次的整数不能是任何矩形的一部分。因此，在我们的解决方案中，我们将只考虑出现不止一次的整数。

*   面积与其直径的比值 <sup>2</sup> 为**lb/(l<sup>2</sup>+b<sup>2</sup>)**是一个单调递减函数
    就一个变量而言。这意味着，如果我们固定长度，那么当我们减小宽度时，得到的比率会减小，因此对于固定宽度也是如此。利用这一点，我们不需要迭代整个数组来寻找固定宽度的长度。

**算法:**

1.  给定数组排序。
2.  创建一个在数组中出现两次的整数数组(arr_pairs[])。
3.  设置长度= arr_pairs[0]，宽度= arr_pairs[0]。
4.  从 i=2 迭代到 sizeof (arr_pairs)
    *   if(长度/宽度+宽度/长度> arr _ pairs[I]/arr _ pairs[I-1]+arr _ pairs[I-1]/arr _ pairs[I])
        *   更新长度= arr_pairs[i]，宽度= arr_pairs[i-1]
5.  打印长度和宽度。

下面是上述方法的实现。

## C++

```
// CPP for finding maximum
// p^2/A ratio of rectangle
#include <bits/stdc++.h>
using namespace std;

// function to print length and breadth
void findLandB(int arr[], int n)
{
    // sort the input array
    sort(arr, arr + n);

    // create array vector of integers occurring in pairs
    vector<double> arr_pairs;
    for (int i = 0; i < n; i++) {

        // push the same pairs
        if (arr[i] == arr[i + 1]) {
            arr_pairs.push_back(arr[i]);
            i++;
        }
    }

    double length = arr_pairs[0];
    double breadth = arr_pairs[1];
    double size = arr_pairs.size();

    // calculate length and breadth as per requirement
    for (int i = 2; i < size; i++) {

        // check for given condition
        if ((length / breadth + breadth / length) > (arr_pairs[i] / arr_pairs[i - 1] + arr_pairs[i - 1] / arr_pairs[i])) {

            length = arr_pairs[i];
            breadth = arr_pairs[i - 1];
        }
    }

    // print the required answer
    cout << length << ", " << breadth << endl;
}

// Driver Code
int main()
{
    int arr[] = { 4, 2, 2, 2, 5, 6, 5, 6, 7, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findLandB(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA for finding maximum
// p^2/A ratio of rectangle
import java.util.*;

class GFG
{

// function to print length and breadth
static void findLandB(int arr[], int n)
{
    // sort the input array
    Arrays.sort(arr);

    // create array vector of integers occurring in pairs
    Vector<Double> arr_pairs = new Vector<Double>();
    for (int i = 0; i < n - 1; i++)
    {

        // push the same pairs
        if (arr[i] == arr[i + 1])
        {
            arr_pairs.add((double) arr[i]);
            i++;
        }
    }

    double length = arr_pairs.get(0);
    double breadth = arr_pairs.get(1);
    double size = arr_pairs.size();

    // calculate length and breadth as per requirement
    for (int i = 2; i < size; i++)
    {

        // check for given condition
        if ((length / breadth + breadth / length) >
            (arr_pairs.get(i) / arr_pairs.get(i - 1) +
            arr_pairs.get(i - 1) / arr_pairs.get(i)))
        {
            length = arr_pairs.get(i);
            breadth = arr_pairs.get(i - 1);
        }
    }

    // print the required answer
    System.out.print((int)length + ", " + (int)breadth +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 2, 2, 2, 5, 6, 5, 6, 7, 2 };
    int n = arr.length;
    findLandB(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 for finding maximum p^2/A
# ratio of rectangle

# function to print length and breadth
def findLandB(arr, n):

    # sort the input array
    arr.sort(reverse = False)

    # create array vector of integers
    # occurring in pairs
    arr_pairs = []
    for i in range(n - 1):

        # push the same pairs
        if (arr[i] == arr[i + 1]):
            arr_pairs.append(arr[i])
            i += 1

    length = arr_pairs[0]
    breadth = arr_pairs[1]
    size = len(arr_pairs)

    # calculate length and breadth as
    # per requirement
    for i in range(1, size - 1):

        # check for given condition
        if ((int(length / breadth) +
             int(breadth / length)) >
            (int(arr_pairs[i] / arr_pairs[i - 1]) +
             int(arr_pairs[i - 1] / arr_pairs[i]))):
            length = arr_pairs[i]
            breadth = arr_pairs[i - 1]

    # print the required answer
    print(length, ",", breadth)

# Driver Code
if __name__== '__main__':
    arr = [4, 2, 2, 2, 5, 6, 5, 6, 7, 2]
    n = len(arr)
    findLandB(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# for finding maximum
// p^2/A ratio of rectangle
using System;
using System.Collections.Generic;

class GFG
{

// function to print length and breadth
static void findLandB(int []arr, int n)
{
    // sort the input array
    Array.Sort(arr);

    // create array vector of integers occurring in pairs
    List<Double> arr_pairs = new List<Double>();
    for (int i = 0; i < n - 1; i++)
    {

        // push the same pairs
        if (arr[i] == arr[i + 1])
        {
            arr_pairs.Add((double) arr[i]);
            i++;
        }
    }

    double length = arr_pairs[0];
    double breadth = arr_pairs[1];
    double size = arr_pairs.Count;

    // calculate length and breadth as per requirement
    for (int i = 2; i < size; i++)
    {

        // check for given condition
        if ((length / breadth + breadth / length) >
            (arr_pairs[i] / arr_pairs[i - 1] +
            arr_pairs[i - 1] / arr_pairs[i]))
        {
            length = arr_pairs[i];
            breadth = arr_pairs[i - 1];
        }
    }

    // print the required answer
    Console.Write((int)length + ", " + (int)breadth +"\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 2, 2, 2, 5, 6, 5, 6, 7, 2 };
    int n = arr.Length;
    findLandB(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript for finding maximum
// p^2/A ratio of rectangle

// function to print length and breadth
function findLandB(arr, n)
{
    // sort the input array
    arr.sort();

    // create array vector of integers occurring in pairs
    var arr_pairs =[];
    for (var i = 0; i < n; i++) {

        // push the same pairs
        if (arr[i] == arr[i + 1]) {
            arr_pairs.push(arr[i]);
            i++;
        }
    }

    var length = arr_pairs[0];
    var breadth = arr_pairs[1];
    var size = arr_pairs.length;

    // calculate length and breadth as per requirement
    for (var i = 2; i < size; i++) {

        // check for given condition
        if ((length / breadth + breadth / length) > (arr_pairs[i] / arr_pairs[i - 1] + arr_pairs[i - 1] / arr_pairs[i])) {

            length = arr_pairs[i];
            breadth = arr_pairs[i - 1];
        }
    }

    // print the required answer
    document.write( length + ", " + breadth );
}

// Driver Code
var arr = [ 4, 2, 2, 2, 5, 6, 5, 6, 7, 2 ];
var n = arr.length;
findLandB(arr, n);

</script>
```

**Output:** 

```
2, 2
```

**时间复杂度:** O(N * log N)