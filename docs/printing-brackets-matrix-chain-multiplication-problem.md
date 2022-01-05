# 矩阵链乘法题中打印括号

> 原文:[https://www . geesforgeks . org/printing-括号-矩阵-链-乘法-问题/](https://www.geeksforgeeks.org/printing-brackets-matrix-chain-multiplication-problem/)

先决条件:[动态规划|集合 8(矩阵链乘法)](https://www.geeksforgeeks.org/dynamic-programming-set-8-matrix-chain-multiplication/)
给定一个矩阵序列，找到将这些矩阵相乘的最有效方法。问题不在于实际执行乘法，而仅仅在于决定以何种顺序执行乘法。
我们有很多选择来相乘矩阵链，因为矩阵乘法是关联的。换句话说，无论我们如何给产品加上括号，结果都是一样的。例如，如果我们有四个矩阵 A、B、C 和 D，我们会有:

```
(ABC)D = (AB)(CD) = A(BCD) = ....
```

然而，我们给乘积加括号的顺序会影响计算乘积所需的简单算术运算的次数，或者效率。例如，假设 A 是 10 × 30 矩阵，B 是 30 × 5 矩阵，C 是 5 × 60 矩阵。然后，

```
(AB)C = (10×30×5) + (10×5×60) = 1500 + 3000 = 4500 operations
A(BC) = (30×5×60) + (10×30×60) = 9000 + 18000 = 27000 operations.
```

显然，第一个括号需要较少的操作次数。
*给定一个表示矩阵链的数组 p[]，使得矩阵 Ai 的维数为 p[i-1] x p[i]。我们需要编写一个 MatrixChainOrder()函数，该函数应该返回乘法链所需的最小乘法次数。*

```
Input:  p[] = {40, 20, 30, 10, 30} 
Output: Optimal parenthesization is  ((A(BC))D)
 Optimal cost of parenthesization is 26000
There are 4 matrices of dimensions 40x20, 20x30, 
30x10 and 10x30\. Let the input 4 matrices be A, B, 
C and D.  The minimum number of  multiplications are 
obtained by putting parenthesis in following way
(A(BC))D --> 20*30*10 + 40*20*10 + 40*10*30

Input: p[] = {10, 20, 30, 40, 30} 
Output: Optimal parenthesization is (((AB)C)D)
 Optimal cost of parenthesization is 30000
There are 4 matrices of dimensions 10x20, 20x30, 
30x40 and 40x30\. Let the input 4 matrices be A, B, 
C and D.  The minimum number of multiplications are 
obtained by putting parenthesis in following way
((AB)C)D --> 10*20*30 + 10*30*40 + 10*40*30

Input: p[] = {10, 20, 30} 
Output: Optimal parenthesization is (AB)
 Optimal cost of parenthesization is 6000
There are only two matrices of dimensions 10x20 
and 20x30\. So there is only one way to multiply 
the matrices, cost of which is 10*20*30
```

这个问题主要是[之前的帖子](https://www.geeksforgeeks.org/dynamic-programming-set-8-matrix-chain-multiplication/)的延伸。在前一篇文章中，我们只讨论了寻找最优成本的算法。这里我们也需要打印括号。

其思想是将每个子表达式(I，j)的最佳断点存储在 2D 数组括号[n][n]中。一旦我们构造了括号数组，我们就可以使用下面的代码打印括号。

```
// Prints parenthesization in subexpression (i, j)
printParenthesis(i, j, bracket[n][n], name)
{
    // If only one matrix left in current segment
    if (i == j)
    {
        print name;
        name++;
        return;
    }

    print "(";

    // Recursively put brackets around subexpression
    // from i to bracket[i][j].
    printParenthesis(i, bracket[i][j], bracket, name);

    // Recursively put brackets around subexpression
    // from bracket[i][j] + 1 to j.
    printParenthesis(bracket[i][j]+1, j, bracket, name);

    print ")";
}
```

下面是上述步骤的实现。

## C++

```
// C++ program to print optimal parenthesization
// in matrix chain multiplication.
#include <bits/stdc++.h>
using namespace std;

// Function for printing the optimal
// parenthesization of a matrix chain product
void printParenthesis(int i, int j, int n, int* bracket,
                      char& name)
{
    // If only one matrix left in current segment
    if (i == j) {
        cout << name++;
        return;
    }

    cout << "(";

    // Recursively put brackets around subexpression
    // from i to bracket[i][j].
    // Note that "*((bracket+i*n)+j)" is similar to
    // bracket[i][j]
    printParenthesis(i, *((bracket + i * n) + j), n,
                     bracket, name);

    // Recursively put brackets around subexpression
    // from bracket[i][j] + 1 to j.
    printParenthesis(*((bracket + i * n) + j) + 1, j, n,
                     bracket, name);
    cout << ")";
}

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
// Please refer below article for details of this
// function
// https://goo.gl/k6EYKj
void matrixChainOrder(int p[], int n)
{
    /* For simplicity of the program, one extra
       row and one extra column are allocated in
        m[][]. 0th row and 0th column of m[][]
        are not used */
    int m[n][n];

    // bracket[i][j] stores optimal break point in
    // subexpression from i to j.
    int bracket[n][n];

    /* m[i,j] = Minimum number of scalar multiplications
    needed to compute the matrix A[i]A[i+1]...A[j] =
    A[i..j] where dimension of A[i] is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for (int i = 1; i < n; i++)
        m[i][i] = 0;

    // L is chain length.
    for (int L = 2; L < n; L++)
    {
        for (int i = 1; i < n - L + 1; i++)
        {
            int j = i + L - 1;
            m[i][j] = INT_MAX;
            for (int k = i; k <= j - 1; k++)
            {
                // q = cost/scalar multiplications
                int q = m[i][k] + m[k + 1][j]
                        + p[i - 1] * p[k] * p[j];
                if (q < m[i][j])
                {
                    m[i][j] = q;

                    // Each entry bracket[i,j]=k shows
                    // where to split the product arr
                    // i,i+1....j for the minimum cost.
                    bracket[i][j] = k;
                }
            }
        }
    }

    // The first matrix is printed as 'A', next as 'B',
    // and so on
    char name = 'A';

    cout << "Optimal Parenthesization is : ";
    printParenthesis(1, n - 1, n, (int*)bracket, name);
    cout << "nOptimal Cost is : " << m[1][n - 1];
}

// Driver code
int main()
{
    int arr[] = { 40, 20, 30, 10, 30 };
    int n = sizeof(arr) / sizeof(arr[0]);
    matrixChainOrder(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print optimal parenthesization
// in matrix chain multiplication.
class GFG
{
  static char name;

  // Function for printing the optimal
  // parenthesization of a matrix chain product
  static void printParenthesis(int i, int j,
                               int n, int[][] bracket)
  {

    // If only one matrix left in current segment
    if (i == j)
    {
      System.out.print(name++);
      return;
    }
    System.out.print("(");

    // Recursively put brackets around subexpression
    // from i to bracket[i][j].
    // Note that "*((bracket+i*n)+j)" is similar to
    // bracket[i][j]
    printParenthesis(i, bracket[i][j], n, bracket);

    // Recursively put brackets around subexpression
    // from bracket[i][j] + 1 to j.
    printParenthesis(bracket[i][j] + 1, j, n, bracket);
    System.out.print(")");
  }

  // Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
  // Please refer below article for details of this
  // function
  // https://goo.gl/k6EYKj
  static void matrixChainOrder(int p[], int n)
  {
    /*
         * For simplicity of the program,
         one extra row and one extra column are
         * allocated in m[][]. 0th row and
         0th column of m[][] are not used
         */
    int[][] m = new int[n][n];

    // bracket[i][j] stores optimal break point in
    // subexpression from i to j.
    int[][] bracket = new int[n][n];

    /*
         * m[i,j] = Minimum number of scalar
         multiplications needed to compute the
         * matrix A[i]A[i+1]...A[j] = A[i..j] where
         dimension of A[i] is p[i-1] x p[i]
         */

    // cost is zero when multiplying one matrix.
    for (int i = 1; i < n; i++)
      m[i][i] = 0;

    // L is chain length.
    for (int L = 2; L < n; L++)
    {
      for (int i = 1; i < n - L + 1; i++)
      {
        int j = i + L - 1;
        m[i][j] = Integer.MAX_VALUE;
        for (int k = i; k <= j - 1; k++)
        {

          // q = cost/scalar multiplications
          int q = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
          if (q < m[i][j])
          {
            m[i][j] = q;

            // Each entry bracket[i,j]=k shows
            // where to split the product arr
            // i,i+1....j for the minimum cost.
            bracket[i][j] = k;
          }
        }
      }
    }

    // The first matrix is printed as 'A', next as 'B',
    // and so on
    name = 'A';
    System.out.print("Optimal Parenthesization is : ");
    printParenthesis(1, n - 1, n, bracket);
    System.out.print("\nOptimal Cost is : " + m[1][n - 1]);
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 40, 20, 30, 10, 30 };
    int n = arr.length;
    matrixChainOrder(arr, n);
  }
}

// This code is contributed by sanjeev2552
```

## C#

```
// C# program to print optimal parenthesization
// in matrix chain multiplication.
using System;

class GFG{

static char name;

// Function for printing the optimal
// parenthesization of a matrix chain product
static void printParenthesis(int i, int j,
                             int n, int[,] bracket)
{

    // If only one matrix left in current segment
    if (i == j)
    {
        Console.Write(name++);
        return;
    }
    Console.Write("(");

    // Recursively put brackets around subexpression
    // from i to bracket[i,j].
    // Note that "*((bracket+i*n)+j)" is similar to
    // bracket[i,j]
    printParenthesis(i, bracket[i, j], n, bracket);

    // Recursively put brackets around subexpression
    // from bracket[i,j] + 1 to j.
    printParenthesis(bracket[i, j] + 1, j, n, bracket);
    Console.Write(")");
}

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
// Please refer below article for details of this
// function
// https://goo.gl/k6EYKj
static void matrixChainOrder(int []p, int n)
{

    /*
    * For simplicity of the program,
    one extra row and one extra column are
    * allocated in m[,]. 0th row and
    0th column of m[,] are not used
    */
    int[,] m = new int[n, n];

    // bracket[i,j] stores optimal break point in
    // subexpression from i to j.
    int[,] bracket = new int[n, n];

    /*
    * m[i,j] = Minimum number of scalar
    multiplications needed to compute the
    * matrix A[i]A[i+1]...A[j] = A[i..j] where
    dimension of A[i] is p[i-1] x p[i]
    */

    // cost is zero when multiplying one matrix.
    for(int i = 1; i < n; i++)
        m[i, i] = 0;

    // L is chain length.
    for(int L = 2; L < n; L++)
    {
        for(int i = 1; i < n - L + 1; i++)
        {
            int j = i + L - 1;
            m[i, j] = int.MaxValue;
            for (int k = i; k <= j - 1; k++)
            {

                // q = cost/scalar multiplications
                int q = m[i, k] + m[k + 1, j] +
                       p[i - 1] * p[k] * p[j];

                if (q < m[i, j])
                {
                    m[i, j] = q;

                    // Each entry bracket[i,j]=k shows
                    // where to split the product arr
                    // i,i+1....j for the minimum cost.
                    bracket[i, j] = k;
                }
            }
        }
    }

    // The first matrix is printed as 'A', next as 'B',
    // and so on
    name = 'A';
    Console.Write("Optimal Parenthesization is : ");
    printParenthesis(1, n - 1, n, bracket);
    Console.Write("\nOptimal Cost is : " + m[1, n - 1]);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 40, 20, 30, 10, 30 };
    int n = arr.Length;

    matrixChainOrder(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to print optimal parenthesization
// in matrix chain multiplication.

  var name=0;

  // Function for printing the optimal
  // parenthesization of a matrix chain product
  function printParenthesis(i , j, n, bracket)
  {

    // If only one matrix left in current segment
    if (i == j)
    {
      document.write(name++);
      return;
    }
    document.write("(");

    // Recursively put brackets around subexpression
    // from i to bracket[i][j].
    // Note that "*((bracket+i*n)+j)" is similar to
    // bracket[i][j]
    printParenthesis(i, bracket[i][j], n, bracket);

    // Recursively put brackets around subexpression
    // from bracket[i][j] + 1 to j.
    printParenthesis(bracket[i][j] + 1, j, n, bracket);
    document.write(")");
  }

  // Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
  // Please refer below article for details of this
  // function
  // https://goo.gl/k6EYKj
  function matrixChainOrder( p , n)
  {
    /*
         * For simplicity of the program,
         one extra row and one extra column are
         * allocated in m. 0th row and
         0th column of m are not used
         */
    var m = Array(n).fill(0).map(x => Array(n).fill(0));

    // bracket[i][j] stores optimal break point in
    // subexpression from i to j.
    var bracket = Array(n).fill(0).map(x => Array(n).fill(0));

    /*
         * m[i,j] = Minimum number of scalar
         multiplications needed to compute the
         * matrix A[i]A[i+1]...A[j] = A[i..j] where
         dimension of A[i] is p[i-1] x p[i]
         */

    // cost is zero when multiplying one matrix.
    for (var i = 1; i < n; i++)
      m[i][i] = 0;

    // L is chain length.
    for (var L = 2; L < n; L++)
    {
      for (var i = 1; i < n - L + 1; i++)
      {
        var j = i + L - 1;
        m[i][j] = Number.MAX_VALUE;
        for (var k = i; k <= j - 1; k++)
        {

          // q = cost/scalar multiplications
          var q = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
          if (q < m[i][j])
          {
            m[i][j] = q;

            // Each entry bracket[i,j]=k shows
            // where to split the product arr
            // i,i+1....j for the minimum cost.
            bracket[i][j] = k;
          }
        }
      }
    }

    // The first matrix is printed as 'A', next as 'B',
    // and so on
    name = 'A';
    document.write("Optimal Parenthesization is : ");
    printParenthesis(1, n - 1, n, bracket);
    document.write("\nOptimal Cost is : " + m[1][n - 1]);
  }

  // Driver code
  var arr = [ 40, 20, 30, 10, 30 ];
  var n = arr.length;
  matrixChainOrder(arr, n);

// This code is contributed by 29AjayKumar
</script>
```

**Output**

```
Optimal Parenthesization is : ((A(BC))D)nOptimal Cost is : 26000
```

**时间复杂度:**O(n<sup>3</sup>)
T5】辅助空间: O(n <sup>2</sup>

**另一种方法:**

——————————————

这个解决方案试图使用置换递归来解决这个问题。

```
Let's take example:  {40, 20, 30, 10, 30}
n = 5
```

让我们把它分成一个矩阵

```
[ [40, 20], [20, 30], [30, 10], [10, 30] ]

[ A , B , C , D ]

it contains 4 matrices i.e. (n - 1)
```

我们有 3 个组合要相乘，即(n-2)

```
AB    or    BC    or     CD
```

### <u>算法:</u>

1)给定长度为 M 的矩阵阵列，循环通过 M–1 次

2)合并每个循环中的连续矩阵

```
for (int i = 0; i < M - 1; i++) {
   int cost =  (matrices[i][0] * 
                 matrices[i][1] * matrices[i+1][1]);

   // STEP - 3
   // STEP - 4
}
```

3)将当前的两个矩阵合并为一个，并从列表中删除合并的矩阵列表。

```
If  A, B merged, then A, B must be removed from the List

and NEW matrix list will be like
newMatrices = [  AB,  C ,  D ]

We have now 3 matrices, in any loop
Loop#1:  [ AB,  C,   D ]
Loop#2:  [ A,   BC,  D ]
Loop#3   [ A,   B,   CD ]
```

4)重复:以**新矩阵**作为输入 M-递归进入步骤 1

