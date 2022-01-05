# 两个整数之间的汉明距离

> 原文:[https://www . geeksforgeeks . org/hamming-两个整数之间的距离/](https://www.geeksforgeeks.org/hamming-distance-between-two-integers/)

给定两个整数，任务是找出两个整数之间的汉明距离。[两个整数之间的汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)是两个数中同一位置不同的位数。
**例:**

```
Input: n1 = 9, n2 = 14
Output: 3
9 = 1001, 14 = 1110
No. of Different bits = 3

Input: n1 = 4, n2 = 8
Output: 2
```

**进场:**

1.  计算两个数的异或。
2.  [计数设定位数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate hamming distance
int hammingDistance(int n1, int n2)
{
    int x = n1 ^ n2;
    int setBits = 0;

    while (x > 0) {
        setBits += x & 1;
        x >>= 1;
    }

    return setBits;
}

// Driver code
int main()
{
    int n1 = 9, n2 = 14;
    cout << hammingDistance(9, 14) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to calculate hamming distance
static int hammingDistance(int n1, int n2)
{
    int x = n1 ^ n2;
    int setBits = 0;

    while (x > 0)
    {
        setBits += x & 1;
        x >>= 1;
    }

    return setBits;
}

// Driver code
public static void main(String[] args)
{
    int n1 = 9, n2 = 14;
    System.out.println(hammingDistance(n1, n2));
}
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to calculate hamming distance
def hammingDistance(n1, n2) :

    x = n1 ^ n2
    setBits = 0

    while (x > 0) :
        setBits += x & 1
        x >>= 1

    return setBits

if __name__=='__main__':
    n1 = 9
    n2 = 14
    print(hammingDistance(9, 14))

# this code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# implementation of above approach
class GFG
{

// Function to calculate
// hamming distance
static int hammingDistance(int n1, int n2)
{
    int x = n1 ^ n2;
    int setBits = 0;

    while (x > 0)
    {
        setBits += x & 1;
        x >>= 1;
    }

    return setBits;
}

// Driver code
static void Main()
{
    int n1 = 9, n2 = 14;
    System.Console.WriteLine(hammingDistance(n1, n2));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP implementation of above approach

// Function to calculate hamming distance
function hammingDistance($n1, $n2)
{
    $x = $n1 ^ $n2;
    $setBits = 0;

    while ($x > 0)
    {
        $setBits += $x & 1;
        $x >>= 1;
    }

    return $setBits;
}

// Driver code
$n1 = 9;
$n2 = 14;
echo(hammingDistance(9, 14));

// This code is contributed by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to calculate hamming distance
function hammingDistance(n1, n2)
{
    let x = n1 ^ n2;
    let setBits = 0;

    while (x > 0) {
        setBits += x & 1;
        x >>= 1;
    }

    return setBits;
}

// Driver code
    let n1 = 9, n2 = 14;
    document.write(hammingDistance(9, 14));

</script>
```

**Output**

```
3

```

**注意:**可以使用 __builtin_popcount()函数对设置的位数进行计数。

**方法 2:**

1.计算两个数的最大值。

2.检查两个位置的设置位。

## C++

```
#include <bits/stdc++.h>
using namespace std;
int hammingDistance(int x, int y)
{
    int ans = 0;
    int m = max(x, y);
    while (m) {
        int c1 = x & 1;
        int c2 = y & 1;
        if (c1 != c2)
            ans += 1;
        m = m >> 1;
        x = x >> 1;
        y = y >> 1;
    }
    return ans;
}
int main()
{
    int n1 = 4, n2 = 8;
    int hdist = hammingDistance(n1, n2);
    cout << hdist << endl;
    return 0;
}
```

**Output**

```
2

```