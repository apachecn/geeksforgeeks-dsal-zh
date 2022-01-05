# 在无限线上找到到达目标的最小移动次数

> 原文:[https://www . geesforgeks . org/find-最小移动-到达-目标-无限线/](https://www.geeksforgeeks.org/find-minimum-moves-reach-target-infinite-line/)

给定无限数线上的目标位置，即-无穷大到+无穷大。从 0 开始，你必须按照描述的方式移动才能到达目标:在移动中，你可以向前或向后迈一步。找到到达目标所需的最小移动次数。
**例:**

```
Input : target = 3
Output : 2
Explanation:
On the first move we step from 0 to 1.
On the second step we step from 1 to 3.

Input: target = 2
Output: 3
Explanation:
On the first move we step from 0 to 1.
On the second move we step  from 1 to -1.
On the third move we step from -1 to 2.
```

我们在下面的帖子中讨论了一个简单的递归解决方案。
[到达目的地的最小步数](https://www.geeksforgeeks.org/minimum-steps-to-reach-a-destination/)
如果目标为负，我们可以将其视为正，因为我们是以对称的方式从 0 开始的。
想法是尽可能长时间朝一个方向移动，这样会给出最少的移动。从 0 开始第一招带我们到 1，第二招带我们到 3 (1+2)位置，第三招带我们到 6 (1+2+3)位置，ans 以此类推；所以为了找到目标，我们不断增加移动，直到找到第 n 个移动，这样 1+2+3+…+n>=目标。现在，如果总和(1+2+3+…+n)等于目标，我们的工作就完成了，也就是说，我们需要 n 次移动才能达到目标。现在下一种情况**总和大于目标**。根据我们领先的程度找出差距，即总和目标。让差值为 d =总和–目标。
如果我们进行第 I 次向后移动，那么新的总和将变成(sum–2i)，即 1+2+3+…-x+x+1…+n。现在如果 sum-2i = target，那么我们的工作就完成了。因为，sum–target = 2i，即差值应该是偶数，因为我们将得到一个整数 I 翻转，这将给出答案。于是出现了以下情况。
**情况 1 :** 差是偶数那么答案是 n，(因为我们总是会得到一个会导致目标的移动翻转)。
**情况 2 :** 差是奇数，那么我们再走一步，即加 n+1 求和，现在再取差。如果差是偶数，n+1 就是答案，否则我们必须再走一步，这肯定会有所不同，即使答案是 n+2。
说明:既然差是奇数。目标不是奇数就是偶数。
情况 1: n 为偶数(1+2+3+……+n)，那么加 n+1 就使差为偶数。
情况 2: n 是奇数，那么加 n+1 也没有区别，所以我们必须再走一步，所以 n+2。
**例:**
目标= 5。
我们不断采取行动，直到我们达到目标或者我们越过它。
和= 1 + 2 + 3 = 6 > 5，步= 3。
差值= 6–5 = 1。因为这个差是一个奇数，所以我们不能通过从+i 翻转到-i 来达到目标。所以我们增加了步长。我们需要将步长增加 2 以获得偶数差(因为 n 是奇数，目标也是奇数)。现在我们有一个偶数差，我们可以简单地向左切换任何移动(即改变+到-)只要改变的值的总和等于差的一半。我们可以切换 1 和 4 或者 2 和 3 或者 5。

## C++

```
// CPP program to find minimum moves to
// reach target if we can move i steps in
// i-th move.
#include <iostream>
using namespace std;

int reachTarget(int target)
{
    // Handling negatives by symmetry
    target = abs(target);

    // Keep moving while sum is smaller or difference
    // is odd.
    int sum = 0, step = 0;
    while (sum < target || (sum - target) % 2 != 0) {
        step++;
        sum += step;
    }
    return step;
}

// Driver code
int main()
{
    int target = 5;
    cout << reachTarget(target);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum 
//moves to reach target if we can
// move i steps in i-th move.
import java.io.*;
import java.math.*;

class GFG {

    static int reachTarget(int target)
    {
        // Handling negatives by symmetry
        target = Math.abs(target);

        // Keep moving while sum is smaller
        // or difference is odd.
        int sum = 0, step = 0;

        while (sum < target || (sum - target) % 2
                                        != 0) {
            step++;
            sum += step;
        }
        return step;
    }

    // Driver code
    public static void main(String args[])
    {
       int target = 5;
       System.out.println(reachTarget(target));
    }
}

// This code is contributed by Nikita tiwari.
```

## 蟒蛇 3

```
# Python 3 program to find minimum 
# moves to reach target if we can
# move i steps in i-th move.

def reachTarget(target) :

    # Handling negatives by symmetry
    target = abs(target)

    # Keep moving while sum is
    # smaller or difference is odd.
    sum = 0
    step = 0
    while (sum < target or (sum - target) %
                                  2 != 0) :
        step = step + 1
        sum = sum + step

    return step

# Driver code
target = 5
print(reachTarget(target))

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# program to find minimum
//moves to reach target if we can
// move i steps in i-th move.
using System;

class GFG {

    static int reachTarget(int target)
    {
        // Handling negatives by symmetry
        target = Math.Abs(target);

        // Keep moving while sum is smaller
        // or difference is odd.
        int sum = 0, step = 0;

        while (sum < target ||
              (sum - target) % 2!= 0)
        {
            step++;
            sum += step;
        }
        return step;
    }

    // Driver code
    public static void Main()
    {
    int target = 5;
    Console.WriteLine(reachTarget(target));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find 
// minimum moves to reach
// target if we can move i
// steps in i-th move.

function reachTarget($target)
{
    // Handling negatives
    // by symmetry
    $target = abs($target);

    // Keep moving while sum is
    // smaller or difference is odd.
    $sum = 0; $step = 0;
    while ($sum < $target or
          ($sum - $target) % 2 != 0)
          {
            $step++;
            $sum += $step;
          }
    return $step;
}

// Driver code
$target = 5;
echo reachTarget($target);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum 
//moves to reach target if we can
// move i steps in i-th move.

function reachTarget(target)
    {
        // Handling negatives by symmetry
        target = Math.abs(target);

        // Keep moving while sum is smaller
        // or difference is odd.
        let sum = 0, step = 0;

        while (sum < target || (sum - target) % 2
                                        != 0) {
            step++;
            sum += step;
        }
        return step;
    }

// Driver code

    let target = 5;
      document.write(reachTarget(target));

</script>
```

**输出:**

```
5
```