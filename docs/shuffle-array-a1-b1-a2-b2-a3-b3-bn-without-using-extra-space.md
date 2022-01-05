# Shuffle 数组{a1，a2，..an，b1，b2，..bn}为{a1，b1，a2，b2，a3，b3，…，an，bn}而不使用额外空间

> 原文:[https://www . geesforgeks . org/shuffle-array-a1-B1-a2-B2-a3-B3-bn-不使用额外空间/](https://www.geeksforgeeks.org/shuffle-array-a1-b1-a2-b2-a3-b3-bn-without-using-extra-space/)

给定以下格式的 2n 个元素的数组{ a1，a2，a3，a4，…..，an，b1，b2，b3，b4，…，bn }。任务是在不使用额外空间的情况下将数组洗牌到{a1，b1，a2，b2，a3，b3，…，an，bn }。
**例:**

```
Input : arr[] = { 1, 2, 9, 15 }
Output : 1 9 2 15

Input :  arr[] = { 1, 2, 3, 4, 5, 6 }
Output : 1 4 2 5 3 6

```

我们在下面的帖子中讨论了这个问题的 O(n <sup>2</sup> )和 O(n Log n)解决方案。
[在不使用额外空间的情况下，以{a1，b1，a2，b2，a3，b3，…，an，bn}的格式洗牌 2n 个整数](https://www.geeksforgeeks.org/shuffle-2n-integers-format-a1-b1-a2-b2-a3-b3-bn-without-using-extra-space/)
这里讨论了一种在线性时间内有效的新解决方案。我们知道第一个和最后一个数字不会离开它们的位置。并且，我们跟踪从中挑选任何数字的索引以及目标索引的位置。我们知道，如果我们选择人工智能，它必须进入索引 2 * i–1，如果是 bi，它必须进入 2 * I。我们可以根据选择索引检查我们从哪里选择了某个数字，如果它大于或小于 n。
假设 n =数组长度的一半，我们必须这样做 2 * n–2 次。
我们得到两种情况，当 n 是偶数和奇数时，因此我们适当地初始化起始变量。
**注意:**为了简单起见，索引被认为是基于 1 的数组。

C++

```
 // C++ program to shuffle an array in O(n) time
// and O(1) extra space
#include <bits/stdc++.h>
using namespace std;

// Shuffles an array of size 2n. Indexes
// are considered starting from 1.
void shufleArray(int a[], int n)
{
    n = n / 2;

    for (int start = n + 1, j = n + 1, done = 0, i;
         done < 2 * n - 2; done++) {
        if (start == j) {
            start--;
            j--;
        }

        i = j > n ? j - n : j;
        j = j > n ? 2 * i : 2 * i - 1;

        swap(a[start], a[j]);
    }
}

// Driven Program
int main()
{
    // The first element is bogus. We have used
    // one based indexing for simplicity.
    int a[] = { -1, 1, 3, 5, 7, 2, 4, 6, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    shufleArray(a, n);

    for (int i = 1; i < n; i++)
        cout << a[i] << " ";

    return 0;
} 
```

Java 语言(一种计算机语言，尤用于创建网站)

```
 // Java program to shuffle an
// array in O(n) time and O(1)
// extra space
import java.io.*;

public class GFG {

    // Shuffles an array of size 2n.
    // Indexes are considered starting
    // from 1.
    static void shufleArray(int[] a, int n)
    {
        int temp;
        n = n / 2;

        for (int start = n + 1, j = n + 1, done = 0, i;
             done < 2 * n - 2; done++) {
            if (start == j) {
                start--;
                j--;
            }

            i = j > n ? j - n : j;
            j = j > n ? 2 * i : 2 * i - 1;
            temp = a[start];
            a[start] = a[j];
            a[j] = temp;
        }
    }

    // Driver code
    static public void main(String[] args)
    {
        // The first element is bogus. We have used
        // one based indexing for simplicity.
        int[] a = { -1, 1, 3, 5, 7, 2, 4, 6, 8 };
        int n = a.length;

        shufleArray(a, n);

        for (int i = 1; i < n; i++)
            System.out.print(a[i] + " ");
    }
}

// This Code is contributed by vt_m. 
```

蟒蛇 3

```
 # Python 3 program to shuffle an array 
# in O(n) time and O(1) extra space

# Shuffles an array of size 2n. Indexes
# are considered starting from 1.
def shufleArray(a, n):

    n = n // 2

    start = n + 1
    j = n + 1
    for done in range( 2 * n - 2) :
        if (start == j) :
            start -= 1
            j -= 1

        i = j - n if j > n else j
        j = 2 * i if j > n else 2 * i - 1

        a[start], a[j] = a[j], a[start]

# Driver Code
if __name__ == "__main__":

    # The first element is bogus. We have used
    # one based indexing for simplicity.
    a = [ -1, 1, 3, 5, 7, 2, 4, 6, 8 ]
    n = len(a)

    shufleArray(a, n)

    for i in range(1, n):
        print(a[i], end = " ")

# This code is contributed 
# by ChitraNayal 
```

C#

```
 // C# program to shuffle an
// array in O(n) time and O(1)
// extra space
using System;

public class GFG {

    // Shuffles an array of size 2n.
    // Indexes are considered starting
    // from 1.
    static void shufleArray(int[] a, int n)
    {
        int temp;
        n = n / 2;

        for (int start = n + 1, j = n + 1, done = 0, i;
             done < 2 * n - 2; done++) {
            if (start == j) {
                start--;
                j--;
            }

            i = j > n ? j - n : j;
            j = j > n ? 2 * i : 2 * i - 1;
            temp = a[start];
            a[start] = a[j];
            a[j] = temp;
        }
    }

    // Driven code
    static public void Main(String[] args)
    {
        // The first element is bogus. We have used
        // one based indexing for simplicity.
        int[] a = { -1, 1, 3, 5, 7, 2, 4, 6, 8 };
        int n = a.Length;

        shufleArray(a, n);

        for (int i = 1; i < n; i++)
            Console.Write(a[i] + " ");
    }
}

// This Code is contributed by vt_m. 
```

服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
 <?php
// PHP program to shuffle an 
// array in O(n) time and O(1)
// extra space

// Shuffles an array of size 2n.
// Indexes are considered starting
// from 1.
function shufleArray($a, $n)
{

    $k = intval($n / 2);

    for ($start = $k + 1, 
         $j = $k + 1, $done = 0; 
         $done < 2 * $k - 2; $done++)
    {
        if ($start == $j)
        {
            $start--;
            $j--;
        }

        $i = $j > $k ? $j - $k : $j;
        $j = $j > $k ? 2 * $i : 2 * $i - 1;
        $temp = $a[$start];
        $a[$start] = $a[$j];
        $a[$j] = $temp;

    }
    for ($i = 1; $i < $n; $i++)
                echo $a[$i] . " ";
}

// Driver code

// The first element is bogus. 
// We have used one based 
// indexing for simplicity.
$a = array(-1, 1, 3, 5, 7, 2, 4, 6, 8);
$n = count($a);
shufleArray($a, $n);

// This code is contributed by Sam007
?> 
```