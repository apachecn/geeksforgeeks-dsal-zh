# 奇数和偶数的子序列数|集合 2

> 原文:[https://www . geeksforgeeks . org/带奇偶和集的子序列数-2/](https://www.geeksforgeeks.org/number-of-subsequences-with-even-and-odd-sum-set-2/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是找出和为偶数的子序列数和和为奇数的子序列数。
**例:**

> **输入:** arr[] = {1，2，2，3}
> **输出:** EvenSum = 7，OddSum = 8
> 有 2 个 <sup>N</sup> -1 个可能的子序列。
> 偶和的子序列是
> 1) {1，3} Sum = 4
> 2) {1，2，2，3} Sum = 8
> 3) {1，2，3} Sum = 6(指数 1)
> 4) {1，2，3} Sum = 6(指数 2)
> 5) {2} Sum = 2(指数 1)
> 6) {2，2} Sum = 4
> 7) {2} Sum
> **输入:** arr[] = { 2，2，2，2 }
> **输出:** EvenSum = 15，OddSum = 0

**途径:**本文已经存在[这里](https://www.geeksforgeeks.org/number-of-subsequences-with-even-and-odd-sum/)有![O(N)   ](img/23f09f991be3459af525bfd21659fc83.png "Rendered by QuickLaTeX.com")的时间复杂度 **N** 就是阵的大小。在继续前进之前，请访问这里的。

*   如果我们能找到奇数子序列的数目，那么我们就能很容易地找到偶数子序列的数目。
*   奇数子序列可以通过两种方式形成:
    1.  通过奇数次取奇数。
    2.  取偶数和奇数的奇数时间。
*   以下是一些变量及其定义:
    *   **N** =数组中元素的总数。
    *   **偶数** =数组中偶数的总数。
    *   **奇数** =数组中的奇数总数。
    *   **Tseq** =子序列总数。
    *   **Oseq** =只有奇数的子序列总数。
    *   **Eseq** =偶数子序列总数。
    *   **奇数序列** =奇数和的子序列总数。
    *   **偶数列** =偶数列的总数。

> **Tseq = 2<sup>N</sup>–1 =偶数子序列+奇数子序列**
> **Eseq = 2 <sup>偶数</sup>**
> **Oseq = <sup>奇数</sup> C <sub>1</sub> + <sup>奇数</sup> C <sub>3</sub> + <sup>奇数</sup> C <sub>5</sub>** +。。。。
> 其中 **<sup>奇数</sup>C<sub>1</sub>T30】=选择 **1** 奇数
> T34<sup>奇数</sup>C<sub>3</sub>T39】=选择 **3** 奇数以此类推
> 我们可以通过[这个](https://www.quora.com/How-do-I-prove-nC0+nC2+nC4+-nC1+nC3+nC5+)恒等式来简化上面的等式，因此
> T46】Oseq = 2<sup>奇数–1【 将以上结果
> **相乘即可计算出 OddSumSeq = 2 <sup>偶数</sup> * 2 <sup>奇数–1</sup>**
> T59】偶数 sumseq = 2<sup>N</sup>–1–Odd sumseq</sup>**T63】

以下是上述方法的实现:

## C++

```
// CPP program to find number of
// Subsequences with Even and Odd Sum
#include <bits/stdc++.h>
using namespace std;

// Function to find number of
// Subsequences with Even and Odd Sum
pair<int, int> countSum(int arr[], int n)
{
    int NumberOfOdds = 0, NumberOfEvens = 0;

    // Counting number of odds
    for (int i = 0; i < n; i++)
        if (arr[i] & 1)
            NumberOfOdds++;

    // Even count
    NumberOfEvens = n - NumberOfOdds;

    int NumberOfOddSubsequences = (1 << NumberOfEvens)
                                  * (1 << (NumberOfOdds - 1));

    // Total Subsequences is (2^n - 1)
    // For NumberOfEvenSubsequences subtract
    // NumberOfOddSubsequences from total
    int NumberOfEvenSubsequences = (1 << n) - 1
                                   - NumberOfOddSubsequences;

    return { NumberOfEvenSubsequences,
             NumberOfOddSubsequences };
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Calling the function
    pair<int, int> ans = countSum(arr, n);

    cout << "EvenSum = " << ans.first;
    cout << " OddSum = " << ans.second;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// Subsequences with Even and Odd Sum
import java.util.*;

class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find number of
// Subsequences with Even and Odd Sum
static pair countSum(int arr[], int n)
{
    int NumberOfOdds = 0, NumberOfEvens = 0;

    // Counting number of odds
    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            NumberOfOdds++;

    // Even count
    NumberOfEvens = n - NumberOfOdds;

    int NumberOfOddSubsequences = (1 << NumberOfEvens) *
                                  (1 << (NumberOfOdds - 1));

    // Total Subsequences is (2^n - 1)
    // For NumberOfEvenSubsequences subtract
    // NumberOfOddSubsequences from total
    int NumberOfEvenSubsequences = (1 << n) - 1 -
                                    NumberOfOddSubsequences;

    return new pair(NumberOfEvenSubsequences,
                    NumberOfOddSubsequences);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 3 };

    int n = arr.length;

    // Calling the function
    pair ans = countSum(arr, n);

    System.out.print("EvenSum = " + ans.first);
    System.out.print(" OddSum = " + ans.second);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find number of
# Subsequences with Even and Odd Sum

# Function to find number of
# Subsequences with Even and Odd Sum
def countSum(arr, n) :

    NumberOfOdds = 0; NumberOfEvens = 0;

    # Counting number of odds
    for i in range(n) :
        if (arr[i] & 1) :
            NumberOfOdds += 1;

    # Even count
    NumberOfEvens = n - NumberOfOdds;

    NumberOfOddSubsequences = (1 << NumberOfEvens) * \
                              (1 << (NumberOfOdds - 1));

    # Total Subsequences is (2^n - 1)
    # For NumberOfEvenSubsequences subtract
    # NumberOfOddSubsequences from total
    NumberOfEvenSubsequences = (1 << n) - 1 - \
                                NumberOfOddSubsequences;

    return (NumberOfEvenSubsequences,
            NumberOfOddSubsequences);

# Driver code
if __name__ == "__main__":

    arr = [ 1, 2, 2, 3 ];

    n = len(arr);

    # Calling the function
    ans = countSum(arr, n);

    print("EvenSum =", ans[0], end = " ");
    print("OddSum =", ans[1]);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find number of
// Subsequences with Even and Odd Sum
using System;

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find number of
// Subsequences with Even and Odd Sum
static pair countSum(int []arr, int n)
{
    int NumberOfOdds = 0, NumberOfEvens = 0;

    // Counting number of odds
    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            NumberOfOdds++;

    // Even count
    NumberOfEvens = n - NumberOfOdds;

    int NumberOfOddSubsequences = (1 << NumberOfEvens) *
                                  (1 << (NumberOfOdds - 1));

    // Total Subsequences is (2^n - 1)
    // For NumberOfEvenSubsequences subtract
    // NumberOfOddSubsequences from total
    int NumberOfEvenSubsequences = (1 << n) - 1 -
                                    NumberOfOddSubsequences;

    return new pair(NumberOfEvenSubsequences,
                    NumberOfOddSubsequences);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 2, 3 };

    int n = arr.Length;

    // Calling the function
    pair ans = countSum(arr, n);

    Console.Write("EvenSum = " + ans.first);
    Console.Write(" OddSum = " + ans.second);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find number of
// Subsequences with Even and Odd Sum

// Function to find number of
// Subsequences with Even and Odd Sum
function countSum(arr, n) {
    let NumberOfOdds = 0, NumberOfEvens = 0;

    // Counting number of odds
    for (let i = 0; i < n; i++)
        if (arr[i] & 1)
            NumberOfOdds++;

    // Even count
    NumberOfEvens = n - NumberOfOdds;

    let NumberOfOddSubsequences = (1 << NumberOfEvens)
        * (1 << (NumberOfOdds - 1));

    // Total Subsequences is (2^n - 1)
    // For NumberOfEvenSubsequences subtract
    // NumberOfOddSubsequences from total
    let NumberOfEvenSubsequences = (1 << n) - 1
        - NumberOfOddSubsequences;

    return [NumberOfEvenSubsequences,
        NumberOfOddSubsequences];
}

// Driver code
let arr = [1, 2, 2, 3];

let n = arr.length;

// Calling the function
let ans = countSum(arr, n);

document.write("EvenSum = " + ans[0]);
document.write(" OddSum = " + ans[1]);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
EvenSum = 7 OddSum = 8
```