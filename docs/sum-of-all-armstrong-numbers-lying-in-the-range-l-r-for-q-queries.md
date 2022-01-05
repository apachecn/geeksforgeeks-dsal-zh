# 所有阿姆斯特朗数的总和，范围为 Q 查询的[L，R]

> 原文:[https://www . geeksforgeeks . org/all-sum-Armstrong-numbers-in-range-l-r-for-q-query/](https://www.geeksforgeeks.org/sum-of-all-armstrong-numbers-lying-in-the-range-l-r-for-q-queries/)

给定以 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【】【】**形式的 **Q** 查询，其中每行由两个数字 **L** 和表示范围**【L，R】**的 **R** 组成，任务是找出位于给定范围**【L，R】内的所有[阿姆斯特朗数字](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)的和。**
**例:**

> **输入:** Q = 2，arr = [ [1，13]，[121，211] ]
> **输出:**
> 45
> 153
> **说明:**
> 从 1 到 13，1，2，3，4，5，6，7，8 和 9 是阿姆斯壮数。因此总和是 45。
> 从 121 到 211 只有一个阿姆斯特朗号，即 153。所以总和是 153。
> **输入:** Q = 4，arr = [ [ 10，10 ]，[ 258，785 ]，[45，245]，[ 1，1000]]
> **输出:**
> 0
> 1148
> 153
> 1346

**方法:**
思路是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。直到该特定索引的所有[阿姆斯特朗数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)的总和被预先计算并存储在一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**pref【】**中，使得每个查询都可以在 **O(1)** 时间内被回答。

1.  初始化前缀数组 **pref[]** 。
2.  从 1 到 N 迭代，检查数字是否为阿姆斯特朗:
    *   如果该号码是阿姆斯壮，那么 **pref[]** 的当前索引将存储通过(1 +在 **pref[]** 的先前索引处的号码)计算的迄今为止找到的阿姆斯壮号码的计数。
    *   否则**pref【】**当前指数与**pref【】**前一指数值相同。
3.  对于 **Q** 查询范围**【L，R】**的所有[阿姆斯壮号](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)之和可以计算如下:

```
sum = pref[R] - pref[L - 1]
```

以下是上述方法的实施

## C++

```
// C++ program to find the sum
// of all armstrong  numbers
// in the given range
#include <bits/stdc++.h>
using namespace std;

// pref[] array to precompute
// the sum of all armstrong
// number
int pref[100001] = {0};

// Function that return number
// num if num is armstrong
// else return 0
static int checkArmstrong(int x) {
    int n = to_string(x).size();
    int sum1 = 0;
    int temp = x;
    while (temp > 0) {
        int digit = temp % 10;
        sum1 += pow(digit, n);
        temp /= 10;
    }
    if (sum1 == x)
        return x;
    return 0;
}

// Function to precompute the
// sum of all armstrong numbers
// upto 100000
void preCompute() {
    for (int i = 1; i < 100001; i++) {

         // checkarmstrong ()
        // return the number i
        // if i is armstrong
        // else return 0
        pref[i] = pref[i - 1] + checkArmstrong(i);
    }
}

// Function to print the sum
// for each query
void printSum(int L, int R) {
    cout<<(pref[R] - pref[L - 1])<<endl;

}

// Function to prsum of all
// armstrong numbers between
// [L, R]
void printSumarmstrong(int arr[2][2], int Q) {

    // Function that pre computes
    // the sum of all armstrong
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }

}

int main()
{
    // Queries
        int Q = 2;
        int arr[2][2] = { { 1, 13 }, { 121, 211 } };

        // Function that print the
        // the sum of all armstrong
        // number in Range [L, R]
        printSumarmstrong(arr, Q);

    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum
// of all armstrong  numbers
// in the given range
class GFG {
    // pref[] array to precompute
    // the sum of all armstrong
    // number
    static int[] pref = new int[100001];

    // Function that return number
    // num if num is armstrong
    // else return 0
    static int checkArmstrong(int x) {
        int n = String.valueOf(x).length();
        int sum1 = 0;
        int temp = x;
        while (temp > 0) {
            int digit = temp % 10;
            sum1 += Math.pow(digit, n);
            temp /= 10;
        }
        if (sum1 == x)
            return x;
        return 0;
    }

    // Function to precompute the
    // sum of all armstrong numbers
    // upto 100000
    static void preCompute() {
        for (int i = 1; i < 100001; i++) {
            // checkarmstrong ()
            // return the number i
            // if i is armstrong
            // else return 0
            pref[i] = pref[i - 1] + checkArmstrong(i);
        }
    }

    // Function to print the sum
    // for each query
    static void printSum(int L, int R) {
        System.out.println(pref[R] - pref[L - 1]);

    }

    // Function to prsum of all
    // armstrong numbers between
    // [L, R]
    static void printSumarmstrong(int[][] arr, int Q) {

        // Function that pre computes
        // the sum of all armstrong
        // numbers
        preCompute();

        // Iterate over all Queries
        // to print the sum
        for (int i = 0; i < Q; i++) {
            printSum(arr[i][0], arr[i][1]);
        }

    }

    // Driver code
    public static void main(String[] args) {
        // Queries
        int Q = 2;
        int[][] arr = { { 1, 13 }, { 121, 211 } };

        // Function that print the
        // the sum of all armstrong
        // number in Range [L, R]
        printSumarmstrong(arr, Q);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of all armstrong  numbers
# in the given range

# pref[] array to precompute
# the sum of all armstrong 
# number
pref =[0]*100001

# Function that return number
# num if num is armstrong 
# else return 0
def checkArmstrong(x):
    n = len(str(x))
    sum1 = 0 
    temp = x 
    while temp > 0:
        digit = temp % 10
        sum1 += digit **n
        temp //= 10
    if sum1 == x:
        return x
    return 0

# Function to precompute the
# sum of all armstrong  numbers
# upto 100000
def preCompute():
    for i in range(1, 100001):
        # checkarmstrong ()
        # return the number i
        # if i is armstrong 
        # else return 0
        pref[i] = pref[i - 1]+ checkArmstrong(i)

# Function to print the sum
# for each query
def printSum(L, R):
    print(pref[R] - pref[L - 1])

# Function to prsum of all
# armstrong  numbers between
# [L, R]
def printSumarmstrong (arr, Q):

    # Function that pre computes
    # the sum of all armstrong 
    # numbers
    preCompute()

    # Iterate over all Queries
    # to print the sum
    for i in range(Q):
        printSum(arr[i][0], arr[i][1])

# Driver code

# Queries
Q = 2
arr = [[1, 13 ], [ 121, 211 ]]

# Function that print the
# the sum of all armstrong 
# number in Range [L, R]
printSumarmstrong (arr, Q)
```

## C#

```
// C# program to find the sum
// of all armstrong numbers
// in the given range
using System;

class GFG
{
    // pref[] array to precompute
    // the sum of all armstrong
    // number
    static int[] pref = new int[100001];

    // Function that return number
    // num if num is armstrong
    // else return 0
    static int checkArmstrong(int x) {
        int n = x.ToString().Length;
        int sum1 = 0;
        int temp = x;
        while (temp > 0) {
            int digit = temp % 10;
            sum1 += (int)Math.Pow(digit, n);
            temp /= 10;
        }
        if (sum1 == x)
            return x;
        return 0;
    }

    // Function to precompute the
    // sum of all armstrong numbers
    // upto 100000
    static void preCompute()
    {
        for (int i = 1; i < 100001; i++)
        {

            // checkarmstrong ()
            // return the number i
            // if i is armstrong
            // else return 0
            pref[i] = pref[i - 1] + checkArmstrong(i);
        }
    }

    // Function to print the sum
    // for each query
    static void printSum(int L, int R) {
        Console.WriteLine(pref[R] - pref[L - 1]);

    }

    // Function to prsum of all
    // armstrong numbers between
    // [L, R]
    static void printSumarmstrong(int[,] arr, int Q) {

        // Function that pre computes
        // the sum of all armstrong
        // numbers
        preCompute();

        // Iterate over all Queries
        // to print the sum
        for (int i = 0; i < Q; i++) {
            printSum(arr[i, 0], arr[i, 1]);
        }

    }

    // Driver code
    public static void Main(string[] args)
    {

        // Queries
        int Q = 2;
        int[,] arr = { { 1, 13 }, { 121, 211 } };

        // Function that print the
        // the sum of all armstrong
        // number in Range [L, R]
        printSumarmstrong(arr, Q);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program to find the sum
    // of all armstrong  numbers
    // in the given range

    // pref[] array to precompute
    // the sum of all armstrong
    // number
    let pref = new Array(100001);
    pref.fill(0);

    // Function that return number
    // num if num is armstrong
    // else return 0
    function checkArmstrong(x) {
        let n = (x.toString()).length;
        let sum1 = 0;
        let temp = x;
        while (temp > 0) {
            let digit = temp % 10;
            sum1 += Math.pow(digit, n);
            temp = parseInt(temp / 10, 10);
        }
        if (sum1 == x)
            return x;
        return 0;
    }

    // Function to precompute the
    // sum of all armstrong numbers
    // upto 100000
    function preCompute() {
        for (let i = 1; i < 100001; i++) {
            // checkarmstrong ()
            // return the number i
            // if i is armstrong
            // else return 0
            pref[i] = pref[i - 1] + checkArmstrong(i);
        }
    }

    // Function to print the sum
    // for each query
    function printSum(L, R) {
        document.write((pref[R] - pref[L - 1]) + "</br>");
    }

    // Function to prsum of all
    // armstrong numbers between
    // [L, R]
    function printSumarmstrong(arr, Q) {

        // Function that pre computes
        // the sum of all armstrong
        // numbers
        preCompute();

        // Iterate over all Queries
        // to print the sum
        for (let i = 0; i < Q; i++) {
            printSum(arr[i][0], arr[i][1]);
        }
    }

    // Queries
    let Q = 2;
    let arr = [ [ 1, 13 ], [ 121, 211 ] ];

    // Function that print the
    // the sum of all armstrong
    // number in Range [L, R]
    printSumarmstrong(arr, Q);

    // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
45
153
```

**时间复杂度:** O(N)，其中 N 是查询中最大的元素。

**辅助空间:** O(10 <sup>5</sup> )