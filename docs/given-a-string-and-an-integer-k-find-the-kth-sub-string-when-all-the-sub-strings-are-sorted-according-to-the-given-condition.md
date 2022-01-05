# 给定一个字符串和一个整数 k，当所有子字符串按照给定条件

排序后，找到第 kth 个子字符串

> 原文:[https://www . geesforgeks . org/给定一个字符串和一个整数 k-find-the-kth-sub-string-当所有的子字符串都根据给定的条件进行排序时/](https://www.geeksforgeeks.org/given-a-string-and-an-integer-k-find-the-kth-sub-string-when-all-the-sub-strings-are-sorted-according-to-the-given-condition/)

给定一个字符串 **str** ，它的子字符串以这样一种方式形成，即以字符串的第一个字符开始的所有子字符串将首先以其长度的排序顺序出现，然后以字符串的第二个字符开始的所有子字符串以其长度的排序顺序出现，以此类推。
例如对于字符串 **abc** ，其所需顺序的子字符串为 **a** 、 **ab** 、 **abc** 、 **b** 、 **bc** 和 **c** 。
现在给定一个整数 **k** ，任务是按照需要的顺序找到 **kth 子串**。
**举例:**

> **输入:** str = abc，k = 4
> **输出:** b
> 所需顺序为“a”、“ab”、“abc”、“b”、“bc”和“c”
> **输入:** str = abc，k = 9
> **输出:** -1
> 只能有 6 个子串。

**进场:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。一个数组**子串**将用于存储以第一个字符+子串[I–1]开始的子串的数量。现在在数组**子串**上使用二分搜索法，找到所需子串的**起始索引**，然后找到相同子串的**结束索引**，其中**end = length _ of _ string–(子串[start]–k)。**
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to prints kth sub-string
void Printksubstring(string str, int n, int k)
{

    // Total sub-strings possible
    int total = (n * (n + 1)) / 2;

    // If k is greater than total
    // number of sub-strings
    if (k > total) {
        printf("-1\n");
        return;
    }

    // To store number of sub-strings starting
    // with ith character of the string
    int substring[n + 1];
    substring[0] = 0;

    // Compute the values
    int temp = n;
    for (int i = 1; i <= n; i++) {

        // substring[i - 1] is added
        // to store the cumulative sum
        substring[i] = substring[i - 1] + temp;
        temp--;
    }

    // Binary search to find the starting index
    // of the kth sub-string
    int l = 1;
    int h = n;
    int start = 0;

    while (l <= h) {
        int m = (l + h) / 2;

        if (substring[m] > k) {
            start = m;
            h = m - 1;
        }

        else if (substring[m] < k)
            l = m + 1;

        else {
            start = m;
            break;
        }
    }

    // To store the ending index of
    // the kth sub-string
    int end = n - (substring[start] - k);

    // Print the sub-string
    for (int i = start - 1; i < end; i++)
        cout << str[i];
}

// Driver code
int main()
{
    string str = "abc";
    int k = 4;
    int n = str.length();

    Printksubstring(str, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to prints kth sub-string
    static void Printksubstring(String str, int n, int k)
    {

        // Total sub-strings possible
        int total = (n * (n + 1)) / 2;

        // If k is greater than total
        // number of sub-strings
        if (k > total)
        {
            System.out.printf("-1\n");
            return;
        }

        // To store number of sub-strings starting
        // with ith character of the string
        int substring[] = new int[n + 1];
        substring[0] = 0;

        // Compute the values
        int temp = n;
        for (int i = 1; i <= n; i++)
        {

            // substring[i - 1] is added
            // to store the cumulative sum
            substring[i] = substring[i - 1] + temp;
            temp--;
        }

        // Binary search to find the starting index
        // of the kth sub-string
        int l = 1;
        int h = n;
        int start = 0;

        while (l <= h)
        {
            int m = (l + h) / 2;

            if (substring[m] > k)
            {
                start = m;
                h = m - 1;
            }
            else if (substring[m] < k)
            {
                l = m + 1;
            }
            else
            {
                start = m;
                break;
            }
        }

        // To store the ending index of
        // the kth sub-string
        int end = n - (substring[start] - k);

        // Print the sub-string
        for (int i = start - 1; i < end; i++)
        {
            System.out.print(str.charAt(i));
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        String str = "abc";
        int k = 4;
        int n = str.length();

        Printksubstring(str, n, k);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to prints kth sub-string
def Printksubstring(str1, n, k):

    # Total sub-strings possible
    total = int((n * (n + 1)) / 2)

    # If k is greater than total
    # number of sub-strings
    if (k > total):
        print("-1")
        return

    # To store number of sub-strings starting
    # with ith character of the string
    substring = [0 for i in range(n + 1)]
    substring[0] = 0

    # Compute the values
    temp = n
    for i in range(1, n + 1, 1):

        # substring[i - 1] is added
        # to store the cumulative sum
        substring[i] = substring[i - 1] + temp
        temp -= 1

    # Binary search to find the starting index
    # of the kth sub-string
    l = 1
    h = n
    start = 0

    while (l <= h):
        m = int((l + h) / 2)

        if (substring[m] > k):
            start = m
            h = m - 1

        elif (substring[m] < k):
            l = m + 1

        else:
            start = m
            break

    # To store the ending index of
    # the kth sub-string
    end = n - (substring[start] - k)

    # Print the sub-string
    for i in range(start - 1, end):
        print(str1[i], end = "")

# Driver code
if __name__ == '__main__':
    str1 = "abc"
    k = 4
    n = len(str1)

    Printksubstring(str1, n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to prints kth sub-string
    static void Printksubstring(String str, int n, int k)
    {

        // Total sub-strings possible
        int total = (n * (n + 1)) / 2;

        // If k is greater than total
        // number of sub-strings
        if (k > total)
        {
            Console.Write("-1\n");
            return;
        }

        // To store number of sub-strings starting
        // with ith character of the string
        int []substring = new int[n + 1];
        substring[0] = 0;

        // Compute the values
        int temp = n;
        for (int i = 1; i <= n; i++)
        {

            // substring[i - 1] is added
            // to store the cumulative sum
            substring[i] = substring[i - 1] + temp;
            temp--;
        }

        // Binary search to find the starting index
        // of the kth sub-string
        int l = 1;
        int h = n;
        int start = 0;

        while (l <= h)
        {
            int m = (l + h) / 2;

            if (substring[m] > k)
            {
                start = m;
                h = m - 1;
            }
            else if (substring[m] < k)
            {
                l = m + 1;
            }
            else
            {
                start = m;
                break;
            }
        }

        // To store the ending index of
        // the kth sub-string
        int end = n - (substring[start] - k);

        // Print the sub-string
        for (int i = start - 1; i < end; i++)
        {
            Console.Write(str[i]);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {

        String str = "abc";
        int k = 4;
        int n = str.Length;

        Printksubstring(str, n, k);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to prints kth sub-string
function Printksubstring($str, $n, $k)
{

    // Total sub-strings possible
    $total = floor(($n * ($n + 1)) / 2);

    // If k is greater than total
    // number of sub-strings
    if ($k > $total)
    {
        printf("-1\n");
        return;
    }

    // To store number of sub-strings starting
    // with ith character of the string
    $substring = array();
    $substring[0] = 0;

    // Compute the values
    $temp = $n;
    for ($i = 1; $i <= $n; $i++)
    {

        // substring[i - 1] is added
        // to store the cumulative sum
        $substring[$i] = $substring[$i - 1] + $temp;
        $temp--;
    }

    // Binary search to find the starting index
    // of the kth sub-string
    $l = 1;
    $h = $n;
    $start = 0;

    while ($l <= $h)
    {
        $m = floor(($l + $h) / 2);

        if ($substring[$m] > $k)
        {
            $start = $m;
            $h = $m - 1;
        }

        else if ($substring[$m] < $k)
            $l = $m + 1;

        else
        {
            $start = $m;
            break;
        }
    }

    // To store the ending index of
    // the kth sub-string
    $end = $n - ($substring[$start] - $k);

    // Print the sub-string
    for ($i = $start - 1; $i < $end; $i++)
        print($str[$i]);
}

// Driver code
$str = "abc";
$k = 4;
$n = strlen($str);

Printksubstring($str, $n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to prints kth sub-string
    function Printksubstring(str, n, k)
    {

        // Total sub-strings possible
        let total = parseInt((n * (n + 1)) / 2, 10);

        // If k is greater than total
        // number of sub-strings
        if (k > total)
        {
            document.write("-1" + "</br>");
            return;
        }

        // To store number of sub-strings starting
        // with ith character of the string
        let substring = new Array(n + 1);
        substring[0] = 0;

        // Compute the values
        let temp = n;
        for (let i = 1; i <= n; i++)
        {

            // substring[i - 1] is added
            // to store the cumulative sum
            substring[i] = substring[i - 1] + temp;
            temp--;
        }

        // Binary search to find the starting index
        // of the kth sub-string
        let l = 1;
        let h = n;
        let start = 0;

        while (l <= h)
        {
            let m = parseInt((l + h) / 2, 10);

            if (substring[m] > k)
            {
                start = m;
                h = m - 1;
            }
            else if (substring[m] < k)
            {
                l = m + 1;
            }
            else
            {
                start = m;
                break;
            }
        }

        // To store the ending index of
        // the kth sub-string
        let end = n - (substring[start] - k);

        // Print the sub-string
        for (let i = start - 1; i < end; i++)
        {
            document.write(str[i]);
        }
    }

    let str = "abc";
    let k = 4;
    let n = str.length;

    Printksubstring(str, n, k);

//This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
b
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)