# 检查对角线连接的位与是否超过二进制矩阵的中间行/列元素的位与

> 原文:[https://www . geeksforgeeks . org/check-if-bitwise-and-of-concation-of-the-of-of-the-of-the-of-of-of-of-of-of-of-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a](https://www.geeksforgeeks.org/check-if-bitwise-and-of-concatenation-of-diagonals-exceeds-that-of-middle-row-column-elements-of-a-binary-matrix/)

给定尺寸为 **N * N** 的[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)**mat【】【】【】**，任务是检查通过串联主对角线和次对角线元素获得的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)十进制数是否大于通过中间行和列中的元素获得的十进制数的**位与**。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

***注意:**仅从左到右和从上到下连接矩阵元素。如果 **N** 为偶数，则取两者中的第一个中间*行/列*。*

**示例:**

> **输入:** M[][] = {{1，0，1}，{0，0，1}，{0，1，1}}
> **输出:**否
> **说明:**
> 主对角线元素串联形成的数为“101”。
> 交叉对角元素串联形成的数为“001”。
> 中间一行的元素串联形成的数字为“001”。
> 中间一列的元素串联形成的数字为“001”。
> 因此，“101”和“001”的按位“与”与“001”和“001”的按位“与”相同。
> 
> **输入:** M[][] = {{0，1，1}，{0，0，0}，{0，1，1 } }
> T3】输出:是

**天真方法:**解决问题最简单的方法是[遍历给定的矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)并将相应的数字附加到一个变量上，比如说 **P，**如果当前行等于当前列，那么就附加到一个变量上，比如说 **S，**如果行是 **N 列**，那么就附加到一个变量上，比如说 **MR，**如果行等于 **N/2** ，那么就附加到一个变量上，比如说【T0 完成上述步骤后，如果 **P** 和 **S** 的位与大于 **MR** 和 **MC** 的位与，则打印**“是”**。否则，打印**“否”。**

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert obtained binary
// representation to decimal value
int convert(vector<int> p)
{

    // Stores the resultant number
    int ans = 0;

    // Traverse string arr
    for(int i : p)
    {
        ans = (ans << 1) | i;
    }

    // Return the number formed
    return ans;
}

// Function to count the number of
// set bits in the number num
int count(int num)
{

    // Stores the count of set bits
    int ans = 0;

    // Iterate until num > 0
    while (num > 0)
    {
        ans += num & 1;
        num >>= 1;
    }
    return ans;
}

// Function to check if the given matrix
// satisfies the given condition or not
void checkGoodMatrix(vector<vector<int> > mat)
{
    vector<int> P;
    vector<int> S;
    vector<int> MR;
    vector<int> MC;

    // To get P, S, MR, and MC
    for(int i = 0; i < mat.size(); i++)
    {
        for(int j = 0; j < mat[0].size(); j++)
        {
            if (i == j)
                P.push_back(mat[i][j]);

            if (i + j == mat.size() - 1)
                S.push_back(mat[i][j]);

            if (i == floor((mat.size() - 1) / 2))
                MR.push_back(mat[i][j]);

            if (j == floor((mat.size() - 1) / 2))
                MC.push_back(mat[i][j]);
        }
    }
    reverse(S.begin(), S.end());

    // Stores decimal equivalents
    // of binary representations
    int P0 = convert(P);
    int S0 = convert(S);
    int MR0 = convert(MR);
    int MC0 = convert(MC);

    // Gett the number of set bits
    int setBitsPS = count((P0 & S0));
    int setBitsMM = count((MR0 & MC0));

    // Print the answer
    if (setBitsPS > setBitsMM)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    vector<vector<int>> mat = { { 1, 0, 1 },
                                { 0, 0, 1 },
                                { 0, 1, 1 } };

    checkGoodMatrix(mat);
}

// This code is contributed by nirajgusain5
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Collections;

