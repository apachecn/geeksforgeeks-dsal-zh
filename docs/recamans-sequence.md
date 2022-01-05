# 雷卡曼的序列

> 原文:[https://www.geeksforgeeks.org/recamans-sequence/](https://www.geeksforgeeks.org/recamans-sequence/)

给定一个整数 n .打印[重铸人序列](http://mathworld.wolfram.com/RecamansSequence.html)的前 n 个元素。
**例:**

```
Input : n = 6
Output : 0, 1, 3, 6, 2, 7

Input  : n = 17
Output : 0, 1, 3, 6, 2, 7, 13, 20, 12, 21, 
         11, 22, 10, 23, 9, 24, 8
```

它基本上是一个以定义域和同定义域为自然数和 0 的函数。其递归定义如下:
具体来说，让 a(n)表示第(n+1)项。(0 已经存在)。
规则说:

```
a(0) = 0,
if n > 0 and the number is not 
   already included in the sequence,
     a(n) = a(n - 1) - n 
else 
     a(n) = a(n-1) + n. 
```

下面是一个简单的实现，我们将所有 n 个重铸序列号存储在一个数组中。我们用上面提到的递归公式计算下一个数。

## C++

```
// C++ program to print n-th number in Recaman's
// sequence
#include <bits/stdc++.h>
using namespace std;

// Prints first n terms of Recaman sequence
int recaman(int n)
{
    // Create an array to store terms
    int arr[n];

    // First term of the sequence is always 0
    arr[0] = 0;
    printf("%d, ", arr[0]);

    // Fill remaining terms using recursive
    // formula.
    for (int i=1; i< n; i++)
    {
        int curr = arr[i-1] - i;
        int j;
        for (j = 0; j < i; j++)
        {
            // If arr[i-1] - i is negative or
            // already exists.
            if ((arr[j] == curr) || curr < 0)
            {
                curr = arr[i-1] + i;
                break;
            }
        }

        arr[i] = curr;
        printf("%d, ", arr[i]);
    }
}

// Driver code
int main()
{
    int n = 17;
    recaman(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print n-th number in Recaman's
// sequence
import java.io.*;

class GFG {

    // Prints first n terms of Recaman sequence
    static void recaman(int n)
    {
        // Create an array to store terms
        int arr[] = new int[n];

        // First term of the sequence is always 0
        arr[0] = 0;
        System.out.print(arr[0]+" ,");

        // Fill remaining terms using recursive
        // formula.
        for (int i = 1; i < n; i++)
        {
            int curr = arr[i - 1] - i;
            int j;
            for (j = 0; j < i; j++)
            {
                // If arr[i-1] - i is negative or
                // already exists.
                if ((arr[j] == curr) || curr < 0)
                {
                    curr = arr[i - 1] + i;
                    break;
                }
            }

            arr[i] = curr;
            System.out.print(arr[i]+", ");

        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 17;
        recaman(n);

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to print n-th
# number in Recaman's sequence

# Prints first n terms of Recaman
# sequence
def recaman(n):

    # Create an array to store terms
    arr = [0] * n

    # First term of the sequence
    # is always 0
    arr[0] = 0
    print(arr[0], end=", ")

    # Fill remaining terms using
    # recursive formula.
    for i in range(1, n):

        curr = arr[i-1] - i
        for j in range(0, i):

            # If arr[i-1] - i is
            # negative or already
            # exists.
            if ((arr[j] == curr) or curr < 0):
                curr = arr[i-1] + i
                break

        arr[i] = curr
        print(arr[i], end=", ")

# Driver code
n = 17

recaman(n)

# This code is contributed by Smitha.
```

## C#

```
// C# program to print n-th number in Recaman's
// sequence
using System;

class GFG {

    // Prints first n terms of Recaman sequence
    static void recaman(int n)
    {
        // Create an array to store terms
        int []arr = new int[n];

        // First term of the sequence is always 0
        arr[0] = 0;
        Console.Write(arr[0]+" ,");

        // Fill remaining terms using recursive
        // formula.
        for (int i = 1; i < n; i++)
        {
            int curr = arr[i - 1] - i;
            int j;
            for (j = 0; j < i; j++)
            {
                // If arr[i-1] - i is negative or
                // already exists.
                if ((arr[j] == curr) || curr < 0)
                {
                    curr = arr[i - 1] + i;
                    break;
                }
            }

            arr[i] = curr;
        Console.Write(arr[i]+", ");

        }
    }

    // Driver code
    public static void Main ()
    {
        int n = 17;
        recaman(n);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print n-th
// number in Recaman's sequence

// Prints first n terms
// of Recaman sequence
function recaman($n)
{

    // First term of the
    // sequence is always 0
    $arr[0] = 0;
    echo $arr[0], ", ";

    // Fill remaining terms
    // using recursive formula.
    for ($i = 1; $i < $n; $i++)
    {
            $curr = $arr[$i - 1] - $i;
            $j;
        for ($j = 0; $j < $i; $j++)
        {

            // If arr[i-1] - i
            // is negative or
            // already exists.
            if (($arr[$j] == $curr) || $curr < 0)
            {
                $curr = $arr[$i-1] + $i;
                break;
            }
        }

        $arr[$i] = $curr;
        echo $arr[$i], ", ";
    }
}

    // Driver Code
    $n = 17;
    recaman($n);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to print
    // n-th number in Recaman's sequence

    // Prints first n terms of Recaman sequence
    function recaman(n)
    {
        // Create an array to store terms
        let arr = new Array(n);

        // First term of the sequence is always 0
        arr[0] = 0;
        document.write(arr[0]+" ,");

        // Fill remaining terms using recursive
        // formula.
        for (let i = 1; i < n; i++)
        {
            let curr = arr[i - 1] - i;
            let j;
            for (j = 0; j < i; j++)
            {
                // If arr[i-1] - i is negative or
                // already exists.
                if ((arr[j] == curr) || curr < 0)
                {
                    curr = arr[i - 1] + i;
                    break;
                }
            }

            arr[i] = curr;
        document.write(arr[i]+", ");

        }
    }

      let n = 17;
      recaman(n);

</script>
```

**输出:**

```
0, 1, 3, 6, 2, 7, 13, 20, 12, 21, 11, 22, 10, 23, 9, 24, 8, 
```

时间复杂度:O(n)<sup>2</sup>)
辅助空间:O(n)
**优化:**
我们可以使用哈希来存储之前计算的值，并且可以让这个程序在 O(n)时间内工作。

## C++

```
// C++ program to print n-th number in Recaman's
// sequence
#include <bits/stdc++.h>
using namespace std;

// Prints first n terms of Recaman sequence
void recaman(int n)
{
    if (n <= 0)
      return;

    // Print first term and store it in a hash
    printf("%d, ", 0);
    unordered_set<int> s;
    s.insert(0);

    // Print remaining terms using recursive
    // formula.
    int prev = 0;
    for (int i=1; i< n; i++)
    {
        int curr = prev - i;

        // If arr[i-1] - i is negative or
        // already exists.
        if (curr < 0 || s.find(curr) != s.end())
           curr = prev + i;

        s.insert(curr);

        printf("%d, ", curr);
        prev = curr;
    }
}

// Driver code
int main()
{
    int n = 17;
    recaman(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print n-th number
// in Recaman's sequence
import java.util.*;

class GFG
{

// Prints first n terms of Recaman sequence
static void recaman(int n)
{
    if (n <= 0)
    return;

    // Print first term and store it in a hash
    System.out.printf("%d, ", 0);
    HashSet<Integer> s = new HashSet<Integer>();
    s.add(0);

    // Print remaining terms using
    // recursive formula.
    int prev = 0;
    for (int i = 1; i< n; i++)
    {
        int curr = prev - i;

        // If arr[i-1] - i is negative or
        // already exists.
        if (curr < 0 || s.contains(curr))
            curr = prev + i;

        s.add(curr);

        System.out.printf("%d, ", curr);
        prev = curr;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 17;
    recaman(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print n-th number in
# Recaman's sequence

# Prints first n terms of Recaman sequence
def recaman(n):

    if(n <= 0):
        return

    # Print first term and store it in a hash
    print(0, ",", end='')
    s = set([])
    s.add(0)

    # Print remaining terms using recursive
    # formula.
    prev = 0
    for i in range(1, n):

        curr = prev - i

        # If arr[i-1] - i is negative or
        # already exists.
        if(curr < 0 or curr in s):
            curr = prev + i

        s.add(curr)

        print(curr, ",", end='')
        prev = curr

# Driver code
if __name__=='__main__':
    n = 17
    recaman(n)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print n-th number
// in Recaman's sequence
using System;
using System.Collections.Generic;

class GFG
{

// Prints first n terms of Recaman sequence
static void recaman(int n)
{
    if (n <= 0)
    return;

    // Print first term and store it in a hash
    Console.Write("{0}, ", 0);
    HashSet<int> s = new HashSet<int>();
    s.Add(0);

    // Print remaining terms using
    // recursive formula.
    int prev = 0;
    for (int i = 1; i < n; i++)
    {
        int curr = prev - i;

        // If arr[i-1] - i is negative or
        // already exists.
        if (curr < 0 || s.Contains(curr))
            curr = prev + i;

        s.Add(curr);

        Console.Write("{0}, ", curr);
        prev = curr;
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 17;
    recaman(n);
}
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print n-th number in
// Recaman's sequence

// Prints first n terms of Recaman sequence
function recaman($n)
{
    if($n <= 0)
        return;

    // Print first term and store
    // it in a hash
    print("0, ");
    $s = array();
    array_push($s, 0);

    // Print remaining terms using recursive
    // formula.
    $prev = 0;
    for ($i = 1; $i < $n; $i++)
    {
        $curr = $prev - $i;

        // If arr[i-1] - i is negative or
        // already exists.
        if($curr < 0 or in_array($curr, $s))
            $curr = $prev + $i;

        array_push($s, $curr);

        print($curr.", ");
        $prev = $curr;
    }

}

// Driver code
$n = 17;
recaman($n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

//  Javascript program to print n-th number
// in Recaman's sequence

// Prints first n terms of Recaman sequence
function recaman(n)
{
    if (n <= 0)
    return;

    // Print first term and store it in a hash
    document.write(0 + ", ");
    let s = new Set();
    s.add(0);

    // Print remaining terms using
    // recursive formula.
    let prev = 0;
    for (let i = 1; i< n; i++)
    {
        let curr = prev - i;

        // If arr[i-1] - i is negative or
        // already exists.
        if (curr < 0 || s.has(curr))
            curr = prev + i;

        s.add(curr);

        document.write(curr + ", ");
        prev = curr;
    }
}

    // Driver code

    let n = 17;
    recaman(n);

</script>
```

**输出:**

```
0, 1, 3, 6, 2, 7, 13, 20, 12, 21, 11, 22, 10, 23, 9, 24, 8, 
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由 **Kishlay 维尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。