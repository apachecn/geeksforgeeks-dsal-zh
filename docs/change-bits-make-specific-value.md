# 改变位以产生特定的或值

> 原文:[https://www . geesforgeks . org/change-bits-make-specific-value/](https://www.geeksforgeeks.org/change-bits-make-specific-value/)

给定两个正整数 A 和 B，我们最多可以改变两个数中的 K 位，使它们的 OR 等于给定的目标数 t，在多解的情况下，尽量保持 A 尽可能小。

示例:

```
Input : A = 175,
        B = 66,
        T = 100,
        K = 5
Output : A = 36
         B = 64
Initial bits of A = 1010 1111
Changed bits of A = 0010 0100
Initial bits of B = 0100 0010
Changed bits of B = 0100 0000
OR of changed Bits = 0110 0100
Which has decimal value equal to Target T.

Input : A = 175,
        B = 66,
        T = 100,
        K = 4
Output : Not Possible
It is not possible to get OR of
A and B as T, just by changing K bits.

```

我们可以通过迭代 A 和 B 的所有位并贪婪地改变它们来解决这个问题，

*   如果目标 T 的第 I 位为 0，则将 A 和 B 的第 I 位设置为 0(如果尚未设置)
*   如果目标 T 的第 I 位是 1，那么我们将尝试将其中一个位设置为 1，并且我们将只将 B 的第 I 位更改为 1(如果还没有的话)，以最小化 a

经过上述程序后，如果**改变的比特数大于 K** ，那么最多改变 K 个比特就不可能得到 A 和 B 的或作为 T。
如果**改变的比特小于 k** ，那么我们可以通过使用剩余的 K 值来进一步最小化 A 的值，为此我们将再次循环比特，并且如果在任何时候，

*   第一个 A 位是 1，第一个 B 位是 0，那么我们将进行 2 次更改，并翻转两者。
*   第一个 A 位和第二个 B 位都是 1，那么我们将再次进行 1 次更改并翻转 A 位。

上述解决方案的总时间复杂度为 0(最大位数)。

## C++

```
// C++ program to change least bits to
// get desired OR value
#include <bits/stdc++.h>
using namespace std;

// Returns max of three numbers
int max(int a, int b, int c)
{
    return max(a, max(b, c));
}

// Returns count of bits in N
int bitCount(int N)
{
    int cnt = 0;
    while (N)
    {
        cnt++;
        N >>= 1;
    }
    return cnt;
}

// Returns bit at 'pos' position
bool at_position(int num, int pos)
{
    bool bit = num & (1<<pos);
    return bit;
}

//    Utility method to toggle bit at
// 'pos' position
void toggle(int &num,int pos)
{
    num ^= (1 << pos);
}

//    method returns minimum number of bit flip
// to get T as OR value of A and B
void minChangeToReachTaregetOR(int A, int B,
                               int K, int T)
{
    int maxlen = max(bitCount(A), bitCount(B),
                                  bitCount(T));

    // Loop over maximum number of bits among
    // A, B and T
    for (int i = maxlen - 1; i >= 0; i--)
    {
        bool bitA = at_position(A, i);
        bool bitB = at_position(B, i);
        bool bitT = at_position(T, i);

        // T's bit is set, try to toggle bit
        // of B, if not already
        if (bitT)
        {
            if (!bitA && !bitB)
            {
                toggle(B, i);
                K--;
            }
        }
        else
        {
            //    if A's bit is set, flip that
            if (bitA)
            {
                toggle(A, i);
                K--;
            }

            //    if B's bit is set, flip that
            if (bitB)
            {
                toggle(B, i);
                K--;
            }
        }
    }

    //    if K is less than 0 then we can make A|B == T
    if (K < 0)
    {
        cout << "Not possible\n";
        return;
    }

    // Loop over bits one more time to minimise
    // A further
    for (int i = maxlen - 1; K > 0 && i >= 0; --i)
    {
        bool bitA = at_position(A, i);
        bool bitB = at_position(B, i);
        bool bitT = at_position(T, i);

        if (bitT)
        {
            // If both bit are set, then Unset
            // A's bit to minimise it
            if (bitA && bitB)
            {
                toggle(A, i);
                K--;
            }
        }

        // If A's bit is 1 and B's bit is 0,
        // toggle both
        if (bitA && !bitB && K >= 2)
        {
            toggle(A, i);
            toggle(B, i);
            K -= 2;
        }
    }

    //    Output changed value of A and B
    cout << A << " " << B << endl;
}

// Driver code
int main()
{
    int A = 175, B = 66, K = 5, T = 100;
    minChangeToReachTaregetOR(A, B, K, T);
    return 0;
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to change least 
// bits to get desired OR value

// Returns max of three numbers
function maxDD($a, $b, $c)
{
    return max($a, (max($b, $c)));
}

// Returns count of bits in N
function bitCount($N)
{
    $cnt = 0;
    while ($N)
    {
        $cnt++;
        $N >>= 1;
    }
    return $cnt;
}

// Returns bit at 'pos' position
function at_position($num, $pos)
{
    $bit = $num & (1 << $pos);
    return $bit;
}

// Utility method to toggle
// bit at 'pos' position
function toggle(&$num, $pos)
{
    $num ^= (1 << $pos);
}

// method returns minimum 
// number of bit flip to 
// get T as OR value of A and B
function minChangeToReachTaregetOR($A, $B,
                                   $K, $T)
{
    $maxlen = max(bitCount($A),
                  bitCount($B),
                  bitCount($T));

    // Loop over maximum number 
    // of bits among A, B and T
    for ( $i = $maxlen - 1; $i >= 0; $i--)
    {
        $bitA = at_position($A, $i);
        $bitB = at_position($B, $i);
        $bitT = at_position($T, $i);

        // T's bit is set, try to toggle
        // bit of B, if not already
        if ($bitT)
        {
            if (!$bitA && !$bitB)
            {
                toggle($B, $i);
                $K--;
            }
        }
        else
        {
            // if A's bit is set, 
            // flip that
            if ($bitA)
            {
                toggle($A, $i);
                $K--;
            }

            // if B's bit is set,
            // flip that
            if ($bitB)
            {
                toggle($B, $i);
                $K--;
            }
        }
    }

    // if K is less than 0 then
    // we can make A|B == T
    if ($K < 0)
    {
    echo "Not possible\n";
        return;
    }

    // Loop over bits one more 
    // time to minimise A further
    for ($i = $maxlen - 1; 
         $K > 0 && $i >= 0; --$i)
    {
        $bitA = at_position($A, $i);
        $bitB = at_position($B, $i);
        $bitT = at_position($T, $i);

        if ($bitT)
        {
            // If both bit are set, then 
            // Unset A's bit to minimise it
            if ($bitA && $bitB)
            {
                toggle($A, $i);
                $K--;
            }
        }

        // If A's bit is 1 and B's 
        // bit is 0, toggle both
        if ($bitA && !$bitB && $K >= 2)
        {
            toggle($A, $i);
            toggle($B, $i);
            $K -= 2;
        }
    }

    // Output changed value
    // of A and B
    echo $A , " " , $B , "\n";
}

// Driver Code
$A = 175;
$B = 66;
$K = 5;
$T = 100;
minChangeToReachTaregetOR($A, $B, $K, $T);

// This code is contributed by ajit
?>
```

**Output :**

```
36 64

```

本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。