class GFG{

// Function to convert obtained binary
// representation to decimal value
static int convert(ArrayList<Integer> p)
{

    // Stores the resultant number
    int ans = 0;

    // Traverse string arr
    for(int i: p)
    {
        ans = (ans << 1) | i;
    }

    // Return the number formed
    return ans;
}

// Function to count the number of
// set bits in the number num
static int count(int num)
{

    // Stores the count of set bits
    int ans = 0;

    // Iterate until num > 0
    while (num > 0)
    {
        ans += num & 1;
        num >>= 1;
    }
    return ans;
}

// Function to check if the given matrix
// satisfies the given condition or not
static void checkGoodMatrix(int mat[][])
{
    ArrayList<Integer> P = new ArrayList<Integer>();
    ArrayList<Integer> S = new ArrayList<Integer>();
    ArrayList<Integer> MR = new ArrayList<Integer>();
    ArrayList<Integer> MC = new ArrayList<Integer>();

    // To get P, S, MR, and MC
    for(int i = 0; i < mat.length; i++)
    {
        for(int j = 0; j < mat[0].length; j++)
        {
            if (i == j)
                P.add(mat[i][j]);

            if (i + j == mat.length - 1)
                S.add(mat[i][j]);

            if (i == Math.floor((mat.length - 1) / 2))
                MR.add(mat[i][j]);

            if (j == Math.floor((mat.length - 1) / 2))
                MC.add(mat[i][j]);
        }
    }
    Collections.reverse(S);

    // Stores decimal equivalents
    // of binary representations
    int P0 = convert(P);
    int S0 = convert(S);
    int MR0 = convert(MR);
    int MC0 = convert(MC);

    // Gett the number of set bits
    int setBitsPS = count((P0 & S0));
    int setBitsMM = count((MR0 & MC0));

    // Print the answer
    if (setBitsPS > setBitsMM)
       System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
    int mat[][] = { { 1, 0, 1 },
                    { 0, 0, 1 },
                    { 0, 1, 1 } };
    checkGoodMatrix(mat);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Functio to convert obtained binary
# representation to decimal value
def convert(arr):

      # Stores the resultant number
    ans = 0

    # Traverse string arr
    for i in arr:
        ans = (ans << 1) | i

    # Return the number formed
    return ans

# Function to count the number of
# set bits in the number num
def count(num):

    # Stores the count of set bits
    ans = 0

    # Iterate until num > 0
    while num:
        ans += num & 1
        num >>= 1
    return ans

# Function to check if the given matrix
# satisfies the given condition or not
def checkGoodMatrix(mat):
    P = []
    S = []
    MR = []
    MC = []

    # To get P, S, MR, and MC
    for i in range(len(mat)):
        for j in range(len(mat[0])):

            if i == j:
                P.append(mat[i][j])

            if i + j == len(mat)-1:
                S.append(mat[i][j])

            if i == (len(mat)-1)//2:
                MR.append(mat[i][j])

            if j == (len(mat)-1)//2:
                MC.append(mat[i][j])

    S.reverse()

    # Stores decimal equivalents
    # of binary representations
    P = convert(P)
    S = convert(S)
    MR = convert(MR)
    MC = convert(MC)

    # Gett the number of set bits
    setBitsPS = count(P & S)
    setBitsMM = count(MR & MC)

    # Print the answer
    if setBitsPS > setBitsMM:
        print("Yes")
    else:
        print("No")

# Driver Code

# Given Matrix
mat = [[1, 0, 1], [0, 0, 1], [0, 1, 1]]

checkGoodMatrix(mat)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to convert obtained binary
// representation to decimal value
static int convert(List<int> p)
{

    // Stores the resultant number
    int ans = 0;

    // Traverse string arr
    foreach(int i in p)
    {
        ans = (ans << 1) | i;
    }

    // Return the number formed
    return ans;
}

// Function to count the number of
// set bits in the number num
static int count(int num)
{

    // Stores the count of set bits
    int ans = 0;

    // Iterate until num > 0
    while (num > 0)
    {
        ans += num & 1;
        num >>= 1;
    }
    return ans;
}

// Function to check if the given matrix
// satisfies the given condition or not
static void checkGoodMatrix(int[, ] mat)
{
    List<int> P = new List<int>();
    List<int> S = new List<int>();
    List<int> MR = new List<int>();
    List<int> MC = new List<int>();

    // To get P, S, MR, and MC
    for(int i = 0; i < mat.GetLength(0); i++)
    {
        for(int j = 0; j < mat.GetLength(1); j++)
        {
            if (i == j)
                P.Add(mat[i, j]);

            if (i + j == mat.GetLength(0) - 1)
                S.Add(mat[i, j]);

            if (i == Math.Floor(
                (mat.GetLength(0) - 1) / 2.0))
                MR.Add(mat[i, j]);

            if (j == Math.Floor(
                (mat.GetLength(0) - 1) / 2.0))
                MC.Add(mat[i, j]);
        }
    }
    S.Reverse();

    // Stores decimal equivalents
    // of binary representations
    int P0 = convert(P);
    int S0 = convert(S);
    int MR0 = convert(MR);
    int MC0 = convert(MC);

    // Gett the number of set bits
    int setBitsPS = count((P0 & S0));
    int setBitsMM = count((MR0 & MC0));

    // Print the answer
    if (setBitsPS > setBitsMM)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(string[] args)
{
    int[,] mat = { { 1, 0, 1 },
                   { 0, 0, 1 },
                   { 0, 1, 1 } };

    checkGoodMatrix(mat);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to convert obtained binary
// representation to decimal value
function convert(p) {

    // Stores the resultant number
    let ans = 0;

    // Traverse string arr
    for (let i of p) {
        ans = (ans << 1) | i;
    }

    // Return the number formed
    return ans;
}

// Function to count the number of
// set bits in the number num
function count(num) {

    // Stores the count of set bits
    let ans = 0;

    // Iterate until num > 0
    while (num > 0) {
        ans += num & 1;
        num >>= 1;
    }
    return ans;
}

// Function to check if the given matrix
// satisfies the given condition or not
function checkGoodMatrix(mat) {
    let P = [], S = [], MR = [], MC = [];

    // To get P, S, MR, and MC
    for (let i = 0; i < mat.length; i++) {
        for (let j = 0; j < mat[0].length; j++) {
            if (i == j)
                P.push(mat[i][j]);

            if (i + j == mat.length - 1)
                S.push(mat[i][j]);

            if (i == Math.floor((mat.length - 1) / 2))
                MR.push(mat[i][j]);

            if (j == Math.floor((mat.length - 1) / 2))
                MC.push(mat[i][j]);
        }
    }
    S.reverse();

    // Stores decimal equivalents
    // of binary representations
    let P0 = convert(P);
    let S0 = convert(S);
    let MR0 = convert(MR);
    let MC0 = convert(MC);

    // Gett the number of set bits
    let setBitsPS = count((P0 & S0));
    let setBitsMM = count((MR0 & MC0));

    // Print the answer
    if (setBitsPS > setBitsMM)
        document.write("Yes");
    else
        document.write("No");
}

// Driver code

let mat = [[1, 0, 1],
           [0, 0, 1],
           [0, 1, 1]];

checkGoodMatrix(mat);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
No
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**要优化上述方法，可以通过[遍历每个元素的对角线](https://www.geeksforgeeks.org/efficiently-compute-sums-of-diagonals-of-a-matrix/)、中间行和中间列来优化上述方法。按照以下步骤解决问题:

*   初始化辅助[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **P、S、MR、**和 **MC** 分别存储主对角线、交叉对角线、中间行和中间列的连接元素。
*   迭代范围**【0，N-1】**:
    *   将 **(i，i)** 中的元素追加到 **P** 中，即主对角线。
    *   将**(N–1–I，i)** 中的元素追加到 **S** 中，即交叉对角线。
    *   将 **((N-1)/2，i)** 中的元素追加到 **MR** 中，即中排。
    *   将 **((N-1)/2，i)** 中的元素追加到 **MC** 中，即中柱。
*   迭代范围**【0，N-1】**:
    *   检查**P【I】&S【I】>MR【I】&MC【I】**然后打印**“是”**返回。
    *   否则，检查**p【I】&s【I】<MR【I】&MC【I】**，然后打印**“否”**返回。
*   如果以上条件都不满足，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the matrix
// satisfy the given condition or not
void checkGoodMatrix(
    vector<vector<int> > M, int N)
{
    // Stores the binary representation
    vector<int> p, s, MR, MC;

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {

        // Push element of main diagonal
        p.push_back(M[i][i]);

        // Push element of cross diagona
        s.push_back(M[N - 1 - i][i]);

        // Push element of Mid row
        MR.push_back(M[(N - 1) / 2][i]);

        // Push element of Mid column
        MC.push_back(M[i][(N - 1) / 2]);
    }

    // Check if S & P > MR & MC
    for (int i = 0; i < N; i++) {

        if (p[i] & s[i] > MR[i] & MC[i]) {
            cout << "Yes";
            return;
        }
        else if (p[i] & s[i] < MR[i] & MC[i]) {
            cout << "No";
            return;
        }
    }

    cout << "No";
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > M{ { 0, 1, 1 },
                            { 0, 0, 0 },
                            { 0, 1, 1 } };

    // Size of the matrix
    int N = M.size();

    checkGoodMatrix(M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Vector;

class GFG{

static void checkGoodMatrix(int[][] M, int N)
{

    // Stores the binary representation
    Vector<Integer> p = new Vector<Integer>();
    Vector<Integer> s = new Vector<Integer>();
    Vector<Integer> MR = new Vector<Integer>();
    Vector<Integer> MC = new Vector<Integer>();

    // Iterate over the range [0, N]
    for(int i = 0; i < N; i++)
    {

        // Push element of main diagonal
        p.add(M[i][i]);

        // Push element of cross diagona
        s.add(M[N - 1 - i][i]);

        // Push element of Mid row
        MR.add(M[(N - 1) / 2][i]);

        // Push element of Mid column
        MC.add(M[i][(N - 1) / 2]);
    }

    // Check if S & P > MR & MC
    for(int i = 0; i < N; i++)
    {
        int P = p.get(i);
        int S = s.get(i);
        int Mr = MR.get(i);
        int Mc = MC.get(i);

        if ((P & S) > (Mr & Mc))
        {
            System.out.print("Yes");
            return;
        }
        else if ((P & S) < (Mr & Mc))
        {
            System.out.print("No");
            return;
        }
    }
    System.out.print("No");
}

// Driver code
public static void main(String[] args)
{

    // Given matrix
    int[][] M = { { 0, 1, 1 },
                  { 0, 0, 0 },
                  { 0, 1, 1 } };

    // Size of the matrix
    int N = M.length;

    checkGoodMatrix(M, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the matrix
# satisfy the given condition or not
def checkGoodMatrix(M, N):

    # Stores the binary representation
    p = []
    s = []
    MR = []
    MC = []

    # Iterate over the range [0, N]
    for i in range(N):

        # Push element of main diagonal
        p.append(M[i][i])

        # Push element of cross diagona
        s.append(M[N - 1 - i][i])

        # Push element of Mid row
        MR.append(M[(N - 1) // 2][i])

        # Push element of Mid column
        MC.append(M[i][(N - 1) // 2])

    # Check if S & P > MR & MC
    for i in range(N):
        if (p[i] & s[i] > MR[i] & MC[i]):
            print("Yes")
            return
        elif (p[i] & s[i] < MR[i] & MC[i]):
            print("No")
            return

    print("No")

# Driver Code

# Given matrix
M = [ [ 0, 1, 1 ],
      [ 0, 0, 0 ],
      [ 0, 1, 1 ] ] 

# Size of the matrix
N = len(M)

checkGoodMatrix(M, N)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    static void checkGoodMatrix(int[,] M, int N)
    {

        // Stores the binary representation
        List<int> p = new List<int>();
        List<int> s = new List<int>();
        List<int> MR = new List<int>();
        List<int> MC = new List<int>();

        // Iterate over the range [0, N]
        for(int i = 0; i < N; i++)
        {

            // Push element of main diagonal
            p.Add(M[i,i]);

            // Push element of cross diagona
            s.Add(M[N - 1 - i,i]);

            // Push element of Mid row
            MR.Add(M[(N - 1) / 2,i]);

            // Push element of Mid column
            MC.Add(M[i,(N - 1) / 2]);
        }

        // Check if S & P > MR & MC
        for(int i = 0; i < N; i++)
        {
            int P = p[i];
            int S = s[i];
            int Mr = MR[i];
            int Mc = MC[i];

            if ((P & S) > (Mr & Mc))
            {
                Console.WriteLine("Yes");
                return;
            }
            else if ((P & S) < (Mr & Mc))
            {
                Console.WriteLine("No");
                return;
            }
        }
        Console.WriteLine("No");
    }

  static void Main() {
    // Given matrix
    int[,] M = { { 0, 1, 1 },
                  { 0, 0, 0 },
                  { 0, 1, 1 } };

    // Size of the matrix
    int N = 3;

    checkGoodMatrix(M, N);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    function checkGoodMatrix(M, N)
    {

        // Stores the binary representation
        let p = [];
        let s = [];
        let MR = [];
        let MC = [];

        // Iterate over the range [0, N]
        for(let i = 0; i < N; i++)
        {

            // Push element of main diagonal
            p.push(M[i][i]);

            // Push element of cross diagona
            s.push(M[N - 1 - i][i]);

            // Push element of Mid row
            MR.push(M[parseInt((N - 1) / 2, 10)][i]);

            // Push element of Mid column
            MC.push(M[i][parseInt((N - 1) / 2, 10)]);
        }

        // Check if S & P > MR & MC
        for(let i = 0; i < N; i++)
        {
            let P = p[i];
            let S = s[i];
            let Mr = MR[i];
            let Mc = MC[i];

            if ((P & S) > (Mr & Mc))
            {
                document.write("Yes");
                return;
            }
            else if ((P & S) < (Mr & Mc))
            {
                document.write("No");
                return;
            }
        }
        document.write("No");
    }

    // Given matrix
    let M = [ [ 0, 1, 1 ],
               [ 0, 0, 0 ],
               [ 0, 1, 1 ] ];

    // Size of the matrix
    let N = M.length;

    checkGoodMatrix(M, N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)