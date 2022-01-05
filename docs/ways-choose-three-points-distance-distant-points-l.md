# 选择距离最远的三个点的方法< = L

> 原文:[https://www . geesforgeks . org/way-choose-三点-distance-distance-points-l/](https://www.geeksforgeeks.org/ways-choose-three-points-distance-distant-points-l/)

给定一组 n 个不同的点 x <sub>1</sub> 、x <sub>2</sub> 、x <sub>3</sub> … x <sub>n</sub> 都位于 X 轴上并且是一个整数 L，任务是找到选择三个点的方法的数量，使得最远处的点之间的距离小于或等于 L
**注**:顺序并不重要，即点{3，2，1}和{1，2，3}代表三个点的同一组

**示例:**

> 输入:x = {1，2，3，4}
> L = 3
> 输出:4
> **解释:**
> 选择三个点的方法使得
> 最远点之间的距离< = L 为:
> 1) {1，2，3}此处最远点之间的距离= 3–1 = 2<= L
> 2){ 1，2，4}此处最远点之间的距离= 4–1 = 3<= L
> 3 3，4}此处最远点之间的距离= 4–1 = 3<= L
> 4){ 2，3，4}此处最远点之间的距离= 4–2 = 2<= L
> **因此，总路数= 4**

**天真方法:**
首先，对点的数组进行排序，生成三元组{a，b，c}，这样 a 和 c 就是三元组中最远的点，a < b < c，因为所有的点都是不同的。我们可以生成所有可能的三元组，并检查两个最远点之间的距离是否在<= 1。如果它成立，我们就这样计数，否则我们就不这样计数

## C++

```
// C++ program to count ways to choose
// triplets such that the distance
// between the farthest points <= L
#include<bits/stdc++.h>
using namespace std;

// Returns the number of triplets with
// distance between farthest points <= L
int countTripletsLessThanL(int n, int L, int* arr)
{
    // sort to get ordered triplets so that we can
    // find the distance between farthest points
    // belonging to a triplet
    sort(arr, arr + n);

    int ways = 0;

    // generate and check for all possible
    // triplets: {arr[i], arr[j], arr[k]}
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {

                // Since the array is sorted the
                // farthest points will be a[i]
                // and a[k];
                int mostDistantDistance = arr[k] - arr[i];
                if (mostDistantDistance <= L) {
                    ways++;
                }
            }
        }
    }

    return ways;
}

// Driver Code
int main()
{
    // set of n points on the X axis
    int arr[] = { 1, 2, 3, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);
    int L = 3;
    int ans = countTripletsLessThanL(n, L, arr);
    cout << "Total Number of ways = " << ans << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count ways to choose
// triplets such that the distance
// between the farthest points <= L
import java .io.*;
import java .util.Arrays;
class GFG {

    // Returns the number of triplets with
    // distance between farthest points <= L
    static int countTripletsLessThanL(int n, int L,
                                        int []arr)
    {

        // sort to get ordered triplets
        // so that we can find the
        // distance between farthest
        // points belonging to a triplet
        Arrays.sort(arr);

        int ways = 0;

        // generate and check for all possible
        // triplets: {arr[i], arr[j], arr[k]}
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {

                    // Since the array is sorted the
                    // farthest points will be a[i]
                    // and a[k];
                    int mostDistantDistance =
                                    arr[k] - arr[i];
                    if (mostDistantDistance <= L)
                    {
                        ways++;
                    }
                }
            }
        }

        return ways;
    }

    // Driver Code
    static public void main (String[] args)
    {

        // set of n points on the X axis
        int []arr = {1, 2, 3, 4};

        int n =arr.length;
        int L = 3;
        int ans = countTripletsLessThanL(n, L, arr);
        System.out.println("Total Number of ways = "
                                             + ans);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to count ways to choose
# triplets such that the distance
# between the farthest points <= L

# Returns the number of triplets with
# distance between farthest points <= L
def countTripletsLessThanL(n, L, arr):

    # sort to get ordered triplets so that
    # we can find the distance between
    # farthest points belonging to a triplet
    arr.sort()

    ways = 0

    # generate and check for all possible
    # triplets: {arr[i], arr[j], arr[k]}
    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):

                # Since the array is sorted the
                # farthest points will be a[i]
                # and a[k];
                mostDistantDistance = arr[k] - arr[i]
                if (mostDistantDistance <= L):
                    ways += 1

    return ways

# Driver Code
if __name__ == "__main__":

    # set of n points on the X axis
    arr = [1, 2, 3, 4 ]

    n = len(arr)
    L = 3
    ans = countTripletsLessThanL(n, L, arr)
    print ("Total Number of ways =", ans)

# This code is contributed by ita_c
```

