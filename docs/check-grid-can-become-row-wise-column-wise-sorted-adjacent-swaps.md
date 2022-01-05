# 检查相邻交换后网格是否可以按行和列排序

> 原文:[https://www . geesforgeks . org/check-grid-can-wise-row-column-wise-sorted-neighbor-swaps/](https://www.geeksforgeeks.org/check-grid-can-become-row-wise-column-wise-sorted-adjacent-swaps/)

给定一个大小为 n×len 的网格，用小写字符填充。我们可以在同一行和同一列中交换两个相邻的字符。现在我们必须检查是否有可能以这样的顺序排列，即网格中的每一行和每一列都是按字典顺序排序的。
示例:

```
Input : abcde
        fghij
        olmkn
        trpqs
        xywuv
Output : Yes
Explanation :
The grid can be rearranged as
abcde
fghij
klmno
pqrst
uvwxy
```

做上面这道题的思路真的很简单我们可以简单的对同一行的字符进行排序然后只需
检查列虎钳新网格是否排序列虎钳。请不要以为相邻互换可以排序([冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)例如只做相邻互换)
下面给出上述思路的实现。

## C++

```
// C++ program to check if we can make a
// grid of character sorted using adjacent
// swaps.
#include <bits/stdc++.h>
using namespace std;

// v[] is vector of strings. len is length
// of strings in every row.
bool check(vector<string> v, int len)
{
    int n = v.size();
    for (int i = 0; i < n; i++)
        sort(v[i].begin(), v[i].end());

    for (int i = 0; i < len-1; i++)
        for (int j = 0; j < n; j++)
            if (v[i][j] > v[i+1][j])
                return false;
    return true;
}

// Driver code
int main()
{
    vector<string> v = { "ebcda", "ihgfj", "klmno",
                               "pqrst", "yvwxu" };
    int len = 5; // Length of strings
    check(v, len)? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if we can make a grid
// of character sorted using adjacent swaps.
import java.util.Arrays;

class GfG
{

    // v[] is vector of strings. len is
    // length of strings in every row.
    static boolean check(String[] v, int len)
    {
        int n = v.length;
        char[] tempArray;

        for (int i = 0; i < n; i++)
        {
            tempArray = v[i].toCharArray();
            Arrays.sort(tempArray);
            v[i] = new String(tempArray);
        }

        for (int i = 0; i < len-1; i++)
            for (int j = 0; j < n; j++)
                if (v[i].charAt(j) > v[i+1].charAt(j))
                    return false;
        return true;
    }

    // Driver code
    public static void main(String []args)
    {

        String[] v = { "ebcda", "ihgfj", "klmno",
                            "pqrst", "yvwxu" };

        int len = 5; // Length of strings
        if (check(v, len))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Rituraj Jain
```

## 计算机编程语言

```
# Python program to check if we can make a
# grid of character sorted using adjacent
# swaps.

# v[] is vector of strings. len is length
# of strings in every row.
def check(v, l):
    n = len(v)
    for i in v:
        i = ''.join(sorted(i))

    for i in range(l - 1):
        for j in range(n):
            if (v[i][j] > v[i + 1][j]):
                return False
    return True

# Driver code
v = [ "ebcda", "ihgfj", "klmno", "pqrst", "yvwxu" ]
l = 5 # Length of strings
if check(v, l):
    print "Yes"
else:
    print "No"

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to check if we can make a grid
// of character sorted using adjacent swaps.
using System;

class GfG
{

    // v[] is vector of strings. len is
    // length of strings in every row.
    static Boolean check(String[] v, int len)
    {
        int n = v.Length;
        char[] tempArray;

        for (int i = 0; i < n; i++)
        {
            tempArray = v[i].ToCharArray();
            Array.Sort(tempArray);
            v[i] = new String(tempArray);
        }

        for (int i = 0; i < len-1; i++)
            for (int j = 0; j < n; j++)
                if (v[i][j] > v[i+1][j])
                    return false;
        return true;
    }

    // Driver code
    public static void Main(String []args)
    {

        String[] v = { "ebcda", "ihgfj", "klmno",
                            "pqrst", "yvwxu" };

        int len = 5; // Length of strings
        if (check(v, len))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to check if we can make a grid
// of character sorted using adjacent swaps.

// v[] is vector of strings. len is
    // length of strings in every row.
function check(v,len)
{
    let n = v.length;
        let tempArray;

        for (let i = 0; i < n; i++)
        {
            tempArray = v[i].split("");
            (tempArray).sort();
            v[i] = (tempArray).join("");
        }

        for (let i = 0; i < len-1; i++)
            for (let j = 0; j < n; j++)
                if (v[i][j] > v[i+1][j])
                    return false;
        return true;
}

// Driver code
let v = ["ebcda", "ihgfj", "klmno",
                            "pqrst", "yvwxu" ];
let len = 5; // Length of strings

if (check(v, len))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rag2127
</script>
```

**输出:**

```
Yes
```

本文由**萨尔特哈克·科利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。