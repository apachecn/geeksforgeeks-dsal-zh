# 重复替换两个不同相邻的最小长度字符串

> 原文:[https://www . geesforgeks . org/最小长度字符串重复替换两个不同的相邻/](https://www.geeksforgeeks.org/smallest-length-string-with-repeated-replacement-of-two-distinct-adjacent/)

给定一个由三个字母' a '，' b '和' c '组成的任意组合的字符串，通过重复应用以下操作，找出可以获得的最小字符串的长度:

*取任意两个相邻的、不同的字符，用第三个替换。*

**示例:**

```
Input : cab
Output : 2
We can select any two adjacent letters, 
say 'ca' and transform it into 'b', this 
leaves us with string 'bb' of length two.

Input : bcab
Output : 1
Selecting 'bc' and transforming it to 'a' 
leaves us with 'aab'. We can then select
'ab' and transform it to 'c', giving 'ac'. 
This can further be transformed into 'b',
which is of length one.
```

一个天真的方法是找到所有可能的替换，并递归直到我们找到最小的字符串。这需要指数级的时间。

**引理**:字母的顺序不影响最小字符串的长度或值。

**归纳法证明**
**底例**:取字符串‘ab’和‘ba’，两者均化简为‘c’

**归纳假设**:假设每个字符串中每个字母出现的次数相同，那么长度为< = k 的所有字符串都减少到同一个字符串。

**归纳步骤**:取两个长度为 k + 1 的字符串，每个字母出现的次数相同。找出一对相邻的字母

在两个弦上。这里出现了两种情况:

1.  我们设法找到了这样一对字母。然后，我们可以用第三个字母替换这些字母，从而得到长度为 k 的两个字符串，每个字母都有相同的出现，通过归纳假设，可以简化为相同的字符串。也就是说，我们有“abccb”和“accbba”，并减少两个字符串中的“ac”，因此我们得到“abccb”和“bcbba”。
2.  我们找不到这样的一对。当字符串中的所有字母都相同时，就会出现这种情况。在这种情况下，两个字符串本身是相同的，即“ccccccc”和“ccccccc”。

因此，通过归纳法，我们证明了这个引理。

**动态规划方法**
我们现在可以设计一个使用动态规划的函数来解决这个问题。

## C++

```
// C++ program to find smallest possible length
// of a string of only three characters
#include<bits/stdc++.h>
using namespace std;

// Program to find length of reduced string
// in a string made of three characters.
#define MAX_LEN 110

// To store results of subproblems
int DP[MAX_LEN][MAX_LEN][MAX_LEN];

// A memoized function find result recursively.
// a, b and c are counts of 'a's, 'b's and
// 'c's in str
int length(int a, int b, int c)
{
    // If this subproblem is already evaluated
    if (DP[a][b] != -1)
        return DP[a][b];

    // If there is only one type of character
    if (a == 0 && b == 0)
        return (DP[a][b] = c);
    if (a == 0 && c == 0)
        return (DP[a][b] = b);
    if (b == 0 && c == 0)
        return (DP[a][b] = a);

    // If only two types of characters are present
    if (a == 0)
        return (DP[a][b] =
                    length(a + 1, b - 1, c - 1));
    if (b == 0)
        return (DP[a][b] =
                    length(a - 1, b + 1, c - 1));
    if (c == 0)
        return (DP[a][b] =
                    length(a - 1, b - 1, c + 1));

    // If all types of characters are present.
    // Try combining all pairs.
    return (DP[a][b] =
                min(length(a - 1, b - 1, c + 1),
                    min(length(a - 1, b + 1, c - 1),
                        length(a + 1, b - 1, c - 1))));
}

// Returns smallest possible length with given
// operation allowed.
int stringReduction(string str)
{
    int n = str.length();

    // Counting occurrences of three different
    // characters 'a', 'b' and 'c' in str
    int count[3] = {0};
    for (int i=0; i<n; ++i)
        count[str[i]-'a']++;

    // Initialize DP[][] entries as -1
    for (int i = 0; i <= count[0]; ++i)
        for (int j = 0; j < count[1]; ++j)
            for (int k = 0; k < count[2]; ++k)
                DP[i][j][k] = -1;

    return length(count[0], count[1], count[2]);
}

// Driver code
int main()
{
    string str = "abcbbaacb";
    cout << stringReduction(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest possible length
// of a string of only three characters
import java.io.*;
class GFG
{
  static int MAX_LEN = 110;

  // Program to find length of reduced string
  // in a string made of three characters.
  static int[][][] DP = new int[MAX_LEN][MAX_LEN][MAX_LEN];

  // A memoized function find result recursively.
  // a, b and c are counts of 'a's, 'b's and
  // 'c's in str
  static int length(int a, int b, int c)
  {

    // If this subproblem is already
    // evaluated
    if(a < 0 || b < 0 || c < 0)

      // If this subproblem is already evaluated
      if (DP[a][b] != -1)
        return DP[a][b];

    // If there is only one type of character
    if (a == 0 && b == 0)
      return (DP[a][b] = c);
    if (a == 0 && c == 0)
      return (DP[a][b] = b);
    if (b == 0 && c == 0)
      return (DP[a][b] = a);

    // If only two types of characters are present
    if (a == 0)
      return (DP[a][b] =
              length(a + 1, b - 1, c - 1));
    if (b == 0)
      return (DP[a][b] =
              length(a - 1, b + 1, c - 1));
    if (c == 0)
      return (DP[a][b] =
              length(a - 1, b - 1, c + 1));

    // If all types of characters are present.
    // Try combining all pairs.
    DP[a][b] =
      Math.min(length(a - 1, b - 1, c + 1),
               Math.min(length(a - 1, b + 1, c - 1),
                        length(a + 1, b - 1, c - 1)));

    return DP[a][b];
  }

  // Returns smallest possible length with given
  // operation allowed.
  static int stringReduction(String str)
  {
    int n = str.length();

    // Counting occurrences of three different
    // characters 'a', 'b' and 'c' in str
    int[] count = new int[3];
    for (int i = 0; i < n; ++i)
      count[str.charAt(i) - 'a']++;

    // Initialize DP[][] entries as -1
    for (int i = 0; i <= count[0]; ++i)
      for (int j = 0; j < count[1]; ++j)
        for (int k = 0; k < count[2]; ++k)
          DP[i][j][k] = -1;

    return length(count[0], count[1], count[2]);
  }

  // Driver code
  public static void main (String[] args) {
    String str = "abcbbaacb";
    System.out.println(stringReduction(str));
  }
}

//  This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to find smallest possible
# length of a string of only three characters

# A memoized function find result recursively.
# a, b and c are counts of 'a's, 'b's and
# 'c's in str
def length(a, b, c):

    global DP

    #print(a, b, c)

    # If this subproblem is already
    # evaluated
    if a < 0 or b < 0 or c < 0:
        return 0

    if (DP[a][b] != -1):
        return DP[a][b]

    # If there is only one type
    # of character
    if (a == 0 and b == 0):
        DP[a][b] = c
        return c
    if (a == 0 and c == 0):
        DP[a][b] = b
        return b
    if (b == 0 and c == 0):
        DP[a][b] = a
        return a

    # If only two types of characters
    # are present
    if (a == 0):
        DP[a][b] = length(a + 1, b - 1,
                             c - 1)
        return DP[a][b]

    if (b == 0):
        DP[a][b] = length(a - 1, b + 1,
                             c - 1)
        return DP[a][b]

    if (c == 0):
        DP[a][b] = length(a - 1, b - 1,
                             c + 1)
        return DP[a][b]

    # If all types of characters are present.
    # Try combining all pairs.
    x = length(a - 1, b - 1, c + 1)
    y = length(a - 1, b + 1, c - 1)
    z = length(a + 1, b - 1, c - 1)

    DP[a][b] = min([x, y, z])

    return DP[a][b]

# Returns smallest possible length with
# given operation allowed.
def stringReduction(str):

    n = len(str)

    # Counting occurrences of three different
    # characters 'a', 'b' and 'c' in str
    count = [0] * 3

    for i in range(n):
        count[ord(str[i]) - ord('a')] += 1

    return length(count[0], count[1], count[2])

# Driver code
if __name__ == '__main__':

    DP = [[[-1 for i in range(110)]
               for i in range(110)]
               for i in range(110)]

    str = "abcbbaacb"

    print(stringReduction(str))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find smallest possible length
// of a string of only three characters
using System;
public class GFG
{

  static int MAX_LEN = 110;

  // Program to find length of reduced string
  // in a string made of three characters.
  static int[,,] DP = new int[MAX_LEN, MAX_LEN, MAX_LEN];

  // A memoized function find result recursively.
  // a, b and c are counts of 'a's, 'b's and
  // 'c's in str
  static int length(int a, int b, int c)
  {

    // If this subproblem is already
    // evaluated
    if(a < 0 || b < 0 || c < 0)

      // If this subproblem is already evaluated
      if (DP[a, b, c] != -1)
        return DP[a, b, c];

    // If there is only one type of character
    if (a == 0 && b == 0)
      return (DP[a, b, c] = c);
    if (a == 0 && c == 0)
      return (DP[a, b, c] = b);
    if (b == 0 && c == 0)
      return (DP[a, b, c] = a);

    // If only two types of characters are present
    if (a == 0)
      return (DP[a, b, c] =
              length(a + 1, b - 1, c - 1));
    if (b == 0)
      return (DP[a, b, c] =
              length(a - 1, b + 1, c - 1));
    if (c == 0)
      return (DP[a, b, c] =
              length(a - 1, b - 1, c + 1));

    // If all types of characters are present.
    // Try combining all pairs.
    DP[a, b, c] =
      Math.Min(length(a - 1, b - 1, c + 1),
               Math.Min(length(a - 1, b + 1, c - 1),
                        length(a + 1, b - 1, c - 1)));

    return DP[a, b, c];
  }

  // Returns smallest possible length with given
  // operation allowed.
  static int stringReduction(string str)
  {
    int n = str.Length;

    // Counting occurrences of three different
    // characters 'a', 'b' and 'c' in str
    int[] count = new int[3];
    for (int i = 0; i < n; ++i)
      count[str[i] - 'a']++;

    // Initialize DP[][] entries as -1
    for (int i = 0; i <= count[0]; ++i)
      for (int j = 0; j < count[1]; ++j)
        for (int k = 0; k < count[2]; ++k)
          DP[i, j, k] = -1;

    return length(count[0], count[1], count[2]);
  }

  // Driver code
  static public void Main ()
  {
    string str = "abcbbaacb";
    Console.WriteLine(stringReduction(str));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program to find smallest possible length
// of a string of only three characters
    let  MAX_LEN = 110;

    // Program to find length of reduced string
  // in a string made of three characters.
    let DP = new Array(MAX_LEN);
    for(let i = 0; i < DP.length; i++)
    {
        DP[i] = new Array(MAX_LEN);
        for(let j = 0; j < DP[i].length; j++)
        {
            DP[i][j] = new Array(MAX_LEN);
            for(let k = 0; k < MAX_LEN; k++)
            {
                DP[i][j][k] = 0;
            }
        }
    }

    // A memoized function find result recursively.
  // a, b and c are counts of 'a's, 'b's and
  // 'c's in str
    function length(a, b, c)
    {
        // If this subproblem is already
    // evaluated
    if(a < 0 || b < 0 || c < 0)

      // If this subproblem is already evaluated
      if (DP[a][b] != -1)
        return DP[a][b];

    // If there is only one type of character
    if (a == 0 && b == 0)
      return (DP[a][b] = c);
    if (a == 0 && c == 0)
      return (DP[a][b] = b);
    if (b == 0 && c == 0)
      return (DP[a][b] = a);

    // If only two types of characters are present
    if (a == 0)
      return (DP[a][b] =
              length(a + 1, b - 1, c - 1));
    if (b == 0)
      return (DP[a][b] =
              length(a - 1, b + 1, c - 1));
    if (c == 0)
      return (DP[a][b] =
              length(a - 1, b - 1, c + 1));

    // If all types of characters are present.
    // Try combining all pairs.
    DP[a][b] =
      Math.min(length(a - 1, b - 1, c + 1),
               Math.min(length(a - 1, b + 1, c - 1),
                        length(a + 1, b - 1, c - 1)));

    return DP[a][b];
    }

    // Returns smallest possible length with given
  // operation allowed.
    function stringReduction(str)
    {
        let n = str.length;

    // Counting occurrences of three different
    // characters 'a', 'b' and 'c' in str
    let count = new Array(3);
    for(let i = 0; i < 3; i++)
    {
        count[i] = 0;
    }
    for (let i = 0; i < n; ++i)
      count[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // Initialize DP[][] entries as -1
    for (let i = 0; i <= count[0]; ++i)
      for (let j = 0; j < count[1]; ++j)
        for (let k = 0; k < count[2]; ++k)
          DP[i][j][k] = -1;

    return length(count[0], count[1], count[2]);
    }

    // Driver code
    let str = "abcbbaacb";
    document.write(stringReduction(str));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
1
```

在最坏的情况下，每个字母出现在整个字符串的 1/3 处。这导致辅助空间= 0(N<sup>3</sup>)和时间复杂度= 0(N<sup>3</sup>

```
Space Complexity = O(N^3)
Time Complexity = O(N^3)
```

**数学方法**
我们可以用三个主要原则做得更好:

1.  如果字符串不能进一步缩减，那么字符串中的所有字母都是相同的。
2.  最小字符串的长度是< = 2 或等于原始字符串的长度，或者 2
3.  如果字符串的每个字母出现奇数次，在一个缩减步骤后，它们都将出现偶数次。反之亦然，也就是说，如果字符串的每个字母出现偶数次，则在一个缩减步骤后，它们将出现奇数次。

这些可以证明如下:

1.  如果存在任何两个不同的字母，我们可以选择它们，并进一步缩短字符串长度。
2.  矛盾证明:
    假设我们有一个长度小于原始字符串的缩减字符串。例如“bbbbbbb”。那么这个字符串一定来自于一个字符串，比如' acbbbbbb '，' bbacbbbb '或者任何其他类似的组合。在这种情况下，我们可以选择“bc”而不是“ac”，并进一步减少。
3.  从上面的递归步骤，我们增加一个字母，减少另外两个字母。因此，如果我们有一个组合为(奇数，奇数，奇数)，那么它将变成(奇数+ 1，奇数–1，奇数–1)或(偶数，偶数，偶数)。相反的情况以类似的方式显示。

现在我们可以结合以上原则。
如果字符串由相同的字母重复组成，那么它的最小缩减字符串就是它自己，长度就是字符串的长度。
现在，其他可能的选项是减少一两个字符长度的字符串。现在，如果所有字符出现偶数次或奇数次，唯一可能的答案是 2，因为(0，2，0)是(偶数，偶数，偶数)，而(0，1，0)是(偶数，奇数，偶数)，所以只有 2 保持这种均匀性。
在任何其他条件下，答案都变成 1。

## C++

```
// C++ program to find smallest possible length
// of a string of only three characters
#include<bits/stdc++.h>
using namespace std;

// Returns smallest possible length with given
// operation allowed.
int stringReduction(string str)
{
    int n = str.length();

    // Counint occurrences of three different
    // characters 'a', 'b' and 'c' in str
    int count[3] = {0};
    for (int i=0; i<n; ++i)
        count[str[i]-'a']++;

    // If all characters are same.
    if (count[0] == n || count[1] == n ||
        count[2] == n)
        return n;

    // If all characters are present even number
    // of times or all are present odd number of
    // times.
    if ((count[0] % 2) == (count[1] % 2) &&
        (count[1] % 2) == (count[2] % 2))
        return 2;

    // Answer is 1 for all other cases.
    return 1;
}

// Driver code
int main()
{
    string str = "abcbbaacb";
    cout << stringReduction(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest possible length
// of a string of only three characters
public class GFG {

// Returns smallest possible length with given
// operation allowed.
    static int stringReduction(String str) {
        int n = str.length();

        // Counint occurrences of three different
        // characters 'a', 'b' and 'c' in str
        int count[] = new int[3];
        for (int i = 0; i < n; ++i) {
            count[str.charAt(i) - 'a']++;
        }

        // If all characters are same.
        if (count[0] == n || count[1] == n
                || count[2] == n) {
            return n;
        }

        // If all characters are present even number
        // of times or all are present odd number of
        // times.
        if ((count[0] % 2) == (count[1] % 2)
                && (count[1] % 2) == (count[2] % 2)) {
            return 2;
        }

        // Answer is 1 for all other cases.
        return 1;
    }

// Driver code
    public static void main(String[] args) {
        String str = "abcbbaacb";
        System.out.println(stringReduction(str));
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find smallest possible
# length of a string of only three characters

# Returns smallest possible length
# with given operation allowed.
def stringReduction(str):

    n = len(str)

    # Counint occurrences of three different
    # characters 'a', 'b' and 'c' in str
    count = [0] * 3
    for i in range(n):
        count[ord(str[i]) - ord('a')] += 1

    # If all characters are same.
    if (count[0] == n or count[1] == n or
                         count[2] == n):
        return n

    # If all characters are present even number
    # of times or all are present odd number of
    # times.
    if ((count[0] % 2) == (count[1] % 2) and
        (count[1] % 2) == (count[2] % 2)):
        return 2

    # Answer is 1 for all other cases.
    return 1

# Driver code
if __name__ == "__main__":

    str = "abcbbaacb"
    print(stringReduction(str))

# This code is contributed by ita_c
```

## C#

```
// C# program to find smallest possible length
// of a string of only three characters
using System;
public class GFG {

// Returns smallest possible length with given
// operation allowed.
    static int stringReduction(String str) {
        int n = str.Length;

        // Counint occurrences of three different
        // characters 'a', 'b' and 'c' in str
        int []count = new int[3];
        for (int i = 0; i < n; ++i) {
            count[str[i] - 'a']++;
        }

        // If all characters are same.
        if (count[0] == n || count[1] == n
                || count[2] == n) {
            return n;
        }

        // If all characters are present even number
        // of times or all are present odd number of
        // times.
        if ((count[0] % 2) == (count[1] % 2)
                && (count[1] % 2) == (count[2] % 2)) {
            return 2;
        }

        // Answer is 1 for all other cases.
        return 1;
    }

// Driver code
    public static void Main() {
        String str = "abcbbaacb";
        Console.WriteLine(stringReduction(str));
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest possible length
// of a string of only three characters

// Returns smallest possible length with
// given operation allowed.
function stringReduction($str)
{
    $n = strlen($str);

    // Counint occurrences of three different
    // characters 'a', 'b' and 'c' in str
    $count = array_fill(0, 3, 0);
    for ($i = 0; $i < $n; ++$i)
        $count[ord($str[$i]) - ord('a')]++;

    // If all characters are same.
    if ($count[0] == $n || $count[1] == $n ||
        $count[2] == $n)
        return $n;

    // If all characters are present even number
    // of times or all are present odd number of
    // times.
    if (($count[0] % 2) == ($count[1] % 2) &&
        ($count[1] % 2) == ($count[2] % 2))
        return 2;

    // Answer is 1 for all other cases.
    return 1;
}

// Driver code
$str = "abcbbaacb";
print(stringReduction($str));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find smallest
// possible length of a string of only
// three characters

// Returns smallest possible length
// with given operation allowed.
function stringReduction(str)
{
    var n = str.length;

    // Counvar occurrences of three different
    // characters 'a', 'b' and 'c' in str
    var count = Array.from({length: 3}, (_, i) => 0);
    for(var i = 0; i < n; ++i)
    {
        count[str.charAt(i).charCodeAt(0) -
                        'a'.charCodeAt(0)]++;
    }

    // If all characters are same.
    if (count[0] == n ||
        count[1] == n ||
        count[2] == n)
    {
        return n;
    }

    // If all characters are present even number
    // of times or all are present odd number of
    // times.
    if ((count[0] % 2) == (count[1] % 2) &&
        (count[1] % 2) == (count[2] % 2))
    {
        return 2;
    }

    // Answer is 1 for all other cases.
    return 1;
}

// Driver code
var str = "abcbbaacb";
document.write(stringReduction(str));

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
1
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由 **Aditya Kamath** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。