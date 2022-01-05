# 在尼姆游戏

中找到赢家

> 原文:[https://www.geeksforgeeks.org/find-winner-nim-game/](https://www.geeksforgeeks.org/find-winner-nim-game/)

给你一个由 n 个元素组成的数组。有两个玩家爱丽丝和鲍勃。玩家可以从数组中选择任何元素并移除它。如果移除所选元素后，所有剩余元素的按位异或等于 0，则该玩家失败。这个问题是[尼姆游戏的变种。](https://www.geeksforgeeks.org/combinatorial-game-theory-set-2-game-nim/)

**注意:**每个玩家交替进行游戏。找出赢家，如果两个球员都发挥最佳。爱丽丝先开始游戏。如果数组中有一个元素，将其值视为数组的异或。

**示例:**

> 输入:A[] = {3，3，2}
> 输出:Winner = Bob
> 说明:Alice 可以选择 2 并移除它，使数组的 XOR 等于零如果 Alice 选择 3 来移除，那么 Bob 可以选择 2/3 中的任何一个，最后 Alice 必须完成他的步骤。
> 
> 输入:A[] = {3，3}
> 输出:Winner = Alice
> 说明:由于数组的 XOR 已经为零，Alice 无法选择任何要移除的元素，因此 Alice 是 Winner。

让我们一步步开始解决方案。我们总共有三个数组异或选项和这个游戏。

1.  **数组的异或已经是 0:** 在这种情况下，爱丽丝将无法移动，因此爱丽丝是赢家。
2.  **数组的 XOR 不为零:**现在，在这种情况下我们有两个选择，数组的大小要么是奇数，要么是偶数。
    *   <u>情况 A:</u> 如果阵列大小是奇数，那么鲍勃肯定会赢得比赛。
    *   <u>案例 B:</u> 如果数组大小相等，那么爱丽丝将赢得游戏。

借助数学归纳法可以证明上述结论。
<u>设 A[] = {1}即数组的大小为奇数，数组的异或为非零:</u>在这种情况下，Alice 可以选择元素 1，然后 A[]将变为空，因此数组的异或可以认为是零。结果鲍勃成了赢家。
<u>让数组的大小为偶数，数组的异或为非零。</u>现在我们可以证明 Alice 总能找到一个要移除的元素，这样数组剩余元素的 XOR 就会非零。

为了证明这一点，让我们从矛盾开始，也就是说，假设剩余数组中你应该选择异或的任何元素必须为零。
那么，让 A1 Xor A2 Xor … An = X，n 为偶数。
根据我们的矛盾假设，Ai XOR X = 0 为 1 < = i < = n.
计算所有 X Xor Ai(即 N 个方程)的 Xor，
对所有 N 个方程进行 Xor 后，我们有 X Xor X…Xor X (n 次)= 0，因为 N 是偶数。
现在，我们也有 A1 Xor A2 Xor..An = 0，但我们知道 A1 Xor A2…Xor = X。这意味着我们在偶数大小的数组中至少有一个元素，这样在它被移除后，非零数组中的剩余元素将被异或。

<u>设数组大小为偶数，数组异或为非零。</u>爱丽丝不能去掉一个元素 Ai 使得剩余数的异或为零，因为那样会让鲍勃赢。现在，举另一个例子，当剩余 N 的异或？1 个数字不为零。据我们所知，N？1 是偶数而从归纳假设来看，我们可以说当前移动后的位置对于 Bob 来说将是一个获胜的位置。因此，对于爱丽丝来说，这是一个失败的位置。

```
int res = 0;
for (int i = 1; i <= N; i++) {
    res ^= a[i];
}

if (res == 0)
    return "ALice";
if (N%2 == 0)
    return "Alice";
else
    return "Bob";
```

## C++

```
// CPP to find nim-game winner
#include <bits/stdc++.h>
using namespace std;

// function to find winner of NIM-game
string findWinner(int A[], int n)
{
    int res = 0;
    for (int i = 0; i < n; i++)
        res ^= A[i];

    // case when Alice is winner
    if (res == 0 || n % 2 == 0)
        return "Alice";

    // when Bob is winner
    else
        return "Bob";
}

// driver program
int main()
{
    int A[] = { 1, 4, 3, 5 };
    int n = sizeof(A) / sizeof(A[0]);
    cout << "Winner = " << findWinner(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to find nim-game winner
class GFG {

    // function to find winner of NIM-game
    static String findWinner(int A[], int n)
    {
        int res = 0;

        for (int i = 0; i < n; i++)
            res ^= A[i];

        // case when Alice is winner
        if (res == 0 || n % 2 == 0)
            return "Alice";

        // when Bob is winner
        else
            return "Bob";
    }

    //Driver code
    public static void main (String[] args)
    {
        int A[] = { 1, 4, 3, 5 };
        int n =A.length;

        System.out.print("Winner = "
                    + findWinner(A, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find nim-game winner

# Function to find winner of NIM-game
def findWinner(A, n):

    res = 0
    for i in range(n):
        res ^= A[i]

    # case when Alice is winner
    if (res == 0 or n % 2 == 0):
        return "Alice"

    # when Bob is winner
    else:
        return "Bob"

# Driver code
A = [ 1, 4, 3, 5 ]
n = len(A)
print("Winner = ", findWinner(A, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# to find nim-game winner
using System;

class GFG {

    // function to find winner of NIM-game
    static String findWinner(int []A, int n)
    {
        int res = 0;

        for (int i = 0; i < n; i++)
            res ^= A[i];

        // case when Alice is winner
        if (res == 0 || n % 2 == 0)
            return "Alice";

        // when Bob is winner
        else
            return "Bob";
    }

    //Driver code
    public static void Main ()
    {
        int []A = { 1, 4, 3, 5 };
        int n =A.Length;

        Console.WriteLine("Winner = "
                    + findWinner(A, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to find nim-game winner

// function to find
// winner of NIM-game
function findWinner($A, $n)
{
    $res = 0;
    for ($i = 0; $i < $n; $i++)
        $res ^= $A[$i];

    // case when Alice is winner
    if ($res == 0 or $n % 2 == 0)
        return "Alice";

    // when Bob is winner
    else
        return "Bob";
}

// Driver Code
$A = array(1, 4, 3, 5 );
$n = count($A);
echo "Winner = " , findWinner($A, $n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find nim-game winner

    // function to find winner of NIM-game
    function findWinner(A, n)
    {
        let res = 0;

        for (let i = 0; i < n; i++)
            res ^= A[i];

        // case when Alice is winner
        if (res == 0 || n % 2 == 0)
            return "Alice";

        // when Bob is winner
        else
            return "Bob";
    }

// Driver Code

        let A = [ 1, 4, 3, 5 ];
        let n = A.length;

        document.write("Winner = "
                    + findWinner(A, n));

</script>
```

**输出:**

```
Winner = Alice
```