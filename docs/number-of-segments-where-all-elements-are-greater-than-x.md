# 所有元素都大于 X 的线段数

> 原文:[https://www . geesforgeks . org/segments-其中所有元素都大于-x/](https://www.geeksforgeeks.org/number-of-segments-where-all-elements-are-greater-than-x/)

给定一个由 N 个整数和一个数字 X 组成的数组，任务是找到段的数量，使得段中的所有元素都大于 X。计数不应包括重叠的段，两个或多个连续的段应被视为一个。
**例:**

> **输入** : a[] = {3，4，5，6，7，2，10，11}，X = 5
> **输出** : 2
> 两段是{6，7}和{10，11}。
> **输入** : a[] = {8，25，10，19，19，18，20，11，18}，X = 13
> **输出** : 3
> 分段为{25}、{19，19，18，20}和{18}

**方法:**初始化一个**标志**计数器为*假*，当任何大于 X 的元素出现时标记为真。当任何元素不大于 X 时，如果**标志**为*真*，则对该段进行计数。每当任何元素 *< =X* 出现时，重新初始化标志为假。
以下是上述办法的实施情况。

## C++

```
// C++ program to count the number of segments
// in which all elements are greater than X
#include <bits/stdc++.h>
using namespace std;

// Function to count number of segments
int countSegments(int a[], int n, int x)
{
    bool flag = false;

    int count = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            flag = true;
        }
        else {

            // if flag is true
            if (flag)
                count += 1;

            flag = false;
        }
    }

    // After iteration complete
    // check for the last segment
    if (flag)
        count += 1;

    return count;
}

// Driver Code
int main()
{
    int a[] = { 8, 25, 10, 19, 19, 18, 20, 11, 18 };
    int n = sizeof(a) / sizeof(a[0]);
    int x = 13;
    cout << countSegments(a, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of segments
// in which all elements are greater than X

import java.io.*;

class GFG {

// Function to count number of segments
static int countSegments(int a[], int n, int x)
{
    boolean flag = false;

    int count = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            flag = true;
        }
        else {

            // if flag is true
            if (flag)
                count += 1;

            flag = false;
        }
    }

    // After iteration complete
    // check for the last segment
    if (flag)
        count += 1;

    return count;
}

// Driver Code

    public static void main (String[] args) {
        int a[] = { 8, 25, 10, 19, 19, 18, 20, 11, 18 };
    int n =a.length;
    int x = 13;
    System.out.println(countSegments(a, n, x));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to count the number of segments
# in which all elements are greater than X

# Function to count number of segments
def countSegments(a, n, x):
    flag = False

    count = 0

    # Iterate in the array
    for i in range(n):

        # check if array element greater
        # then X or not
        if (a[i] > x):
            flag = True

        else:

            # if flag is true
            if (flag):
                count += 1

            flag = False

    # After iteration complete
    # check for the last segment
    if (flag):
        count += 1

    return count

# Driver Code
if __name__ == '__main__':
    a = [8, 25, 10, 19, 19, 18, 20, 11, 18]
    n = len(a)
    x = 13
    print(countSegments(a, n, x))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count the number of segments
// in which all elements are greater than X
using System;

public class GFG{

// Function to count number of segments
static int countSegments(int []a, int n, int x)
{
    bool flag = false;

    int count = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            flag = true;
        }
        else {

            // if flag is true
            if (flag)
                count += 1;

            flag = false;
        }
    }

    // After iteration complete
    // check for the last segment
    if (flag)
        count += 1;

    return count;
}

    static public void Main (){

    int []a = { 8, 25, 10, 19, 19, 18, 20, 11, 18 };
    int n =a.Length;
    int x = 13;
    Console.WriteLine(countSegments(a, n, x));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the number
// of segments in which all elements
// are greater than X

// Function to count number of segments
function countSegments($a, $n, $x)
{
    $flag = false;

    $count = 0;

    // Iterate in the array
    for ($i = 0; $i < $n; $i++)
    {

        // check if array element
        // greater then X or not
        if ($a[$i] > $x)
        {
            $flag = true;
        }
        else
        {

            // if flag is true
            if ($flag)
                $count += 1;

            $flag = false;
        }
    }

    // After iteration complete
    // check for the last segment
    if ($flag)
        $count += 1;

    return $count;
}

// Driver Code
$a = array( 8, 25, 10, 19, 19,
            18, 20, 11, 18 );
$n = sizeof($a);
$x = 13;
echo countSegments($a, $n, $x);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to count
    // the number of segments
       // in which all elements
    // are greater than X

    // Function to count number of segments
       function countSegments(a, n,  x)
    {
        let flag = false;

        let count = 0;

        // Iterate in the array
        for (let i = 0; i < n; i++) {

             // check if array element
            // greater then X or not
               if (a[i] > x)
            {
              flag = true;
            }
               else {

                // if flag is true
                if (flag)
                    count += 1;

                flag = false;
            }
        }

        // After iteration complete
        // check for the last segment
        if (flag)
            count += 1;

        return count;
    }

    let a = [ 8, 25, 10, 19, 19, 18, 20, 11, 18 ];
    let n = a.length;
    let x = 13;
    document.write(countSegments(a, n, x));

</script>
```

**Output:** 

```
3
```

**时间复杂度**:O(N)
T3】辅助空间: O(1)