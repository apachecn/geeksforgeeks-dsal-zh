# 完成 N 公里路程的补充次数

> 原文:[https://www . geeksforgeeks . org/n 公里旅程的补充次数/](https://www.geeksforgeeks.org/number-of-refills-to-complete-the-journey-of-n-km/)

给定一个数字 N，表示汽车在单条道路上行驶的总距离，单位为公里。在 1 公里的距离上有 N 个汽油泵(1，2，3，..n)。汽车油箱的容量是这样的，即油箱加满时，它能行驶 K 公里。汽车必须强制停在 M 个油箱处，这些油箱与起始位置的距离以 M 个整数给出。任务是找出汽车需要加满油箱的次数，包括完成 N 公里旅程的强制停车次数。
**例:**

> **输入:** N = 5，K = 2，M = 1
> arr[] = {3}
> **输出:** 2
> 汽车从 0 开始，油箱加满，行驶 2 公里，然后在 2 公里时再加满油箱。汽车在 3 点钟强制停车，如果再加满油箱。它还要行驶 2 公里才能到达 5 公里的目的地。
> **输入:** N = 10，K = 2，M = 3
> arr[] = { 6，7，8 }
> **输出:** 5
> 汽车从 0 开始，停在 2，4 处加满油箱，然后在 6，7，8 处强制停车。它从 8 公里行驶 2 公里，完成 10 公里的旅程。

**接近**:由于总行程为 N 公里，所以在一个变量中记录到目前为止所覆盖的距离，比如 **distCovered** ，该变量将被初始化为 0。将*距离*增加 K 公里，直到 ***距离*** 小于 N，因为 K 是自上次加注后车辆可以行驶的距离。此外，每次递增时，检查在**和 ***之间是否有强制停油泵，如果有，那么 ***将是 K 加上最后一个在 ***之间停油泵的强制停油泵*** 和 ***之间的强制停油泵*** + K
以下是上述方法的实施:******** 

## C++

```
// CPP program for finding the total
// number of stops for refilling to
// reach destination of N km
#include <iostream>
using namespace std;

// Function that returns the total number of
// refills made to reach the destination of N km
int countRefill(int N, int K, int M, int compulsory[])
{
    int count = 0;
    int i = 0;
    int distCovered = 0;

    // While we complete the whole journey.
    while (distCovered < N) {
        // If must visited petrol pump lie
        // between distCovered and distCovered+K.
        if (i < M && compulsory[i] <= (distCovered + K)) {
            // make last mustVisited as distCovered
            distCovered = compulsory[i];

            // increment the index of compulsory visited.
            i++;
        }

        // if no such must visited pump is
        // there then increment distCovered by K.
        else
            distCovered += K;

        // Counting the number of refill.
        if (distCovered < N)
            count++;
    }

    return count;
}

// Driver Code
int main()
{
    int N = 10;
    int K = 2;
    int M = 3;
    // compulsory petrol pumps to refill at
    int compulsory[] = { 6, 7, 8 };

    // function call that returns the answer to the problem
    cout << countRefill(N, K, M, compulsory) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding the
// total number of stops for
// refilling to reach
// destination of N km
import java.io.*;

class GFG
{

;

// Function that returns the
// total number of refills made
// to reach the destination of N km
static int countRefill(int N, int K,
                       int M, int compulsory[])
{
    int count = 0;
    int i = 0;
    int distCovered = 0;

    // While we complete
    // the whole journey.
    while (distCovered < N)
    {
        // If must visited petrol pump lie
        // between distCovered and distCovered+K.
        if (i < M && compulsory[i] <=
                                (distCovered + K))
        {
            // make last mustVisited
            // as distCovered
            distCovered = compulsory[i];

            // increment the index
            // of compulsory visited.
            i++;
        }

        // if no such must visited
        // pump is there then
        // increment distCovered by K.
        else
            distCovered += K;

        // Counting the number of refill.
        if (distCovered < N)
            count++;
    }

    return count;
}

// Driver Code
public static void main (String[] args)
{
    int N = 10;
    int K = 2;
    int M = 3;
    // compulsory petrol
    // pumps to refill at
    int compulsory[] = { 6, 7, 8 };

    // function call that returns
    // the answer to the problem
    System.out.println(countRefill(N, K,
                        M, compulsory));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program for finding the total
# number of stops for refilling to reach
# destination of N km

# Function that returns the total number of
# refills made to reach the destination of N km
def countRefill(N, K, M, compulsory):
    count = 0
    i = 0
    distCovered = 0

    # While we complete the whole journey.
    while (distCovered < N):

        # If must visited petrol pump lie
        # between distCovered and distCovered+K.
        if (i < M and compulsory[i] <= (distCovered + K)):

            # make last mustVisited as distCovered
            distCovered = compulsory[i]

            # increment the index of
            # compulsory visited.
            i += 1

        # if no such must visited pump is
        # there then increment distCovered by K.
        else:
            distCovered += K

        # Counting the number of refill.
        if (distCovered < N):
            count += 1

    return count

# Driver Code
if __name__ == '__main__':
    N = 10
    K = 2
    M = 3

    # compulsory petrol pumps to refill at
    compulsory = [6, 7, 8]

    # function call that returns the
    # answer to the problem
    print(countRefill(N, K, M, compulsory))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program for finding the
// total number of stops for
// refilling to reach
// destination of N km
using System;

class GFG
{

// Function that returns
// the total number of
// refills made to reach
// the destination of N km
static int countRefill(int N, int K,
                       int M, int []compulsory)
{
    int count = 0;
    int i = 0;
    int distCovered = 0;

    // While we complete
    // the whole journey.
    while (distCovered < N)
    {
        // If must visited petrol pump
        // lie between distCovered and
        // distCovered+K.
        if (i < M && compulsory[i] <=
                (distCovered + K))
        {
            // make last mustVisited
            // as distCovered
            distCovered = compulsory[i];

            // increment the index
            // of compulsory visited.
            i++;
        }

        // if no such must visited
        // pump is there then
        // increment distCovered by K.
        else
            distCovered += K;

        // Counting the number of refill.
        if (distCovered < N)
            count++;
    }

    return count;
}

// Driver Code
public static void Main ()
{
    int N = 10;
    int K = 2;
    int M = 3;

    // compulsory petrol
    // pumps to refill at
    int []compulsory = {6, 7, 8};

    // function call that returns
    // the answer to the problem
    Console.WriteLine(countRefill(N, K,
                       M, compulsory));
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding the total
// number of stops for refilling to
// reach destination of N km

// Function that returns the total
// number of refills made to reach
// the destination of N km
function countRefill($N, $K, $M,
                     $compulsory)
{
    $count = 0;
    $i = 0;
    $distCovered = 0;

    // While we complete
    // the whole journey.
    while ($distCovered < $N)
    {
        // If must visited petrol
        // pump lie between distCovered
        // and distCovered + K.
        if ($i < $M and $compulsory[$i] <=
                       ($distCovered + $K))
        {
            // make last mustVisited
            // as distCovered
            $distCovered = $compulsory[$i];

            // increment the index
            // of compulsory visited.
            $i++;
        }

        // if no such must visited
        // pump is there then
        // increment distCovered by K.
        else
            $distCovered += $K;

        // Counting the number
        // of refill.
        if ($distCovered < $N)
            $count++;
    }

    return $count;
}

// Driver Code
$N = 10;
$K = 2;
$M = 3;

// compulsory petrol
// pumps to refill at
$compulsory = array(6, 7, 8);

// function call that returns
// the answer to the problem
echo countRefill($N, $K, $M,
                 $compulsory) , "\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program for finding the total
// number of stops for refilling to
// reach destination of N km

// Function that returns the total number of
// refills made to reach the destination of N km
function countRefill(N, K, M, compulsory)
{
    var count = 0;
    var i = 0;
    var distCovered = 0;

    // While we complete the whole journey.
    while (distCovered < N) {
        // If must visited petrol pump lie
        // between distCovered and distCovered+K.
        if (i < M && compulsory[i] <= (distCovered + K))
        {
            // make last mustVisited as distCovered
            distCovered = compulsory[i];

            // increment the index of compulsory visited.
            i++;
        }

        // if no such must visited pump is
        // there then increment distCovered by K.
        else
            distCovered += K;

        // Counting the number of refill.
        if (distCovered < N)
            count++;
    }

    return count;
}

// Driver Code
var N = 10;
var K = 2;
var M = 3;

// compulsory petrol pumps to refill at
var compulsory = [ 6, 7, 8 ];

// function call that returns the answer to the problem
document.write( countRefill(N, K, M, compulsory));

</script>
```

**Output :** 

```
5
```

**时间复杂度**:O(N)
T3】辅助空间 : O(1)