5)当我们得到列表中的 2 个矩阵时，停止递归。

### <u>工作流程</u>

矩阵按以下方式缩减:

在递归过程中，必须保留成本，并将其与每个父步骤的先前值相加。

```
[ A, B , C, D ]

[(AB), C, D ]
 [ ((AB)C), D ]--> [ (((AB)C)D) ] 
 - return & sum-up total cost of this step.
 [ (AB),  (CD)] --> [ ((AB)(CD)) ] 
 - return .. ditto..

 [ A, (BC), D ]
 [ (A(BC)), D ]--> [ ((A(BC))D) ] 
  - return
 [ A, ((BC)D) ]--> [ (A((BC)D)) ] 
  - return

 [ A, B, (CD) ]
 [ A, (B(CD)) ]--> [ (A(B(CD))) ] 
  - return
 [ (AB), (CD) ]--> [ ((AB)(CD)) ] 
  - return .. ditto..
```

返回时，即每次递归的最后一步，检查该值是否小于任何其他值。

下面是上述步骤的 JAVA 实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

public class MatrixMultiplyCost {

    static class FinalCost
    {
        public String label = "";
        public int cost = Integer.MAX_VALUE;
    }

    private void optimalCost(int[][] matrices,
                             String[] labels, int prevCost,
                             FinalCost finalCost)
    {
        int len = matrices.length;

        if (len < 2)
        {
            finalCost.cost = 0;
            return;
        }
        else if (len == 2)
        {
            int cost = prevCost
                       + (matrices[0][0] *
                          matrices[0][1] *
                          matrices[1][1]);

            // This is where minimal cost has been caught
            // for whole program
            if (cost < finalCost.cost)
            {
                finalCost.cost = cost;
                finalCost.label
                    = "(" + labels[0]
                    + labels[1] + ")";
            }
            return;
        }

        // recursive Reduce
        for (int i = 0; i < len - 1; i++)
        {
            int j;
            int[][] newMatrix = new int[len - 1][2];
            String[] newLabels = new String[len - 1];
            int subIndex = 0;

            // STEP-1:
            //   - Merge two matrices's into one - in each
            //   loop, you move merge position
            //        - if i = 0 THEN  (AB) C D ...
            //        - if i = 1 THEN  A (BC) D ...
            //        - if i = 2 THEN  A B (CD) ...
            //   - and find the cost of this two matrices
            //   multiplication
            int cost = (matrices[i][0] * matrices[i][1]
                        * matrices[i + 1][1]);

            // STEP - 2:
            //    - Build new matrices after merge
            //    - Keep track of the merged labels too
            for (j = 0; j < i; j++) {
                newMatrix[subIndex] = matrices[j];
                newLabels[subIndex++] = labels[j];
            }

            newMatrix[subIndex][0] = matrices[i][0];
            newMatrix[subIndex][1] = matrices[i + 1][1];
            newLabels[subIndex++]
                = "(" + labels[i] + labels[i + 1] + ")";

            for (j = i + 2; j < len; j++) {
                newMatrix[subIndex] = matrices[j];
                newLabels[subIndex++] = labels[j];
            }

            optimalCost(newMatrix, newLabels,
                        prevCost + cost, finalCost);
        }
    }

