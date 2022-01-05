# 任意两个元素的绝对差为 2 的幂的最大子集

> 原文:[https://www . geesforgeks . org/最大子集任意两个元素的绝对差是 2 的幂/](https://www.geeksforgeeks.org/largest-subset-where-absolute-difference-of-any-two-element-is-a-power-of-2/)

给定不同元素的数组**arr[]****-10<sup>9</sup>≤a<sub>I</sub>≤10<sup>9</sup>**。任务是从给定的数组中找到最大的子集，这样子集中任意两个数字之间的绝对差就是 2 的正幂。如果无法进行这样的设置，则打印 **-1** 。
**示例:**

> **输入:** arr[] = {3，4，5，6，7}
> **输出:**3 5 7
> | 3–5 | = 2<sup>1</sup>，| 5–7 | = 2<sup>1</sup>和| 3–7 | = 2<sup>2</sup>。
> **输入:** arr[] = {2，5，8}
> **输出:** -1

**进场:**我们来证明子集的大小不会是 **> 3** 。假设 **a** 、 **b** 、 **c** 和 **d** 是一个子集的四个元素， **a < b < c < d** 。
让**ABS(a–b)= 2<sup>k</sup>T18】和**ABS(b–c)= 2<sup>l</sup>T22】然后**ABS(a–c)= ABS(a–b)+ABS(b–c)= 2<sup>k</sup>+2<sup>l</sup>= 2<sup>m</sup>T30】。意思是 **k = l** 。三重 **(b，c，d)** 的条件也必须成立。现在很容易看出，如果**ABS(a–b)= ABS(b–c)= ABS(c–d)= 2<sup>k</sup>T38】那么**ABS(a–d)= ABS(a–b)* 3**不是 2 的幂。所以子集的大小永远不会大于 3。******** 

*   让我们检查一下**如果答案是 3** 。对子集的中间元素和从 1 到 30 的 2 的幂迭代给定的数组。假设 xi 是子集的中间元素，j 是 2 的当前幂。那么如果数组中有元素 **x <sub>i</sub> -2 <sub>j</sub> 和 x <sub>i</sub> +2 <sub>j</sub>** ，那么答案就是 **3** 。
*   否则检查**如果答案是 2** 。重复上一步，但在这里可以得到左点**x<sub>I</sub>-2<sub>j</sub>T7】或**x<sub>I</sub>+2<sub>j</sub>T13】。****
*   如果答案是**既不是 2 也不是 3** ，则打印 **-1** 。

以下是上述方法的实现:

## C++

```
// CPP program to find sub-set with
// maximum possible size
#include <bits/stdc++.h>
using namespace std;

// Function to find sub-set with
// maximum possible size
void PowerOfTwo(vector<int> x, int n)
{
    // Sort the given array
    sort(x.begin(), x.end());

    // To store required sub-set
    vector<int> res;

    for (int i = 0; i < n; ++i) {

        // Iterate for all powers of two
        for (int j = 1; j < 31; ++j) {

            // Left number
            int lx = x[i] - (1 << j);

            // Right number
            int rx = x[i] + (1 << j);

            // Predefined binary search in c++
            bool isl = binary_search(x.begin(), x.end(), lx);
            bool isr = binary_search(x.begin(), x.end(), rx);

            // If possible to get sub-set of size 3
            if (isl && isr && int(res.size()) < 3)
                res = { lx, x[i], rx };

            // If possible to get sub-set of size 2
            if (isl && int(res.size()) < 2)
                res = { lx, x[i] };

            // If possible to get sub-set of size 2
            if (isr && int(res.size()) < 2)
                res = { x[i], rx };
        }
    }

    // If not possible to get sub-set
    if (!res.size()) {
        cout << -1;
        return;
    }

    // Print the sub-set
    for (auto it : res)
        cout << it << " ";
}

// Driver Code
int main()
{

    vector<int> a = { 3, 4, 5, 6, 7 };

    int n = a.size();
    PowerOfTwo(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sub-set with
// maximum possible size
import java.util.*;

class GFG
{

// Function to find sub-set with
// maximum possible size
static void PowerOfTwo(int []x, int n)
{
    // Sort the given array
    Arrays.sort(x);

    // To store required sub-set
    ArrayList<Integer> res = new ArrayList<Integer>();

    for (int i = 0; i < n; ++i)
    {

        // Iterate for all powers of two
        for (int j = 1; j < 31; ++j)
        {

            // Left number
            int lx = x[i] - (1 << j);

            // Right number
            int rx = x[i] + (1 << j);

            // Predefined binary search in Java
            boolean isl = Arrays.binarySearch(x,lx) <
                                    0 ? false : true;
            boolean isr = Arrays.binarySearch(x,rx) <
                                    0 ? false : true;

            // If possible to get sub-set of size 3
            if (isl && isr && res.size() < 3)
            {
                res.clear();
                res.add(lx);
                res.add(x[i]);
                res.add(rx);
            }

            // If possible to get sub-set of size 2
            if (isl && res.size() < 2)
            {
                res.clear();
                res.add(lx);
                res.add(x[i]);
            }
            // If possible to get sub-set of size 2
            if (isr && res.size() < 2)
            {
                res.clear();
                res.add(x[i]);
                res.add(rx);
            }
        }
    }

    // If not possible to get sub-set
    if (res.size() == 0)
    {
        System.out.println("-1");
        return;
    }

    // Print the sub-set
    for (int i = 0; i < res.size(); i++)
        System.out.print(res.get(i) + " ");
}

// Driver Code
public static void main (String[] args)
{
    int[] a = {3, 4, 5, 6, 7};
    int n = a.length;
    PowerOfTwo(a, n);
}
}

// This code is Contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find sub-set with
# maximum possible size

# Function to find sub-set with
# maximum possible size
def PowerOfTwo(x, n) :

    # Sort the given array
    x.sort()

    # To store required sub-set
    res = []

    for i in range(n) :

        # Iterate for all powers of two
        for j in range(1, 31) :

            # Left number
            lx = x[i] - (1 << j)

            # Right number
            rx = x[i] + (1 << j)

            if lx in x :
                isl = True
            else :
                isl = False

            if rx in x :
                isr = True
            else :
                isr = False

            # If possible to get sub-set of size 3
            if (isl and isr and len(res) < 3) :
                res = [ lx, x[i], rx ]

            # If possible to get sub-set of size 2
            if (isl and len(res) < 2) :
                res = [ lx, x[i] ]

            # If possible to get sub-set of size 2
            if (isr and len(res) < 2) :
                res = [ x[i], rx ]

    # If not possible to get sub-set
    if (not len(res)) :
        print(-1)
        return

    # Print the sub-set
    for it in res :
        print(it, end = " ")

# Driver Code
if __name__ == "__main__" :

    a = [ 3, 4, 5, 6, 7 ]

    n = len(a)
    PowerOfTwo(a, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to find sub-set with
// maximum possible size
using System;
using System.Collections;

class GFG
{

// Function to find sub-set with
// maximum possible size
static void PowerOfTwo(int[] x, int n)
{
    // Sort the given array
    Array.Sort(x);

    // To store required sub-set
    ArrayList res = new ArrayList();

    for (int i = 0; i < n; ++i)
    {

        // Iterate for all powers of two
        for (int j = 1; j < 31; ++j)
        {

            // Left number
            int lx = x[i] - (1 << j);

            // Right number
            int rx = x[i] + (1 << j);

            // Predefined binary search in C#
            bool isl = Array.IndexOf(x, lx) < 0? false : true;
            bool isr = Array.IndexOf(x, rx) < 0? false : true;

            // If possible to get sub-set of size 3
            if (isl && isr && res.Count < 3)
            {
                res.Clear();
                res.Add(lx);
                res.Add(x[i]);
                res.Add(rx);
            }

            // If possible to get sub-set of size 2
            if (isl && res.Count < 2)
            {
                res.Clear();
                res.Add(lx);
                res.Add(x[i]);
            }
            // If possible to get sub-set of size 2
            if (isr && res.Count < 2)
            {
                res.Clear();
                res.Add(x[i]);
                res.Add(rx);
            }
        }
    }

    // If not possible to get sub-set
    if (res.Count == 0)
    {
        Console.Write("-1");
        return;
    }

    // Print the sub-set
    for (int i = 0; i < res.Count; i++)
        Console.Write(res[i] + " ");
}

// Driver Code
public static void Main()
{
    int[] a = {3, 4, 5, 6, 7};
    int n = a.Length;
    PowerOfTwo(a, n);
}
}

// This code is Contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sub-set with
// maximum possible size

// Function to find sub-set with
// maximum possible size
function PowerOfTwo($x, $n)
{
    // Sort the given array
    sort($x);

    // To store required sub-set
    $res = array();

    for ($i = 0; $i < $n; ++$i)
    {

        // Iterate for all powers of two
        for ($j = 1; $j < 31; ++$j)
        {

            // Left number
            $lx = $x[$i] - (1 << $j);

            // Right number
            $rx = $x[$i] + (1 << $j);

            // Predefined binary search in PHP
            $isl = in_array($lx, $x);
            $isr = in_array($rx, $x);

            // If possible to get sub-set of size 3
            if ($isl && $isr && count($res) < 3)
            {
                unset($res);
                $res = array();
                array_push($res, $lx);
                array_push($res, $x[$i]);
                array_push($res, $rx);
            }

            // If possible to get sub-set of size 2
            if ($isl && count($res) < 2)
            {
                unset($res);
                $res = array();
                array_push($res, $lx);
                array_push($res, $x[$i]);
            }

            // If possible to get sub-set of size 2
            if ($isr && count($res) < 2)
            {
                unset($res);
                $res = array();
                array_push($res, $x[$i]);
                array_push($res, $rx);
            }
        }
    }

    // If not possible to get sub-set
    if (!count($res))
    {
        echo "-1";
        return;
    }

    // Print the sub-set
    for ($i = 0; $i < count($res); $i++)
        echo $res[$i] . " ";
}

// Driver Code
$a = array( 3, 4, 5, 6, 7 );

$n = count($a);
PowerOfTwo($a, $n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript program to find sub-set with
    // maximum possible size

    // Function to find sub-set with
    // maximum possible size
    function PowerOfTwo(x, n)
    {

        // Sort the given array
        x.sort();

        // To store required sub-set
        let res = [];

        for (let i = 0; i < n; ++i)
        {

            // Iterate for all powers of two
            for (let j = 1; j < 31; ++j)
            {

                // Left number
                let lx = x[i] - (1 << j);

                // Right number
                let rx = x[i] + (1 << j);

                // Predefined binary search in Java
                let isl = x.indexOf(lx) <
                                        0 ? false : true;
                let isr = x.indexOf(rx) <
                                        0 ? false : true;

                // If possible to get sub-set of size 3
                if (isl && isr && res.length < 3)
                {
                    res = [];
                    res.push(lx);
                    res.push(x[i]);
                    res.push(rx);
                }

                // If possible to get sub-set of size 2
                if (isl && res.length < 2)
                {
                    res = [];
                    res.push(lx);
                    res.push(x[i]);
                }
                // If possible to get sub-set of size 2
                if (isr && res.length < 2)
                {
                    res = [];
                    res.push(x[i]);
                    res.push(rx);
                }
            }
        }

        // If not possible to get sub-set
        if (res.length == 0)
        {
            document.write("-1" + "</br>");
            return;
        }

        // Print the sub-set
        for (let i = 0; i < res.length; i++)
            document.write(res[i] + " ");
    }

    let a = [3, 4, 5, 6, 7];
    let n = a.length;
    PowerOfTwo(a, n);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
3 5 7
```

时间复杂度:O(N*logN)
辅助空间:O(1)