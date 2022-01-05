# 给定矩形框形成的金字塔高度

> 原文:[https://www . geeksforgeeks . org/给定矩形盒金字塔形高度/](https://www.geeksforgeeks.org/height-of-pyramid-formed-with-given-rectangular-box/)

给定长度为 **m** 的尺寸为{l，b}的矩形块阵列。我们可以通过修剪其中一个维度或两个维度，将每个矩形块成形为一个正方形块。有了这些方块，就形成了金字塔。我们的任务是找到可以形成的金字塔的最大高度。
**注:**
金字塔是通过在底部放置一个正方形块，比如说 N * N，在顶部放置另一个正方形块 N-1 * N-1，在顶部放置一个 N-2 * N-2 的正方形块，以此类推，最后在顶部放置一个 1*1 的块。这种金字塔的高度是 n。

**示例:**

> **输入:** n = 4，arr[] = {{8，8}，{2，8}，{4，2}，{2，1}}
> **输出:**金字塔高度为 3
> **说明:**
> {8，8}块可修剪为{3，3}
> {2，8}块可修剪为{2，2}或{4，2}块可修剪为{2，2}
> {2，1
> 
> **输入:** n = 5，arr[] = {{9，8}，{7，4}，{8，1}，{4，4}，{2，1}}
> **输出:**金字塔高度为 4

**进场:**

*   我们必须为每个区块制作尺寸

    ```
    l * l or b * b
    ```

*   因为我们只能修剪而不能连接，所以我们选择方块的尺寸为 **min(l，b)**
*   用每个矩形块上的最小值(l，b)创建一个数组 **a**
*   将数组 **a** 排序，并将高度初始化为 0
*   遍历数组 **a** 如果数组中的元素大于高度+ 1
    ，则将高度值增加 1。
*   返回高度

## C++

```
#include <bits/stdc++.h>
#include <iostream>

using namespace std;

// Function to return
// The height of pyramid
int pyramid(int n, int arr[][2])
{
    vector<int> a;
    int height = 0;
    for (int i = 0; i < n; i++) {
        // For every ith array
        // append the minimum value
        // between two elements
        a.push_back(min(arr[i][0], arr[i][1]));
    }
    sort(a.begin(), a.end());
    for (int i = 0; i < a.size(); i++) {
        // if the element in array is
        // greater than height then
        // increment the value the
        // value of height by 1
        if (a[i] > height)
            height++;
    }
    return height;
}

// Driver code
int main()
{
    int n = 4;
    int arr[][2] = { { 8, 8 },
                     { 8, 2 },
                     { 4, 2 },
                     { 2, 1 } };
    cout << "Height of pyramid is "
         << pyramid(n, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class Gfg {

    static int pyramid(int n, int arr[][])
    {
        int[] a = new int[n];
        int height = 0;

        for (int i = 0; i < n; i++) {

            // For every ith array
            // append the minimum value
            // between two elements
            a[i] = arr[i][0] < arr[i][1]
                       ? arr[i][0]
                       : arr[i][1];
        }

        // sorting the array
        Arrays.sort(a);
        for (int i = 0; i < n; i++) {

            // if the element in array is
            // greater than height then
            // increment the value the
            // value of height by 1
            if (a[i] > height)
                height++;
        }
        return height;
    }
    public static void main(String[] args)
    {
        int n = 4;
        int arr[][] = { { 8, 8 },
                        { 8, 2 },
                        { 4, 2 },
                        { 2, 1 } };
        System.out.println("Height of pyramid is "
                           + pyramid(n, arr));
    }
}
```

## 计算机编程语言

```
# Function to return
# The height of pyramid
def pyramid(n, arr):
    # Empty array
    a = []
    height = 0
    for i in arr:
        # For every ith array
        # append the minimum value
        # between two elements
        a.append(min(i))
    # Sort the array
    a.sort()
    # Traverse through the array a
    for i in range(len(a)):
        # if the element in array is
        # greater than height then
        # increment the value the
        # value of height by 1
        if a[i] > height:
            height = height + 1

    return height
# Driver code
if __name__ == '__main__':
    n = 4
    arr = [[8, 8], [2, 8], [4, 2], [2, 1]]
    print("Height of pyramid is", pyramid(n, arr))
```

## C#

```
using System;

class Gfg 
{ 

    static int pyramid(int n, int [,]arr) 
    { 
        int[] a = new int[n]; 
        int height = 0; 

        for (int i = 0; i < n; i++)
        { 

            // For every ith array 
            // append the minimum value 
            // between two elements 
            a[i] = arr[i, 0] < arr[i, 1] 
                    ? arr[i, 0] 
                    : arr[i, 1]; 
        } 

        // sorting the array 
        Array.Sort(a); 
        for (int i = 0; i < n; i++) 
        { 

            // if the element in array is 
            // greater than height then 
            // increment the value the 
            // value of height by 1 
            if (a[i] > height) 
                height++; 
        } 
        return height; 
    } 

    // Driver code
    public static void Main() 
    { 
        int n = 4; 
        int [,]arr = { { 8, 8 }, 
                        { 8, 2 }, 
                        { 4, 2 }, 
                        { 2, 1 } }; 

        Console.WriteLine("Height of pyramid is "
                        + pyramid(n, arr)); 
    } 
} 

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Function to return
// The height of pyramid
function pyramid(n, arr) {
    let a = new Array();
    let height = 0;
    for (let i = 0; i < n; i++) {
        // For every ith array
        // append the minimum value
        // between two elements
        a.push(Math.min(arr[i][0], arr[i][1]));
    }
    a.sort((a, b) => a - b);
    for (let i = 0; i < a.length; i++) {
        // if the element in array is
        // greater than height then
        // increment the value the
        // value of height by 1
        if (a[i] > height)
            height++;
    }
    return height;
}

// Driver code

let n = 4;
let arr = [[8, 8],
[8, 2],
[4, 2],
[2, 1]];
document.write("Height of pyramid is " + pyramid(n, arr));

</script>
```

**Output:** 

```
Height of pyramid is  3
```