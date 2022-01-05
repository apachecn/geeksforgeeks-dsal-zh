# 生成 K 个元素的数组，使得元素的和为 N，并且满足条件 a[I]<a[I+1]<= 2 * a[I]|集合 2

> 原文:[https://www . geesforgeks . org/generate-a-array-of-k-elements-so-elements-sum-is-n-and-condition-ai-ai1/](https://www.geeksforgeeks.org/generate-an-array-of-k-elements-such-that-sum-of-elements-is-n-and-the-condition-ai-ai1/)

给定两个整数 **N** 和 **K** ，任务是生成一个长度为 **K** 的数组**arr【】**:

1.  **arr[0]+arr[1]+…+arr[K–1]= N**。
2.  **arr【I】>0**为 **0 ≤ i < K** 。
3.  **疤痕[i] < 疤痕[i + 1] ≤ 2 * 疤痕[i]** 对于 **0 ≤在 < K – 1** 。

如果有多个答案，找到其中任意一个，否则打印 **-1** 。
**例:**

> **输入:** N = 26，K = 6
> **输出:** 1 2 3 4 6 10
> 以上数组满足所有条件。
> **输入:** N = 8，k = 3
> **输出:** -1

**接近**:最初我们用最低可能的配置形成阵列，用 1、2、3、4 填充阵列..其满足给定的条件。如果总和为 1..k 大于 N，则不能形成数组。为了形成阵列，首先用 1、2、3，..k .再次向数组中的每个元素添加( **n-sum)/k** ，因为在这样添加时，没有任何条件是无效的，因为我们正在向每个数字添加相等的元素。
剩余的数字**雷姆**贪婪地从后面加上，使每一个数字都是前一个数字的两倍。填充数组后，如果任何给定的条件不满足，打印-1，否则形成的数组将是我们想要的答案。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that print the
// desired array which
// satisfies the given conditions
void solve(int n, int k)
{

    int mini = 0;
    int x1 = 1;
    int a[k];
    for (int i = 1; i <= k; i++) {
        mini += x1;
        a[i - 1] = x1;
        x1 += 1;
    }

    // If the lowest filling condition
    // is void, then it is not possible to
    // generate the required array
    if (n < mini) {
        cout << "-1";
        return;
    }

    int rem = n - mini;
    int cnt = rem / k;
    rem = rem % k;

    // Increase all the elements by cnt
    for (int i = 0; i < k; i++)
        a[i] += cnt;

    // Start filling from the back
    // till the number is a[i+1] <= 2*a[i]
    for (int i = k - 1; i > 0 && rem > 0; i--) {

        // Get the number to be filled
        int xx = a[i - 1] * 2;
        int left = xx - a[i];

        // If it is less than the
        // remaining numbers to be filled
        if (rem >= left) {
            a[i] = xx;
            rem -= left;
        }

        // less than remaining numbers
        // to be filled
        else {
            a[i] += rem;
            rem = 0;
        }
    }

    // Get the sum of the array
    int sum = a[0];
    for (int i = 1; i < k; i++) {

        // If this condition is void at any stage
        // during filling up, then print -1
        if (a[i] > 2 * a[i - 1]) {
            cout << "-1";
            return;
        }

        // Else add it to the sum
        sum += a[i];
    }

    // If the sum condition is not
    // satisified, then print -1
    if (sum != n) {
        cout << "-1";
        return;
    }

    // Print the generated array
    for (int i = 0; i < k; i++)
        cout << a[i] << " ";
}

// Driver code
int main()
{
    int n = 26, k = 6;
    solve(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function that print the
    // desired array which
    // satisfies the given conditions
    static void solve(int n, int k)
    {

        int mini = 0;
        int x1 = 1;
        int[] a = new int[k];
        for (int i = 1; i <= k; i++) {
            mini += x1;
            a[i - 1] = x1;
            x1 += 1;
        }

        // If the lowest filling condition
        // is void, then it is not possible to
        // generate the required array
        if (n < mini) {
            System.out.print("-1");
            return;
        }

        int rem = n - mini;
        int cnt = rem / k;
        rem = rem % k;

        // Increase all the elements by cnt
        for (int i = 0; i < k; i++)
            a[i] += cnt;

        // Start filling from the back
        // till the number is a[i+1] <= 2*a[i]
        for (int i = k - 1; i > 0 && rem > 0; i--) {

            // Get the number to be filled
            int xx = a[i - 1] * 2;
            int left = xx - a[i];

            // If it is less than the
            // remaining numbers to be filled
            if (rem >= left) {
                a[i] = xx;
                rem -= left;
            }

            // less than remaining numbers
            // to be filled
            else {
                a[i] += rem;
                rem = 0;
            }
        }

        // Get the sum of the array
        int sum = a[0];
        for (int i = 1; i < k; i++) {

            // If this condition is void at any stage
            // during filling up, then print -1
            if (a[i] > 2 * a[i - 1]) {
                System.out.print("-1");
                return;
            }

            // Else add it to the sum
            sum += a[i];
        }

        // If the sum condition is not
        // satisified, then print -1
        if (sum != n) {
            System.out.print("-1");
            return;
        }

        // Print the generated array
        for (int i = 0; i < k; i++)
            System.out.print(a[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 26, k = 6;
        solve(n, k);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that print the
# desired array which
# satisfies the given conditions
def solve(n, k):
    mini = 0
    x1 = 1
    a = [0 for i in range(k)]
    for i in range(1, k + 1):
        mini += x1
        a[i - 1] = x1
        x1 += 1

    # If the lowest filling condition
    # is void, then it is not possible to
    # generate the required array
    if (n < mini):
        print("-1",end = "")
        return

    rem = n - mini
    cnt = int(rem / k)
    rem = rem % k

    # Increase all the elements by cnt
    for i in range(k):
        a[i] += cnt

    # Start filling from the back
    # till the number is a[i+1] <= 2*a[i]
    i = k - 1
    while (i > 0 and rem > 0):
        # Get the number to be filled
        xx = a[i - 1] * 2
        left = xx - a[i]
        # If it is less than the
        # remaining numbers to be filled
        if (rem >= left):
            a[i] = xx
            rem -= left

        # less than remaining numbers
        # to be filled
        else:
            a[i] += rem
            rem = 0

        i -= 1

    # Get the sum of the array
    sum = a[0]
    for i in range(1, k):
        # If this condition is void at any stage
        # during filling up, then print -1
        if (a[i] > 2 * a[i - 1]):
            print("-1", end = "")
            return

        # Else add it to the sum
        sum += a[i]

    # If the sum condition is not
    # satisified, then print -1
    if (sum != n):
        print("-1", end = "")
        return

    # Print the generated array
    for i in range(k):
        print(a[i], end = " ")

# Driver code
if __name__ == '__main__':
    n = 26
    k = 6
    solve(n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that print the
    // desired array which
    // satisfies the given conditions
    static void solve(int n, int k)
    {

        int mini = 0;
        int x1 = 1;
        int[] a = new int[k];
        for (int i = 1; i <= k; i++)
        {
            mini += x1;
            a[i - 1] = x1;
            x1 += 1;
        }

        // If the lowest filling condition
        // is void, then it is not possible to
        // generate the required array
        if (n < mini)
        {
            Console.Write("-1");
            return;
        }

        int rem = n - mini;
        int cnt = rem / k;
        rem = rem % k;

        // Increase all the elements by cnt
        for (int i = 0; i < k; i++)
            a[i] += cnt;

        // Start filling from the back
        // till the number is a[i+1] <= 2*a[i]
        for (int i = k - 1; i > 0 && rem > 0; i--)
        {

            // Get the number to be filled
            int xx = a[i - 1] * 2;
            int left = xx - a[i];

            // If it is less than the
            // remaining numbers to be filled
            if (rem >= left)
            {
                a[i] = xx;
                rem -= left;
            }

            // less than remaining numbers
            // to be filled
            else
            {
                a[i] += rem;
                rem = 0;
            }
        }

        // Get the sum of the array
        int sum = a[0];
        for (int i = 1; i < k; i++)
        {

            // If this condition is void at any stage
            // during filling up, then print -1
            if (a[i] > 2 * a[i - 1])
            {
                Console.Write("-1");
                return;
            }

            // Else add it to the sum
            sum += a[i];
        }

        // If the sum condition is not
        // satisified, then print -1
        if (sum != n) {
            Console.Write("-1");
            return;
        }

        // Print the generated array
        for (int i = 0; i < k; i++)
            Console.Write(a[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int n = 26, k = 6;
        solve(n, k);
    }
}

// This code contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that print the
// desired array which
// satisfies the given conditions
function solve($n, $k)
{

    $mini = 0;
    $x1 = 1;
    $a = array();
    for ($i = 1; $i <= $k; $i++)
    {
        $mini += $x1;
        $a[$i - 1] = $x1;
        $x1 += 1;
    }

    // If the lowest filling condition
    // is void, then it is not possible to
    // generate the required array
    if ($n < $mini)
    {
        echo "-1";
        return;
    }

    $rem = $n - $mini;
    $cnt = floor($rem / $k);
    $rem = $rem % $k;

    // Increase all the elements by cnt
    for ($i = 0; $i < $k; $i++)
        $a[$i] += $cnt;

    // Start filling from the back
    // till the number is a[i+1] <= 2*a[i]
    for ($i = $k - 1; $i > 0 && $rem > 0; $i--)
    {

        // Get the number to be filled
        $xx = $a[$i - 1] * 2;
        $left = $xx - $a[$i];

        // If it is less than the
        // remaining numbers to be filled
        if ($rem >= $left)
        {
            $a[$i] = $xx;
            $rem -= $left;
        }

        // less than remaining numbers
        // to be filled
        else
        {
            $a[$i] += $rem;
            $rem = 0;
        }
    }

    // Get the sum of the array
    $sum = $a[0];
    for ($i = 1; $i < $k; $i++)
    {

        // If this condition is void at any stage
        // during filling up, then print -1
        if ($a[$i] > 2 * $a[$i - 1])
        {
            echo "-1";
            return;
        }

        // Else add it to the sum
        $sum += $a[$i];
    }

    // If the sum condition is not
    // satisified, then print -1
    if ($sum != $n)
    {
        echo "-1";
        return;
    }

    // Print the generated array
    for ($i = 0; $i < $k; $i++)
        echo $a[$i], " ";
}

// Driver code
$n = 26; $k = 6;
solve($n, $k);

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that print the
// desired array which
// satisfies the given conditions
function solve(n, k)
{

    let mini = 0;
    let x1 = 1;
    let a = new Array(k);
    for (let i = 1; i <= k; i++) {
        mini += x1;
        a[i - 1] = x1;
        x1 += 1;
    }

    // If the lowest filling condition
    // is void, then it is not possible to
    // generate the required array
    if (n < mini) {
        document.write("-1");
        return;
    }

    let rem = n - mini;
    let cnt = parseInt(rem / k);
    rem = rem % k;

    // Increase all the elements by cnt
    for (let i = 0; i < k; i++)
        a[i] += cnt;

    // Start filling from the back
    // till the number is a[i+1] <= 2*a[i]
    for (let i = k - 1; i > 0 && rem > 0; i--) {

        // Get the number to be filled
        let xx = a[i - 1] * 2;
        let left = xx - a[i];

        // If it is less than the
        // remaining numbers to be filled
        if (rem >= left) {
            a[i] = xx;
            rem -= left;
        }

        // less than remaining numbers
        // to be filled
        else {
            a[i] += rem;
            rem = 0;
        }
    }

    // Get the sum of the array
    let sum = a[0];
    for (let i = 1; i < k; i++) {

        // If this condition is void at any stage
        // during filling up, then print -1
        if (a[i] > 2 * a[i - 1]) {
            document.write("-1");
            return;
        }

        // Else add it to the sum
        sum += a[i];
    }

    // If the sum condition is not
    // satisified, then print -1
    if (sum != n) {
        document.write("-1");
        return;
    }

    // Print the generated array
    for (let i = 0; i < k; i++)
        document.write(a[i] + " ");
}

// Driver code
    let n = 26, k = 6;
    solve(n, k);

</script>
```

**Output:** 

```
1 2 3 4 6 10
```

**时间复杂度:** O(K)

**辅助空间:** O(K)