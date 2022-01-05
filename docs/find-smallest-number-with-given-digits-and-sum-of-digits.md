# 找到给定位数和位数总和的最小数

> 原文:[https://www . geesforgeks . org/find-给定位数和位数之和的最小数/](https://www.geeksforgeeks.org/find-smallest-number-with-given-digits-and-sum-of-digits/)

给定两个正整数 **P** 和 **Q** ，求只包含数字 **P** 和 **Q** 的最小整数，使得[的整数数字之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)为 **N** 。

**示例:**

> **输入:** N = 11，P = 4，Q = 7
> **输出:** 47
> **说明:**有两个可能的整数可以由 4 和 7 组成，它们的和是 11，即 47 和 74。因为我们需要找到最小可能值，所以 47 是必需的答案。
> 
> **输入:** N = 11，P = 9，Q = 7
> **输出:**不可能
> **解释:**不可能用数字 7 和 9 创建一个整数，使它们的和为 11。

**有效方法:**我们来考虑一下 **P** 大于等于 **Q** ， **count_P** 表示 **P** 的[出现次数](https://www.geeksforgeeks.org/count-the-number-of-occurrences-of-a-particular-digit-in-a-number/)， **count_Q** 表示结果整数中 **Q** 的[出现次数](https://www.geeksforgeeks.org/count-the-number-of-occurrences-of-a-particular-digit-in-a-number/)。所以，这个问题可以用一个方程的形式来表示(**P * count _ P)+(Q * count _ Q)= N**，并且为了使结果整数**中的位数最小化，count_P + count_Q** 应该尽可能的小。可以观察到，由于**P****>=****Q**，满足(**P * count _ P)+(Q * count _ Q)= N**的 **count_P** 最大可能值将是最优选择。以下是上述方法的步骤:

1.  初始化 **count_P** 和 **count_Q** 为 0。
2.  如果 **N** 被 **P** 整除， **count_P = N/P** 和 **N=0** 。
3.  如果 **N** 不能被 **P** 整除，则从 **N** 中减去 **Q** ，并将 **count_Q** 增加 1。
4.  重复步骤 2 和 3，直到 **N** 大于 0。
5.  如果 **N！= 0** ，不可能生成满足要求条件的整数。否则得到的整数将是*计数 Q 乘以 Q* ，然后是*计数 P 乘以 P*

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the minimum
// integer having only digits P and
// Q and the sum of digits as N
void printMinInteger(int P, int Q, int N)
{
    // If Q is greater that P then
    // swap the values of P and Q
    if (Q > P) {
        swap(P, Q);
    }

    // If P and Q are both zero or
    // if Q is zero and N is not
    // divisible by P then there
    // is no possible integer which
    // satisfies the given conditions
    if (Q == 0 && (P == 0 || N % P != 0)) {
        cout << "Not Possible";
        return;
    }

    int count_P = 0, count_Q = 0;

    // Loop to find the maximum value
    // of count_P that also satisfy
    // P*count_P + Q*count_Q = N
    while (N > 0) {
        if (N % P == 0) {
            count_P += N / P;
            N = 0;
        }
        else {
            N = N - Q;
            count_Q++;
        }
    }

    // If N is 0, their is a valid
    // integer possible that satisfies
    // all the requires conditions
    if (N == 0) {

        // Print Answer
        for (int i = 0; i < count_Q; i++)
            cout << Q;
        for (int i = 0; i < count_P; i++)
            cout << P;
    }
    else {
        cout << "Not Possible";
    }
}

// Driver Code
int main()
{
    int N = 32;
    int P = 7;
    int Q = 4;

    // Function Call
    printMinInteger(P, Q, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to print the minimum
// integer having only digits P and
// Q and the sum of digits as N
static void printMinInteger(int P, int Q, int N)
{

    // If Q is greater that P then
    // swap the values of P and Q
    if (Q > P) {
        int temp;
        temp = P;
        P = Q;
        Q = temp;
    }

    // If P and Q are both zero or
    // if Q is zero and N is not
    // divisible by P then there
    // is no possible integer which
    // satisfies the given conditions
    if (Q == 0 && (P == 0 || N % P != 0)) {
        System.out.println("Not Possible");
        return;
    }

    int count_P = 0, count_Q = 0;

    // Loop to find the maximum value
    // of count_P that also satisfy
    // P*count_P + Q*count_Q = N
    while (N > 0) {
        if (N % P == 0) {
            count_P += N / P;
            N = 0;
        }
        else {
            N = N - Q;
            count_Q++;
        }
    }

    // If N is 0, their is a valid
    // integer possible that satisfies
    // all the requires conditions
    if (N == 0) {

        // Print Answer
        for (int i = 0; i < count_Q; i++)
            System.out.print(Q);
        for (int i = 0; i < count_P; i++)
            System.out.print(P);
    }
    else {
        System.out.println("Not Possible");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 32;
    int P = 7;
    int Q = 4;

    // Function Call
    printMinInteger(P, Q, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print minimum
# integer having only digits P and
# Q and the sum of digits as N
def printMinInteger(P, Q, N):

    # If Q is greater that P then
    # swap the values of P and Q
    if (Q > P):
        t = P
        P = Q
        Q = t

    # If P and Q are both zero or
    # if Q is zero and N is not
    # divisible by P then there
    # is no possible integer which
    # satisfies the given conditions
    if (Q == 0 and (P == 0 or N % P != 0)):
        print("Not Possible")
        return

    count_P = 0
    count_Q = 0

    # Loop to find the maximum value
    # of count_P that also satisfy
    # P*count_P + Q*count_Q = N
    while (N > 0):
        if (N % P == 0):
            count_P += N / P
            N = 0
        else:
            N = N - Q
            count_Q += 1

    # If N is 0, their is a valid
    # integer possible that satisfies
    # all the requires conditions
    if (N == 0):

        # Print Answer
        for i in range(count_Q):
            print(Q, end = "")
        for i in range(int(count_P)):
            print(P, end = "")
    else:
        print("Not Possible")

# Driver Code
N = 32
P = 7
Q = 4

# Function Call
printMinInteger(P, Q, N)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

// Function to print the minimum
// integer having only digits P and
// Q and the sum of digits as N
static void printMinint(int P, int Q, int N)
{

    // If Q is greater that P then
    // swap the values of P and Q
    if (Q > P) {
        int temp;
        temp = P;
        P = Q;
        Q = temp;
    }

    // If P and Q are both zero or
    // if Q is zero and N is not
    // divisible by P then there
    // is no possible integer which
    // satisfies the given conditions
    if (Q == 0 && (P == 0 || N % P != 0)) {
        Console.WriteLine("Not Possible");
        return;
    }

    int count_P = 0, count_Q = 0;

    // Loop to find the maximum value
    // of count_P that also satisfy
    // P*count_P + Q*count_Q = N
    while (N > 0) {
        if (N % P == 0) {
            count_P += N / P;
            N = 0;
        }
        else {
            N = N - Q;
            count_Q++;
        }
    }

    // If N is 0, their is a valid
    // integer possible that satisfies
    // all the requires conditions
    if (N == 0) {

        // Print Answer
        for (int i = 0; i < count_Q; i++)
            Console.Write(Q);
        for (int i = 0; i < count_P; i++)
            Console.Write(P);
    }
    else {
        Console.WriteLine("Not Possible");
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 32;
    int P = 7;
    int Q = 4;

    // Function Call
    printMinint(P, Q, N);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript Program of the above approach

// Function to print the minimum
// integer having only digits P and
// Q and the sum of digits as N
function printMinInteger(P, Q, N) {
  // If Q is greater that P then
  // swap the values of P and Q
  if (Q > P) {
    swap(P, Q);
  }

  // If P and Q are both zero or
  // if Q is zero and N is not
  // divisible by P then there
  // is no possible integer which
  // satisfies the given conditions
  if (Q == 0 && (P == 0 || N % P != 0)) {
    document.write("Not Possible");
    return;
  }

  let count_P = 0,
    count_Q = 0;

  // Loop to find the maximum value
  // of count_P that also satisfy
  // P*count_P + Q*count_Q = N
  while (N > 0) {
    if (N % P == 0) {
      count_P += Math.floor(N / P);
      N = 0;
    } else {
      N = N - Q;
      count_Q++;
    }
  }

  // If N is 0, their is a valid
  // integer possible that satisfies
  // all the requires conditions
  if (N == 0) {
    // Print Answer
    for (let i = 0; i < count_Q; i++) document.write(Q);
    for (let i = 0; i < count_P; i++) document.write(P);
  } else {
    document.write("Not Possible");
  }
}

// Driver Code
let N = 32;
let P = 7;
let Q = 4;

// Function Call
printMinInteger(P, Q, N);

// This code is contributed by gfgking.
</script>
```

**Output**

```
47777
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(1)*