# 找到使两个字符串相等所需的最小预处理移动次数

> 原文:[https://www . geeksforgeeks . org/find-最小数量的预处理移动-需要使两个字符串相等/](https://www.geeksforgeeks.org/find-the-minimum-number-of-preprocess-moves-required-to-make-two-strings-equal/)

给定两个长度相等的字符串 **A** 和 **B** ，由小写英文字母组成。任务是在应用以下操作后，计算使其等于弦 **B** 所需的弦 **A** 上的**预处理移动**的最小次数:

1.  选择任意指数 i (0 ≤ i < n) and swap characters a <sub>i</sub> 和 b <sub>i</sub> 。
2.  选择任意指数 i (0 ≤ i < n) and swap characters a <sub>i</sub> 和 a<sub>n–I–1</sub>。
3.  选择任意指数 i (0 ≤ i < n) and swap characters b <sub>i</sub> 和 b<sub>n–I–1</sub>。

在一个**预处理步骤**中，你可以用英语字母表中的任何其他字符替换 A 中的一个字符。

**示例:**

> **输入:** A =“阿巴卡巴”，B =“巴卡巴”
> T3】输出: 4
> 预处理动作如下:
> 设置 A<sub>0</sub>=“B”，A<sub>2</sub>=“c”，A<sub>3</sub>=“A”和 A<sub>4</sub>=“B”，A 变成“bbcabba”。
> 然后我们可以通过以下操作顺序获得相等的字符串:
> 交换(A <sub>1</sub> 、B <sub>1</sub> )和交换(A <sub>1</sub> 、A <sub>5</sub> )。
> 
> **输入:** A = "zcabd" B = "dbacz"
> **输出:** 0
> 不需要预处理移动。
> 我们可以用下面的变化顺序让 A 和 B 相等:
> 互换(B <sub>0</sub> ，B <sub>4</sub> )然后互换(A <sub>1</sub> ，A <sub>3</sub> )。

**方法:**让我们将两个字符串的所有字符分成组，使得每组中的字符可以随着变化而相互交换。所以会有以下几组:{A <sub>0</sub> 、A<sub>n–1</sub>、B <sub>0</sub> 、B<sub>n–1</sub>}、{A <sub>1</sub> 、A<sub>n–2</sub>、B <sub>1</sub> 、B<sub>n–2</sub>等等。由于这几组互不影响，我们可以计算出每组的预处理步数，然后进行汇总。
如何判断一个组是否不需要任何预处理动作？

对于一个由 2 个字符组成的组(如果 n 是奇数，将有一个这样的组)，这很容易——如果这个组中的字符相等，答案是 0，否则是 1。

要确定由四个字符组成的组所需的预处理移动次数，我们可以使用以下事实:如果该组中的字符可以分成对，则该组不需要任何预处理移动。所以如果这个组包含四个相等的字符或者两对相等的字符，那么这个组的答案是 0。否则，我们可能会检查仅替换 A <sub>i</sub> 和 A<sub>n–I–1</sub>中的一个字符就足够了。如果是，那么答案就是 1，否则就是 2。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number of
// pre-processing moves required on string A
int Preprocess(string A, string B)
{
    // Length of the given strings
    int n = A.size();

    // To store the required answer
    int ans = 0;

    // Run a loop upto n/2
    for (int i = 0; i < n / 2; i++) {

        // To store frequency of 4 characters
        map<char, int> mp;
        mp[A[i]]++;
        mp[A[n - i - 1]]++;
        mp[B[i]]++;
        mp[B[n - i - 1]]++;
        int sz = mp.size();

        // If size is 4
        if (sz == 4)
            ans += 2;

        // If size is 3
        else if (sz == 3)
            ans += 1 + (A[i] == A[n - i - 1]);

        // If size is 2
        else if (sz == 2)
            ans += mp[A[i]] != 2;
    }

    // If n is odd
    if (n % 2 == 1 && A[n / 2] != B[n / 2])
        ans++;

    return ans;
}

// Driver code
int main()
{
    string A = "abacaba", B = "bacabaa";
    cout << Preprocess(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Function to return the minimum number of
    // pre-processing moves required on string A
    static int Preprocess(String A, String B)
    {
        // Length of the given strings
        int n = A.length();

        // To store the required answer
        int ans = 0;

        // Run a loop upto n/2
        for (int i = 0; i < n / 2; i++)
        {

            // To store frequency of 4 characters

            HashMap<Character, Integer> mp = new HashMap<>();

            if(mp.containsKey(A.charAt(i)))
                mp.put(A.charAt(i), mp.get(A.charAt(i))+1);
            else
            mp.put(A.charAt(i), 1);

            if(mp.containsKey(A.charAt(n-i-1)))
                mp.put(A.charAt(n-i-1), mp.get(A.charAt(n-i-1))+1);
            else
            mp.put(A.charAt(n-i-1), 1);

            if(mp.containsKey(B.charAt(i)))
                mp.put(B.charAt(i), mp.get(B.charAt(i))+1);
            else
            mp.put(B.charAt(i), 1);

            if(mp.containsKey(B.charAt(n-i-1)))
                mp.put(B.charAt(n-i-1), mp.get(B.charAt(n-i-1))+1);
            else
            mp.put(B.charAt(n-i-1), 1);

            int sz = mp.size();

            // If size is 4
            if (sz == 4)
                ans += 2;

            // If size is 3
            else if (sz == 3)
                ans += 1 + (A.charAt(i) == A.charAt(n - i - 1) ? 1 : 0 );

            // If size is 2
            else if (sz == 2)
                ans += mp.get(A.charAt(i)) != 2 ? 1 : 0;
        }

        // If n is odd
        if (n % 2 == 1 && A.charAt(n / 2) != B.charAt(n / 2))
            ans++;

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        String A = "abacaba", B = "bacabaa";
        System.out.println(Preprocess(A, B));

    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number of
# pre-processing moves required on string A
def Preprocess(A, B):

    # Length of the given strings
    n = len(A)

    # To store the required answer
    ans = 0

    # Run a loop upto n/2
    for i in range(n // 2):

        # To store frequency of 4 characters
        mp = dict()

        mp[A[i]] = 1
        if A[i] == A[n - i - 1]:
            mp[A[n - i - 1]] += 1

        if B[i] in mp.keys():
            mp[B[i]] += 1
        else:
            mp[B[i]] = 1

        if B[n - i - 1] in mp.keys():
            mp[B[n - 1 - i]] += 1
        else:
            mp[B[n - 1 - i]] = 1

        sz = len(mp)

        # If size is 4
        if (sz == 4):
            ans += 2

        # If size is 3   
        elif (sz == 3):
            ans += 1 + (A[i] == A[n - i - 1])

        # If size is 2
        elif (sz == 2):
            ans += mp[A[i]] != 2

    # If n is odd
    if (n % 2 == 1 and A[n // 2] != B[n // 2]):
        ans += 1

    return ans

# Driver code
A = "abacaba"
B = "bacabaa"
print(Preprocess(A, B))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    // Function to return the minimum number of
    // pre-processing moves required on string A
    static int Preprocess(string A, string B)
    {
        // Length of the given strings
        int n = A.Length;

        // To store the required answer
        int ans = 0;

        // Run a loop upto n/2
        for (int i = 0; i < n / 2; i++)
        {

            // To store frequency of 4 characters

            Dictionary<char, int> mp = new Dictionary<char, int>();

            if(mp.ContainsKey(A[i]))
                mp[A[i]]++;
            else
            mp[A[i]] = 1;

            if(mp.ContainsKey(A[n-i-1]))
                mp[A[n - i - 1]]++;
            else
                mp[A[n - i - 1]] = 1;

            if(mp.ContainsKey(B[i]))
                mp[B[i]]++;
            else
            mp[B[i]] = 1;

            if(mp.ContainsKey(B[n-i-1]))
                mp[B[n - i - 1]]++;
            else
                mp[B[n - i - 1]] = 1;

            int sz = mp.Count;

            // If size is 4
            if (sz == 4)
                ans += 2;

            // If size is 3
            else if (sz == 3)
                ans += 1 + (A[i] == A[n - i - 1] ? 1 : 0 );

            // If size is 2
            else if (sz == 2)
                ans += mp[A[i]] != 2 ? 1 : 0;
        }

        // If n is odd
        if (n % 2 == 1 && A[n / 2] != B[n / 2])
            ans++;

        return ans;
    }

    // Driver code
    public static void Main ()
    {
        string A = "abacaba", B = "bacabaa";
        Console.WriteLine(Preprocess(A, B));

    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum number of
// pre-processing moves required on string A
function Preprocess($A, $B)
{

    // Length of the given strings
    $n = strlen($A);

    // To store the required answer
    $ans = 0;

    // To store frequency of 4 characters
    $mp = array();

    for($i = 0; $i < $n ; $i++)
        $mp[$A[$i]] = 0;

    // Run a loop upto n/2
    for ($i = 0; $i < floor($n / 2); $i++)
    {
        $mp[$A[$i]]++;
        $mp[$A[$n - $i - 1]]++;
        $mp[$B[$i]]++;
        $mp[$B[$n - $i - 1]]++;
        $sz = sizeof($mp);

        // If size is 4
        if ($sz == 4)
            $ans += 2;

        // If size is 3
        else if ($sz == 3)
            if($A[$i] == $A[$n - $i - 1])
                $ans += 1;
            else
                $ans += 1;

        // If size is 2
        else if ($sz == 2)
            $ans += $mp[$A[$i]] != 2;
    }

    // If n is odd
    if ($n % 2 == 1 && ($A[floor($n / 2)] !=
                        $B[floor($n / 2)]))
        $ans++;

    return $ans;
}

// Driver code
$A = "abacaba";
$B = "bacabaa";
echo Preprocess($A, $B);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum number of
// pre-processing moves required on string A
function Preprocess(A, B)
{

    // Length of the given strings
    let n = A.length;

    // To store the required answer
    let ans = 0;

    // Run a loop upto n/2
    for(let i = 0; i < n / 2; i++)
    {

        // To store frequency of 4 characters
        let mp = new Map();

        if (mp.has(A[i]))
            mp.set(A[i], mp.get(A[i]) + 1);
        else
        mp.set(A[i], 1);

        if (mp.has(A[n - i - 1]))
            mp.set(A[n - i - 1],
            mp.get(A[n - i - 1]) + 1);
        else
            mp.set(A[n - i - 1], 1);

        if (mp.has(B[i]))
            mp.set(B[i], mp.get(B[i]) + 1);
        else
            mp.set(B[i], 1);

        if (mp.has(B[n - i - 1]))
            mp.set(B[n - i - 1],
            mp.get(B[n - i - 1]) + 1);
        else
            mp.set(B[n - i - 1], 1);

        let sz = mp.size;

        // If size is 4
        if (sz == 4)
            ans += 2;

        // If size is 3
        else if (sz == 3)
            ans += 1 + (A[i] ==
             A[n - i - 1] ? 1 : 0);

        // If size is 2
        else if (sz == 2)
            ans += mp.get(A[i]) != 2 ? 1 : 0;
    }

    // If n is odd
    if (n % 2 == 1 && A[Math.floor(n / 2)] !=
                      B[Math.floor(n / 2)])
        ans++;

    return ans;
}

// Driver code
let A = "abacaba", B = "bacabaa";
document.write(Preprocess(A, B));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4
```