# 长度可被 1 整除的子串数量

> 原文:[https://www . geesforgeks . org/长度可被 1 整除的子字符串数/](https://www.geeksforgeeks.org/number-of-substrings-with-length-divisible-by-the-number-of-1s-in-it/)

给定一个仅由 0 和 1 组成的二进制字符串。计算该字符串的子字符串数，使子字符串的长度可被子字符串中的 1 整除。

**示例:**

> **输入:**S = " 01010 "
> T3】输出: 10
> 
> **输入:**S = " 1111100000 "
> T3】输出: 25

**天真方法:**

*   遍历所有子字符串，并对每个子字符串计算 1 的个数。如果子字符串的长度可被 1 的个数整除，则增加个数。这种方法需要 O(N <sup>3</sup> )时间。
*   为了使解决方案更有效，我们可以使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，而不是遍历整个子串来计算其中的 1 的数量。

> 子串[l:r]= prefix _ sum[r]–prefix _ sum[l–1]中的 1 个数

下面是上述方法的实现。

## C++

```
// C++ program to count number of
// substring under given condition
#include <bits/stdc++.h>
using namespace std;

// Function return count of
// such substring
int countOfSubstrings(string s)
{
    int n = s.length();

    int prefix_sum[n] = { 0 };

    // Mark 1 at those indices
    // where '1' appears
    for (int i = 0; i < n; i++) {
        if (s[i] == '1')
            prefix_sum[i] = 1;
    }

    // Take prefix sum
    for (int i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1];

    int answer = 0;

    // Iterate through all the
    // substrings
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int countOfOnes = prefix_sum[j]
                - (i - 1 >= 0 ?
                   prefix_sum[i - 1] : 0);
            int length = j - i + 1;

            if (countOfOnes > 0 &&
                length % countOfOnes == 0)
                answer++;
        }
    }
    return answer;
}

// Driver Code
int main()
{
    string S = "1111100000";

    cout << countOfSubstrings(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// subString under given condition

import java.util.*;

class GFG{

// Function return count of
// such substring
static int countOfSubStrings(String s)
{
    int n = s.length();

    int []prefix_sum = new int[n];

    // Mark 1 at those indices
    // where '1' appears
    for (int i = 0; i < n; i++) {
        if (s.charAt(i) == '1')
            prefix_sum[i] = 1;
    }

    // Take prefix sum
    for (int i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1];

    int answer = 0;

    // Iterate through all the
    // subStrings
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int countOfOnes = prefix_sum[j]
                - (i - 1 >= 0 ?
                prefix_sum[i - 1] : 0);
            int length = j - i + 1;

            if (countOfOnes > 0 &&
                length % countOfOnes == 0)
                answer++;
        }
    }
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    String S = "1111100000";

    System.out.print(countOfSubStrings(S));

}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to count number of
# substring under given condition

# Function return count of
# such substring
def countOfSubstrings(s):
    n = len(s)
    prefix_sum = [0 for i in range(n)]

    # Mark 1 at those indices
    # where '1' appears
    for i in range(n):
        if (s[i] == '1'):
            prefix_sum[i] = 1

    # Take prefix sum
    for i in range(1, n, 1):
        prefix_sum[i] += prefix_sum[i - 1]

    answer = 0

    # Iterate through all the
    # substrings
    for i in range(n):
        for j in range(i, n, 1):
            if (i - 1 >= 0):
                countOfOnes = prefix_sum[j]- prefix_sum[i - 1]
            else:
                countOfOnes = prefix_sum[j]
            length = j - i + 1

            if (countOfOnes > 0 and length % countOfOnes == 0):
                answer += 1

    return answer

# Driver Code
if __name__ == '__main__':
    S = "1111100000"

    print(countOfSubstrings(S))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to count number of
// subString under given condition
using System;

class GFG{

// Function return count of
// such substring
static int countOfSubStrings(String s)
{
    int n = s.Length;
    int []prefix_sum = new int[n];

    // Mark 1 at those indices
    // where '1' appears
    for(int i = 0; i < n; i++)
    {
        if (s[i] == '1')
            prefix_sum[i] = 1;
    }

    // Take prefix sum
    for(int i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1];

    int answer = 0;

    // Iterate through all the
    // subStrings
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {
            int countOfOnes = prefix_sum[j] -
                                  (i - 1 >= 0 ?
                              prefix_sum[i - 1] : 0);
            int length = j - i + 1;

            if (countOfOnes > 0 &&
                length % countOfOnes == 0)
            answer++;
        }
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "1111100000";
    Console.Write(countOfSubStrings(S));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program to count number of
// subString under given condition

// Function return count of
// such substring
function countOfSubStrings(s)
{
    let n = s.length;

    let prefix_sum = Array.from({length: n}, (_, i) => 0);

    // Mark 1 at those indices
    // where '1' appears
    for (let i = 0; i < n; i++) {
        if (s[i] == '1')
            prefix_sum[i] = 1;
    }

    // Take prefix sum
    for (let i = 1; i < n; i++)
        prefix_sum[i] += prefix_sum[i - 1];

    let answer = 0;

    // Iterate through all the
    // subStrings
    for (let i = 0; i < n; i++) {
        for (let j = i; j < n; j++) {
            let countOfOnes = prefix_sum[j]
                - (i - 1 >= 0 ?
                prefix_sum[i - 1] : 0);
            let length = j - i + 1;

            if (countOfOnes > 0 &&
                length % countOfOnes == 0)
                answer++;
        }
    }
    return answer;
}

// Driver Code

    let S = "1111100000";

    document.write(countOfSubStrings(S));

</script>
```

**Output:** 

```
25
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(N)

**有效方法:**

*   让我们使用前面讨论过的前缀和数组。让我们取一个符合给定条件的子串[l: r]，我们可以说:

> r–l+1 = k *(prefix _ sum[r]–prefix _ sum[l-1])，其中 k 是某个整数

*   这也可以写成:

> r–k * prefix _ sum[r]= l–1–k * prefix _ sum[l-1]

观察这个等式，我们可以为 0 <= k < n 创建另一个 B[I]= I–k * prefix _ sum[I]的数组。所以，现在的问题是计算 B 中每 k 个相等整数对的数量。

*   让我们取一个固定的数 x，如果 k > x，那么作为 r–l+1 < = n(对于任何一对 l，r)，我们得到如下不等式:

> prefix _ sum[r]–prefix _ sum[l-1]=(r–l+1)/k < = n/x

*   这进一步表明，在满足给定条件的子串中，1 和 k 的数量并不大。(这只是对效率的估计)。现在对于 k <= x，我们需要计算相等整数对的个数。这里满足以下不等式:

> (-1)* n * x < = I–k–prefix _ sum[I]< = n

*   所以，我们可以把所有的数字独立地放入一个数组中，找到相等整数的个数。
*   下一步是固定 l 的值，并迭代字符串中的 1 的数量，对于每个值，得到 r 的界限。对于给定的 1 的数量计数，我们可以计算哪个余数将给出 r。现在的问题是计算一些段上的整数的数量，当除以某个固定整数时，给出某个固定余数(rem)。这个计算可以在 O(1)中完成。此外，请注意，重要的是只计算 k > x.
    的 r 值

下面是上述方法的实现。

## C++

```
// C++ program to count number of
// substring under given condition
#include <bits/stdc++.h>
using namespace std;

// Function return count of such
// substring
int countOfSubstrings(string s)
{

    int n = s.length();

    // Selection of adequate x value
    int x = sqrt(n);

    // Store where 1's are located
    vector<int> ones;

    for (int i = 0; i < n; i++) {
        if (s[i] == '1')
            ones.push_back(i);
    }

    // If there are no ones,
    // then answer is 0
    if (ones.size() == 0)
        return 0;

    // For ease of implementation
    ones.push_back(n);

    // Count storage
    vector<int> totCount(n * x + n);

    int sum = 0;

    // Iterate on all k values less
    // than fixed x
    for (int k = 0; k <= x; k++) {
        // Keeps a count of 1's occured
        // during string traversal
        int now = 0;
        totCount[k * n]++;

        // Iterate on string and modify
        // the totCount
        for (int j = 1; j <= n; j++) {
            // If this character is 1
            if (s[j - 1] == '1')
                now++;
            int index = j - k * now;

            // Add to the final sum/count
            sum += totCount[index + k * n];

            // Increase totCount at exterior
            // position
            totCount[index + k * n]++;
        }
        now = 0;
        totCount[k * n]--;

        for (int j = 1; j <= n; j++) {
            if (s[j - 1] == '1')
                now++;
            int index = j - k * now;

            // Reduce totCount at index + k*n
            totCount[index + k * n]--;
        }
    }

    // Slightly modified prefix sum storage
    int prefix_sum[n];
    memset(prefix_sum, -1, sizeof(prefix_sum));

    // Number of 1's till i-1
    int cnt = 0;

    for (int i = 0; i < n; i++) {
        prefix_sum[i] = cnt;
        if (s[i] == '1')
            cnt++;
    }

    // Traversing over string considering
    // each position and finding bounds
    // and count using the inequalities
    for (int k = 0; k < n; k++)
    {
        for (int j = 1; j <= (n / x)
             && prefix_sum[k] + j <= cnt; j++)
        {
            // Calculating bounds for l and r
            int l = ones[prefix_sum[k] + j - 1]
                    - k + 1;

            int r = ones[prefix_sum[k] + j] - k;

            l = max(l, j * (x + 1));

            // If valid then add to answer
            if (l <= r) {
                sum += r / j - (l - 1) / j;
            }
        }
    }

    return sum;
}
int main()
{
    string S = "1111100000";

    cout << countOfSubstrings(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// subString under given condition
import java.util.*;

class GFG{

// Function return count of such
// substring
static int countOfSubStrings(String s)
{
    int n = s.length();

    // Selection of adequate x value
    int x = (int)Math.sqrt(n);

    // Store where 1's are located
    Vector<Integer> ones = new Vector<Integer>();

    for(int i = 0; i < n; i++)
    {
        if (s.charAt(i) == '1')
            ones.add(i);
    }

    // If there are no ones,
    // then answer is 0
    if (ones.size() == 0)
        return 0;

    // For ease of implementation
    ones.add(n);

    // Count storage
    int []totCount = new int[n * x + n];

    int sum = 0;

    // Iterate on all k values less
    // than fixed x
    for(int k = 0; k <= x; k++)
    {

        // Keeps a count of 1's occured
        // during String traversal
        int now = 0;
        totCount[k * n]++;

        // Iterate on String and modify
        // the totCount
        for(int j = 1; j <= n; j++)
        {

            // If this character is 1
            if (s.charAt(j - 1) == '1')
                now++;

            int index = j - k * now;

            // Add to the final sum/count
            sum += totCount[index + k * n];

            // Increase totCount at exterior
            // position
            totCount[index + k * n]++;
        }
        now = 0;
        totCount[k * n]--;

        for(int j = 1; j <= n; j++)
        {
            if (s.charAt(j - 1) == '1')
                now++;

            int index = j - k * now;

            // Reduce totCount at index + k*n
            totCount[index + k * n]--;
        }
    }

    // Slightly modified prefix sum storage
    int []prefix_sum = new int[n];
    Arrays.fill(prefix_sum, -1);

    // Number of 1's till i-1
    int cnt = 0;

    for(int i = 0; i < n; i++)
    {
        prefix_sum[i] = cnt;
        if (s.charAt(i) == '1')
            cnt++;
    }

    // Traversing over String considering
    // each position and finding bounds
    // and count using the inequalities
    for(int k = 0; k < n; k++)
    {
        for(int j = 1; j <= (n / x) &&
            prefix_sum[k] + j <= cnt; j++)
        {

            // Calculating bounds for l and r
            int l = ones.get(prefix_sum[k] + j - 1)-
                                             k + 1;

            int r = ones.get(prefix_sum[k] + j) - k;
            l = Math.max(l, j * (x + 1));

            // If valid then add to answer
            if (l <= r)
            {
                sum += r / j - (l - 1) / j;
            }
        }
    }
    return sum;
}

// Driver code
public static void main(String[] args)
{
    String S = "1111100000";

    System.out.print(countOfSubStrings(S));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to count number of
# substring under given condition
import math

# Function return count of such
# substring
def countOfSubstrings(s):

    n = len(s)

    # Selection of adequate x value
    x = int(math.sqrt(n))

    # Store where 1's are located
    ones = []

    for i in range (n):
        if (s[i] == '1'):
            ones.append(i)

    # If there are no ones,
    # then answer is 0
    if (len(ones) == 0):
        return 0

    # For ease of implementation
    ones.append(n)

    # Count storage
    totCount = [0] * (n * x + n)

    sum = 0

    # Iterate on all k values less
    # than fixed x
    for k in range(x + 1):

        # Keeps a count of 1's occured
        # during string traversal
        now = 0
        totCount[k * n] += 1

        # Iterate on string and modify
        # the totCount
        for j in range(1, n + 1):

            # If this character is 1
            if (s[j - 1] == '1'):
                now += 1
            index = j - k * now

            # Add to the final sum/count
            sum += totCount[index + k * n]

            # Increase totCount at exterior
            # position
            totCount[index + k * n] += 1

        now = 0
        totCount[k * n] -= 1

        for j in range(1, n + 1):
            if (s[j - 1] == '1'):
                now += 1
            index = j - k * now

            # Reduce totCount at index + k*n
            totCount[index + k * n] -= 1

    # Slightly modified prefix sum storage
    prefix_sum = [-1] * n

    # Number of 1's till i-1
    cnt = 0

    for i in range(n):
        prefix_sum[i] = cnt
        if (s[i] == '1'):
            cnt += 1

    # Traversing over string considering
    # each position and finding bounds
    # and count using the inequalities
    for k in range(n):
        j = 1
        while (j <= (n // x) and
               prefix_sum[k] + j <= cnt):

            # Calculating bounds for l and r
            l = (ones[prefix_sum[k] + j - 1] -
                                      k + 1)

            r = ones[prefix_sum[k] + j] - k
            l = max(l, j * (x + 1))

            # If valid then add to answer
            if (l <= r):
                sum += r // j - (l - 1) // j

            j += 1

    return sum

# Driver code
if __name__ == "__main__":

    S = "1111100000"

    print (countOfSubstrings(S))

# This code is contributed by chitranayal
```

## C#

```
// C# program to count number of
// subString under given condition
using System;
using System.Collections.Generic;

class GFG{

// Function return count of such
// substring
static int countOfSubStrings(String s)
{
    int n = s.Length;

    // Selection of adequate x value
    int x = (int)Math.Sqrt(n);

    // Store where 1's are located
    List<int> ones = new List<int>();

    for(int i = 0; i < n; i++)
    {
        if (s[i] == '1')
            ones.Add(i);
    }

    // If there are no ones,
    // then answer is 0
    if (ones.Count == 0)
        return 0;

    // For ease of implementation
    ones.Add(n);

    // Count storage
    int []totCount = new int[n * x + n];

    int sum = 0;

    // Iterate on all k values less
    // than fixed x
    for(int k = 0; k <= x; k++)
    {

        // Keeps a count of 1's occured
        // during String traversal
        int now = 0;
        totCount[k * n]++;

        // Iterate on String and modify
        // the totCount
        for(int j = 1; j <= n; j++)
        {

            // If this character is 1
            if (s[j-1] == '1')
                now++;

            int index = j - k * now;

            // Add to the readonly sum/count
            sum += totCount[index + k * n];

            // Increase totCount at exterior
            // position
            totCount[index + k * n]++;
        }
        now = 0;
        totCount[k * n]--;

        for(int j = 1; j <= n; j++)
        {
            if (s[j-1] == '1')
                now++;

            int index = j - k * now;

            // Reduce totCount at index + k*n
            totCount[index + k * n]--;
        }
    }

    // Slightly modified prefix sum storage
    int []prefix_sum = new int[n];
    for(int i = 0; i < n; i++)
        prefix_sum [i]= -1;

    // Number of 1's till i-1
    int cnt = 0;

    for(int i = 0; i < n; i++)
    {
        prefix_sum[i] = cnt;
        if (s[i] == '1')
            cnt++;
    }

    // Traversing over String considering
    // each position and finding bounds
    // and count using the inequalities
    for(int k = 0; k < n; k++)
    {
        for(int j = 1; j <= (n / x) &&
            prefix_sum[k] + j <= cnt; j++)
        {

            // Calculating bounds for l and r
            int l = ones[prefix_sum[k] + j - 1]-
                                         k + 1;

            int r = ones[prefix_sum[k] + j] - k;
            l = Math.Max(l, j * (x + 1));

            // If valid then add to answer
            if (l <= r)
            {
                sum += r / j - (l - 1) / j;
            }
        }
    }
    return sum;
}

// Driver code
public static void Main(String[] args)
{
    String S = "1111100000";

    Console.Write(countOfSubStrings(S));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to count number of
// substring under given condition

// Function return count of such
// substring
function countOfSubstrings(s)
{

    var n = s.length;

    // Selection of adequate x value
    var x = parseInt(Math.sqrt(n));

    // Store where 1's are located
    var ones = [];

    for (var i = 0; i < n; i++) {
        if (s[i] == '1')
            ones.push(i);
    }

    // If there are no ones,
    // then answer is 0
    if (ones.length == 0)
        return 0;

    // For ease of implementation
    ones.push(n);

    // Count storage
    var totCount = Array(n * x + n).fill(0);

    var sum = 0;

    // Iterate on all k values less
    // than fixed x
    for (var k = 0; k <= x; k++) {
        // Keeps a count of 1's occured
        // during string traversal
        var now = 0;
        totCount[k * n]++;

        // Iterate on string and modify
        // the totCount
        for (var j = 1; j <= n; j++) {
            // If this character is 1
            if (s[j - 1] == '1')
                now++;
            var index = j - k * now;

            // Add to the final sum/count
            sum += totCount[index + k * n];

            // Increase totCount at exterior
            // position
            totCount[index + k * n]++;
        }
        now = 0;
        totCount[k * n]--;

        for (var j = 1; j <= n; j++) {
            if (s[j - 1] == '1')
                now++;
            var index = j - k * now;

            // Reduce totCount at index + k*n
            totCount[index + k * n]--;
        }
    }

    // Slightly modified prefix sum storage
    var prefix_sum = Array(n).fill(-1);

    // Number of 1's till i-1
    var cnt = 0;

    for (var i = 0; i < n; i++) {
        prefix_sum[i] = cnt;
        if (s[i] == '1')
            cnt++;
    }

    // Traversing over string considering
    // each position and finding bounds
    // and count using the inequalities
    for (var k = 0; k < n; k++)
    {
        for (var j = 1; j <= parseInt(n / x)
             && prefix_sum[k] + j <= cnt; j++)
        {
            // Calculating bounds for l and r
            var l = ones[prefix_sum[k] + j - 1]
                    - k + 1;

            var r = ones[prefix_sum[k] + j] - k;

            l = Math.max(l, j * (x + 1));

            // If valid then add to answer
            if (l <= r) {
                sum += parseInt(r / j) - parseInt((l - 1) / j);
            }
        }
    }

    return sum;
}

var S = "1111100000";
document.write( countOfSubstrings(S));

</script>
```

**Output:** 

```
25
```

**时间复杂度:** ![O(N\sqrt{N})        ](img/aace87fab9376fc580fbc39fe372b430.png "Rendered by QuickLaTeX.com")

**辅助空间:** O(N <sup>3/2</sup> )