# 使用一次遍历对二进制数组进行排序

> 原文:[https://www . geesforgeks . org/sort-binary-array-use-one-traversation/](https://www.geeksforgeeks.org/sort-binary-array-using-one-traversal/)

给定一个二进制数组，使用一次遍历进行排序，不需要额外的空间。
**例:**

```
Input : 1 0 0 1 0 1 0 1 1 1 1 1 1 0 0 1 1 0 1 0 0 
Output : 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1 1
Explanation: The output is a sorted array of 0 and 1

Input : 1 0 1 0 1 0 1 0 
Output : 0 0 0 0 1 1 1 1
Explanation: The output is a sorted array of 0 and 1
```

**进场:**这个概念与【快速排序】的[分区有关。在“快速排序”分区中，一次扫描后，数组的左边最小，而数组的右边是所选透视元素的最大值。
**算法:**](https://www.geeksforgeeks.org/quick-sort/) 

1.  创建一个变量索引*索引= 0*
2.  从头到尾遍历数组
3.  如果元素为 0，则将当前元素与位于索引位置的元素交换，并将索引增加 1。
4.  如果元素是 1，保持元素原样。

**执行:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to sort a binary array
#include <iostream>
using namespace std;

void sortBinaryArray(int a[], int n)
{
    int j = -1;
    for (int i = 0; i < n; i++) {

        // if number is smaller than 1
        // then swap it with j-th number
        if (a[i] < 1) {
            j++;
            swap(a[i], a[j]);
        }
    }
}

// Driver code
int main()
{
    int a[] = { 1, 0, 0, 1, 0, 1, 0, 1, 1, 1,
                1, 1, 1, 0, 0, 1, 1, 0, 1, 0, 0 };
    int n = sizeof(a) / sizeof(a[0]);
    sortBinaryArray(a, n);
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Sort a binary
// array using one traversal
import java.util.*;

class GFG {

    static void sortBinaryArray(int a[], int n)
    {
        int j = -1;
        for (int i = 0; i < n; i++) {

            // if number is smaller than 1
            // then swap it with j-th number
            if (a[i] < 1) {
                j++;
                int temp = a[j];
                a[j] = a[i];
                a[i] = temp;
            }
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {

        int a[] = { 1, 0, 0, 1, 0, 1, 0, 1, 1, 1,
                    1, 1, 1, 0, 0, 1, 1, 0, 1, 0, 0 };

        int n = a.length;

        sortBinaryArray(a, n);

        for (int i = 0; i < n; i++)
            System.out.print(a[i] + " ");
    }
}
```

## 蟒蛇 3

```
# A Python program to sort a
# binary array
def sortBinaryArray(a, n):
    j = -1
    for i in range(n):

        # if number is smaller
        # than 1 then swap it
        # with j-th number
        if a[i] < 1:
            j = j + 1

            # swap
            a[i], a[j] = a[j], a[i]

# Driver program
a = [1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1,
        1, 1, 0, 0, 1, 1, 0, 1, 0, 0]
n = len(a)

sortBinaryArray(a, n)

for i in range(n):
        print(a[i], end = " ")

# This code is contributed by Shrikant13.
```

## C#

```
// C# Code for Sort a binary
// array using one traversal
using System;

class GFG {

    static void sortBinaryArray(int[] a,
                                  int n)
    {
        int j = -1;
        for (int i = 0; i < n; i++)
        {

            // if number is smaller than
            // 1 then swap it with j-th
            // number
            if (a[i] < 1) {
                j++;
                int temp = a[j];
                a[j] = a[i];
                a[i] = temp;
            }
        }
    }

    /* Driver program to test above
    function */
    public static void Main()
    {

        int[] a = { 1, 0, 0, 1, 0, 1, 0,
                    1, 1, 1, 1, 1, 1, 0,
                    0, 1, 1, 0, 1, 0, 0 };

        int n = a.Length;

        sortBinaryArray(a, n);

        for (int i = 0; i < n; i++)
            Console.Write(a[i] + " ");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code for Sort a binary
// array using one traversal
function sortBinaryArray($a, $n)
{
    $j = -1;
    for ($i = 0; $i < $n; $i++)
    {

        // if number is smaller than
        // 1 then swap it with j-th
        // number
        if ($a[$i] < 1)
        {
            $j++;
            $temp = $a[$j];
            $a[$j] = $a[$i];
            $a[$i] = $temp;
        }
    }
for ($i = 0; $i < $n; $i++)
        echo $a[$i] . " ";

}

// Driver Code
$a = array(1, 0, 0, 1, 0, 1, 0,
           1, 1, 1, 1, 1, 1, 0,
           0, 1, 1, 0, 1, 0, 0);

$n = count($a);
sortBinaryArray($a, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// Javascript Code for Sort a binary
// array using one traversal

    function sortBinaryArray(a, n)
    {
        let j = -1;
        for (let i = 0; i < n; i++) {

            // if number is smaller than 1
            // then swap it with j-th number
            if (a[i] < 1) {
                j++;
                let temp = a[j];
                a[j] = a[i];
                a[i] = temp;
            }
        }
    }

// driver function
        let a = [ 1, 0, 0, 1, 0, 1, 0, 1, 1, 1,
                    1, 1, 1, 0, 0, 1, 1, 0, 1, 0, 0 ];

        let n = a.length;

        sortBinaryArray(a, n);

        for (let i = 0; i < n; i++)
            document.write(a[i] + " ");

  // This code is contributed by code_hunt.
</script>   
```

**输出:**

```
0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1 1
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要遍历一次数组，所以时间复杂度为 O(n)。

*   **空间复杂度:** O(1)。
    所需的空间是恒定的。

本文由**德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。