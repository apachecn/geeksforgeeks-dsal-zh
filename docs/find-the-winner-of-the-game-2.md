# 找到游戏的赢家

> 原文:[https://www . geesforgeks . org/find-the-winner-the-game-2/](https://www.geeksforgeeks.org/find-the-winner-of-the-game-2/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，两个玩家 **A** 和 **B** 正在玩一个游戏，玩家轮流挑选数字和最大的元素。最终，具有所选元素的最大总和的玩家赢得游戏。假设玩家 **A** 总是先开始游戏，并且两个玩家都以最佳状态玩，那么任务就是找到游戏的赢家。
**举例:**

> **输入:** arr[] = {12，43，25，23，30}
> **输出:** B
> A 选择 43
> B 选择 25
> A 选择 23
> B 选择 30
> A 选择 12
> A 的分数= 43 + 23 + 12 = 78
> B 的分数= 25 + 30 = 55
> **输入:**

**方法:** [根据整数的数字和值对数组进行排序](https://www.geeksforgeeks.org/merge-sort/)，如果两个整数的数字和相同，那么会根据它们的值进行比较，这是因为最后值会最大化和。根据自定义比较器对数组进行排序后，玩家 A 将尝试从最大的(贪婪地)开始挑选元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the
// sum of the digits of n
int digit_sum(int n)
{
    int s = 0;
    while (n > 0) {
        s += n % 10;
        n /= 10;
    }
    return s;
}

// Compares two integers according
// to their digit sum
bool comparator(int a, int b)
{

    // Sum of digits of a
    int s1 = digit_sum(a);

    // Sum of digits of b
    int s2 = digit_sum(b);

    // If the digit sum of a is equal
    // to the digit sum of b
    if (s1 == s2)
        return (a < b);
    return (s1 < s2);
}

// Function to return the winner of the game
string findTheWinner(int arr[], int n)
{

    // Sort the elements based on
    // the digit sum values
    sort(arr, arr + n, comparator);

    // Find player A's score
    int scoreA = 0;
    for (int i = n - 1; i >= 0; i -= 2)
        scoreA += arr[i];

    // Find player A's score
    int scoreB = 0;
    for (int i = n - 2; i >= 0; i -= 2)
        scoreB += arr[i];

    // Find the winner
    if (scoreA == scoreB)
        return "Draw";
    else if (scoreA > scoreB)
        return "A";
    return "B";
}

// Driver code
int main()
{
    int arr[] = { 12, 43, 25, 23, 30 };
    int n = sizeof(arr) / sizeof(int);

    cout << findTheWinner(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that returns the
# sum of the digits of n
def digit_sum(n):

    s = 0;
    while n > 0:
        s += n % 10
        n /= 10

    return s

# Function to return the winner
# of the game
def findTheWinner(arr, n):

    # Sort the elements based on
    # the digit sum values
    arr.sort(key = digit_sum)

    # Find player A's score
    scoreA = 0
    i = n - 1
    while i >= 0:
        scoreA += arr[i]
        i -= 2

    # Find player A's score
    scoreB = 0
    i = n - 2
    while i >= 0:
        scoreA += arr[i]
        i -= 2

    # Find the winner
    if scoreA == scoreB:
        return "Draw"
    elif (scoreA > scoreB):
        return "A"

    return "B"

# Driver code
if __name__=="__main__":

    arr = [ 12, 43, 25, 23, 30 ]
    n = len(arr);

    print(findTheWinner(arr, n))

# This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns the
// sum of the digits of n
function digit_sum(n)
{
    var s = 0;
    while (n > 0) {
        s += n % 10;
        n = parseInt(n/10);
    }
    return s;
}

// Compares two integers according
// to their digit sum
function comparator(a, b)
{
    // Sum of digits of a
    var s1 = digit_sum(a);

    // Sum of digits of b
    var s2 = digit_sum(b);

    // If the digit sum of a is equal
    // to the digit sum of b
    if (s1 == s2)
        return (a < b);
    return (s1 < s2);
}

// Function to return the winner of the game
function findTheWinner(arr, n)
{

    // Sort the elements based on
    // the digit sum values
    arr.sort(comparator);

    // Find player A's score
    var scoreA = 0;
    for (var i = n - 1; i >= 0; i -= 2)
        scoreA += arr[i];

    // Find player A's score
    var scoreB = 0;
    for (var i = n - 2; i >= 0; i -= 2)
        scoreB += arr[i];

    // Find the winner
    if (scoreA == scoreB)
        return "Draw";
    else if (scoreA > scoreB)
        return "A";
    return "B";
}

// Driver code
var arr = [ 12, 43, 25, 23, 30 ];
var n = arr.length;
document.write( findTheWinner(arr, n));

</script>
```

**Output:** 

```
A
```