## C#

```
// C# program to count ways to choose
// triplets such that the distance
// between the farthest points <= L
using System;
class GFG {

// Returns the number of triplets with
// distance between farthest points <= L
static int countTripletsLessThanL(int n, int L,
                                     int []arr)
{

    // sort to get ordered triplets
    // so that we can find the
    // distance between farthest
    // points belonging to a triplet
    Array.Sort(arr);

    int ways = 0;

    // generate and check for all possible
    // triplets: {arr[i], arr[j], arr[k]}
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {

                // Since the array is sorted the
                // farthest points will be a[i]
                // and a[k];
                int mostDistantDistance = arr[k] - arr[i];
                if (mostDistantDistance <= L)
                {
                    ways++;
                }
            }
        }
    }

    return ways;
}

    // Driver Code
    static public void Main ()
    {

        // set of n points on the X axis
        int []arr = {1, 2, 3, 4};

        int n =arr.Length;
        int L = 3;
        int ans = countTripletsLessThanL(n, L, arr);
        Console.WriteLine("Total Number of ways = " + ans);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count ways to choose
// triplets such that the distance
// between the farthest points <= L

// Returns the number of triplets with
// distance between farthest points <= L
function countTripletsLessThanL($n, $L, $arr)
{
    // sort to get ordered triplets so that
    // we can find the distance between
    // farthest points belonging to a triplet
    sort($arr);

    $ways = 0;

    // generate and check for all possible
    // triplets: {arr[i], arr[j], arr[k]}
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = $i + 1; $j < $n; $j++)
        {
            for ($k = $j + 1; $k < $n; $k++)
            {

                // Since the array is sorted the
                // farthest points will be a[i]
                // and a[k];
                $mostDistantDistance = $arr[$k] -
                                       $arr[$i];
                if ($mostDistantDistance <= $L)
                {
                    $ways++;
                }
            }
        }
    }

    return $ways;
}

// Driver Code

// set of n points on the X axis
$arr = array( 1, 2, 3, 4 );

$n = sizeof($arr);
$L = 3;
$ans = countTripletsLessThanL($n, $L, $arr);
echo "Total Number of ways = " , $ans, "\n";

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// javascript program to count ways to choose
// triplets such that the distance
// between the farthest points <= L

    // Returns the number of triplets with
    // distance between farthest points <= L
    function countTripletsLessThanL(n , L,  arr)
    {

        // sort to get ordered triplets
        // so that we can find the
        // distance between farthest
        // points belonging to a triplet
        arr.sort();

        var ways = 0;

        // generate and check for all possible
        // triplets: {arr[i], arr[j], arr[k]}
        for (i = 0; i < n; i++) {
            for (j = i + 1; j < n; j++) {
                for (k = j + 1; k < n; k++) {

                    // Since the array is sorted the
                    // farthest points will be a[i]
                    // and a[k];
                    var mostDistantDistance = arr[k] - arr[i];
                    if (mostDistantDistance <= L) {
                        ways++;
                    }
                }
            }
        }

        return ways;
    }

    // Driver Code
        // set of n points on the X axis
        var arr = [ 1, 2, 3, 4 ];

        var n = arr.length;
        var L = 3;
        var ans = countTripletsLessThanL(n, L, arr);
        document.write("Total Number of ways = " + ans);

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
Total Number of ways = 4
```

