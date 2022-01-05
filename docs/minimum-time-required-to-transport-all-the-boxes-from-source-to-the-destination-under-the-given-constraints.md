# 在给定的约束条件下，将所有箱子从源头运输到目的地所需的最短时间

> 原文:[https://www . geeksforgeeks . org/在给定限制条件下将所有箱子从源运输到目的地所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-transport-all-the-boxes-from-source-to-the-destination-under-the-given-constraints/)

给定两个数组， **box[]** 和 **truck[]，**其中 **box[i]** 代表**I<sup>th</sup>T9】box 和 **truck[i]** 代表**I<sup>th</sup>T15】truck 可以承载的最大负载。现在每辆卡车从**源到目的地****需要 **1 小时**运输一箱，从**到**再需要 1 小时**回来。现在，假设所有的箱子都保存在源头，任务是找到将所有箱子从源头运输到目的地所需的最短时间。****

**注意**总会有一段时间可以运输箱子，在任何时候都只能用卡车运输一个箱子。

**示例:**

> **输入:** box[] = {7，6，5，4，3}，卡车[] = {10，3}
> **输出:** 7
> 第 1 小时:卡车[0]运载 box[0]，卡车[1]运载 box[4]
> 第 2 小时:两辆卡车都回到了源位置。
> 现在，卡车[1]不能再运送箱子了，因为所有剩余的箱子
> 的重量都超过了卡车[1]的容量。
> 所以，卡车【0】将在总共四个小时内搬运箱子【1】和箱子【2】
> 。(源-目的地，然后目的地-源)
> 最后，方框[3]将需要一个小时才能到达目的地。
> 所以，总耗时= 2 + 4 + 1 = 7
> 
> **输入:** box[] = {10，2，16，19}，truck[] = {29，25}
> **输出:** 3

**方法:**思路是用二分搜索法对两个数组进行排序。这里的下限将是 **0** ，上限将是 **2 *大小的箱子[]** ，因为在最坏的情况下，运输所有箱子所需的时间将是 2 *大小的箱子阵列。现在计算中间值，对于每个中间值，检查装载机是否能及时运输所有箱子=中间。如果是，则将上限更新为**mid–1**，如果不是，则将下限更新为 **mid + 1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it is
// possible to transport all the boxes
// in the given amount of time
bool isPossible(int box[], int truck[],
                int n, int m, int min_time)
{
    int temp = 0;
    int count = 0;

    while (count < m) {
        for (int j = 0; j < min_time
                        && temp < n
                        && truck[count] >= box[temp];
             j += 2)
            temp++;

        count++;
    }

    // If all the boxes can be
    // transported in the given time
    if (temp == n)
        return true;

    // If all the boxes can't be
    // transported in the given time
    return false;
}

// Function to return the minimum time required
int minTime(int box[], int truck[], int n, int m)
{

    // Sort the two arrays
    sort(box, box + n);
    sort(truck, truck + m);

    int l = 0;
    int h = 2 * n;

    // Stores minimum time in which
    // all the boxes can be transported
    int min_time = 0;

    // Check for the minimum time in which
    // all the boxes can be transported
    while (l <= h) {
        int mid = (l + h) / 2;

        // If it is possible to transport all
        // the boxes in mid amount of time
        if (isPossible(box, truck, n, m, mid)) {
            min_time = mid;
            h = mid - 1;
        }
        else
            l = mid + 1;
    }

    return min_time;
}

// Driver code
int main()
{
    int box[] = { 10, 2, 16, 19 };
    int truck[] = { 29, 25 };

    int n = sizeof(box) / sizeof(int);
    int m = sizeof(truck) / sizeof(int);

    printf("%d", minTime(box, truck, n, m));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function that returns true if it is
// possible to transport all the boxes
// in the given amount of time
static boolean isPossible(int box[], int truck[],
                int n, int m, int min_time)
{
    int temp = 0;
    int count = 0;

    while (count < m)
    {
        for (int j = 0; j < min_time
                        && temp < n
                        && truck[count] >= box[temp];
            j += 2)
            temp++;

        count++;
    }

    // If all the boxes can be
    // transported in the given time
    if (temp == n)
        return true;

    // If all the boxes can't be
    // transported in the given time
    return false;
}

// Function to return the minimum time required
static int minTime(int box[], int truck[], int n, int m)
{

    // Sort the two arrays
    Arrays.sort(box);
    Arrays.sort(truck);

    int l = 0;
    int h = 2 * n;

    // Stores minimum time in which
    // all the boxes can be transported
    int min_time = 0;

    // Check for the minimum time in which
    // all the boxes can be transported
    while (l <= h) {
        int mid = (l + h) / 2;

        // If it is possible to transport all
        // the boxes in mid amount of time
        if (isPossible(box, truck, n, m, mid))
        {
            min_time = mid;
            h = mid - 1;
        }
        else
            l = mid + 1;
    }

    return min_time;
}

// Driver code
public static void main(String[] args)
{
    int box[] = { 10, 2, 16, 19 };
    int truck[] = { 29, 25 };

    int n = box.length;
    int m = truck.length;

    System.out.printf("%d", minTime(box, truck, n, m));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it is
# possible to transport all the boxes
# in the given amount of time
def isPossible(box, truck, n, m, min_time) :

    temp = 0
    count = 0

    while (count < m) :
        j = 0
        while (j < min_time and temp < n and
                    truck[count] >= box[temp] ):
            temp +=1
            j += 2

        count += 1

    # If all the boxes can be
    # transported in the given time
    if (temp == n) :
        return True

    # If all the boxes can't be
    # transported in the given time
    return False

# Function to return the minimum time required
def minTime(box, truck, n, m) :

    # Sort the two arrays
    box.sort();
    truck.sort();

    l = 0
    h = 2 * n

    # Stores minimum time in which
    # all the boxes can be transported
    min_time = 0

    # Check for the minimum time in which
    # all the boxes can be transported
    while (l <= h) :
        mid = (l + h) // 2

        # If it is possible to transport all
        # the boxes in mid amount of time
        if (isPossible(box, truck, n, m, mid)) :
            min_time = mid
            h = mid - 1

        else :

            l = mid + 1

    return min_time

# Driver code
if __name__ == "__main__" :

    box = [ 10, 2, 16, 19 ]
    truck = [ 29, 25 ]

    n = len(box)
    m = len(truck)

    print(minTime(box, truck, n, m))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if it is
// possible to transport all the boxes
// in the given amount of time
static bool isPossible(int []box, int []truck,
                int n, int m, int min_time)
{
    int temp = 0;
    int count = 0;

    while (count < m)
    {
        for (int j = 0; j < min_time
                        && temp < n
                        && truck[count] >= box[temp];
            j += 2)
            temp++;

        count++;
    }

    // If all the boxes can be
    // transported in the given time
    if (temp == n)
        return true;

    // If all the boxes can't be
    // transported in the given time
    return false;
}

// Function to return the minimum time required
static int minTime(int []box, int []truck, int n, int m)
{

    // Sort the two arrays
    Array.Sort(box);
    Array.Sort(truck);

    int l = 0;
    int h = 2 * n;

    // Stores minimum time in which
    // all the boxes can be transported
    int min_time = 0;

    // Check for the minimum time in which
    // all the boxes can be transported
    while (l <= h)
    {
        int mid = (l + h) / 2;

        // If it is possible to transport all
        // the boxes in mid amount of time
        if (isPossible(box, truck, n, m, mid))
        {
            min_time = mid;
            h = mid - 1;
        }
        else
            l = mid + 1;
    }

    return min_time;
}

// Driver code
public static void Main(String[] args)
{
    int[] box = { 10, 2, 16, 19 };
    int []truck = { 29, 25 };

    int n = box.Length;
    int m = truck.Length;

    Console.WriteLine("{0}", minTime(box, truck, n, m));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach

// Function that returns true if it is
// possible to transport all the boxes
// in the given amount of time
function isPossible($box, $truck,
                $n, $m, $min_time)
{
    $temp = 0;
    $count = 0;

    while ($count < $m)
    {
        for ( $j = 0; $j < $min_time
                        && $temp < $n
                        && $truck[$count] >= $box[$temp];
            $j += 2)
            $temp++;

        $count++;
    }

    // If all the boxes can be
    // transported in the given time
    if ($temp == $n)
        return true;

    // If all the boxes can't be
    // transported in the given time
    return false;
}

// Function to return the minimum time required
function minTime( $box, $truck, $n, $m)
{

    // Sort the two arrays
    sort($box);
    sort($truck);

    $l = 0;
    $h = 2 * $n;

    // Stores minimum time in which
    // all the boxes can be transported
    $min_time = 0;

    // Check for the minimum time in which
    // all the boxes can be transported
    while ($l <= $h) {
        $mid = intdiv(($l + $h) , 2);

        // If it is possible to transport all
        // the boxes in mid amount of time
        if (isPossible($box, $truck, $n, $m, $mid))
        {
            $min_time = $mid;
            $h = $mid - 1;
        }
        else
            $l = $mid + 1;
    }

    return $min_time;
}

// Driver code
$box = array( 10, 2, 16, 19 );
$truck = array( 29, 25 );

$n = sizeof($box);
$m = sizeof($truck);

echo minTime($box, $truck, $n, $m);

// This code is contributed by ihritik

?>
```

## java 描述语言

```
<script>

// Js implementation of the approach

// Function that returns true if it is
// possible to transport all the boxes
// in the given amount of time
function isPossible( box, truck,
                 n, m, min_time)
{
    let temp = 0;
    let count = 0;

    while (count < m) {
        for (let j = 0; j < min_time
                        && temp < n
                        && truck[count] >= box[temp];
             j += 2)
            temp++;

        count++;
    }

    // If all the boxes can be
    // transported in the given time
    if (temp == n)
        return true;

    // If all the boxes can't be
    // transported in the given time
    return false;
}

// Function to return the minimum time required
function minTime(box, truck, n, m)
{

    // Sort the two arrays
    box.sort(function(a,b){return a-b });
    truck.sort(function(a,b){return a-b });

    let l = 0;
    let h = 2 * n;

    // Stores minimum time in which
    // all the boxes can be transported
    let min_time = 0;

    // Check for the minimum time in which
    // all the boxes can be transported
    while (l <= h) {
        let mid = Math.floor((l + h) / 2);

        // If it is possible to transport all
        // the boxes in mid amount of time
        if (isPossible(box, truck, n, m, mid)) {
            min_time = mid;
            h = mid - 1;
        }
        else
            l = mid + 1;
    }

    return min_time;
}

// Driver code
let box = [ 10, 2, 16, 19 ];
let truck = [ 29, 25 ];
let n = box.length;
let m = truck.length;
document.write(minTime(box, truck, n, m));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N * log(N))
**辅助空间:** O(1)