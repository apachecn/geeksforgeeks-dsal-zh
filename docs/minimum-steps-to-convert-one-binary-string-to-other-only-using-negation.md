# 仅使用否定将一个二进制字符串转换为另一个二进制字符串的最小步骤

> 原文:[https://www . geesforgeks . org/最小步数-转换-一-二进制-字符串-其他-仅使用-否定/](https://www.geeksforgeeks.org/minimum-steps-to-convert-one-binary-string-to-other-only-using-negation/)

给定两个二进制字符串 **A** 和 **B** ，任务是通过选择 A 的任意子字符串并否定它(用 1 替换每个 0，用 0 替换每个 1)来将 A 转换为 B。打印所需的最小操作数。
**例:**

> **输入:**A =“101010”，B =“110011”
> **输出:** 2
> 从索引 1 到索引 2 中选择长度为 2 的子串取反，然后 A 变成“110010”，再取最后一个字符取反。
> 最终字符串变为“110011”
> **输入:**A =“1010101”，B =“0011100”
> **输出:** 3

**方法:**创建一个空白数组，标记需要求反的索引。那么答案将是数组中连续 1 的块数，因为单个块可以在单个操作中求反。
例如 A =“101010”和 B =“110011”
新创建的数组将是{0，1，1，0，0，1}所以答案将是 2，
A 在第一次操作后将是“110010”
在第二次操作后将是“110011”
下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to find the minimum steps
// to convert string a to string b
void convert(int n, string a, string b)
{
    // array to mark the positions
    // needed to be negated
    int l[n];
    int i;

    for (i = 0; i < n; i++)
        l[i] = 0;

    for (i = 0; i < n; i++) {

        // If two character are not same
        // then they need to be negated
        if (a[i] != b[i])
            l[i] = 1;
    }

    // To count the blocks of 1
    int cc = 0;

    // To count the number of 1's in
    // each block of 1's
    int vl = 0;
    for (i = 0; i < n; i++) {
        if (l[i] == 0) {
            if (vl != 0)
                cc += 1;

            vl = 0;
        }
        else
            vl += 1;
    }

    // For the last block of 1's
    if (vl != 0)
        cc += 1;

    cout << cc << endl;
}

// Driver code
int main()
{
    string a = "101010";
    string b = "110011";

    int n = a.length();
    convert(n, a, b);

    return 0;
}

// This code is contributed by ANKITRAI1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class solution {

    // Function to find the minimum steps
    // to convert string a to string b
    static void convert(int n, String a, String b)
    {
        // array to mark the positions
        // needed to be negated
        int[] l = new int[n];
        int i;

        for (i = 0; i < n; i++)
            l[i] = 0;

        for (i = 0; i < n; i++) {

            // If two character are not same
            // then they need to be negated
            if (a.charAt(i) != b.charAt(i))
                l[i] = 1;
        }

        // To count the blocks of 1
        int cc = 0;

        // To count the number of 1's in
        // each block of 1's
        int vl = 0;
        for (i = 0; i < n; i++) {
            if (l[i] == 0) {
                if (vl != 0)
                    cc += 1;

                vl = 0;
            }
            else
                vl += 1;
        }

        // For the last block of 1's
        if (vl != 0)
            cc += 1;

        System.out.println(cc);
    }

    // Driver code
    public static void main(String args[])
    {
        String a = "101010";
        String b = "110011";

        int n = a.length();
        convert(n, a, b);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the minimum steps
# to convert string a to string b
def convert(n, a, b):

    # List to mark the positions needed to
    # be negated
    l = [0] * n
    for i in range(n):

        # If two character are not same
        # then they need to be negated
        if(a[i] != b[i]):
            l[i] = 1

    # To count the blocks of 1
    cc = 0

    # To count the number of 1's in each
    # block of 1's
    vl = 0
    for i in range(n):
        if (l[i] == 0):
            if(vl != 0):
                cc += 1
            vl = 0
        else:
            vl += 1

    # For the last block of 1's
    if(vl != 0):
        cc += 1

    print(cc)

# Driver code
a = "101010"
b = "110011"
n = len(a)
convert(n, a, b)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Function to find the minimum steps
    // to convert string a to string b
    static void convert(int n, String a, String b)
    {
        // array to mark the positions
        // needed to be negated
        int[] l = new int[n];
        int i;

        for (i = 0; i < n; i++)
            l[i] = 0;

        for (i = 0; i < n; i++) {

            // If two character are not same
            // then they need to be negated
            if (a[i] != b[i])
                l[i] = 1;
        }

        // To count the blocks of 1
        int cc = 0;

        // To count the number of 1's in
        // each block of 1's
        int vl = 0;
        for (i = 0; i < n; i++) {
            if (l[i] == 0) {
                if (vl != 0)
                    cc += 1;

                vl = 0;
            }
            else
                vl += 1;
        }

        // For the last block of 1's
        if (vl != 0)
            cc += 1;
        Console.WriteLine(cc);
    }

    // Driver code
    static public void Main()
    {

        String a = "101010";
        String b = "110011";

        int n = a.Length;
        convert(n, a, b);
    }
}

// This code is contributed by jit_t.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the minimum steps
// to convert string a to string b
function convert($n, $a, $b)
{
    // array to mark the positions
    // needed to be negated
    $l = array_fill(0, $n, NULL);

    for ($i = 0; $i < $n; $i++)
        $l[$i] = 0 ;

    for($i = 0; $i < $n; $i++)
    {

        // If two character are not same
        // then they need to be negated
        if($a[$i] != $b[$i])
            $l[$i] = 1 ;
    }

    // To count the blocks of 1
    $cc = 0;

    // To count the number of 1's in
    // each block of 1's
    $vl = 0 ;
    for($i = 0; $i < $n ; $i++)
    {
        if ($l[$i] == 0)
        {
            if($vl != 0)
                $cc += 1 ;

            $vl = 0 ;
        }
        else
            $vl += 1 ;
    }

    // For the last block of 1's
    if($vl != 0)
        $cc += 1 ;

    echo $cc . "\n";
}

// Driver code
$a = "101010";
$b = "110011";

$n = strlen($a);
convert($n, $a, $b) ;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

    // Function to find the minimum steps
    // to convert string a to string b
    function convert(n, a, b)
    {
        // array to mark the positions
        // needed to be negated
        let l = new Array(n);
        let i;

        for (i = 0; i < n; i++)
            l[i] = 0;

        for (i = 0; i < n; i++) {

            // If two character are not same
            // then they need to be negated
            if (a[i] != b[i])
                l[i] = 1;
        }

        // To count the blocks of 1
        let cc = 0;

        // To count the number of 1's in
        // each block of 1's
        let vl = 0;
        for (i = 0; i < n; i++) {
            if (l[i] == 0) {
                if (vl != 0)
                    cc += 1;

                vl = 0;
            }
            else
                vl += 1;
        }

        // For the last block of 1's
        if (vl != 0)
            cc += 1;
        document.write(cc + "</br>");
    }

    let a = "101010";
    let b = "110011";

    let n = a.length;
    convert(n, a, b);

</script>
```

**Output:** 

```
2
```