**时间复杂度:** **O(n <sup>3</sup> )** 用于生成所有可能的三胞胎。

**有效方法:**

*   这个问题可以用二分搜索法来解决。
*   首先，对数组进行排序。
*   现在，对于数组的每个元素，我们找到大于它的元素数量(通过保持点的排序顺序)并且位于范围(x <sub>i</sub> + 1，x <sub>i</sub> + L)内(注意这里所有的点都是不同的，所以我们需要考虑等于 x <sub>i</sub> 本身的元素)。
*   这样做，我们会发现所有这样的点，其中最远的点之间的距离总是小于或等于 l。
*   现在假设对于第 I<sup>点，我们有小于或等于 x <sub>i</sub> + L 的 M 个这样的点，那么我们可以从 M 个这样的点中选择 2 个点的方法的数量就是简单的
    M *(M–1)/2</sup>

## C++

```
// C++ program to count ways to choose
// triplets such that the distance between
// the farthest points <= L */
#include<bits/stdc++.h>
using namespace std;

// Returns the number of triplets with the
// distance between farthest points <= L
int countTripletsLessThanL(int n, int L, int* arr)
{
    // sort the array
    sort(arr, arr + n);

    int ways = 0;
    for (int i = 0; i < n; i++) {

        // find index of element greater than arr[i] + L
        int indexGreater = upper_bound(arr, arr + n,
                                         arr[i] + L) - arr;

        // find Number of elements between the ith
        // index and indexGreater since the Numbers
        // are sorted and the elements are distinct
        // from the points btw these indices represent
        // points within range (a[i] + 1 and a[i] + L)
        // both inclusive

        int numberOfElements = indexGreater - (i + 1);

        // if there are at least two elements in between
        // i and indexGreater find the Number of ways
        // to select two points out of these

        if (numberOfElements >= 2) {
            ways += (numberOfElements
                        * (numberOfElements - 1) / 2);
        }
    }

    return ways;
}

// Driver Code
int main()
{
    // set of n points on the X axis
    int arr[] = { 1, 2, 3, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);
    int L = 4;

    int ans = countTripletsLessThanL(n, L, arr);

    cout << "Total Number of ways = " << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count ways to choose
// triplets such that the distance between
// the farthest points <= L */
import java.util.*;

class GFG
{

// Returns the number of triplets with the
// distance between farthest points <= L
static int countTripletsLessThanL(int n, int L,
                                  int[] arr)
{
    // sort the array
    Arrays.sort(arr);

    int ways = 0;
    for (int i = 0; i < n; i++)
    {

        // find index of element greater than arr[i] + L
        int indexGreater = upper_bound(arr, 0, n,
                                       arr[i] + L);

        // find Number of elements between the ith
        // index and indexGreater since the Numbers
        // are sorted and the elements are distinct
        // from the points btw these indices represent
        // points within range (a[i] + 1 and a[i] + L)
        // both inclusive
        int numberOfElements = indexGreater - (i + 1);

        // if there are at least two elements in between
        // i and indexGreater find the Number of ways
        // to select two points out of these

        if (numberOfElements >= 2)
        {
            ways += (numberOfElements *
                    (numberOfElements - 1) / 2);
        }
    }
    return ways;
}

static int upper_bound(int[] a, int low,
                       int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low) / 2;
        if(a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

// Driver Code
public static void main(String[] args)
{
    // set of n points on the X axis
    int arr[] = { 1, 2, 3, 4 };

    int n = arr.length;
    int L = 4;

    int ans = countTripletsLessThanL(n, L, arr);

    System.out.println("Total Number of ways = " + ans);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to count ways to choose
# triplets such that the distance between
# the farthest points <= L '''

# Returns the number of triplets with the
# distance between farthest points <= L
def countTripletsLessThanL(n, L, arr):
    # sort the array
    arr = sorted(arr);

    ways = 0;
    for i in range(n):

        # find index of element greater than arr[i] + L
        indexGreater = upper_bound(arr, 0, n, arr[i] + L);

        # find Number of elements between the ith
        # index and indexGreater since the Numbers
        # are sorted and the elements are distinct
        # from the points btw these indices represent
        # points within range (a[i] + 1 and a[i] + L)
        # both inclusive
        numberOfElements = indexGreater - (i + 1);

        # if there are at least two elements in between
        # i and indexGreater find the Number of ways
        # to select two points out of these

        if (numberOfElements >= 2):
            ways += (numberOfElements * (numberOfElements - 1) / 2);

    return ways;

def upper_bound(a, low, high, element):
    while (low < high):
        middle = int(low + (high - low) / 2);
        if (a[middle] > element):
            high = middle;
        else:
            low = middle + 1;

    return low;

# Driver Code
if __name__ == '__main__':
    # set of n points on the X axis
    arr = [1, 2, 3, 4];

    n = len(arr);
    L = 4;

    ans = countTripletsLessThanL(n, L, arr);

    print("Total Number of ways = " , ans);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program to count ways to choose
// triplets such that the distance between
// the farthest points <= L */
using System;

class GFG
{

// Returns the number of triplets with the
// distance between farthest points <= L
static int countTripletsLessThanL(int n, int L,
                                int[] arr)
{
    // sort the array
    Array.Sort(arr);

    int ways = 0;
    for (int i = 0; i < n; i++)
    {

        // find index of element greater than arr[i] + L
        int indexGreater = upper_bound(arr, 0, n,
                                    arr[i] + L);

        // find Number of elements between the ith
        // index and indexGreater since the Numbers
        // are sorted and the elements are distinct
        // from the points btw these indices represent
        // points within range (a[i] + 1 and a[i] + L)
        // both inclusive
        int numberOfElements = indexGreater - (i + 1);

        // if there are at least two elements in between
        // i and indexGreater find the Number of ways
        // to select two points out of these
        if (numberOfElements >= 2)
        {
            ways += (numberOfElements *
                    (numberOfElements - 1) / 2);
        }
    }
    return ways;
}

static int upper_bound(int[] a, int low,
                    int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low) / 2;
        if(a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

// Driver Code
public static void Main(String[] args)
{
    // set of n points on the X axis
    int []arr = { 1, 2, 3, 4 };

    int n = arr.Length;
    int L = 4;

    int ans = countTripletsLessThanL(n, L, arr);

    Console.WriteLine("Total Number of ways = " + ans);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to count ways to choose
// triplets such that the distance between
// the farthest points <= L

// Returns the number of triplets with the
// distance between farthest points <= L
function countTripletsLessThanL(n, L, arr)
{

    // Sort the array
    arr.sort(function(a, b){return a - b});

    let ways = 0;
    for(let i = 0; i < n; i++)
    {

        // Find index of element greater
        // than arr[i] + L
        let indexGreater = upper_bound(arr, 0, n,
                                       arr[i] + L);

        // Find Number of elements between the ith
        // index and indexGreater since the Numbers
        // are sorted and the elements are distinct
        // from the points btw these indices represent
        // points within range (a[i] + 1 and a[i] + L)
        // both inclusive
        let numberOfElements = indexGreater - (i + 1);

        // If there are at least two elements in between
        // i and indexGreater find the Number of ways
        // to select two points out of these
        if (numberOfElements >= 2)
        {
            ways += (numberOfElements *
                    (numberOfElements - 1) / 2);
        }
    }
    return ways;
}

function upper_bound(a, low, high, element)
{
    while(low < high)
    {
        let middle = low +
          parseInt((high - low) / 2, 10);

        if (a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

// Driver code

// Set of n points on the X axis
let arr = [ 1, 2, 3, 4 ];
let n = arr.length;
let L = 4;

let ans = countTripletsLessThanL(n, L, arr);

document.write("Total Number of ways = " + ans);

// This code is contributed by suresh07

</script>
```

**输出**

```
Total Number of ways = 4
```

时间复杂度: **O(NlogN)** 其中 N 为点数。