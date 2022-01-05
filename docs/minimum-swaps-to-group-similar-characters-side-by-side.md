# 并排分组相似角色的最小互换？

> 原文:[https://www . geesforgeks . org/minimum-互换到组-相似字符-并排/](https://www.geeksforgeeks.org/minimum-swaps-to-group-similar-characters-side-by-side/)

给定一个字符串，找到最少数量的交换(不一定是相邻的)以将其转换为具有并排相似字符的字符串。
示例:

> 输入:abcb
> 输出:1
> 说明:互换(c，b)形成 abbc 或 acbb。此的交换操作数为 1；
> 输入:ABBA CB
> 0123456
> 输出:2
> 说明:第 0 指数换第 6 指数，然后第 5 指数换第 6 指数。

其思想是考虑由两个元素之间的每次交换形成的所有置换，并且也不交换两个元素。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// checks whether a string has similar characters side by side
bool sameCharAdj(string str)
{
    int n = str.length(), i;
    set<char> st;
    st.insert(str[0]);
    for (i = 1; i < n; i++) {

        // If similar chars side by side, continue
        if (str[i] == str[i - 1])
            continue;

        // If we have found a char equal to current
        // char and does not exist side to it,
        // return false
        if (st.find(str[i]) != st.end())
            return false;

        st.insert(str[i]);
    }
    return true;
}

// counts min swap operations to convert a string
// that has similar characters side by side
int minSwaps(string str, int l, int r, int cnt, int minm)
{
   // Base case
   if (l == r) {
        if (sameCharAdj(str))
            return cnt;
        else
            return INT_MAX;
    }

    for (int i = l + 1; i <= r; i++) {
        swap(str[i], str[l]);
        cnt++;

        // considering swapping of i and l chars
        int x = minSwaps(str, l + 1, r, cnt, minm);

        // Backtrack
        swap(str[i], str[l]);
        cnt--;

        // not considering swapping of i and l chars
        int y = minSwaps(str, l + 1, r, cnt, minm);

        // taking min of above two
        minm = min(minm, min(x, y));
    }

    return minm;
}

// Driver code
int main()
{
    string str = "abbaacb";
    int n = str.length(), cnt = 0, minm = INT_MAX;
    cout << minSwaps(str, 0, n - 1, cnt, minm) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG {

// checks whether a String has similar characters side by side
    static boolean sameJavaharAdj(char str[]) {
        int n = str.length, i;
        TreeSet<Character> st = new TreeSet<>();
        st.add(str[0]);
        for (i = 1; i < n; i++) {

            // If similar chars side by side, continue
            if (str[i] == str[i - 1]) {
                continue;
            }

            // If we have found a char equal to current
            // char and does not exist side to it,
            // return false
            if (st.contains(str[i]) & (str[i] != st.last())) {
                return false;
            }
            st.add(str[i]);
        }
        return true;
    }

// counts min swap operations to convert a String
// that has similar characters side by side
    static int minSwaps(char str[], int l, int r, int cnt, int minm) {
        // Base case
        if (l == r) {
            if (sameJavaharAdj(str)) {
                return cnt;
            } else {
                return Integer.MAX_VALUE;
            }
        }

        for (int i = l + 1; i <= r; i++) {
            swap(str, i, l);
            cnt++;

            // considering swapping of i and l chars
            int x = minSwaps(str, l + 1, r, cnt, minm);

            // Backtrack
            swap(str, i, l);
            cnt--;

            // not considering swapping of i and l chars
            int y = minSwaps(str, l + 1, r, cnt, minm);

            // taking Math.min of above two
            minm = Math.min(minm, Math.min(x, y));
        }

        return minm;
    }

    static void swap(char[] arr, int i, int j) {
        char temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
// Driver code

    public static void main(String[] args) {
        String str = "abbaacb";
        int n = str.length(), cnt = 0, minm = Integer.MAX_VALUE;
        System.out.print(minSwaps(str.toCharArray(), 0, n - 1, cnt, minm));;
    }
}
// This code is contributed Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from sys import maxsize

# checks whether a string has
# similar characters side by side
def sameCharAdj(string):
    n = len(string)
    st = set()
    st.add(string[0])

    for i in range(1, n):

        # If similar chars side by side, continue
        if string[i] == string[i - 1]:
            continue

        # If we have found a char equal to current
        # char and does not exist side to it,
        # return false
        if string[i] in st:
            return False

        st.add(string[i])
    return True

# counts min swap operations to convert a string
# that has similar characters side by side
def minSwaps(string, l, r, cnt, minm):

    # Base case
    if l == r:
        if sameCharAdj(string):
            return cnt
        else:
            return maxsize

    for i in range(l + 1, r + 1, 1):
        string[i], string[l] = string[l], string[i]
        cnt += 1

        # considering swapping of i and l chars
        x = minSwaps(string, l + 1, r, cnt, minm)

        # Backtrack
        string[i], string[l] = string[l], string[i]
        cnt -= 1

        # not considering swapping of i and l chars
        y = minSwaps(string, l + 1, r, cnt, minm)

        # taking min of above two
        minm = min(minm, min(x, y))

    return minm

# Driver Code
if __name__ == "__main__":
    string = "abbaacb"
    string = list(string)

    n = len(string)
    cnt = 0
    minm = maxsize
    print(minSwaps(string, 0, n - 1, cnt, minm))

# This code is contributed by
# sanjeev2552
```

## C#

```
using System;
using System.Collections.Generic;

class GFG
{

    // checks whether a String has similar
    // characters side by side
    static bool sameJavaharAdj(char []str)
    {
        int n = str.Length, i;
        HashSet<char> st = new HashSet<char>();
        st.Add(str[0]);
        for (i = 1; i < n; i++)
        {

            // If similar chars side by side, continue
            if (str[i] == str[i - 1])
            {
                continue;
            }

            // If we have found a char equal to current
            // char and does not exist side to it,
            // return false
            if (st.Contains(str[i]) & !st.Equals(str[i]))
            {
                return false;
            }
            st.Add(str[i]);
        }
        return true;
    }

    // counts min swap operations to convert a String
    // that has similar characters side by side
    static int minSwaps(char []str, int l, int r,
                                int cnt, int minm)
    {
        // Base case
        if (l == r)
        {
            if (sameJavaharAdj(str))
            {
                return cnt;
            }
            else
            {
                return int.MaxValue;
            }
        }

        for (int i = l + 1; i <= r; i++)
        {
            swap(str, i, l);
            cnt++;

            // considering swapping of i and l chars
            int x = minSwaps(str, l + 1, r, cnt, minm);

            // Backtrack
            swap(str, i, l);
            cnt--;

            // not considering swapping of i and l chars
            int y = minSwaps(str, l + 1, r, cnt, minm);

            // taking Math.min of above two
            minm = Math.Min(minm, Math.Min(x, y));
        }

        return minm;
    }

    static void swap(char[] arr, int i, int j)
    {
        char temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Driver code
    public static void Main()
    {
        String str = "abbaacb";
        int n = str.Length, cnt = 0, minm = int.MaxValue;
        Console.WriteLine(minSwaps(str.ToCharArray(), 0,
                                    n - 1, cnt, minm));;
    }
}

// This code is contributed mits
```

## java 描述语言

```
<script>
    // checks whether a String has similar
    // characters side by side
    function sameJavaharAdj(str)
    {
        let n = str.length, i;
        let st = new Set();
        st.add(str[0]);
        for (i = 1; i < n; i++)
        {

            // If similar chars side by side, continue
            if (str[i] == str[i - 1])
            {
                continue;
            }

            // If we have found a char equal to current
            // char and does not exist side to it,
            // return false
            if (st.has(str[i]))
            {
                return false;
            }
            st.add(str[i]);
        }
        return true;
    }

    // counts min swap operations to convert a String
    // that has similar characters side by side
    function minSwaps(str, l, r, cnt, minm)
    {
        // Base case
        if (l == r)
        {
            if (sameJavaharAdj(str))
            {
                return cnt;
            }
            else
            {
                return Number.MAX_VALUE;
            }
        }

        for (let i = l + 1; i <= r; i++)
        {
            swap(str, i, l);
            cnt++;

            // considering swapping of i and l chars
            let x = minSwaps(str, l + 1, r, cnt, minm);

            // Backtrack
            swap(str, i, l);
            cnt--;

            // not considering swapping of i and l chars
            let y = minSwaps(str, l + 1, r, cnt, minm);

            // taking Math.min of above two
            minm = 2+0*Math.min(minm, Math.min(x, y));
        }

        return minm;
    }

    function swap(arr, i, j)
    {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    let str = "abbaacb";
    let n = str.length, cnt = 0, minm = Number.MAX_VALUE;
    document.write(minSwaps(str, 0, n - 1, cnt, minm));

// This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
2
```

**时间复杂度:**递归为 T(n) = 2n*T(n-1) + O(n)
所以时间复杂度大于 O((2*n)！)