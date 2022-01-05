# 从给定的线段长度中找到中点线段

> 原文:[https://www . geeksforgeeks . org/find-中点-分段-从给定的分段-长度/](https://www.geeksforgeeks.org/find-middle-point-segment-from-given-segment-lengths/)

给定大小为 m 的数组 **arr[]** ，该数组表示不同大小的段长度。这些线段划分一条以 0 开始的线。arr[0]的值表示从 0 到 arr[0]的段，arr[1]的值表示从 arr[0]到 arr[1]的段，依此类推。
任务是找到包含中间点的线段，如果中间线段不存在，打印“-1”。
**示例:**

> **输入:** arr = {3，2，8}
> **输出:** 3
> 三段为(0，3)，(3，5)，(5，13)
> 中点为 6.5，在第三段。
> **输入:** arr = {3，2，5}
> **输出:** -1
> 中间点为 5，位于线段 2 和 3 之间。

**进场:**中点始终为 N / 2。现在，检查该点存在于哪个段中，并打印段号。如果它是任何段的开始或结束，则打印“-1”。
以下是上述办法的实施情况:

## C++

```
// C/C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns the segment for the
// middle point
 int findSegment(int n, int m, int segment_length[])
    {

        // the middle point
        double meet_point = (1.0 * n) / 2.0;
        int sum = 0;

        // stores the segment index
        int segment_number = 0;

        for (int i = 0; i < m; i++) {

            // increment sum by
            // length of the segment
            sum += segment_length[i];

            // if the middle is
            // in between two segments
            if ((double)sum == meet_point) {
                segment_number = -1;
                break;
            }

            // if sum is greater
            // than middle point
            if (sum > meet_point) {
                segment_number = i + 1;
                break;
            }
        }

        return segment_number;
    }

    // Driver code
int main() {
        int n = 13;
        int m = 3;
        int segment_length[] = { 3, 2, 8 };

        int ans = findSegment(n, m, segment_length);
        cout<<(ans);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns the segment for the
    // middle point
    static int findSegment(int n, int m, int[] segment_length)
    {

        // the middle point
        double meet_point = (1.0 * n) / 2.0;
        int sum = 0;

        // stores the segment index
        int segment_number = 0;

        for (int i = 0; i < m; i++) {

            // increment sum by
            // length of the segment
            sum += segment_length[i];

            // if the middle is
            // in between two segments
            if ((double)sum == meet_point) {
                segment_number = -1;
                break;
            }

            // if sum is greater
            // than middle point
            if (sum > meet_point) {
                segment_number = i + 1;
                break;
            }
        }

        return segment_number;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 13;
        int m = 3;
        int[] segment_length = new int[] { 3, 2, 8 };

        int ans = findSegment(n, m, segment_length);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns the segment for the
# middle point
def findSegment(n, m, segment_length):
        # the middle point
        meet_point = (1.0 * n) / 2.0
        sum = 0

        # stores the segment index
        segment_number = 0

        for i in range(0,m,1):
            # increment sum by
            # length of the segment
            sum += segment_length[i]

            # if the middle is
            # in between two segments
            if (sum == meet_point):
                segment_number = -1
                break

            # if sum is greater
            # than middle point
            if (sum > meet_point):
                segment_number = i + 1
                break

        return segment_number

# Driver code
if __name__ == '__main__':
        n = 13
        m = 3
        segment_length = [3, 2, 8]

        ans = findSegment(n, m, segment_length)
        print(ans)
# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function that returns the
// segment for the middle point
static int findSegment(int n, int m,
                       int[] segment_length)
{

    // the middle point
    double meet_point = (1.0 * n) / 2.0;
    int sum = 0;

    // stores the segment index
    int segment_number = 0;

    for (int i = 0; i < m; i++)
    {

        // increment sum by
        // length of the segment
        sum += segment_length[i];

        // if the middle is
        // in between two segments
        if ((double)sum == meet_point)
        {
            segment_number = -1;
            break;
        }

        // if sum is greater
        // than middle point
        if (sum > meet_point)
        {
            segment_number = i + 1;
            break;
        }
    }

    return segment_number;
}

// Driver code
public static void Main()
{
    int n = 13;
    int m = 3;
    int[] segment_length = new int[] { 3, 2, 8 };

    int ans = findSegment(n, m, segment_length);
    Console.WriteLine(ans);
}
}

// This code is contributed
// by shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP ementation of the approach

// Function that returns the segment
// for the middle point
function findSegment($n, $m,
                     $segment_length)
{

    // the middle point
    $meet_point = (1.0 * $n) / 2.0;
    $sum = 0;

    // stores the segment index
    $segment_number = 0;

    for ($i = 0; $i < $m; $i++)
    {

        // increment sum by
        // length of the segment
        $sum += $segment_length[$i];

        // if the middle is
        // in between two segments
        if ((double)$sum == $meet_point)
        {
            $segment_number = -1;
            break;
        }

        // if sum is greater
        // than middle point
        if ($sum > $meet_point)
        {
            $segment_number = $i + 1;
            break;
        }
    }

    return $segment_number;
}

// Driver code
$n = 13;
$m = 3;
$segment_length = array( 3, 2, 8 );

$ans = findSegment($n, $m,
                   $segment_length);
echo ($ans);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function that returns the segment for the
    // middle point
    function findSegment( n, m ,segment_length) {

        // the middle point
        let meet_point = (1.0 * n) / 2.0;
        let sum = 0;

        // stores the segment index
        let segment_number = 0, i;

        for ( i = 0; i < m; i++) {

            // increment sum by
            // length of the segment
            sum += segment_length[i];

            // if the middle is
            // in between two segments
            if ( sum == meet_point) {
                segment_number = -1;
                break;
            }

            // if sum is greater
            // than middle point
            if (sum > meet_point) {
                segment_number = i + 1;
                break;
            }
        }
        return segment_number;
    }

    // Driver code    
    let n = 13;
    let m = 3;
    let segment_length =[ 3, 2, 8 ];

    let ans = findSegment(n, m, segment_length);
    document.write(ans);

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
3
```