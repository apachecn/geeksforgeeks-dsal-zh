# 给定两个二进制字符串，执行运算直到 B > 0 并打印结果

> 原文:[https://www . geesforgeks . org/给定-两个二进制字符串-执行-操作-直到-B- 0-并打印结果/](https://www.geeksforgeeks.org/given-two-binary-strings-perform-operation-until-b-0-and-print-the-result/)

给定两个长度为 **N** 和 **M** 的二进制字符串 **A** 和 **B** (最多 10 个 <sup>5 个</sup>)。任务是重复下面的过程，找到答案。

```
Initialize ans = 0
while (B > 0)
    ans += A & B (bitwise AND)
    B = B / 2
print ans
```

**注:**答案可以很大所以打印**答案% 100000007**。
**例:**

```
Input: A = "1001", B = "10101"
Output: 11
1001 & 10101 = 1, ans = 1, B = 1010
1001 & 1010 = 8, ans = 9, B = 101
1001 & 101 = 1, ans = 10, B = 10
1001 & 10 = 0, ans = 10, B = 1
1001 & 1 = 1, ans = 11, B = 0

Input: A = "1010", B = "1101"
Output: 12
```

**方法:**由于在所有迭代中只有 **B** 受到影响，将一个二进制数除以 2 意味着将其右移 1 位，因此可以观察到 **A** 中的一个位将仅受到位于左侧的 B 中的**设置位的影响，即比当前位(包括当前位)更重要。例如**A =“1001”****B =“10101”**， **A** 中的最低有效位将仅受 **B** 中的设置位的影响，即**总共 3 位**和 **A** 中的最高有效位将仅受 **B** 中的单个设置位的影响，即 B** 中的**最高有效位，因为在执行**逐位“与”**时，所有其他设置位在循环的任何迭代中都不会对其产生影响 所以最终的结果会是**2<sup>0</sup>* 3+2<sup>3</sup>* 1 = 3+8 = 11**。
以下是上述办法的实施情况。** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define mod (int)(1e9 + 7)

// Function to return the required result
ll BitOperations(string a, int n, string b, int m)
{

    // Reverse the strings
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());

    // Count the number of set bits in b
    int c = 0;
    for (int i = 0; i < m; i++)
        if (b[i] == '1')
            c++;

    // To store the powers of 2
    ll power[n];
    power[0] = 1;

    // power[i] = pow(2, i) % mod
    for (int i = 1; i < n; i++)
        power[i] = (power[i - 1] * 2) % mod;

    // To store the final answer
    ll ans = 0;
    for (int i = 0; i < n; i++) {
        if (a[i] == '1') {

            // Add power[i] to the ans after
            // multiplying it with the number
            // of set bits in b
            ans += c * power[i];
            if (ans >= mod)
                ans %= mod;
        }

        // Divide by 2 means right shift b>>1
        // if b has 1 at right most side than
        // number of set bits will get decreased
        if (b[i] == '1')
            c--;

        // If no more set bits in b i.e. b = 0
        if (c == 0)
            break;
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    string a = "1001", b = "10101";
    int n = a.length(), m = b.length();

    cout << BitOperations(a, n, b, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int mod = (int)(1e9 + 7);

// Function to return the required result
static int BitOperations(String a,
            int n, String b, int m)
{

    // Reverse the strings
    char[] ch1 = a.toCharArray();
    reverse( ch1 );
    a = new String( ch1 );
    char[] ch2 = b.toCharArray();
    reverse( ch2 );
    b = new String( ch2 );

    // Count the number of set bits in b
    int c = 0;
    for (int i = 0; i < m; i++)
        if (b.charAt(i) == '1')
            c++;

    // To store the powers of 2
    int[] power = new int[n];
    power[0] = 1;

    // power[i] = pow(2, i) % mod
    for (int i = 1; i < n; i++)
        power[i] = (power[i - 1] * 2) % mod;

    // To store the final answer
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        if (a.charAt(i) == '1')
        {

            // Add power[i] to the ans after
            // multiplying it with the number
            // of set bits in b
            ans += c * power[i];
            if (ans >= mod)
                ans %= mod;
        }

        // Divide by 2 means right shift b>>1
        // if b has 1 at right most side than
        // number of set bits will get decreased
        if (b.charAt(i) == '1')
            c--;

        // If no more set bits in b i.e. b = 0
        if (c == 0)
            break;
    }

    // Return the required answer
    return ans;
}

static void reverse(char a[])
{
    int i, k,n=a.length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Driver code
public static void main(String[] args)
{
    String a = "1001", b = "10101";
    int n = a.length(), m = b.length();

    System.out.println(BitOperations(a, n, b, m));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
mod = 1000000007

# Function to return the required result
def BitOperations(a, n, b, m):

    # Reverse the strings
    a = a[::-1]
    b = b[::-1]

    # Count the number of set
    # bits in b
    c = 0
    for i in range(m):
        if (b[i] == '1'):
            c += 1

    # To store the powers of 2
    power = [None] * n
    power[0] = 1

    # power[i] = pow(2, i) % mod
    for i in range(1, n):
        power[i] = (power[i - 1] * 2) % mod

    # To store the final answer
    ans = 0
    for i in range(0, n):
        if (a[i] == '1'):

            # Add power[i] to the ans after
            # multiplying it with the number
            # of set bits in b
            ans += c * power[i]
            if (ans >= mod):
                ans %= mod

        # Divide by 2 means right shift b>>1
        # if b has 1 at right most side than
        # number of set bits will get decreased
        if (b[i] == '1'):
            c -= 1

        # If no more set bits in b i.e. b = 0
        if (c == 0):
            break

    # Return the required answer
    return ans

# Driver code
if __name__ == '__main__':
    a = "1001"
    b = "10101"
    n = len(a)
    m = len(b)

    print(BitOperations(a, n, b, m))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{

static int mod = (int)(1e9 + 7);

// Function to return the required result
static int BitOperations(string a,
            int n, string b, int m)
{

    // Reverse the strings
    char[] ch1 = a.ToCharArray();
    Array.Reverse( ch1 );
    a = new string( ch1 );
    char[] ch2 = b.ToCharArray();
    Array.Reverse( ch2 );
    b = new string( ch2 );

    // Count the number of set bits in b
    int c = 0;
    for (int i = 0; i < m; i++)
        if (b[i] == '1')
            c++;

    // To store the powers of 2
    int[] power = new int[n];
    power[0] = 1;

    // power[i] = pow(2, i) % mod
    for (int i = 1; i < n; i++)
        power[i] = (power[i - 1] * 2) % mod;

    // To store the final answer
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        if (a[i] == '1')
        {

            // Add power[i] to the ans after
            // multiplying it with the number
            // of set bits in b
            ans += c * power[i];
            if (ans >= mod)
                ans %= mod;
        }

        // Divide by 2 means right shift b>>1
        // if b has 1 at right most side than
        // number of set bits will get decreased
        if (b[i] == '1')
            c--;

        // If no more set bits in b i.e. b = 0
        if (c == 0)
            break;
    }

    // Return the required answer
    return ans;
}

// Driver code
static void Main()
{
    string a = "1001", b = "10101";
    int n = a.Length, m = b.Length;

    Console.WriteLine(BitOperations(a, n, b, m));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$GLOBALS['mod'] = (1e9 + 7);

// Function to return the required result
function BitOperations($a, $n, $b, $m)
{

    // Reverse the strings
    $a = strrev($a);
    $b = strrev($b);

    // Count the number of set bits in b
    $c = 0;
    for ($i = 0; $i < $m; $i++)
        if ($b[$i] == '1')
            $c++;

    # To store the powers of 2
    $power = array() ;
    $power[0] = 1;

    // power[i] = pow(2, i) % mod
    for ($i = 1; $i < $n; $i++)
        $power[$i] = ($power[$i - 1] * 2) %
                      $GLOBALS['mod'];

    // To store the final answer
    $ans = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] == '1')
        {

            // Add power[i] to the ans after
            // multiplying it with the number
            // of set bits in b
            $ans += $c * $power[$i];
            if ($ans >= $GLOBALS['mod'])
                $ans %= $GLOBALS['mod'];
        }

        // Divide by 2 means right shift b>>1
        // if b has 1 at right most side than
        // number of set bits will get decreased
        if ($b[$i] == '1')
            $c--;

        // If no more set bits in b i.e. b = 0
        if ($c == 0)
            break;
    }

    // Return the required answer
    return $ans;
}

// Driver code
$a = "1001";
$b = "10101";
$n = strlen($a);
$m = strlen($b);

echo BitOperations($a, $n, $b, $m);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let mod = (1e9 + 7);

    // Function to return the required result
    function BitOperations(a, n, b, m)
    {

        // Reverse the strings
        let ch1 = a.split('');
        ch1.reverse();
        a = ch1.join("");
        let ch2 = b.split('');
        ch2.reverse();
        b = ch2.join("");

        // Count the number of set bits in b
        let c = 0;
        for (let i = 0; i < m; i++)
            if (b[i] == '1')
                c++;

        // To store the powers of 2
        let power = new Array(n);
        power[0] = 1;

        // power[i] = pow(2, i) % mod
        for (let i = 1; i < n; i++)
            power[i] = (power[i - 1] * 2) % mod;

        // To store the final answer
        let ans = 0;
        for (let i = 0; i < n; i++)
        {
            if (a[i] == '1')
            {

                // Add power[i] to the ans after
                // multiplying it with the number
                // of set bits in b
                ans += c * power[i];
                if (ans >= mod)
                    ans %= mod;
            }

            // Divide by 2 means right shift b>>1
            // if b has 1 at right most side than
            // number of set bits will get decreased
            if (b[i] == '1')
                c--;

            // If no more set bits in b i.e. b = 0
            if (c == 0)
                break;
        }

        // Return the required answer
        return ans;
    }

    let a = "1001", b = "10101";
    let n = a.length, m = b.length;

    document.write(BitOperations(a, n, b, m));

</script>
```

**Output:** 

```
11
```