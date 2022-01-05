# 最小的 N 位数，其位数的平方和为完美平方

> 原文:[https://www . geesforgeks . org/最小 n 位数，其位数平方和为完美平方/](https://www.geeksforgeeks.org/smallest-n-digit-number-whose-sum-of-square-of-digits-is-a-perfect-square/)

给定一个整数 N，求最小的 N 位数，使得该数的位数的平方和(以十进制表示)也是一个完美的平方。如果没有这样的号码，打印-1。
**例:**

> **输入:** N = 2
> **输出:** 34
> **解释:**
> 最小可能的 2 位数，其位数的平方和是一个完美的平方是 34，因为 3<sup>2</sup>+4<sup>2</sup>= 5<sup>2</sup>。
> **输入:** N = 1
> **输出:** 1
> **解释:**
> 最小可能的 1 位数就是 1 本身。

**方法 1:**
要解决上面提到的问题，我们可以使用**回溯**。因为我们想找到满足给定条件的最小 N 位数，所以答案会有非递减顺序的数字。因此，我们递归地生成可能的数字，并在每个递归步骤中跟踪以下内容:

*   位置:递归步骤的当前位置，即放置哪个位置数字。
*   prev:因为当前数字必须大于等于 prev，所以放置的前一个数字。
*   sum:到目前为止放置的数字的平方和。当放置数字时，这将用于检查放置的所有数字的平方和是否是完美的正方形。
*   一种向量，它存储所有数字在此位置之前的位置。

如果将一个数字放在一个位置并移动到下一个递归步骤得到一个可能的解，那么返回 1，否则回溯。
下面是上述方法的实现:

## C++

```
// C++ implementation to find Smallest N
// digit number whose sum of square
// of digits is a Perfect Square

#include <bits/stdc++.h>
using namespace std;

// function to check if
// number is a perfect square
int isSquare(int n)
{
    int k = sqrt(n);
    return (k * k == n);
}

// function to calculate the
// smallest N digit number
int calculate(int pos, int prev,
              int sum, vector<int>& v)
{

    if (pos == v.size())
        return isSquare(sum);

    // place digits greater than equal to prev
    for (int i = prev; i <= 9; i++) {
        v[pos] = i;
        sum += i * i;

        // check if placing this digit leads
        // to a solution then return it
        if (calculate(pos + 1, i, sum, v))
            return 1;

        // else backtrack
        sum -= i * i;
    }
    return 0;
}

string minValue(int n)
{

    vector<int> v(n);
    if (calculate(0, 1, 0, v)) {

        // create a string representing
        // the N digit number
        string answer = "";
        for (int i = 0; i < v.size(); i++)

            answer += char(v[i] + '0');

        return answer;
    }

    else
        return "-1";
}

// driver code
int main()
{

    // initialise N
    int N = 2;

    cout << minValue(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find Smallest N
// digit number whose sum of square
// of digits is a Perfect Square
class GFG{

// function to check if
// number is a perfect square
static int isSquare(int n)
{
    int k = (int)Math.sqrt(n);
    return k * k == n ? 1 : 0;
}

// Function to calculate the
// smallest N digit number
static int calculate(int pos, int prev,
                     int sum, int[] v)
{
    if (pos == v.length)
        return isSquare(sum);

    // Place digits greater than equal to prev
    for(int i = prev; i <= 9; i++)
    {
        v[pos] = i;
        sum += i * i;

        // Check if placing this digit leads
        // to a solution then return it
        if (calculate(pos + 1, i, sum, v) != 0)
            return 1;

        // Else backtrack
        sum -= i * i;
    }
    return 0;
}

static String minValue(int n)
{
    int[] v = new int[n];
    if (calculate(0, 1, 0, v) != 0)
    {

        // Create a string representing
        // the N digit number
        String answer = "";

        for(int i = 0; i < v.length; i++)
            answer += (char)(v[i] + '0');

        return answer;
    }
    else
        return "-1";
}

// Driver code
public static void main(String[] args)
{

    // Initialise N
    int N = 2;

    System.out.println(minValue(N));
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 implementation to find Smallest N
# digit number whose sum of square
# of digits is a Perfect Square
from math import sqrt

# function to check if
# number is a perfect square
def isSquare(n):
    k = int(sqrt(n))
    return (k * k == n)

# function to calculate the
# smallest N digit number
def calculate(pos, prev, sum, v):

    if (pos == len(v)):
        return isSquare(sum)

    # place digits greater than equal to prev
    for i in range(prev, 9 + 1):
        v[pos] = i
        sum += i * i

        # check if placing this digit leads
        # to a solution then return it
        if (calculate(pos + 1, i, sum, v)):
            return 1

        # else backtrack
        sum -= i * i

    return 0

def minValue(n):
    v = [0]*(n)
    if (calculate(0, 1, 0, v)):

        # create a representing
        # the N digit number
        answer = ""
        for i in range(len(v)):

            answer += chr(v[i] + ord('0'))

        return answer

    else:
        return "-1"

# Driver code
if __name__ == '__main__':

    # initialise N
    N = 2

    print(minValue(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find Smallest N
// digit number whose sum of square
// of digits is a Perfect Square
using System;
class GFG{

// function to check if
// number is a perfect square
static int isSquare(int n)
{
    int k = (int)Math.Sqrt(n);
    return k * k == n ? 1 : 0;
}

// Function to calculate the
// smallest N digit number
static int calculate(int pos, int prev,
                     int sum, int[] v)
{
    if (pos == v.Length)
        return isSquare(sum);

    // Place digits greater than equal to prev
    for(int i = prev; i <= 9; i++)
    {
        v[pos] = i;
        sum += i * i;

        // Check if placing this digit leads
        // to a solution then return it
        if (calculate(pos + 1, i, sum, v) != 0)
            return 1;

        // Else backtrack
        sum -= i * i;
    }
    return 0;
}

static string minValue(int n)
{
    int[] v = new int[n];
    if (calculate(0, 1, 0, v) != 0)
    {

        // Create a string representing
        // the N digit number
        string answer = "";

        for(int i = 0; i < v.Length; i++)
            answer += (char)(v[i] + '0');

        return answer;
    }
    else
        return "-1";
}

// Driver code
public static void Main()
{

    // Initialise N
    int N = 2;

    Console.Write(minValue(N));
}
}
```

## java 描述语言

```
<script>

// Javascript implementation to find Smallest N
// digit number whose sum of square
// of digits is a Perfect Square

// function to check if
// number is a perfect square
function isSquare(n)
{
    let k = Math.floor(Math.sqrt(n));
    return k * k == n ? 1 : 0;
}

// Function to calculate the
// smallest N digit number
function calculate(pos, prev, sum, v)
{
    if (pos == v.length)
        return isSquare(sum);

    // Place digits greater than equal to prev
    for(let i = prev; i <= 9; i++)
    {
        v[pos] = i;
        sum += i * i;

        // Check if placing this digit leads
        // to a solution then return it
        if (calculate(pos + 1, i, sum, v) != 0)
            return 1;

        // Else backtrack
        sum -= (i * i);
    }
    return 0;
}

function minValue(n)
{
    let v = Array.from({length: n}, (_, i) => 0);
    if (calculate(0, 1, 0, v) != 0)
    {

        // Create a string representing
        // the N digit number
        let answer = "";

        for(let i = 0; i < v.length; i++)
            answer += (v[i]  + 0);

        return answer;
    }
    else
        return "-1";
}

// Driver Code

    // Initialise N
    let N = 2;
    document.write(minValue(N));

 // This code is contributed by sanjoy_62.
</script>
```

**Output**

```
34
```

时间复杂度:O(sqrt(n))

辅助空间:O(n)

**方法二:**
上述问题也可以使用**动态规划**解决。如果我们仔细观察这个问题，我们会发现它可以转换成标准的[硬币兑换问题](https://www.geeksforgeeks.org/coin-change-dp-7/)。给定 N 为位数，基本答案将是 N 1，其位数的平方和将是 N

*   **如果 N 本身是一个完美的正方形**那么 N 乘以 1 就是最终的答案。
*   否则，我们将不得不用 2-9 中的其他数字替换答案中的一些 1。数字的每一次替换都将使平方和增加一定的量，并且由于 1 只能改变为 8 个其他可能的数字，因此只有 8 个这样的可能增量。例如，如果将 1 更改为 2，则增量将为 2<sup>2</sup>–1<sup>2</sup>= 3。同样，所有可能的更改为:{3，8，15，24，35，48，63，80}。

因此，现在的问题可以解释为有 8 种具有上述值的硬币，我们可以使用任何硬币任意次数来创建所需的总和。平方和将在 N(所有数字都是 1)到 81 * N(所有数字都是 9)的范围内。我们只需要考虑该范围内的完美平方和，并使用硬币兑换的思想来找到答案中的 N 位数字。我们需要考虑的一个要点是，我们必须找到最小的 N 位数，而不是位数平方和最小的数。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the Smallest
// N digit number whose sum of square
// of digits is a Perfect Square
#include <bits/stdc++.h>
using namespace std;
long long value[8100006];
int first[8100006];
// array for all possible changes
int coins[8] = { 3, 8, 15, 24, 35, 48, 63, 80 };

void coinChange()
{
    const long long inf = INT_MAX;

    // iterating till 81 * N
    // since N is at max 10^5
    for (int x = 1; x <= 8100005; x++) {

        value[x] = inf;

        for (auto c : coins) {
            if (x - c >= 0 && value[x - c] + 1 < value[x]) {
                value[x] = min(value[x], value[x - c] + 1);

                // least value of coin
                first[x] = c;
            }
        }
    }
}

// function to find the
// minimum possible value
string minValue(int n)
{

    // applying coin change for all the numbers
    coinChange();

    string answer = "";

    // check if number is
    // perfect square or not
    if ((sqrt(n) * sqrt(n)) == n) {
        for (int i = 0; i < n; i++)

            answer += "1";

        return answer;
    }

    long long hi = 81 * n;
    long long lo = sqrt(n);

    // keeps a check whether
    // number is found or not
    bool found = false;

    long long upper = 81 * n;
    long long lower = n;

    // sorting suffix strings
    string suffix;
    bool suf_init = false;

    while ((lo * lo) <= hi) {
        lo++;

        long long curr = lo * lo;

        long long change = curr - n;

        if (value[change] <= lower) {

            // build a suffix string
            found = true;

            if (lower > value[change]) {
                // number to be used for updation of lower,
                // first values that will be used
                // to construct the final number later
                lower = value[change];
                upper = change;
                suffix = "";
                suf_init = true;
                int len = change;

                while (len > 0) {
                    int k = sqrt(first[len] + 1);
                    suffix = suffix + char(k + 48);
                    len = len - first[len];
                }
            }

            else if (lower == value[change]) {
                string tempsuf = "";
                int len = change;
                while (len > 0) {
                    int k = sqrt(first[len] + 1);
                    tempsuf = tempsuf + char(k + 48);
                    len = len - first[len];
                }

                if (tempsuf < suffix or suf_init == false) {
                    lower = value[change];
                    upper = change;
                    suffix = tempsuf;
                    suf_init = true;
                }
            }
        }
    }
    // check if number is found
    if (found) {
        // construct the number from first values
        long long x = lower;
        for (int i = 0; i < (n - x); i++)
            answer += "1";

        long long temp = upper;

        // fill in rest of the digits
        while (temp > 0) {
            int dig = sqrt(first[temp] + 1);
            temp = temp - first[temp];
            answer += char(dig + '0');
        }
        return answer;
    }
    else
        return "-1";
}

// driver code
int main()
{

    // initialise N
    int N = 2;

    cout << minValue(N);

    return 0;
}
```

**Output:** 

```
34
```

**时间复杂度:** O(81 * N)

**辅助空间:** O(81 * 10 <sup>5</sup> )