    public FinalCost findOptionalCost(int[] arr)
    {
        // STEP -1 : Prepare and convert inout as Matrix
        int[][] matrices = new int[arr.length - 1][2];
        String[] labels = new String[arr.length - 1];

        for (int i = 0; i < arr.length - 1; i++) {
            matrices[i][0] = arr[i];
            matrices[i][1] = arr[i + 1];
            labels[i] = Character.toString((char)(65 + i));
        }
        printMatrix(matrices);

        FinalCost finalCost = new FinalCost();
        optimalCost(matrices, labels, 0, finalCost);

        return finalCost;
    }

    /**
     * Driver Code
     */
    public static void main(String[] args)
    {
        MatrixMultiplyCost calc = new MatrixMultiplyCost();

        // ======= *** TEST CASES **** ============

        int[] arr = { 40, 20, 30, 10, 30 };
        FinalCost cost = calc.findOptionalCost(arr);
        System.out.println("Final labels: \n" + cost.label);
        System.out.println("Final Cost:\n" + cost.cost
                           + "\n");
    }

    /**
     * Ignore this method
     * - THIS IS for DISPLAY purpose only
     */
    private static void printMatrix(int[][] matrices)
    {
        System.out.print("matrices = \n[");
        for (int[] row : matrices) {
            System.out.print(Arrays.toString(row) + " ");
        }
        System.out.println("]");
    }
}

// This code is contributed by suvera
```

**Output**

```
matrices = 
[[40, 20] [20, 30] [30, 10] [10, 30] ]
Final labels: 
((A(BC))D)
Final Cost:
26000
```

本文由**亚辛·扎法尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。