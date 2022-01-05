# 由给定操作产生的序列中的第 n 个二进制串中的第 m 位

> 原文:[https://www . geesforgeks . org/mth-第 n 位二进制字符串由给定操作生成/](https://www.geeksforgeeks.org/mth-bit-in-nth-binary-string-from-a-sequence-generated-by-the-given-operations/)

给定两个整数 **N** 和 **M** ，通过以下步骤生成一系列**N**T6】二进制字符串:

*   **S<sub>0</sub>=“0”**
*   **S<sub>1</sub>=“1”**
*   通过公式 **S <sub>i</sub> =反向(S<sub>I–2</sub>)+反向(S<sub>I–1</sub>)**生成剩余字符串

任务是在第**N**T6 弦中找到第**M**T2 套位。

**示例:**

> **输入:** N = 4，M = 3
> T3】输出:0
> T6】解释:T8】S<sub>0</sub>=“0”
> S<sub>1</sub>=“1”
> S<sub>2</sub>=“01”
> S<sub>3</sub>=“110”
> S<sub>4【T22</sub>
> 
> **输入:** N = 5，M = 2
> T3】输出: 1

**天真法:**最简单的方法是生成 S <sub>2</sub> 到**S<sub>N–1</sub>**并遍历字符串**S<sub>N–1</sub>**找到 **M <sup>th</sup>** 位。

***时间复杂度:**O(N * 2<sup>N)</sup>* *****辅助空间:*** *O(N)***

****高效方法:**按照以下步骤优化上述方法:**

*   **计算并存储数组中的前 N 个斐波那契数，比如 **fib[]****
*   **现在，在**N**T6 字符串中搜索**M**T2 位。**
*   ****如果 N > 1 :** 考虑到**S<sub>N</sub>T5】是字符串的[逆串**S<sub>N–2</sub>T11】和字符串**S<sub>N–1</sub>T15】的逆串的串联，则字符串**S<sub>N–2</sub>T19】的长度等于**fib【N–2】**和长度******](https://www.geeksforgeeks.org/reverse-a-string-in-java/)**

    *   **如果 M ≤ fib[n-2]:** 则表示 **M** 位于**S<sub>N–2</sub>**中，因此递归搜索字符串**S<sub>N–2</sub>**的**(fib[N-2]+1–M)<sup>第</sup>** 位。
    *   **如果 M>fib[N–2]:**表示 **M** 位于**S<sub>N–1</sub>**，则递归搜索**S<sub>N–1</sub>**的<sup>第</sup>位。** 
*   **如果 N ≤ 1:** 返回 **N** 。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;
#define maxN 10

// Function to calculate N
// Fibonacci numbers
void calculateFib(int fib[], int n)
{
    fib[0] = fib[1] = 1;
    for (int x = 2; x < n; x++) {
        fib[x] = fib[x - 1] + fib[x - 2];
    }
}

// Function to find the mth bit
// in the string Sn
int find_mth_bit(int n, int m, int fib[])
{
    // Base case
    if (n <= 1) {
        return n;
    }

    // Length of left half
    int len_left = fib[n - 2];

    // Length of the right half
    int len_right = fib[n - 1];

    if (m <= len_left) {

        // Recursive check in the left half
        return find_mth_bit(n - 2,
                            len_left + 1 - m, fib);
    }
    else {
        // Recursive check in the right half
        return find_mth_bit(
            n - 1, len_right + 1
                       - (m - len_left),
            fib);
    }
}

void find_mth_bitUtil(int n, int m)
{

    int fib[maxN];
    calculateFib(fib, maxN);
    int ans = find_mth_bit(n, m, fib);
    cout << ans << ' ';
}

// Driver Code
int main()
{

    int n = 5, m = 3;
    find_mth_bitUtil(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

static final int maxN = 10;

// Function to calculate N
// Fibonacci numbers
static void calculateFib(int fib[],
                         int n)
{
  fib[0] = fib[1] = 1;

  for (int x = 2; x < n; x++)
  {
    fib[x] = fib[x - 1] +
             fib[x - 2];
  }
}

// Function to find the mth bit
// in the String Sn
static int find_mth_bit(int n,
                        int m,
                        int fib[])
{
  // Base case
  if (n <= 1)
  {
    return n;
  }

  // Length of left half
  int len_left = fib[n - 2];

  // Length of the right half
  int len_right = fib[n - 1];

  if (m <= len_left)
  {
    // Recursive check in
    // the left half
    return find_mth_bit(n - 2,
                        len_left +
                        1 - m, fib);
  }
  else
  {
    // Recursive check in
    // the right half
    return find_mth_bit(n - 1,
                        len_right +
                        1 - (m -
                        len_left), fib);
  }
}

static void find_mth_bitUtil(int n, int m)
{
  int []fib = new int[maxN];
  calculateFib(fib, maxN);
  int ans = find_mth_bit(n, m, fib);
  System.out.print(ans + " ");
}

// Driver Code
public static void main(String[] args)
{
  int n = 5, m = 3;
  find_mth_bitUtil(n, m);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for above approach
maxN = 10

# Function to calculate N
# Fibonacci numbers
def calculateFib(fib, n):

    fib[0] = fib[1] = 1
    for x in range(2, n):
        fib[x] = (fib[x - 1] +
                  fib[x - 2])

# Function to find the mth bit
# in the string Sn
def find_mth_bit(n, m, fib):

    # Base case
    if (n <= 1):
        return n

    # Length of left half
    len_left = fib[n - 2]

    # Length of the right half
    len_right = fib[n - 1]

    if (m <= len_left):

        # Recursive check in the left half
        return find_mth_bit(n - 2,
                 len_left + 1 - m, fib)
    else:

        # Recursive check in the right half
        return find_mth_bit(n - 1,
                    len_right + 1 -
                    (m - len_left), fib)

def find_mth_bitUtil(n, m):

    fib = [0 for i in range(maxN)]
    calculateFib(fib, maxN)

    ans = find_mth_bit(n, m, fib)

    print(ans)

# Driver Code
if __name__ == '__main__':

    n = 5
    m = 3

    find_mth_bitUtil(n, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

static int maxN = 10;

// Function to calculate N
// Fibonacci numbers
static void calculateFib(int []fib ,
                         int n)
{
  fib[0] = fib[1] = 1;

  for (int x = 2; x < n; x++)
  {
    fib[x] = fib[x - 1] +
             fib[x - 2];
  }
}

// Function to find the mth bit
// in the String Sn
static int find_mth_bit(int n,
                        int m,
                        int []fib)
{
  // Base case
  if (n <= 1)
  {
    return n;
  }

  // Length of left half
  int len_left = fib[n - 2];

  // Length of the right half
  int len_right = fib[n - 1];

  if (m <= len_left)
  {
    // Recursive check in
    // the left half
    return find_mth_bit(n - 2,
                        len_left +
                        1 - m, fib);
  }
  else
  {
    // Recursive check in
    // the right half
    return find_mth_bit(n - 1,
                        len_right +
                        1 - (m -
                        len_left), fib);
  }
}

static void find_mth_bitUtil(int n,
                             int m)
{
  int []fib = new int[maxN];
  calculateFib(fib, maxN);
  int ans = find_mth_bit(n, m, fib);
  Console.Write(ans + " ");
}

// Driver Code
public static void Main()
{
  int n = 5, m = 3;
  find_mth_bitUtil(n, m);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// JavaScript program for above approach

const maxN = 10

// Function to calculate N
// Fibonacci numbers
function calculateFib(fib, n)
{
    fib[0] = fib[1] = 1;
    for (let x = 2; x < n; x++) {
        fib[x] = fib[x - 1] + fib[x - 2];
    }
}

// Function to find the mth bit
// in the string Sn
function find_mth_bit(n, m, fib)
{
    // Base case
    if (n <= 1) {
        return n;
    }

    // Length of left half
    let len_left = fib[n - 2];

    // Length of the right half
    let len_right = fib[n - 1];

    if (m <= len_left) {

        // Recursive check in the left half
        return find_mth_bit(n - 2,
                            len_left + 1 - m, fib);
    }
    else {
        // Recursive check in the right half
        return find_mth_bit(
            n - 1, len_right + 1
                    - (m - len_left),
            fib);
    }
}

function find_mth_bitUtil(n, m)
{

    let fib = new Array(maxN);
    calculateFib(fib, maxN);
    let ans = find_mth_bit(n, m, fib);
    document.write(ans + " ");
}

// Driver Code

    let n = 5, m = 3;
    find_mth_bitUtil(n, m);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)