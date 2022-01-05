# 通过交换两个字符减少汉明距离

> 原文:[https://www.geeksforgeeks.org/reduce-hamming-distance/](https://www.geeksforgeeks.org/reduce-hamming-distance/)

给定两个字符串 S 和 T。找到要在 S 中交换的两个字母的位置，使字符串 S 和 T 之间的汉明距离尽可能小。
[**汉明距离**](https://www.geeksforgeeks.org/hamming-distance-two-strings/) **:** 相同长度的两个字符串 S 和 T 之间的汉明距离，定义为 S 和 T 具有不同字符的位置数量
**示例:**

```
Input : S = "permanent", T = "pergament"
Output: 4 6

Input : S = "double" T = "bundle"
Output : 4 1
```

**解释 1:** 最初，S 和 T 之间的汉明距离是 2(在 4 和 6 处)。在位置 4 和 6 交换字母后，它变成了“pernament”。这里，海明距离只有 1。这是最起码的可能。
**说明 2:** 对换前:“双”“捆”，距离= 4
对换后:“布德”“捆”，距离= 2

**进场:**
在给定的字符串中，汉明距离最多可以减少两个，因为，只能移动两个字符。
**案例一:**如果两个字符串中有两个位置的两个字母相同，但顺序不同(如“捆”和“双”)。
**情况-二:**减少一是可以通过“固定”在错误位置的字符(比如在“永久”和“pergament”中，这里 n 和 m 站错对，还有不匹配的 m，我们可以固定)。
**情况-三:**如果不可能减小汉明距离，打印-1。
**实现:**
Case-I:要将距离减少 2，创建一个二维数组 dp[i][j](i 为 s[]–‘a’，j 为 t[]–‘a’)并赋给字符串 s 中 I 的索引，如果找到重复的对，打印相应的索引。
情况-二:要将距离减少一，维持两个阵列 A[]和 B[]

## C++

```
// C++ code to decrease
// hamming distance using swap.
#include <bits/stdc++.h>
using namespace std;

#define MAX 26

// Function to return the
// swapped indexes to get
// minimum hamming distance.
void Swap(string s, string t, int n)
{
    int dp[MAX][MAX];
    memset(dp, -1, sizeof dp);

    // Find the initial hamming
    // distance
    int tot = 0;
    for (int i = 0; i < n; i++)
        if (s[i] != t[i])
            tot++;

    // Case-I: To decrease distance
    // by two
    for (int i = 0; i < n; i++) {

        // ASCII values of present
        // character.
        int a = s[i] - 'a';
        int b = t[i] - 'a';

        if (a == b)
            continue;

        // If two same letters appear
        // in different positions
        // print their indexes
        if (dp[a][b] != -1) {
            cout << i + 1 << " "
                << dp[a][b] + 1 << endl;
            return;
        }

        // Store the index of
        // letters which is
        // in wrong position
        dp[b][a] = i;
    }

    // Case:II
    int A[MAX], B[MAX];
    memset(A, -1, sizeof A);
    memset(B, -1, sizeof B);

    for (int i = 0; i < n; i++) {
        int a = s[i] - 'a';
        int b = t[i] - 'a';
        if (a == b)
            continue;

        // If misplaced letter
        // is found, print its
        // original index and
        // its new index
        if (A[b] != -1) {
            cout << i + 1 << " " <<
                  A[b] + 1 << endl;
            return;
        }

        if (B[a] != -1) {
            cout << i + 1 << " " <<
                  B[a] + 1 << endl;
            return;
        }

        // Store the index of
        // letters in wrong position
        A[a] = i;
        B[b] = i;
    }

    // Case-III
    cout << -1 << endl;
}

// Driver code
int main()
{
    string S = "permanent";
    string T = "pergament";
    int n = S.length();

    if (S == "" || T == "")
        cout << "Required string is empty.";
    else
        Swap(S, T, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to decrease
// hamming distance using swap.
import java.util.Arrays;

class GFG
{

static final int MAX = 26;

// Function to return the
// swapped indexes to get
// minimum hamming distance.
static void Swap(String s, String t, int n)
{
    int dp[][] = new int[MAX][MAX];
    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            dp[i][j]=-1;
        }
    }

    // Find the initial hamming
    // distance
    int tot = 0;
    for (int i = 0; i < n; i++)
        if (s.charAt(i) != t.charAt(i))
            tot++;

    // Case-I: To decrease distance
    // by two
    for (int i = 0; i < n; i++)
    {

        // ASCII values of present
        // character.
        int a = s.charAt(i)- 'a';
        int b = t.charAt(i) - 'a';

        if (a == b)
            continue;

        // If two same letters appear
        // in different positions
        // print their indexes
        if (dp[a][b] != -1)
        {
            System.out.println(i + 1 + " " +
                            (dp[a][b] + 1));
            return;
        }

        // Store the index of
        // letters which is
        // in wrong position
        dp[b][a] = i;
    }

    // Case:II
    int A[] = new int[MAX], B[] = new int[MAX];
    Arrays.fill(A, -1);
    Arrays.fill(B, -1);

    for (int i = 0; i < n; i++)
    {
        int a = s.charAt(i)- 'a';
        int b = t.charAt(i) - 'a';
        if (a == b)
            continue;

        // If misplaced letter
        // is found, print its
        // original index and
        // its new index
        if (A[b] != -1)
        {
            System.out.println(i + 1 + " " +
                                (A[b] + 1));
            return;
        }

        if (B[a] != -1)
        {
            System.out.println(i + 1 + " " +
                                 (B[a] + 1));
            return;
        }

        // Store the index of
        // letters in wrong position
        A[a] = i;
        B[b] = i;
    }

    // Case-III
    System.out.println(-1);
}

// Driver code
public static void main(String[] args)
{
    String S = "permanent";
    String T = "pergament";
    int n = S.length();

    if (S == "" || T == "")
        System.out.println("Required string is empty.");
    else
        Swap(S, T, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 code to decrease
# hamming distance using swap.
MAX = 26

# Function to return the swapped indexes
# to get minimum hamming distance.
def Swap(s, t, n):

    dp = [[-1 for x in range(MAX)]
              for y in range(MAX)]

    # Find the initial hamming
    # distance
    tot = 0;
    for i in range(n):
        if (s[i] != t[i]):
            tot += 1

    # Case-I: To decrease distance
    # by two
    for i in range(n) :

        # ASCII values of present
        # character.
        a = ord(s[i]) - ord('a')
        b = ord(t[i]) - ord('a')

        if (a == b):
            continue

        # If two same letters appear
        # in different positions
        # print their indexes
        if (dp[a][b] != -1) :
            print(i + 1," ", dp[a][b] + 1)
            return

        # Store the index of
        # letters which is
        # in wrong position
        dp[b][a] = i

    # Case:II
    A = [-1] * MAX
    B = [-1] * MAX

    for i in range(n) :
        a = ord(s[i]) - ord('a')
        b = ord(t[i]) - ord('a')
        if (a == b):
            continue

        # If misplaced letter is found,
        # print its original index and
        # its new index
        if (A[b] != -1) :
            print( i + 1, A[b] + 1)
            return

        if (B[a] != -1) :
            print( i + 1, B[a] + 1)
            return

        # Store the index of
        # letters in wrong position
        A[a] = i
        B[b] = i

    # Case-III
    print( "-1" )

# Driver code
if __name__ == "__main__":
    S = "permanent"
    T = "pergament"
    n = len(S)

    if (S == "" or T == ""):
        print("Required string is empty.")
    else:
        Swap(S, T, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to decrease
// hamming distance using swap.
using System;

class GFG
{

static readonly int MAX = 26;

    // Function to return the
    // swapped indexes to get
    // minimum hamming distance.
    static void Swap(string s, string t, int n)
    {
        int [,]dp = new int[MAX, MAX];
        for(int i = 0; i < MAX; i++)
        {
            for(int j = 0; j < MAX; j++)
            {
                dp[i, j]=-1;
            }
        }

        // Find the initial hamming
        // distance
        int tot = 0;
        for (int i = 0; i < n; i++)
            if (s[i] != t[i])
                tot++;

        // Case-I: To decrease distance
        // by two
        for (int i = 0; i < n; i++)
        {

            // ASCII values of present
            // character.
            int a = s[i] - 'a';
            int b = t[i] - 'a';

            if (a == b)
                continue;

            // If two same letters appear
            // in different positions
            // print their indexes
            if (dp[a,b] != -1)
            {
                Console.WriteLine(i + 1 + " " +
                                (dp[a, b] + 1));
                return;
            }

            // Store the index of
            // letters which is
            // in wrong position
            dp[b,a] = i;
        }

        // Case:II
        int []A = new int[MAX]; int []B = new int[MAX];
        for (int i = 0; i < MAX; i++)
        {
            A[i]=-1;
            B[i]=-1;
        }

        for (int i = 0; i < n; i++)
        {
            int a = s[i] - 'a';
            int b = t[i] - 'a';
            if (a == b)
                continue;

            // If misplaced letter
            // is found, print its
            // original index and
            // its new index
            if (A[b] != -1)
            {
                Console.WriteLine(i + 1 + " " +
                                    (A[b] + 1));
                return;
            }

            if (B[a] != -1)
            {
                Console.WriteLine(i + 1 + " " +
                                    (B[a] + 1));
                return;
            }

            // Store the index of
            // letters in wrong position
            A[a] = i;
            B[b] = i;
        }

        // Case-III
        Console.WriteLine(-1);
    }

    // Driver code
    public static int Main()
    {
        string S = "permanent";
        string T = "pergament";
        int n = S.Length;

        if (S == "" || T == "")
            Console.WriteLine("Required string is empty.");
        else
            Swap(S, T, n);

        return 0;
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript code to decrease
// hamming distance using swap.

    let MAX = 26;

// Function to return the
// swapped indexes to get
// minimum hamming distance. 
function Swap(s,t,n)
{
       let dp=new Array(MAX);
    for(let i = 0; i < MAX; i++)
    {
        dp[i]=new Array(MAX);
        for(let j = 0; j < MAX; j++)
        {
            dp[i][j]=-1;
        }
    }
    // Find the initial hamming
    // distance
    let tot = 0;
    for (let i = 0; i < n; i++)
        if (s[i] != t[i])
            tot++;

    // Case-I: To decrease distance
    // by two
    for (let i = 0; i < n; i++)
    {

        // ASCII values of present
        // character.
        let a = s[i].charCodeAt(0)- 'a'.charCodeAt(0);
        let b = t[i].charCodeAt(0) - 'a'.charCodeAt(0);

        if (a == b)
            continue;

        // If two same letters appear
        // in different positions
        // print their indexes
        if (dp[a][b] != -1)
        {
            document.write(i + 1 + " " +
                            (dp[a][b] + 1)+"<br>");
            return;
        }

        // Store the index of
        // letters which is
        // in wrong position
        dp[b][a] = i;
    }

    // Case:II
    let A = new Array(MAX), B = new Array(MAX);
    for(let i=0;i<MAX;i++)
    {
        A[i]=-1;
        B[i]=-1;
    }

    for (let i = 0; i < n; i++)
    {
        let a = s[i].charCodeAt(0)- 'a'.charCodeAt(0);
        let b = t[i].charCodeAt(0) - 'a'.charCodeAt(0);
        if (a == b)
            continue;

        // If misplaced letter
        // is found, print its
        // original index and
        // its new index
        if (A[b] != -1)
        {
            document.write(i + 1 + " " +
                                (A[b] + 1)+"<br>");
            return;
        }

        if (B[a] != -1)
        {
            document.write(i + 1 + " " +
                                 (B[a] + 1)+"<br>");
            return;
        }

        // Store the index of
        // letters in wrong position
        A[a] = i;
        B[b] = i;
    }

    // Case-III
    document.write(-1);
}

// Driver code
let S = "permanent";
let T = "pergament";
let n = S.length;
if (S == "" || T == "")
    document.write("Required string is empty.");
else
    Swap(S, T, n);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
6 4
```