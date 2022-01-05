# 计算走完一段距离的路数

> 原文:[https://www . geesforgeks . org/count-覆盖距离的途径数/](https://www.geeksforgeeks.org/count-number-of-ways-to-cover-a-distance/)

给定一个距离“dist”，计算用 1 步、2 步和 3 步走完这段距离的方法总数。

**示例:**

```
Input: n = 3
Output: 4
Explanation:
Below are the four ways
 1 step + 1 step + 1 step
 1 step + 2 step
 2 step + 1 step
 3 step

Input: n = 4
Output: 7
Explanation:
Below are the four ways
 1 step + 1 step + 1 step + 1 step
 1 step + 2 step + 1 step
 2 step + 1 step + 1 step 
 1 step + 1 step + 2 step
 2 step + 2 step
 3 step + 1 step
 1 step + 3 step
```

**<u>递归求解</u>**

*   **进场:**有 n 个楼梯，允许一个人下一步，跳过一个位置或跳过两个位置。所以有 n 个位置。这个想法是站在第 I 个位置，人可以移动 i+1，i+2，i+3 的位置。因此可以形成一个递归函数，其中在当前索引 I 处，针对 i+1、i+2 和 i+3 位置递归调用该函数。
    形成递归函数还有另一种方法。要到达位置 I，一个人必须从 i-1、i-2 或 i-3 位置跳下，在那里我是起始位置。

*   **算法:**
    1.  创建一个递归函数( *count(int n)* )，该函数只接受一个参数。
    2.  检查基本情况。如果 n 的值小于 0，则返回 0，如果 n 的值等于 0，则返回 1，因为它是起始位置。
    3.  用值 n-1、n-2 和 n-3 递归调用函数，并对返回的值求和，即*sum = count(n-1)+count(n-2)+count(n-3)*。
    4.  返回*和*的值。
*   **实施:**

## C++

```
// A naive recursive C++ program to count number of ways to cover
// a distance with 1, 2 and 3 steps
#include<iostream>
using namespace std;

// Returns count of ways to cover 'dist'
int printCountRec(int dist)
{
    // Base cases
    if (dist<0)      return 0;
    if (dist==0)  return 1;

    // Recur for all previous 3 and add the results
    return printCountRec(dist-1) +
           printCountRec(dist-2) +
           printCountRec(dist-3);
}

// driver program
int main()
{
    int dist = 4;
    cout << printCountRec(dist);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A naive recursive Java program to count number
// of ways to cover a distance with 1, 2 and 3 steps
import java.io.*;

class GFG
{
    // Function returns count of ways to cover 'dist'
    static int printCountRec(int dist)
    {
        // Base cases
        if (dist<0)   
            return 0;
        if (dist==0)   
            return 1;

        // Recur for all previous 3 and add the results
        return printCountRec(dist-1) +
               printCountRec(dist-2) +
               printCountRec(dist-3);
    }

    // driver program
    public static void main (String[] args)
    {
        int dist = 4;
        System.out.println(printCountRec(dist));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# A naive recursive Python3 program
# to count number of ways to cover
# a distance with 1, 2 and 3 steps

# Returns count of ways to
# cover 'dist'
def printCountRec(dist):

    # Base cases
    if dist < 0:
        return 0

    if dist == 0:
        return 1

    # Recur for all previous 3 and      
   # add the results
    return (printCountRec(dist-1) +
            printCountRec(dist-2) +
            printCountRec(dist-3))

# Driver code
dist = 4
print(printCountRec(dist))
# This code is contributed by Anant Agarwal.
```

## C#

```
// A naive recursive C# program to
// count number of ways to cover a
// distance with 1, 2 and 3 steps
using System;

class GFG {

    // Function returns count of
    // ways to cover 'dist'
    static int printCountRec(int dist)
    {
        // Base cases
        if (dist < 0)
            return 0;
        if (dist == 0)
            return 1;

        // Recur for all previous 3
        // and add the results
        return printCountRec(dist - 1) +
               printCountRec(dist - 2) +
               printCountRec(dist - 3);
    }

    // Driver Code
    public static void Main ()
    {
        int dist = 4;
        Console.WriteLine(printCountRec(dist));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive recursive PHP program to
// count number of ways to cover
// a distance with 1, 2 and 3 steps

// Returns count of ways to cover 'dist'
function printCountRec( $dist)
{

    // Base cases
    if ($dist<0) return 0;
    if ($dist==0) return 1;

    // Recur for all previous 3
    // and add the results
    return printCountRec($dist - 1) +
           printCountRec($dist - 2) +
           printCountRec($dist - 3);
}

    // Driver Code
    $dist = 4;
    echo printCountRec($dist);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// A naive recursive javascript program to count number of ways to cover
// a distance with 1, 2 and 3 steps

// Returns count of ways to cover 'dist'
function printCountRec(dist)
{
    // Base cases
    if (dist<0)     return 0;
    if (dist==0) return 1;

    // Recur for all previous 3 and add the results
    return printCountRec(dist-1) +
        printCountRec(dist-2) +
        printCountRec(dist-3);
}

// driver program
var dist = 4;
document.write(printCountRec(dist));

</script>
```

**输出:**

```
7
```

*   **复杂度分析:**
    *   **时间复杂度:** O(3 <sup>n</sup> )。
        上述解的时间复杂度为指数，一个接近的上限为 O(3 <sup>n</sup> )。从每个状态 3，调用一个递归函数。所以 n 个状态的上限是 O(3 <sup>n</sup> )。
    *   **空间复杂度:** O(1)。
        不需要额外空间。

**<u>高效解决方案</u>**

*   **方法:**思路类似，但可以观察到有 n 个状态但递归函数被调用 3 ^ n 次。这意味着一些状态被反复调用。所以这个想法是存储状态的值。这可以通过两种方式实现。
    *   第一种方法是保持递归结构不变，只需将值存储在 HashMap 中，每当调用该函数时，返回值存储而无需计算(自顶向下方法)。
    *   第二种方法是取一个额外的 n 大小的空间，从 1，2 开始计算状态值..到 n，即计算 I，i+1，i+2 的值，然后用它们来计算 i+3 的值(自下而上方法)。
    *   [动态规划中的重叠子问题。](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)
    *   [动态规划中的最优子结构性质。](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)
    *   [动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)
*   **算法:**
    1.  创建一个大小为 n + 1 的数组，并用 1，1，2 初始化前 3 个变量。基本情况。
    2.  运行从 3 到 n 的循环。
    3.  对于每个指数 I，计算第 I 个位置的值为*DP[I]= DP[I-1]+DP[I-2]+DP[I-3]*。
    4.  打印 dp[n]的值，作为覆盖一段距离的方式数的计数。
*   **实施:**

## C++

```
// A Dynamic Programming based C++ program to count number of ways
// to cover a distance with 1, 2 and 3 steps
#include<iostream>
using namespace std;

int printCountDP(int dist)
{
    int count[dist+1];

    // Initialize base values. There is one way to cover 0 and 1
    // distances and two ways to cover 2 distance
     count[0] = 1;
     if(dist >= 1)
            count[1] = 1;
     if(dist >= 2)
              count[2] = 2;

    // Fill the count array in bottom up manner
    for (int i=3; i<=dist; i++)
       count[i] = count[i-1] + count[i-2] + count[i-3];

    return count[dist];
}

// driver program
int main()
{
    int dist = 4;
    cout << printCountDP(dist);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based Java program
// to count number of ways to cover a distance
// with 1, 2 and 3 steps
import java.io.*;

class GFG
{
    // Function returns count of ways to cover 'dist'
    static int printCountDP(int dist)
    {
        int[] count = new int[dist+1];

        // Initialize base values. There is one way to
        // cover 0 and 1 distances and two ways to
        // cover 2 distance
        count[0] = 1;
          if(dist >= 1)
            count[1] = 1;
        if(dist >= 2)
              count[2] = 2;

        // Fill the count array in bottom up manner
        for (int i=3; i<=dist; i++)
            count[i] = count[i-1] + count[i-2] + count[i-3];

        return count[dist];
    }

    // driver program
    public static void main (String[] args)
    {
        int dist = 4;
        System.out.println(printCountDP(dist));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# A Dynamic Programming based on Python3
# program to count number of ways to
# cover a distance with 1, 2 and 3 steps

def printCountDP(dist):
    count = [0] * (dist + 1)

    # Initialize base values. There is
    # one way to cover 0 and 1 distances
    # and two ways to cover 2 distance
    count[0] = 1
    if dist >= 1 :
        count[1] = 1
    if dist >= 2 :
        count[2] = 2

    # Fill the count array in bottom
    # up manner
    for i in range(3, dist + 1):
        count[i] = (count[i-1] +
                   count[i-2] + count[i-3])

    return count[dist];

# driver program
dist = 4;
print( printCountDP(dist))

# This code is contributed by Sam007.
```

## C#

```
// A Dynamic Programming based C# program
// to count number of ways to cover a distance
// with 1, 2 and 3 steps
using System;

class GFG {

    // Function returns count of ways
    // to cover 'dist'
    static int printCountDP(int dist)
    {
        int[] count = new int[dist + 1];

        // Initialize base values. There is one
        // way to cover 0 and 1 distances
        // and two ways to cover 2 distance
        count[0] = 1;
        count[1] = 1;
        count[2] = 2;

        // Fill the count array
        // in bottom up manner
        for (int i = 3; i <= dist; i++)
            count[i] = count[i - 1] +
                       count[i - 2] +
                       count[i - 3];

        return count[dist];
    }

    // Driver Code
    public static void Main ()
    {
        int dist = 4;
        Console.WriteLine(printCountDP(dist));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based PHP program
// to count number of ways to cover a
// distance with 1, 2 and 3 steps

function printCountDP( $dist)
{
    $count = array();

    // Initialize base values. There is
    // one way to cover 0 and 1 distances
    // and two ways to cover 2 distance
    $count[0] = 1; $count[1] = 1;
    $count[2] = 2;

    // Fill the count array
    // in bottom up manner
    for ( $i = 3; $i <= $dist; $i++)
    $count[$i] = $count[$i - 1] +
                 $count[$i - 2] +
                 $count[$i - 3];

    return $count[$dist];
}

// Driver Code
$dist = 4;
echo printCountDP($dist);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// A Dynamic Programming based Javascript program
// to count number of ways to cover a distance
// with 1, 2 and 3 steps

// Function returns count of ways
// to cover 'dist'
function printCountDP(dist)
{
    let count = new Array(dist + 1);

    // Initialize base values. There is one
    // way to cover 0 and 1 distances
    // and two ways to cover 2 distance
    count[0] = 1;
    if (dist >= 1)
        count[1] = 1;
    if (dist >= 2)
        count[2] = 2;

    // Fill the count array
    // in bottom up manner
    for(let i = 3; i <= dist; i++)
        count[i] = count[i - 1] +
                   count[i - 2] +
                   count[i - 3];

    return count[dist];
}

// Driver code
let dist = 4;
document.write(printCountDP(dist));

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
7
```

*   **复杂度分析:**
    *   **时间复杂度:** O(n)。
        只需要遍历一次数组。所以时间复杂度是 O(n)
    *   **空间复杂度:** O(n)。
        要将这些值存储在 DP O(n)中，需要额外的空间。

**<u>更优解</u>**

**方法:**我们可以使用大小为 3 的数组，而不是使用大小为 n+1 的数组，因为为了计算特定步骤的路数，我们只需要最后 3 步路数。

**算法:**

1.  创建一个大小为 3 的数组，并将步骤 0，1，2 的值初始化为 1，1，2(基本情况)。
2.  运行从 3 到 n(距离)的循环。
3.  对于每个索引，计算值为路[i%3] =路[(i-1)%3] +路[(i-2)%3] +路[(i-3)%3]，并将其值存储在数组路的 i%3 索引处。如果我们正在计算索引 3 的值，那么计算的值将在索引 0，因为对于更大的索引(4，5，6…..)我们不需要索引 0 的值。
4.  返回 way 的值[n%3]。

## C++

```
// A Dynamic Programming based C++ program to count number of ways
#include<iostream>
using namespace std;

int printCountDP(int dist)
{
        //Create the array of size 3.
        int  ways[3] , n = dist;

        //Initialize the bases cases
        ways[0] = 1;
        ways[1] = 1;
        ways[2] = 2;

        //Run a loop from 3 to n
        //Bottom up approach to fill the array
        for(int i=3 ;i<=n ;i++)
            ways[i%3] = ways[(i-1)%3] + ways[(i-2)%3] + ways[(i-3)%3];

        return ways[n%3];
}

// driver program
int main()
{
    int dist = 4;
    cout << printCountDP(dist);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based Java program to count number of ways
import java.util.*;

class GFG {

static int printCountDP(int dist)
{
        // Create the array of size 3.
        int []ways = new int[3];
        int n = dist;

        // Initialize the bases cases
        ways[0] = 1;
        ways[1] = 1;
        ways[2] = 2;

        // Run a loop from 3 to n
        // Bottom up approach to fill the array
        for(int i=3 ;i<=n ;i++)
            ways[i%3] = ways[(i-1)%3] + ways[(i-2)%3] + ways[(i-3)%3];

        return ways[n%3];
}

// driver program
public static void main(String arg[])
    {
    int dist = 4;
    System.out.print(printCountDP(dist));
    }
}

// this code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# A Dynamic Programming based C++ program to count number of ways
def prCountDP( dist):

        # Create the array of size 3.
        ways = [0]*3
        n = dist

        # Initialize the bases cases
        ways[0] = 1
        ways[1] = 1
        ways[2] = 2

        # Run a loop from 3 to n
        # Bottom up approach to fill the array
        for i in range(3, n + 1):
            ways[i % 3] = ways[(i - 1) % 3] + ways[(i - 2) % 3] + ways[(i - 3) % 3]

        return ways[n % 3]

# driver program
dist = 4
print(prCountDP(dist))

# This code is contributed by shivanisinghss2110
```

## C#

```
// A Dynamic Programming based C#
// program to count number of ways
using System;

class GFG{

static int printCountDP(int dist)
{
    // Create the array of size 3.
    int []ways = new int[3];
    int n = dist;

    // Initialize the bases cases
    ways[0] = 1;
    ways[1] = 1;
    ways[2] = 2;

    // Run a loop from 3 to n
    // Bottom up approach to fill the array
    for(int i = 3; i <= n; i++)
        ways[i % 3] = ways[(i - 1) % 3] +
                      ways[(i - 2) % 3] +
                      ways[(i - 3) % 3];

    return ways[n % 3];
}

// Driver code
public static void Main(String []arg)
{
    int dist = 4;

    Console.Write(printCountDP(dist));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// A Dynamic Programming based javascript program to count number of ways

function printCountDP( dist)
{
        //Create the array of size 3.
        var  ways= [] , n = dist;
        ways.length = 3 ;

        //Initialize the bases cases
        ways[0] = 1;
        ways[1] = 1;
        ways[2] = 2;

        //Run a loop from 3 to n
        //Bottom up approach to fill the array
        for(var i=3 ;i<=n ;i++)
            ways[i%3] = ways[(i-1)%3] + ways[(i-2)%3] + ways[(i-3)%3];

        return ways[n%3];
}

// driver code

    var dist = 4;
    document.write(printCountDP(dist));
</script>
```

**输出:**

```
7
```

**时间复杂度:O(n)**

**空间复杂度:O(1)**

本文由维格内斯·文卡特森撰写。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论