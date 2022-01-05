# 将 M 插入 N，使得 M 从位 j 开始，到位 I 结束|设置-2

> 原文:[https://www . geesforgeks . org/insert-m-in-n-so-m-start-bit-j-end-bit-I-set-2/](https://www.geeksforgeeks.org/inserting-m-into-n-such-that-m-starts-at-bit-j-and-ends-at-bit-i-set-2/)

给定两个 32 位数字，N 和 M，以及两个位的位置，I 和 j。编写一个方法，将 M 插入 N，使得 M 从位 j 开始，到位 I 结束。您可以假设位 j 到 I 有足够的空间来容纳所有的 M。假设索引从 0 开始。
**例:**

```
a)  N = 1024 (10000000000),
    M = 19 (10011),
    i = 2, j = 6 
    Output : 1100 (10001001100)
b)  N = 1201 (10010110001)
    M = 8 (1000)
    i = 3, j = 6
    Output: 1217 (10011000001)
```

这个问题在之前的[帖子](https://www.geeksforgeeks.org/insertion-m-n-m-starts-bit-j-ends-bit/)中已经讨论过了。在这篇文章中，讨论了一种不同的方法。
**方法:**想法很简单，下面是分步程序–

*   捕捉 N 中 I 之前的所有位，即从 i-1 到 0。
*   我们不想改变这些位，所以我们将捕获它们并在以后使用
*   清除从 j 到 0 的所有位
*   在 j 至 I 位置将 M 插入 N
*   在各自的位置 ie 插入捕获的位。从 i-1 到 0

让我们试着解决例子 b，以获得对过程的清晰解释。

**捕捉 N 中的位 i-1 到 0:**
创建一个掩码，其 i-1 到 0 位为 1，其余为 0。将 1 移到左边的 I 位置，然后减去 1，得到 i-1 到 0 位设置的位掩码。

```
capture_mask = ( 1 << i ) - 1  
```

例如 b，掩码将是–

```
capture_mask = ( 1 << 3 ) - 1 
Now capture_mask = 1(001)
```

现在*和*这个带有 N、i-1 到 0 位的掩码将保持不变，而其余位变为 0。因此，我们只剩下 i-1 到 0 位。

```
captured_bits = N & capture_mask
```

例如 b，捕获的位将是–

```
captured_bits = N & capture_mask
Now capture_mask = 1 (001)
```

**清除 N 中从 j 到 0 的位:**
由于位已被捕获，清除位 j 到 0 而不丢失位 i-1 到 0。创建一个 j 到 0 位为 0，其余为 1 的掩码。通过向左移动-1 到 j+1 位置来创建这样的掩码。

```
clear_mask = -1 << ( j + 1 )
```

现在将位 j 清零，*和*用 n 屏蔽

```
N  &= clear_mask 
```

例如，b 将是:

```
N &= clear_mask 
Now N = 1152 (10010000000)
```

**N 中插入 M:**

现在，因为 N 已清除了从 j 到 0 的位，所以只需将 M 放入 N 中，并将 M i 位置向左移动，将 M 的 MSB 与 N 中的 j 位置对齐

```
M <<= i
```

例如 b-

```
M <<= 3
Now M = 8 << 3 = 64 (1000000)
```

用 N 做 M 的*或*，将 M 插入所需位置。

```
N |= M
```

例如 b–

```
N |= M 
Now N = 1152 | 64 = 1216 (10011000000) 
```

**将捕获的位插入 N:**

到目前为止，M 已经被插入到 n 中。现在唯一剩下的事情就是将 i-1 位置的捕获位合并回 0。这可以简单地通过 N 和捕获位的或来完成–

```
N |= captured_bits
```

例如 b–

```
N |= captured_bits
N = 1216 | 1 = 1217 (10011000001)
```

所以最后在插入之后，得到下面的位集。

```
N(before) = 1201 (10010110001)
N(after) = 1201 (10011000001)
```

以下是上述方法的实现:

## C++

```
// C++ program to insert 32-bit number
// M into N using bit magic
#include <bits/stdc++.h>
using namespace std;

// print binary representation of n
void bin(unsigned n)
{
    if (n > 1)
        bin(n / 2);
    printf("%d", n % 2);
}

// Insert m into n
int insertion(int n, int m, int i, int j)
{
    int clear_mask = -1 << (j + 1);
    int capture_mask = (1 << i) - 1;

    // Capturing bits from i-1 to 0
    int captured_bits = n & capture_mask;

    // Clearing bits from j to 0
    n &= clear_mask;

    // Shifting m to align with n
    m = m << i;

    // Insert m into n
    n |= m;

    // Insert captured bits
    n |= captured_bits;

    return n;
}

// Driver Code
int main()
{

    // print original bitset
    int N = 1201, M = 8, i = 3, j = 6;
    cout << "N = " << N << "(";
    bin(N);
    cout << ")"
         << "\n";

    // print original bitset
    cout << "M = " << M << "(";
    bin(M);
    cout << ")"
         << "\n";

    // Call function to insert M to N
    N = insertion(N, M, i, j);
    cout << "After inserting M into N from 3 to 6"
         << "\n";

    // Print the inserted bitset
    cout << "N = " << N << "(";
    bin(N);
    cout << ")"
         << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to insert
// 32-bit number M into N
// using bit magic
import java.io.*;

class GFG
{

// print binary
// representation of n
static void bin(long n)
{
    if (n > 1)
        bin(n / 2);
    System.out.print(n % 2);
}

// Insert m into n
static int insertion(int n, int m,
                     int i, int j)
{
    int clear_mask = -1 << (j + 1);
    int capture_mask = (1 << i) - 1;

    // Capturing bits from i-1 to 0
    int captured_bits = n & capture_mask;

    // Clearing bits from j to 0
    n &= clear_mask;

    // Shifting m to align with n
    m = m << i;

    // Insert m into n
    n |= m;

    // Insert captured bits
    n |= captured_bits;

    return n;
}

// Driver Code
public static void main (String[] args)
{
    // print original bitset
    int N = 1201, M = 8, i = 3, j = 6;
    System.out.print("N = " + N + "(");
    bin(N);
    System.out.println(")");

    // print original bitset
    System.out.print("M = " + M + "(");
    bin(M);
    System.out.println(")");

    // Call function to insert M to N
    N = insertion(N, M, i, j);
    System.out.println( "After inserting M " +
                        "into N from 3 to 6");

    // Print the inserted bitset
    System.out.print("N = " + N + "(");
    bin(N);
    System.out.println(")");
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python 3 program to insert 32-bit number
# M into N using bit magic

# insert M into N
def insertion(n, m, i, j):

    clear_mask = -1 << (j + 1)
    capture_mask = (1 << i) - 1

    # Capturing bits from i-1 to 0
    captured_bits = n & capture_mask

    # Clearing bits from j to 0
    n &= clear_mask

    # Shifting m to align with n
    m = m << i

    # Insert m into n
    n |= m

    # Insert captured bits
    n |= captured_bits

    return n

# Driver
def main():
    N = 1201; M = 8; i = 3; j = 6
    print("N = {}({})".format(N, bin(N)))
    print("M = {}({})".format(M, bin(M)))
    N = insertion(N, M, i, j)
    print("***After inserting M into N***")
    print("N = {}({})".format(N, bin(N)))

if __name__ == '__main__':
    main()
```

## C#

```
// C# program to insert
// 32-bit number M into N
// using bit magic
using System;

class GFG
{

// print binary
// representation of n
static void bin(long n)
{
    if (n > 1)
        bin(n / 2);
    Console.Write(n % 2);
}

// Insert m into n
static int insertion(int n, int m,
                     int i, int j)
{
    int clear_mask = -1 << (j + 1);
    int capture_mask = (1 << i) - 1;

    // Capturing bits from i-1 to 0
    int captured_bits = n & capture_mask;

    // Clearing bits from j to 0
    n &= clear_mask;

    // Shifting m to align with n
    m = m << i;

    // Insert m into n
    n |= m;

    // Insert captured bits
    n |= captured_bits;

    return n;
}

// Driver Code
static public void Main (String []args)
{
    // print original bitset
    int N = 1201, M = 8, i = 3, j = 6;
    Console.Write("N = " + N + "(");
    bin(N);
    Console.WriteLine(")");

    // print original bitset
    Console.Write("M = " + M + "(");
    bin(M);
    Console.WriteLine(")");

    // Call function to
    // insert M to N
    N = insertion(N, M, i, j);
    Console.WriteLine("After inserting M " +
                      "into N from 3 to 6");

    // Print the inserted bitset
    Console.Write("N = " + N + "(");
    bin(N);
    Console.WriteLine(")");
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to insert 32-bit number
// M into N using bit magic

// print binary representation of n
function bin($n)
{
    if ($n > 1)
        bin($n / 2);
    echo $n % 2;
}

// Insert m into n
function insertion($n, $m, $i, $j)
{
    $clear_mask = -1 << ($j + 1);
    $capture_mask = (1 << $i) - 1;

    // Capturing bits from i-1 to 0
    $captured_bits = $n & $capture_mask;

    // Clearing bits from j to 0
    $n &= $clear_mask;

    // Shifting m to align with n
    $m = $m << $i;

    // Insert m into n
    $n |= $m;

    // Insert captured bits
    $n |= $captured_bits;

    return $n;
}

// Driver Code

// print original bitset
$N = 1201;
$M = 8;
$i = 3;
$j = 6;
echo "N = " . $N ."(";
bin($N);
echo ")" ."\n";

// print original bitset
echo "M = " . $M ."(";
bin($M);
echo ")". "\n";

// Call function to insert M to N
$N = insertion($N, $M, $i, $j);
echo "After inserting M into N " .
              "from 3 to 6" ."\n";

// Print the inserted bitset
echo "N = " . $N . "(";
bin($N);
echo ")". "\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to insert
// 32-bit number M into N
// using bit magic

    // print binary
// representation of n
    function bin(n)
    {
        if (n > 1)
            bin(Math.floor(n / 2));
        document.write(n % 2);
    }

    // Insert m into n
    function insertion(n,m,i,j)
    {
        let clear_mask = -1 << (j + 1);
    let capture_mask = (1 << i) - 1;

    // Capturing bits from i-1 to 0
    let captured_bits = n & capture_mask;

    // Clearing bits from j to 0
    n &= clear_mask;

    // Shifting m to align with n
    m = m << i;

    // Insert m into n
    n |= m;

    // Insert captured bits
    n |= captured_bits;

    return n;
    }

    // Driver Code

    // print original bitset
    let N = 1201, M = 8, i = 3, j = 6;
    document.write("N = " + N + "(");
    bin(N);
    document.write(")<br>");

    // print original bitset
    document.write("M = " + M + "(");
    bin(M);
    document.write(")<br>");

    // Call function to insert M to N
    N = insertion(N, M, i, j);
    document.write( "After inserting M " +
                        "into N from 3 to 6<br>");

    // Print the inserted bitset
    document.write("N = " + N + "(");
    bin(N);
    document.write(")<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
N = 1201(10010110001)
M = 8(1000)
After inserting M into N from 3 to 6
N = 1217(10011000001)
```