# 将字符串划分为两个平衡子序列的方法数量

> 原文:[https://www . geeksforgeeks . org/将字符串分割成两个平衡子序列的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-partition-a-string-into-two-balanced-subsequences/)

给定由开括号和闭括号组成的字符串“S”，任务是找出将“S”的每个字符分配给字符串“X”或字符串“Y”(两者最初都是空的)的方法数量，以便 X 和 Y 形成的字符串是平衡的。可以假设‘S’本身是平衡的。
**例:**

```
Input: S = "(())"
Output: 6
Valid assignments are :
X = "(())" and Y = "" [All characters in X]
X = "" and Y = "(())" [Nothing in X]
X = "()" and Y = "()" [1st and 3rd characters in X]
X = "()" and Y = "()" [2nd and 3rd characters in X]
X = "()" and Y = "()" [2nd and 4th characters in X]
X = "()" and Y = "()" [1st and 4th characters in X]

Input: S = "()()"
Output: 4
X = "()()", Y = ""
X = "()", Y = "()"  [1st and 2nd in X]
X = "()", Y = ""  [1st and 4th in X]
X = "", Y = "()()"
```

**一个简单的方法:**我们可以生成各种可能的字符分配方式，并检查所形成的字符串是否平衡。有 2 个 <sup>n</sup> 赋值，有效或无效，需要 O(n)时间检查形成的字符串是否平衡。因此，该方法的时间复杂度为 0(n * 2<sup>n</sup>)。
**一种有效的方法(动态规划):**我们可以使用动态规划以更有效的方式解决这个问题。我们可以使用三个变量来描述赋值的当前状态:要赋值的字符的索引 I，以及到该状态为止由 X 和 Y 构成的字符串。将整个字符串传递给函数调用会导致很高的内存需求，所以我们可以用计数变量 c <sub>x</sub> 和 c <sub>y</sub> 来代替。我们将为每个左括号增加计数变量，为每个右括号减少计数变量。这种方法的时间和空间复杂度为 O(n <sup>3</sup> )。
以下是上述方法的实施:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// For maximum length of input string
const int MAX = 10;

// Declaring the DP table
int F[MAX][MAX][MAX];

// Function to calculate the
// number of valid assignments
int noOfAssignments(string& S, int& n, int i,
                    int c_x, int c_y)
{
    if (F[i][c_x][c_y] != -1)
        return F[i][c_x][c_y];

    if (i == n) {

        // Return 1 if both
        // subsequences are balanced
        F[i][c_x][c_y] = !c_x && !c_y;
        return F[i][c_x][c_y];
    }

    // Increment the count
    // if it an opening bracket
    if (S[i] == '(') {
        F[i][c_x][c_y]
            = noOfAssignments(S, n, i + 1,
                              c_x + 1, c_y)
              + noOfAssignments(S, n, i + 1,
                                c_x, c_y + 1);
        return F[i][c_x][c_y];
    }

    F[i][c_x][c_y] = 0;

    // Decrement the count
    // if it a closing bracket
    if (c_x)
        F[i][c_x][c_y]
            += noOfAssignments(S, n, i + 1,
                               c_x - 1, c_y);

    if (c_y)
        F[i][c_x][c_y]
            += noOfAssignments(S, n, i + 1,
                               c_x, c_y - 1);

    return F[i][c_x][c_y];
}

// Driver code
int main()
{
    string S = "(())";
    int n = S.length();

    // Initializing the DP table
    memset(F, -1, sizeof(F));

    // Initial value for c_x
    // and c_y is zero
    cout << noOfAssignments(S, n, 0, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // For maximum length of input string
    static int MAX = 10;

    // Declaring the DP table
    static int[][][] F = new int[MAX][MAX][MAX];

    // Function to calculate the
    // number of valid assignments
    static int noOfAssignments(String s, int n,
                               int i, int c_x, int c_y)
    {
        if (F[i][c_x][c_y] != -1)
            return F[i][c_x][c_y];
        if (i == n)
        {

            // Return 1 if both
            // subsequences are balanced
            F[i][c_x][c_y] = (c_x == 0 &&
                              c_y == 0) ? 1 : 0;
            return F[i][c_x][c_y];
        }

        // Increment the count
        // if it an opening bracket
        if (s.charAt(i) == '(')
        {
            F[i][c_x][c_y] = noOfAssignments(s, n, i + 1,
                                             c_x + 1, c_y) +
                             noOfAssignments(s, n, i + 1,
                                             c_x, c_y + 1);
            return F[i][c_x][c_y];
        }

        F[i][c_x][c_y] = 0;

        // Decrement the count
        // if it a closing bracket
        if (c_x != 0)
            F[i][c_x][c_y] += noOfAssignments(s, n, i + 1,
                                              c_x - 1, c_y);

        if (c_y != 0)
            F[i][c_x][c_y] += noOfAssignments(s, n, i + 1,
                                              c_x, c_y - 1);

        return F[i][c_x][c_y];
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "(())";
        int n = s.length();

        // Initializing the DP table
        for (int i = 0; i < MAX; i++)
            for (int j = 0; j < MAX; j++)
                for (int k = 0; k < MAX; k++)
                    F[i][j][k] = -1;

        // Initial value for c_x
        // and c_y is zero
        System.out.println(noOfAssignments(s, n, 0, 0, 0));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# For maximum length of input string
MAX = 10

# Declaring the DP table
F = [[[-1 for i in range(MAX)]
          for j in range(MAX)]
          for k in range(MAX)]

# Function to calculate the number
# of valid assignments
def noOfAssignments(S, n, i, c_x, c_y):

    if F[i][c_x][c_y] != -1:
        return F[i][c_x][c_y]

    if i == n:

        # Return 1 if both subsequences are balanced
        F[i][c_x][c_y] = not c_x and not c_y
        return F[i][c_x][c_y]

    # Increment the count if
    # it is an opening bracket
    if S[i] == '(':
        F[i][c_x][c_y] = \
            noOfAssignments(S, n, i + 1, c_x + 1, c_y) + \
            noOfAssignments(S, n, i + 1, c_x, c_y + 1)

        return F[i][c_x][c_y]

    F[i][c_x][c_y] = 0

    # Decrement the count
    # if it a closing bracket
    if c_x:
        F[i][c_x][c_y] += \
            noOfAssignments(S, n, i + 1, c_x - 1, c_y)

    if c_y:
        F[i][c_x][c_y] += \
            noOfAssignments(S, n, i + 1, c_x, c_y - 1)

    return F[i][c_x][c_y]

# Driver code
if __name__ == "__main__":

    S = "(())"
    n = len(S)

    # Initial value for c_x and c_y is zero
    print(noOfAssignments(S, n, 0, 0, 0))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // For maximum length of input string
    static int MAX = 10;

    // Declaring the DP table
    static int[,,] F = new int[MAX, MAX, MAX];

    // Function to calculate the
    // number of valid assignments
    static int noOfAssignments(String s, int n,
                         int i, int c_x, int c_y)
    {
        if (F[i, c_x, c_y] != -1)
            return F[i, c_x, c_y];

        if (i == n)
        {

            // Return 1 if both
            // subsequences are balanced
            F[i, c_x, c_y] = (c_x == 0 &&
                              c_y == 0) ? 1 : 0;
            return F[i, c_x, c_y];
        }

        // Increment the count
        // if it an opening bracket
        if (s[i] == '(')
        {
            F[i, c_x, c_y] = noOfAssignments(s, n, i + 1,
                                             c_x + 1, c_y) +
                             noOfAssignments(s, n, i + 1,
                                             c_x, c_y + 1);
            return F[i, c_x, c_y];
        }

        F[i, c_x, c_y] = 0;

        // Decrement the count
        // if it a closing bracket
        if (c_x != 0)
            F[i, c_x, c_y] += noOfAssignments(s, n, i + 1,
                                              c_x - 1, c_y);

        if (c_y != 0)
            F[i, c_x, c_y] += noOfAssignments(s, n, i + 1,
                                              c_x, c_y - 1);

        return F[i, c_x, c_y];
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "(())";
        int n = s.Length;

        // Initializing the DP table
        for (int i = 0; i < MAX; i++)
            for (int j = 0; j < MAX; j++)
                for (int k = 0; k < MAX; k++)
                    F[i, j, k] = -1;

        // Initial value for c_x
        // and c_y is zero
        Console.WriteLine(noOfAssignments(s, n, 0, 0, 0));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // For maximum length of input string
    let MAX = 10;

    // Declaring the DP table
    let F = new Array(MAX);
    for(let i = 0; i < MAX; i++)
    {
        F[i] = new Array(MAX);
        for(let j = 0; j < MAX; j++)
        {
            F[i][j] = new Array(MAX);
            for(let k = 0; k < MAX; k++)
            {
                F[i][j][k] = -1;
            }
        }
    }

    // Function to calculate the
    // number of valid assignments
    function noOfAssignments(s,n,i,c_x,c_y)
    {
        if (F[i][c_x][c_y] != -1)
            return F[i][c_x][c_y];
        if (i == n)
        {

            // Return 1 if both
            // subsequences are balanced
            F[i][c_x][c_y] = (c_x == 0 &&
                              c_y == 0) ? 1 : 0;
            return F[i][c_x][c_y];
        }

        // Increment the count
        // if it an opening bracket
        if (s.charAt(i) == '(')
        {
            F[i][c_x][c_y] = noOfAssignments(s, n, i + 1,
                                             c_x + 1, c_y) +
                             noOfAssignments(s, n, i + 1,
                                             c_x, c_y + 1);
            return F[i][c_x][c_y];
        }

        F[i][c_x][c_y] = 0;

        // Decrement the count
        // if it a closing bracket
        if (c_x != 0)
            F[i][c_x][c_y] += noOfAssignments(s, n, i + 1,
                                              c_x - 1, c_y);

        if (c_y != 0)
            F[i][c_x][c_y] += noOfAssignments(s, n, i + 1,
                                              c_x, c_y - 1);

        return F[i][c_x][c_y];
    }

    // Driver Code
    let  s = "(())";
    let n = s.length;

    // Initial value for c_x
    // and c_y is zero
    document.write(noOfAssignments(s, n, 0, 0, 0));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
6
```

**优化的动态规划方法:**我们可以创建一个前缀数组来存储子串 S[0 : i + 1]的计数变量 c <sub>i</sub> 。我们可以观察到，c_x 和 c_y 的总和将始终等于整个字符串的计数变量。通过利用这一特性，我们可以将动态编程方法简化为两种状态。可以线性复杂度创建前缀数组，因此这种方法的时间和空间复杂度为 O(n <sup>2</sup> )。

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// For maximum length of input string
const int MAX = 10;

// Declaring the DP table
int F[MAX][MAX];

// Declaring the prefix array
int C[MAX];

// Function to calculate the
// number of valid assignments
int noOfAssignments(string& S, int& n,
                    int i, int c_x)
{
    if (F[i][c_x] != -1)
        return F[i][c_x];

    if (i == n) {

        // Return 1 if X is
        // balanced.
        F[i][c_x] = !c_x;
        return F[i][c_x];
    }

    int c_y = C[i] - c_x;

    // Increment the count
    // if it an opening bracket
    if (S[i] == '(') {
        F[i][c_x]
            = noOfAssignments(S, n, i + 1,
                              c_x + 1)
              + noOfAssignments(S, n,
                                i + 1, c_x);
        return F[i][c_x];
    }

    F[i][c_x] = 0;

    // Decrement the count
    // if it a closing bracket
    if (c_x)
        F[i][c_x]
            += noOfAssignments(S, n,
                               i + 1, c_x - 1);

    if (c_y)
        F[i][c_x]
            += noOfAssignments(S, n,
                               i + 1, c_x);

    return F[i][c_x];
}

// Driver code
int main()
{
    string S = "()";
    int n = S.length();

    // Initializing the DP table
    memset(F, -1, sizeof(F));

    C[0] = 0;

    // Creating the prefix array
    for (int i = 0; i < n; ++i)
        if (S[i] == '(')
            C[i + 1] = C[i] + 1;
        else
            C[i + 1] = C[i] - 1;

    // Initial value for c_x
    // and c_y is zero
    cout << noOfAssignments(S, n, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

public class GFG {

// For maximum length of input string
    static int MAX = 10;

// Declaring the DP table
    static int F[][] = new int[MAX][MAX];

// Declaring the prefix array
    static int C[] = new int[MAX];

// Function to calculate the
// number of valid assignments
    static int noOfAssignments(String S, int n, int i, int c_x) {
        if (F[i][c_x] != -1) {
            return F[i][c_x];
        }

        if (i == n) {

            // Return 1 if X is
            // balanced.
            if (c_x == 1) {
                F[i][c_x] = 0;
            } else {
                F[i][c_x] = 1;
            }

            return F[i][c_x];
        }

        int c_y = C[i] - c_x;

        // Increment the count
        // if it an opening bracket
        if (S.charAt(i) == '(') {
            F[i][c_x]
                    = noOfAssignments(S, n, i + 1,
                            c_x + 1)
                    + noOfAssignments(S, n,
                            i + 1, c_x);
            return F[i][c_x];
        }

        F[i][c_x] = 0;

        // Decrement the count
        // if it a closing bracket
        if (c_x == 1) {
            F[i][c_x]
                    += noOfAssignments(S, n,
                            i + 1, c_x - 1);
        }

        if (c_y == 1) {
            F[i][c_x]
                    += noOfAssignments(S, n,
                            i + 1, c_x);
        }

        return F[i][c_x];
    }

// Driver code
    public static void main(String[] args) {
        String S = "()";
        int n = S.length();

        // Initializing the DP table
        for (int i = 0; i < MAX; i++) {
            for (int j = 0; j < MAX; j++) {
                F[i][j] = -1;
            }
        }

        C[0] = 0;

        // Creating the prefix array
        for (int i = 0; i < n; ++i) {
            if (S.charAt(i) == '(') {
                C[i + 1] = C[i] + 1;
            } else {
                C[i + 1] = C[i] - 1;
            }
        }

        // Initial value for c_x
        // and c_y is zero
        System.out.println(noOfAssignments(S, n, 0, 0));

    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# For maximum length of input string
MAX = 10

# Declaring the DP table
F = [[-1 for i in range(MAX)]
         for j in range(MAX)]

# Declaring the prefix array
C = [None] * MAX

# Function to calculate the
# number of valid assignments
def noOfAssignments(S, n, i, c_x):

    if F[i][c_x] != -1:
        return F[i][c_x]

    if i == n:

        # Return 1 if X is balanced.
        F[i][c_x] = not c_x
        return F[i][c_x]

    c_y = C[i] - c_x

    # Increment the count
    # if it is an opening bracket
    if S[i] == '(':
        F[i][c_x] = \
            noOfAssignments(S, n, i + 1, c_x + 1) + \
            noOfAssignments(S, n, i + 1, c_x)

        return F[i][c_x]

    F[i][c_x] = 0

    # Decrement the count if it is a closing bracket
    if c_x:
        F[i][c_x] += \
            noOfAssignments(S, n, i + 1, c_x - 1)

    if c_y:
        F[i][c_x] += \
            noOfAssignments(S, n, i + 1, c_x)

    return F[i][c_x]

# Driver code
if __name__ == "__main__":

    S = "()"
    n = len(S)

    C[0] = 0

    # Creating the prefix array
    for i in range(0, n):
        if S[i] == '(':
            C[i + 1] = C[i] + 1
        else:
            C[i + 1] = C[i] - 1

    # Initial value for c_x and c_y is zero
    print(noOfAssignments(S, n, 0, 0))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach

using System;
public class GFG {

// For maximum length of input string
    static int MAX = 10;

// Declaring the DP table
    static int[,] F = new int[MAX,MAX];

// Declaring the prefix array
    static int[] C = new int[MAX];

// Function to calculate the
// number of valid assignments
    static int noOfAssignments(string S, int n, int i, int c_x) {
        if (F[i,c_x] != -1) {
            return F[i,c_x];
        }

        if (i == n) {

            // Return 1 if X is
            // balanced.
            if (c_x == 1) {
                F[i,c_x] = 0;
            } else {
                F[i,c_x] = 1;
            }

            return F[i,c_x];
        }

        int c_y = C[i] - c_x;

        // Increment the count
        // if it an opening bracket
        if (S[i] == '(') {
            F[i,c_x]
                    = noOfAssignments(S, n, i + 1,
                            c_x + 1)
                    + noOfAssignments(S, n,
                            i + 1, c_x);
            return F[i,c_x];
        }

        F[i,c_x] = 0;

        // Decrement the count
        // if it a closing bracket
        if (c_x == 1) {
            F[i,c_x]
                    += noOfAssignments(S, n,
                            i + 1, c_x - 1);
        }

        if (c_y == 1) {
            F[i,c_x]
                    += noOfAssignments(S, n,
                            i + 1, c_x);
        }

        return F[i,c_x];
    }

// Driver code
    public static void Main() {
        string S = "()";
        int n = S.Length;

        // Initializing the DP table
        for (int i = 0; i < MAX; i++) {
            for (int j = 0; j < MAX; j++) {
                F[i,j] = -1;
            }
        }

        C[0] = 0;

        // Creating the prefix array
        for (int i = 0; i < n; ++i) {
            if (S[i] == '(') {
                C[i + 1] = C[i] + 1;
            } else {
                C[i + 1] = C[i] - 1;
            }
        }

        // Initial value for c_x
        // and c_y is zero
        Console.WriteLine(noOfAssignments(S, n, 0, 0));

    }
}
// This code is contributed by Ita_c.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// For maximum length of input string
var MAX = 10;

// Declaring the DP table
var F = Array.from(Array(MAX), ()=>Array(MAX).fill(0));

// Declaring the prefix array
var C = Array(MAX).fill(0);

// Function to calculate the
// number of valid assignments
function noOfAssignments(S, n, i, c_x) {
        if (F[i][c_x] != -1) {
            return F[i][c_x];
        }

        if (i == n) {

            // Return 1 if X is
            // balanced.
            if (c_x == 1) {
                F[i][c_x] = 0;
            } else {
                F[i][c_x] = 1;
            }

            return F[i][c_x];
        }

        var c_y = C[i] - c_x;

        // Increment the count
        // if it an opening bracket
        if (S[i] == '(') {
            F[i][c_x]
                    = noOfAssignments(S, n, i + 1,
                            c_x + 1)
                    + noOfAssignments(S, n,
                            i + 1, c_x);
            return F[i][c_x];
        }

        F[i][c_x] = 0;

        // Decrement the count
        // if it a closing bracket
        if (c_x == 1) {
            F[i][c_x]
                    += noOfAssignments(S, n,
                            i + 1, c_x - 1);
        }

        if (c_y == 1) {
            F[i][c_x]
                    += noOfAssignments(S, n,
                            i + 1, c_x);
        }

        return F[i][c_x];
    }

// Driver code
var S = "()";
var n = S.length;

// Initializing the DP table
for(var i = 0; i < MAX; i++) {
    for(var j = 0; j < MAX; j++) {
        F[i][j] = -1;
    }
}

C[0] = 0;

// Creating the prefix array
for (var i = 0; i < n; ++i) {
    if (S[i] == '(') {
        C[i + 1] = C[i] + 1;
    } else {
        C[i + 1] = C[i] - 1;
    }
}

// Initial value for c_x
// and c_y is zero
document.write(noOfAssignments(S, n, 0, 0) + "<br>");

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2
```