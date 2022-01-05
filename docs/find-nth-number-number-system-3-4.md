# 在只有 3 和 4 的数系中找到第 n 个数

> 原文:[https://www . geesforgeks . org/find-n th-number-system-3-4/](https://www.geeksforgeeks.org/find-nth-number-number-system-3-4/)

给定一个只有 3 和 4 的数字系统。求数制中的第 n 个数。数字系统中的前几个数字是:3、4、33、34、43、44、333、334、343、344、433、434、443、444、3333、3334、3343、3344、3433、3434、3443、3444、……
来源: [Zoho 访谈](https://www.geeksforgeeks.org/zoho-interview-set-2-campus/)

我们可以用(i-1)位的数字生成所有 I 位的数字。其思想是首先在所有带有(i-1)数字的数字中添加一个“3”作为前缀，然后添加一个“4”。例如，2 位数的数字是 33、34、43 和 44。有 3 个数字的数字是 333、334、343、344、433、434、443 和 444，它们可以通过首先添加 3 作为前缀，然后添加 4 来生成。
以下是详细步骤。

```
1) Create an array 'arr[]' of strings size n+1\. 
2) Initialize arr[0] as empty string. (Number with 0 digits)
3) Do following while array size is smaller than or equal to n
.....a) Generate numbers by adding a 3 as prefix to the numbers generated 
        in previous iteration.  Add these numbers to arr[]
.....a) Generate numbers by adding a 4 as prefix to the numbers generated 
        in previous iteration. Add these numbers to arr[]
```

感谢 kaushik Lele 在评论[这里](https://www.geeksforgeeks.org/zoho-interview-set-2-campus/)提出这个想法。下面是相同的 C++实现。

## C++

```
// C++ program to find n'th number
// in a number system with
// only 3 and 4
#include <iostream>
using namespace std;

// Function to find n'th number
// in a number system with only
// 3 and 4
void find(int n)
{

    // An array of strings to
    // store first n numbers. arr[i]
    // stores i'th number
    string arr[n + 1];

    // arr[0] stores the empty string (String
    // with 0 digits)
    arr[0] = "";

    // size indicates number of
    // current elements in arr[]. m
    // indicates number of elements
    // added to arr[] in
    // previous iteration.
    int size = 1, m = 1;

    // Every iteration of following
    // loop generates and adds
    // 2*m numbers to arr[] using 
    // the m numbers generated in
    // previous iteration.
    while (size <= n) {

        // Consider all numbers added
        // in previous iteration,
        // add a prefix "3" to them and
        // add new numbers to
        // arr[]
        for (int i = 0; i < m && (size + i) <= n; i++)
            arr[size + i] = "3" + arr[size - m + i];

        // Add prefix "4" to numbers
        // of previous iteration
        // and add new numbers to arr[]
        for (int i = 0; i < m && (size + m + i) <= n; i++)
            arr[size + m + i] = "4" + arr[size - m + i];

        // Update no. of elements added in previous
        // iteration
        m = m << 1; // Or m = m*2;

        // Update size
        size = size + m;
    }
    cout << arr[n] << endl;
}

// Driver program to test above functions
int main()
{
    for (int i = 1; i < 16; i++)
        find(i);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n'th number in a number system with
// only 3 and 4
import java.io.*;

class GFG {
    // Function to find n'th number in a number system with
    // only 3 and 4
    static void find(int n)
    {
        // An array of strings to store first n numbers.
        // arr[i] stores i'th number
        String[] arr = new String[n + 1];

        // arr[0] stores the empty string (String with 0
        // digits)
        arr[0] = "";

        // size indicates number of current elements in
        // arr[], m indicates number of elements added to
        // arr[] in previous iteration
        int size = 1, m = 1;

        // Every iteration of following loop generates and
        // adds 2*m numbers to arr[] using the m numbers
        // generated in previous iteration
        while (size <= n) {
            // Consider all numbers added in previous
            // iteration, add a prefix "3" to them and add
            // new numbers to arr[]
            for (int i = 0; i < m && (size + i) <= n; i++)
                arr[size + i] = "3" + arr[size - m + i];

            // Add prefix "4" to numbers of previous
            // iteration and add new numbers to arr[]
            for (int i = 0; i < m && (size + m + i) <= n;
                 i++)
                arr[size + m + i] = "4" + arr[size - m + i];

            // Update no. of elements added in previous
            // iteration
            m = m << 1; // Or m = m*2;

            // Update size
            size = size + m;
        }
        System.out.println(arr[n]);
    }

    // Driver program
    public static void main(String[] args)
    {
        for (int i = 0; i < 16; i++)
            find(i);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to find n'th
# number in a number system
# with only 3 and 4

# Function to find n'th number in a
# number system with only 3 and 4
def find(n):

    # An array of strings to store
    # first n numbers. arr[i] stores
    # i'th number
    arr = [''] * (n + 1);

    # arr[0] = ""; # arr[0] stores
    # the empty string (String with 0 digits)

    # size indicates number of current
    # elements in arr[]. m indicates
    # number of elements added to arr[]
    # in previous iteration.
    size = 1;
    m = 1;

    # Every iteration of following
    # loop generates and adds 2*m
    # numbers to arr[] using the m
    # numbers generated in previous
    # iteration.
    while (size <= n):

        # Consider all numbers added
        # in previous iteration, add
        # a prefix "3" to them and
        # add new numbers to arr[]
        i = 0;
        while(i < m and (size + i) <= n):
            arr[size + i] = "3" + arr[size - m + i];
            i += 1;

        # Add prefix "4" to numbers of
        # previous iteration and add
        # new numbers to arr[]
        i = 0;
        while(i < m and (size + m + i) <= n):
            arr[size + m + i] = "4" + arr[size - m + i];
            i += 1;

        # Update no. of elements added
        # in previous iteration
        m = m << 1; # Or m = m*2;

        # Update size
        size = size + m;
    print(arr[n]);

# Driver Code
for i in range(1, 16):
    find(i);

# This code is contributed by mits
```

## C#

```
// C# program to find n'th number in a
// number system with only 3 and 4
using System;

class GFG {

    // Function to find n'th number in a
    // number system with only 3 and 4
    static void find(int n)
    {

        // An array of strings to store first
        // n numbers. arr[i] stores i'th number
        String[] arr = new String[n + 1];

        // arr[0] stores the empty string
        // (String with 0 digits)
        arr[0] = "";

        // size indicates number of current
        // elements in arr[], m indicates
        // number of elements added to arr[]
        // in previous iteration
        int size = 1, m = 1;

        // Every iteration of following loop
        // generates and adds 2*m numbers to
        // arr[] using the m numbers generated
        // in previous iteration
        while (size <= n)
        {
            // Consider all numbers added in
            // previous iteration, add a prefix
            // "3" to them and add new numbers
            // to arr[]
            for (int i = 0; i < m &&
                             (size + i) <= n; i++)

                arr[size + i] = "3" +
                               arr[size - m + i];

            // Add prefix "4" to numbers of
            // previous iteration and add new
            // numbers to arr[]
            for (int i = 0; i < m &&
                          (size + m + i) <= n; i++)

                arr[size + m + i] = "4" +
                                  arr[size - m + i];

            // Update no. of elements added
            // in previous iteration
            m = m << 1; // Or m = m*2;

            // Update size
            size = size + m;
        }

        Console.WriteLine(arr[n]);
    }

    // Driver program
    public static void Main ()
    {
        for (int i = 0; i < 16; i++)
            find(i);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n'th
// number in a number system
// with only 3 and 4

// Function to find n'th number in a
// number system with only 3 and 4
function find($n)
{
    // An array of strings to store
    // first n numbers. arr[i] stores
    // i'th number
    $arr = array_fill(0, $n + 1, "");

    // $arr[0] = ""; // arr[0] stores
    // the empty string (String with 0 digits)

    // size indicates number of current
    // elements in arr[]. m indicates
    // number of elements added to arr[]
    // in previous iteration.
    $size = 1;
    $m = 1;

    // Every iteration of following
    // loop generates and adds 2*m
    // numbers to arr[] using the m
    // numbers generated in previous
    // iteration.
    while ($size <= $n)
    {
        // Consider all numbers added
        // in previous iteration, add
        // a prefix "3" to them and
        // add new numbers to arr[]
        for ($i = 0; $i < $m &&
            ($size + $i) <= $n; $i++)
            $arr[$size + $i] = "3" .
            $arr[$size - $m + $i];

        // Add prefix "4" to numbers of
        // previous iteration and add
        // new numbers to arr[]
        for ($i = 0; $i < $m &&
            ($size + $m + $i) <= $n; $i++)
            $arr[$size + $m + $i] = "4" .
            $arr[$size - $m + $i];

        // Update no. of elements added
        // in previous iteration
        $m = $m << 1; // Or m = m*2;

        // Update size
        $size = $size + $m;
    }
    echo $arr[$n] . "\n";
}

// Driver Code
for ($i = 1; $i < 16; $i++)
    find($i);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to find n'th number in a number system with
// only 3 and 4

   // Function to find n'th number in a number system with
    // only 3 and 4
function find(n)
{

    // An array of strings to store first n numbers.
    // arr[i] stores i'th number
    var arr = Array.from({length: n + 1}, (_, i) => " ");

    // arr[0] stores the empty string (String with 0
    // digits)
    arr[0] = "";

    // size indicates number of current elements in
    // arr, m indicates number of elements added to
    // arr in previous iteration
    var size = 1, m = 1;

    // Every iteration of following loop generates and
    // adds 2*m numbers to arr using the m numbers
    // generated in previous iteration
    while (size <= n)
    {

        // Consider all numbers added in previous
        // iteration, add a prefix "3" to them and add
        // new numbers to arr
        for (var i = 0; i < m && (size + i) <= n; i++)
            arr[size + i] = "3" + arr[size - m + i];

        // Add prefix "4" to numbers of previous
        // iteration and add new numbers to arr
        for (var i = 0; i < m && (size + m + i) <= n;
             i++)
            arr[size + m + i] = "4" + arr[size - m + i];

        // Update no. of elements added in previous
        // iteration
        m = m << 1; // Or m = m*2;

        // Update size
        size = size + m;
    }
    document.write(arr[n]+"<br>");
}

// Driver program
for (i = 0; i < 16; i++)
    find(i);

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
3
4
33
34
43
44
333
334
343
344
433
434
443
444
3333
```

#### 更好的方法(使用位) :

这个想法是由 Arjun J 提出的(https://auth . geeksforgeeks . org/user/camsboyfriend/profile)。

这里的想法是，因为我们将只处理两个数字，即 3 和 4，所以我们可以将它们与二进制数进行比较。

**说明:**

```
1)  3   -  0     (0)
2)  4   -  1     (1)

3)  33  -  00    (0)
4)  34  -  01    (1)
5)  43  -  10    (2)  
6)  44  -  11    (3)

7)  333 -  000   (0)
8)  334 -  001   (1)
9)  343 -  010   (2) 
10) 344 -  011   (3)
11) 433 -  100   (4)
12) 434 -  101   (5)
13) 443 -  110   (6)
14) 444 -  111   (7)
15) 3333 - 1000  (8)
```

> 这里我们可以注意到
> 
> 1.  每(*n–1)*个数字会得到一个新的数字，其中 *n* 是 2 的幂
> 2.  每当增加一个新的数字，我们就从 0 开始计算二进制数。
> 3.  二进制形式的 **0** 对应于我们的数字系统中的 **3** ，类似地 **1** 对应于 **4。**

下面是相同的 C++实现:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// function to find highest power of 2
// less than or equal to n
int highestPowerof2(unsigned int n)
{
    if (n < 1)
        return 0;

    int res = 1;

    for (int i = 0; i < 8 * sizeof(unsigned int); i++) {
        int curr = 1 << i;

        if (curr > n)
            break;

        res = curr;
    }

    return res;
}

// function to convert decimal to binary form
vector<int> decToBinary(int n, int size)
{
    vector<int> binaryNum(size + 1);

    int i = 0;
    while (n > 0) {
        binaryNum[i] = n % 2;
        n = (n >> 1);
        i++;
    }

    return binaryNum;
}

// Driver Code
signed main()
{
    for (int n = 1; n < 16; n++) {
        int hp2 = highestPowerof2(n + 1);

        int howMany = n - hp2 + 1;

        vector<int> arr
            = decToBinary(howMany, log2(hp2 - 1));

        for (int i = log2(hp2 - 1); i >= 0; i--) {
            if (arr[i])
                cout << 4;
            else
                cout << 3;
        }
        cout << '\n';
    }
}
```

**输出:**

```
3
4
33
34
43
44
333
334
343
344
433
434
443
444
3333
```

本文由**拉曼**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。