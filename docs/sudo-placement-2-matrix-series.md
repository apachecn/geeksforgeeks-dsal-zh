# Sudo 放置 2 |矩阵系列

> 原文:[https://www . geesforgeks . org/sudo-placement-2-matrix-series/](https://www.geeksforgeeks.org/sudo-placement-2-matrix-series/)

矩阵系列的定义如下:

> **M，M <sup>T</sup> ，M(M <sup>T</sup> ，M(M <sup>T</sup> ) <sup>2</sup> ，M<sup>2</sup>(M<sup>T</sup>)<sup>3</sup>，M<sup>3</sup>(M<sup>T</sup>)<sup>5</sup>，M <sup>5</sup> (M <sup>T【。。。。。。。</sup>**，
> 
> 其中 M 是大小为 K×K 的二进制方阵(二进制矩阵是一种特殊类型的矩阵，其中矩阵的每个元素要么是 0 要么是 1)，而**M<sup>T</sup>T3】代表矩阵 M 的**转置****

给定 **N** 和 **K** ，找到该系列的第 N <sup>个</sup>术语。

**先决条件:** [模幂运算](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)

示例:

```
Input : N = 2, K = 4
        M = {
               {1, 1},
               {0, 1}
            }
Output : [ 3 1]
         [ 2 1]
Explanation:
The 4th term of the series is M2(MT)3 and the value of M<sup>2</sup>(M<sup>T</sup>)<sup>3</sup>  
is {{3, 1}, {2, 1}}.

Input : N = 2, K = 5
        M = {
              {1, 1},
              {0, 1}
        }
Output : [7 2]
         [3 1]
Explanation:
The 4th term of the series is M<sup>3</sup>(M<sup>T</sup>)<sup>5</sup> and the value of M<sup>3</sup>(M<sup>T</sup>)<sup>5</sup> 
is {{7, 2}, {3, 1}}.

```

**进场:**
可以观察到 **M <sup>T</sup>** 的幂是 0，1，1，2，3，5，8…..对于 1 <sup>st</sup> 、2 <sup>nd</sup> 、3 <sup>rd</sup> …..分别术语。这种 M <sup>T</sup> 幂的模式只不过是斐波那契数列。

除了第一项，可以看到 **M** 的幂也是一样的模式，但是，这里 M 的幂和上一项的 M <sup>T</sup> 的幂是一样的。
既然在 K <sup>第</sup>项 M <sup>T</sup> 有 fib <sub>K</sub> 的力量，M 就有 fib<sub>K–1</sub>的力量。
其中 fib <sub>i</sub> 代表第 i <sup>个</sup>斐波那契数。

因此，对于序列的第 K <sup>个</sup>项(对于 K ≠ 1)可以计算为:

```
Sk = Mfib(k - 1)(MT) fib(K) 
```

随着斐波那契值的快速增加，第 45 个斐波那契数接近 10 个 to 10 个 T3。所以第 K <sup>次</sup>次幂不能通过矩阵 K 次的重复乘法来计算。为了做到这一点，我们可以使用类似于模幂运算的思想来有效地计算矩阵的第 K <sup>次</sup>次幂。

和模幂运算一样，幂在每一步都被 2 除，这里我们也遵循同样的分治策略，除了这里我们不乘法数字，相反，这里需要矩阵乘法，这可以在 O(N <sup>3</sup> 中完成，其中 N 是方阵的大小。

下面的程序说明了上述方法:

```
// CPP code to find Kth term of the Matrix Series
#include <bits/stdc++.h>

#define ll long long
#define mod 1000000007

using namespace std;

// This function multiplies two matrices A and B, under modulo mod
// and returns the resultant matrix after multiplication
vector<vector<int> > multiply(vector<vector<int> > A,
                              vector<vector<int> > B)
{

    // n is the size of the matrix
    int n = A.size();

    // Resultant matrix formded after multiplying matrix A and B
    vector<vector<int> > result(n, vector<int>(n, 0));

    // Matrix Multiplication
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            for (int k = 0; k < n; k++) {
                result[i][j] = (result[i][j] + (A[i][k] * B[k][j]) % mod) % mod;
            }
        }
    }

    return result;
}

// Function to find the Kth power of matrix A of size nXn in O(logK)
// similar to Modular Exponentiation
vector<vector<int> > fastpower(vector<vector<int> > A, int n, ll K)
{
    // Base Case
    if (K == 1)
        return A;

    // Recursive Case1: If power is Odd
    if (K & 1) {
        // power(A, K) = power(A, K/2) * power(A, K/2) * A
        // when K is odd, Note than in this implementation
        // multiply (power(A, K - 1) * A) as in the case
        // the power becomes even in the next recursive call
        return multiply(A, fastpower(A, n, K - 1));
    }

    // power(A, K) = power(A, K/2) * power(A, K/2) if K is even
    vector<vector<int> > result = fastpower(A, n, K / 2);
    return multiply(result, result);
}

// Returns the transpose of the matrix A
vector<vector<int> > transpose(vector<vector<int> > A)
{
    int N = A.size();
    vector<vector<int> > transposeMatrix(N, vector<int>(N, 0));

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            transposeMatrix[i][j] = A[j][i];
        }
    }

    return transposeMatrix;
}

// Prints the matrix A
void printMatrix(vector<vector<int> > A)
{
    int n = A.size();

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << A[i][j] << " ";
        }
        cout << endl;
    }
}

// Return the Kth term of the series where matrix M
// is a boolean matrix of size n X n
void getKthTerm(vector<vector<int> > M, int n, int K)
{

    // precompue fibonacci till the Kth term
    ll fibonacci[K + 1];

    // ith fibonacci number denotes the power of M' in
    // the ith term, M' represents the transpose of M
    // 1st term has power of M' as 0 thus fib[0] = 1
    fibonacci[1] = 0ll;
    fibonacci[2] = 1ll;
    for (int i = 3; i <= K; i++) {
        fibonacci[i] = fibonacci[i - 1] + fibonacci[i - 2];
    }

    // stores the transpose of Matrix M
    vector<vector<int> > transposeM = transpose(M);

    // K = 1 and K = 2, is handled separately
    if (K == 1) {
        printMatrix(M);
    }
    else if (K == 2) {
        printMatrix(transposeM);
    }

    else {
        vector<vector<int> > MpowerFibKminusOne;
        MpowerFibKminusOne = fastpower(M, n, fibonacci[K - 1]);

        vector<vector<int> > MTransposePowerFibK;
        MTransposePowerFibK = fastpower(transposeM, n, fibonacci[K]);

        // kthTerm = (M^fib[K - 1]) * (transposeM ^ fib[K])
        vector<vector<int> > kthTerm = multiply(MpowerFibKminusOne,
                                                MTransposePowerFibK);

        // Print the Resultant Matrix
        printMatrix(kthTerm);
    }
}

// Driver Code
int main()
{

    int n, K;
    n = 2;
    K = 4;
    vector<vector<int> > M{ { 1, 1 }, { 0, 1 } };
    getKthTerm(M, n, K);

    // prints the 5th term
    K = 5;
    getKthTerm(M, n, K);

    return 0;
}

```

**输出:**

```
3 1 
2 1 
7 2 
3 1 

```