# 给定范围内偶数和奇数位置的数字之和之间存在斐波那契差的数字

> 原文:[https://www . geeksforgeeks . org/numbers-with-a-Fibonacci-给定范围内偶数和奇数位置的数字总和之差/](https://www.geeksforgeeks.org/numbers-with-a-fibonacci-difference-between-sum-of-digits-at-even-and-odd-positions-in-a-given-range/)

**先决条件:** [数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)

给定一个范围**【L，R】**，任务是将这个范围内的数字计数为斐波那契数，该数字具有偶数位置的数字总和和奇数位置的数字总和之间的差值。

**注:**将数字中最低有效位的位置视为奇数位置。

**示例:**

> **输入:** L = 1，R = 10
> **输出:** 1
> **说明:**
> 唯一满足给定条件的数字是 10。
> 
> **输入:** L = 50，R = 100
> T3】输出: 27

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念来解决这个问题。[数字 dp](https://www.geeksforgeeks.org/digit-dp-introduction/) 的概念用于形成 [DP 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)。

*   形成一个四维表，在每次[递归调用](https://www.geeksforgeeks.org/recursion/)时，我们需要检查所需的差值是否为[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
*   由于该范围内的最大数是 10 <sup>18</sup> ，所以偶数或奇数位置的最大和最大为 9 乘以 9，因此为最大差。因此，我们只需要在基本条件下检查最多 100 的斐波那契数。
*   要检查该数字是否为斐波那契数，请生成所有斐波那契数，并创建一个[哈希](https://www.geeksforgeeks.org/hashing-set-1-introduction/)集。

下表列出了差压状态:

*   因为我们可以把我们的数字看作一个数字序列，一个状态是我们当前所处的**位置**。如果我们处理的数字高达 10 <sup>18</sup> ，则该位置的值可以从 0 到 18。在每次递归调用中，我们试图通过放置一个从 0 到 9 的数字从左到右构建序列。
*   第一个状态是我们到目前为止在**甚至**位置的数字的**和**。
*   第二种状态是到目前为止我们已经放置的奇数**位置的数字的**和**。**
*   另一个状态是布尔变量**紧密**，它告诉我们试图构建的数字已经变得比 R 小，因此在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放在 r 中当前位置的最大位数限制

以下是上述方法的实现:

## C++

```
// C++ program to count the numbers in
// the range having the difference
// between the sum of digits at even
// and odd positions as a Fibonacci Number

#include <bits/stdc++.h>
using namespace std;

const int M = 18;
int a, b, dp[M][90][90][2];

// To store all the
// Fibonacci numbers
set<int> fib;

// Function to generate Fibonacci
// numbers upto 100
void fibonacci()
{
    // Adding the first two Fibonacci
    // numbers in the set
    int prev = 0, curr = 1;
    fib.insert(prev);
    fib.insert(curr);

    // Computing the remaining Fibonacci
    // numbers using the first two
    // Fibonacci numbers
    while (curr <= 100) {
        int temp = curr + prev;
        fib.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to return the count of
// required numbers from 0 to num
int count(int pos, int even,
          int odd, int tight,
          vector<int> num)
{
    // Base Case
    if (pos == num.size()) {
        if (num.size() & 1)
            swap(odd, even);
        int d = even - odd;

        // Check if the difference is equal
        // to any fibonacci number
        if (fib.find(d) != fib.end())
            return 1;

        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][even][odd][tight] != -1)
        return dp[pos][even][odd][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight ? 9 : num[pos]);

    for (int d = 0; d <= limit; d++) {
        int currF = tight, currEven = even;
        int currOdd = odd;

        if (d < num[pos])
            currF = 1;

        // If the current position is odd
        // add it to currOdd, otherwise to
        // currEven
        if (pos & 1)
            currOdd += d;
        else
            currEven += d;

        ans += count(pos + 1,
                     currEven, currOdd,
                     currF, num);
    }

    return dp[pos][even][odd][tight]
           = ans;
}

// Function to convert x
// into its digit vector
// and uses count() function
// to return the required count
int solve(int x)
{
    vector<int> num;

    while (x) {
        num.push_back(x % 10);
        x /= 10;
    }

    reverse(num.begin(), num.end());

    // Initialize dp
    memset(dp, -1, sizeof(dp));
    return count(0, 0, 0, 0, num);
}

// Driver Code
int main()
{
    // Generate fibonacci numbers
    fibonacci();

    int L = 1, R = 50;
    cout << solve(R) - solve(L - 1)
         << endl;

    L = 50, R = 100;
    cout << solve(R) - solve(L - 1)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the numbers in
// the range having the difference
// between the sum of digits at even
// and odd positions as a Fibonacci Number
import java.util.*;

class GFG{

static int M = 18;
static int a, b;
static int [][][][]dp = new int[M][90][90][2];

// To store all the
// Fibonacci numbers
static HashSet<Integer> fib = new HashSet<Integer>();

// Function to generate Fibonacci
// numbers upto 100
static void fibonacci()
{
    // Adding the first two Fibonacci
    // numbers in the set
    int prev = 0, curr = 1;
    fib.add(prev);
    fib.add(curr);

    // Computing the remaining Fibonacci
    // numbers using the first two
    // Fibonacci numbers
    while (curr <= 100) {
        int temp = curr + prev;
        fib.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to return the count of
// required numbers from 0 to num
static int count(int pos, int even,
          int odd, int tight,
          Vector<Integer> num)
{
    // Base Case
    if (pos == num.size()) {
        if (num.size() % 2 == 1) {
            odd = odd + even;
            even = odd - even;
            odd = odd - even;
        }
        int d = even - odd;

        // Check if the difference is equal
        // to any fibonacci number
        if (fib.contains(d))
            return 1;

        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][even][odd][tight] != -1)
        return dp[pos][even][odd][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight==1 ? 9 : num.get(pos));

    for (int d = 0; d <= limit; d++) {
        int currF = tight, currEven = even;
        int currOdd = odd;

        if (d < num.get(pos))
            currF = 1;

        // If the current position is odd
        // add it to currOdd, otherwise to
        // currEven
        if (pos % 2 == 1)
            currOdd += d;
        else
            currEven += d;

        ans += count(pos + 1,
                     currEven, currOdd,
                     currF, num);
    }

    return dp[pos][even][odd][tight]
           = ans;
}

// Function to convert x
// into its digit vector
// and uses count() function
// to return the required count
static int solve(int x)
{
    Vector<Integer> num = new Vector<Integer>();

    while (x > 0) {
        num.add(x % 10);
        x /= 10;
    }

    Collections.reverse(num);

    // Initialize dp

    for(int i = 0; i < M; i++){
       for(int j = 0; j < 90; j++){
           for(int l = 0; l < 90; l++) {
               for (int k = 0; k < 2; k++) {
                   dp[i][j][l][k] = -1;
               }
           }
       }
   }
    return count(0, 0, 0, 0, num);
}

// Driver Code
public static void main(String[] args)
{
    // Generate fibonacci numbers
    fibonacci();

    int L = 1, R = 50;
    System.out.print(solve(R) - solve(L - 1)
         +"\n");

    L = 50;
    R = 100;
    System.out.print(solve(R) - solve(L - 1)
         +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count the numbers in
# the range having the difference
# between the sum of digits at even
# and odd positions as a Fibonacci Number

M = 18
a = 0
b = 0
dp = [[[[-1 for i in range(2)] for j in range(90)] for
        k in range(90)] for l in range(M)]

# To store all the
# Fibonacci numbers
fib = set()

# Function to generate Fibonacci
# numbers upto 100
def fibonacci():
    # Adding the first two Fibonacci
    # numbers in the set
    prev = 0
    curr = 1
    fib.add(prev)
    fib.add(curr)

    # Computing the remaining Fibonacci
    # numbers using the first two
    # Fibonacci numbers
    while (curr <= 100):
        temp = curr + prev
        fib.add(temp)
        prev = curr
        curr = temp

# Function to return the count of
# required numbers from 0 to num
def count(pos,even,odd,tight,num):
    # Base Case
    if (pos == len(num)):
        if ((len(num)& 1)):
            val = odd
            odd = even
            even = val
        d = even - odd

        # Check if the difference is equal
        # to any fibonacci number
        if ( d in fib):
            return 1

        return 0

    # If this result is already computed
    # simply return it
    if (dp[pos][even][odd][tight] != -1):
        return dp[pos][even][odd][tight]

    ans = 0

    # Maximum limit upto which we can place
    # digit. If tight is 1, means number has
    # already become smaller so we can place
    # any digit, otherwise num[pos]
    if (tight == 1):
        limit = 9
    else:
        limit = num[pos]

    for d in range(limit):
        currF = tight
        currEven = even
        currOdd = odd

        if (d < num[pos]):
            currF = 1

        # If the current position is odd
        # add it to currOdd, otherwise to
        # currEven
        if (pos & 1):
            currOdd += d
        else:
            currEven += d

        ans += count(pos + 1, currEven, 
                    currOdd, currF, num)

    return ans

# Function to convert x
# into its digit vector
# and uses count() function
# to return the required count
def solve(x):
    num = []

    while (x > 0):
        num.append(x % 10)
        x //= 10

    num = num[::-1]

    return count(0, 0, 0, 0, num)

# Driver Code
if __name__ == '__main__':

    # Generate fibonacci numbers
    fibonacci()

    L = 1
    R = 50
    print(solve(R) - solve(L - 1)+1)

    L = 50
    R = 100
    print(solve(R) - solve(L - 1)+2)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to count the numbers in
// the range having the difference
// between the sum of digits at even
// and odd positions as a Fibonacci Number
using System;
using System.Collections.Generic;

public class GFG{

static int M = 18;
static int a, b;
static int [,,,]dp = new int[M,90,90,2];

// To store all the
// Fibonacci numbers
static HashSet<int> fib = new HashSet<int>();

// Function to generate Fibonacci
// numbers upto 100
static void fibonacci()
{
    // Adding the first two Fibonacci
    // numbers in the set
    int prev = 0, curr = 1;
    fib.Add(prev);
    fib.Add(curr);

    // Computing the remaining Fibonacci
    // numbers using the first two
    // Fibonacci numbers
    while (curr <= 100) {
        int temp = curr + prev;
        fib.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to return the count of
// required numbers from 0 to num
static int count(int pos, int even,
          int odd, int tight,
          List<int> num)
{
    // Base Case
    if (pos == num.Count) {
        if (num.Count % 2 == 1) {
            odd = odd + even;
            even = odd - even;
            odd = odd - even;
        }
        int d = even - odd;

        // Check if the difference is equal
        // to any fibonacci number
        if (fib.Contains(d))
            return 1;

        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos,even,odd,tight] != -1)
        return dp[pos,even,odd,tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight==1 ? 9 : num[pos]);

    for (int d = 0; d <= limit; d++) {
        int currF = tight, currEven = even;
        int currOdd = odd;

        if (d < num[pos])
            currF = 1;

        // If the current position is odd
        // add it to currOdd, otherwise to
        // currEven
        if (pos % 2 == 1)
            currOdd += d;
        else
            currEven += d;

        ans += count(pos + 1,
                     currEven, currOdd,
                     currF, num);
    }

    return dp[pos,even,odd,tight]
           = ans;
}

// Function to convert x
// into its digit vector
// and uses count() function
// to return the required count
static int solve(int x)
{
    List<int> num = new List<int>();

    while (x > 0) {
        num.Add(x % 10);
        x /= 10;
    }

    num.Reverse();

    // Initialize dp

    for(int i = 0; i < M; i++){
       for(int j = 0; j < 90; j++){
           for(int l = 0; l < 90; l++) {
               for (int k = 0; k < 2; k++) {
                   dp[i,j,l,k] = -1;
               }
           }
       }
   }
    return count(0, 0, 0, 0, num);
}

// Driver Code
public static void Main(String[] args)
{
    // Generate fibonacci numbers
    fibonacci();

    int L = 1, R = 50;
    Console.Write(solve(R) - solve(L - 1)
         +"\n");

    L = 50;
    R = 100;
    Console.Write(solve(R) - solve(L - 1)
         +"\n");
}
}
// This code contributed by Rajput-Ji
```

**Output:**

```
14
27

```