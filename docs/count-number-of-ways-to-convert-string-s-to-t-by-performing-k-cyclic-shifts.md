# 计算通过执行 K 次循环移位将字符串 S 转换为 T 的方式数

> 原文:[https://www . geeksforgeeks . org/count-通过执行 k 循环移位将字符串转换为 t 的方式数/](https://www.geeksforgeeks.org/count-number-of-ways-to-convert-string-s-to-t-by-performing-k-cyclic-shifts/)

给定两个字符串 **S 和 T** 以及一个数字 **K** ，任务是通过执行 **K 循环移位**来计算将字符串 **S** 转换为字符串 **T** 的方法数量。

> 循环移位被定义为字符串 **S** 可以被分成两个非空部分 **X + Y** ，并且在一次操作中我们可以将 **S** 从 **X + Y** 转换为 **Y + X** 。

**注意:**既然计数可以很大打印答案以 **10 <sup>9</sup> + 7** 为模。
**举例:**

> **输入:**S =“ab”，T =“ab”，K = 2
> **输出:** 1
> **说明:**
> 唯一的办法就是第一招转换**【ab 到 ba】**，第二招再转换【ba 到 ab】。
> **输入:**S =“ababab”，T =“ababab”，K = 1
> **输出:** 2
> **解释:**
> 一步将 S 转换为 T 的一种可能方式是**【ab | abab】**->**【ababab】**，第二种方式是**【abab | ab】**->总共有两种方法。

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。如果最后我们在弦 **T** 处，我们称循环移位**为“好”**，反之亦然**。以下是步骤:** 

1.  **预计算好的(用 a 表示)和坏的(用 b 表示)循环移位的数量。**
2.  **初始化两个 dp [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，使得**dp1【I】**表示在 **i 移动**时到达好的档位的方法数量，而**dp2【I】**表示在 **i 移动**时到达坏的档位的方法数量。**
3.  **对于过渡，我们只关心前一个状态，即**(I–1)第一个状态**，这个问题的答案是**dp1【K】**。**
4.  **所以 **i 招式**达到好状态的方式数等于 **i-1** 招式达到好档位的方式数乘以 **(a-1)** (因为最后一个档位也不错)**
5.  **所以在 **i-1 移动**中到达一个坏的移动的方式的数量乘以 **(a)** (因为下一个移动可以是任何一个好的移动)。**

**下面是好和坏班次的循环关系:** 

> **所以对于好的班次我们有:
> ![dp1[i]= dp1[i-1]*(a-1) + dp2[i-1]*a ](img/b9e5f7c7253d5191475019201d618dcb.png "Rendered by QuickLaTeX.com")
> 同样，对于不好的班次我们有:
> ![dp2[i]=dp1[i-1]*b + dp2[i-1]*(b-1) ](img/4879fa9532417d978630212b7100e281.png "Rendered by QuickLaTeX.com")**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define mod 10000000007

// Function to count number of ways to
// convert string S to string T by
// performing K cyclic shifts
long long countWays(string s, string t,
                    int k)
{
    // Calculate length of string
    int n = s.size();

    // 'a' is no of good cyclic shifts
    // 'b' is no of bad cyclic shifts
    int a = 0, b = 0;

    // Iterate in the string
    for (int i = 0; i < n; i++) {

        string p = s.substr(i, n - i)
                + s.substr(0, i);

        // Precompute the number of good
        // and bad cyclic shifts
        if (p == t)
            a++;
        else
            b++;
    }

    // Initialize two dp arrays
    // dp1[i] to store the no of ways to
    // get to a good shift in i moves

    // dp2[i] to store the no of ways to
    // get to a bad shift in i moves
    vector<long long> dp1(k + 1), dp2(k + 1);

    if (s == t) {
        dp1[0] = 1;
        dp2[0] = 0;
    }
    else {
        dp1[0] = 0;
        dp2[0] = 1;
    }

    // Calculate good and bad shifts
    for (int i = 1; i <= k; i++) {

        dp1[i]
            = ((dp1[i - 1] * (a - 1)) % mod
            + (dp2[i - 1] * a) % mod)
            % mod;

        dp2[i]
            = ((dp1[i - 1] * (b)) % mod
            + (dp2[i - 1] * (b - 1)) % mod)
            % mod;
    }

    // Return the required number of ways
    return dp1[k];
}

// Driver Code
int main()
{
    // Given Strings
    string S = "ab", T = "ab";

    // Given K shifts required
    int K = 2;

    // Function Call
    cout << countWays(S, T, K);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
class GFG{

static long mod = 10000000007L;

// Function to count number of ways to
// convert string S to string T by
// performing K cyclic shifts
static long countWays(String s, String t,
                    int k)
{

    // Calculate length of string
    int n = s.length();

    // 'a' is no of good cyclic shifts
    // 'b' is no of bad cyclic shifts
    int a = 0, b = 0;

    // Iterate in the string
    for(int i = 0; i < n; i++)
    {
    String p = s.substring(i, n - i) +
                s.substring(0, i);

    // Precompute the number of good
    // and bad cyclic shifts
    if (p == t)
        a++;
    else
        b++;
    }

    // Initialize two dp arrays
    // dp1[i] to store the no of ways to
    // get to a good shift in i moves

    // dp2[i] to store the no of ways to
    // get to a bad shift in i moves
    long dp1[] = new long[k + 1];
    long dp2[] = new long[k + 1];

    if (s == t)
    {
        dp1[0] = 1;
        dp2[0] = 0;
    }
    else
    {
        dp1[0] = 0;
        dp2[0] = 1;
    }

    // Calculate good and bad shifts
    for(int i = 1; i <= k; i++)
    {
    dp1[i] = ((dp1[i - 1] * (a - 1)) % mod +
                (dp2[i - 1] * a) % mod) % mod;
    dp2[i] = ((dp1[i - 1] * (b)) % mod +
                (dp2[i - 1] * (b - 1)) % mod) % mod;
    }

    // Return the required number of ways
    return dp1[k];
}

// Driver code
public static void main(String[] args)
{

    // Given Strings
    String S = "ab", T = "ab";

    // Given K shifts required
    int K = 2;

    // Function Call
    System.out.print(countWays(S, T, K));
}
}

// This code is contributed by Pratima Pandey
```

## **蟒蛇 3**

```
# Python3 program for the above approach
mod = 1000000007

# Function to count number of ways
# to convert string S to string T by
# performing K cyclic shifts
def countWays(s, t, k):

    # Calculate length of string
    n = len(s)

    # a is no. of good cyclic shifts
    # b is no. of bad cyclic shifts
    a = 0
    b = 0

    # Iterate in string
    for i in range(n):
        p = s[i : n - i + 1] + s[: i + 1]

        # Precompute the number of good
        # and bad cyclic shifts
        if(p == t):
            a += 1
        else:
            b += 1

    # Initialize two dp arrays
    # dp1[i] to store the no of ways to
    # get to a goof shift in i moves

    # dp2[i] to store the no of ways to
    # get to a bad shift in i moves
    dp1 = [0] * (k + 1)
    dp2 = [0] * (k + 1)

    if(s == t):
        dp1[0] = 1
        dp2[0] = 0
    else:
        dp1[0] = 0
        dp2[0] = 1

    # Calculate good and bad shifts    
    for i in range(1, k + 1):
        dp1[i] = ((dp1[i - 1] * (a - 1)) % mod +
                (dp2[i - 1] * a) % mod) % mod

        dp2[i] = ((dp1[i - 1] * (b)) % mod +
                (dp2[i - 1] * (b - 1)) % mod) % mod

    # Return the required number of ways
    return(dp1[k])

# Driver Code

# Given Strings
S = 'ab'
T = 'ab'

# Given K shifts required
K = 2

# Function call
print(countWays(S, T, K))

# This code is contributed by Arjun Saini
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

static long mod = 10000000007L;

// Function to count number of ways to
// convert string S to string T by
// performing K cyclic shifts
static long countWays(string s, string t,
                      int k)
{

    // Calculate length of string
    int n = s.Length;

    // 'a' is no of good cyclic shifts
    // 'b' is no of bad cyclic shifts
    int a = 0, b = 0;

    // Iterate in the string
    for(int i = 0; i < n; i++)
    {
        string p = s.Substring(i, n - i) +
                   s.Substring(0, i);

        // Precompute the number of good
        // and bad cyclic shifts
        if (p == t)
            a++;
        else
            b++;
    }

    // Initialize two dp arrays
    // dp1[i] to store the no of ways to
    // get to a good shift in i moves

    // dp2[i] to store the no of ways to
    // get to a bad shift in i moves
    long []dp1 = new long[k + 1];
    long []dp2 = new long[k + 1];

    if (s == t)
    {
        dp1[0] = 1;
        dp2[0] = 0;
    }
    else
    {
        dp1[0] = 0;
        dp2[0] = 1;
    }

    // Calculate good and bad shifts
    for(int i = 1; i <= k; i++)
    {
        dp1[i] = ((dp1[i - 1] * (a - 1)) % mod +
                  (dp2[i - 1] * a) % mod) % mod;
        dp2[i] = ((dp1[i - 1] * (b)) % mod +
                  (dp2[i - 1] * (b - 1)) % mod) % mod;
    }

    // Return the required number of ways
    return dp1[k];
}

// Driver code
public static void Main(string[] args)
{

    // Given Strings
    string S = "ab", T = "ab";

    // Given K shifts required
    int K = 2;

    // Function call
    Console.Write(countWays(S, T, K));
}
}

// This code is contributed by rutvik_56
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

let mod = 10000000007;

// Function to count number of ways to
// convert string S to string T by
// performing K cyclic shifts
function countWays(s, t, k)
{

    // Calculate length of string
    let n = s.length;

    // 'a' is no of good cyclic shifts
    // 'b' is no of bad cyclic shifts
    let a = 0, b = 0;

    // Iterate in the string
    for(let i = 0; i < n; i++)
    {
    let p = s.substr(i, n - i) +
                s.substr(0, i);

    // Precompute the number of good
    // and bad cyclic shifts
    if (p == t)
        a++;
    else
        b++;
    }

    // Initialize two dp arrays
    // dp1[i] to store the no of ways to
    // get to a good shift in i moves

    // dp2[i] to store the no of ways to
    // get to a bad shift in i moves
    let dp1 = Array.from({length: k+1}, (_, i) => 0);
    let dp2 = Array.from({length: k+1}, (_, i) => 0);

    if (s == t)
    {
        dp1[0] = 1;
        dp2[0] = 0;
    }
    else
    {
        dp1[0] = 0;
        dp2[0] = 1;
    }

    // Calculate good and bad shifts
    for(let i = 1; i <= k; i++)
    {
    dp1[i] = ((dp1[i - 1] * (a - 1)) % mod +
                (dp2[i - 1] * a) % mod) % mod;
    dp2[i] = ((dp1[i - 1] * (b)) % mod +
                (dp2[i - 1] * (b - 1)) % mod) % mod;
    }

    // Return the required number of ways
    return dp1[k];
}

// Driver Code

    // Given Strings
    let S = "ab", T = "ab";

    // Given K shifts required
    let K = 2;

    // Function Call
    document.write(countWays(S, T, K));

</script>
```

****Output:** 

```
1
```** 

****时间复杂度:***O(N)*
T5】辅助空间: *O(K)***