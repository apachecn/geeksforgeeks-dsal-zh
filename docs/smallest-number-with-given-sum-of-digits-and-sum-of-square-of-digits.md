# 给定位数和位数平方和的最小数

> 原文:[https://www . geesforgeks . org/给定位数和位数平方和的最小数/](https://www.geeksforgeeks.org/smallest-number-with-given-sum-of-digits-and-sum-of-square-of-digits/)

给定位数之和![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")和位数平方之和![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。用给定的位数总和和位数平方总和求最小数。数字不能超过 100 位。如果不存在这样的数字，或者位数超过 100，则打印-1。
**例:**

> **输入:** a = 18，b = 162
> **输出:** 99
> **说明:** 99 是最小可能数，其位数之和= 9 + 9 = 18，位数平方和为 9 <sup>2</sup> +9 <sup>2</sup> = 162。
> **输入:** a = 12，b = 9
> **输出:** -1

**进场:**
因为最小的数字可以是 100 位数，所以不能存储。因此，解决这个问题的第一步将是找到最小位数，它可以给我们的数字之和为![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")，数字的平方之和为![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。为了找到最小位数，我们可以使用动态规划。DP[a][b]表示一个数中的最小位数，其位数之和为![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")，位数之和为![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。如果不存在任何此类数字，则 DP[a][b]将为-1。
由于数字不能超过 100 位，DP 数组的大小为 **101*8101** 。对每个数字进行迭代，尝试所有可能的数字组合，给我们的数字总和为![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")，数字平方的总和为![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。使用以下循环关系
在 DP[a][b]中存储最小位数

> DP[a][b] = min(最小数字位数(a–I，b –( I * I))+1)
> 其中 1 < =i < =9

得到最小位数后，找到位数。要查找数字，请检查所有组合，并打印满足以下条件的数字:

> 1+DP[a–I][b–I * I]= = DP[a][b]
> 其中 1 < =i < =9

如果 I 中的任何一个满足上述条件，则将![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")减少 I，将![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")减少 i*i，并断开。继续重复上述过程，找到所有数字，直到![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")为 0，![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")为 0。
以下是上述方法的实施:

## C++

```
// CPP program to find the Smallest number
// with given sum of digits and
// sum of square of digits
#include <bits/stdc++.h>
using namespace std;

int dp[901][8101];

// Top down dp to find minimum number of digits with
// given sum of dits a and sum of square of digits as b
int minimumNumberOfDigits(int a, int b)
{
    // Invalid condition
    if (a > b || a < 0 || b < 0 || a > 900 || b > 8100)
        return -1;

    // Number of digits satisfied
    if (a == 0 && b == 0)
        return 0;

    // Memoization
    if (dp[a][b] != -1)
        return dp[a][b];

    // Initialize ans as maximum as we have to find the 
    // minimum number of digits
    int ans = 101;

    // Check for all possible combinations of digits
    for (int i = 9; i >= 1; i--) {

        // recurrence call
        int k = minimumNumberOfDigits(a - i, b - (i * i));

        // If the combination of digits cannot give sum as a
        // and sum of square of digits as b
        if (k != -1)
            ans = min(ans, k + 1);
    }

    // Returns the minimum number of digits
    return dp[a][b] = ans;
}

// Function to print the digits that gives
// sum as a and sum of square of digits as b
void printSmallestNumber(int a,int b)
{

    // initialize the dp array as -1
    memset(dp, -1, sizeof(dp));

    // base condition
    dp[0][0] = 0;

    // function call to get the minimum number of digits 
    int k = minimumNumberOfDigits(a, b);

    // When there does not exists any number
    if (k == -1 || k > 100)
        cout << "-1";
    else {
        // Printing the digits from the most significant digit
        while (a > 0 && b > 0) {

            // Trying all combinations
            for (int i = 1; i <= 9; i++) {
                // checking conditions for minimum digits
                if (a >= i && b >= i * i &&
                    1 + dp[a - i][b - i * i] == dp[a][b]) {
                    cout << i;
                    a -= i;
                    b -= i * i;
                    break;
                }
            }
        }
    }
}

// Driver Code
int main()
{
    int a = 18, b = 162;
    // Function call to print the smallest number
    printSmallestNumber(a,b);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program to find the Smallest number
// with given sum of digits and
// sum of square of digits
class GFG {

    static int dp[][] = new int[901][8101];

// Top down dp to find minimum number of digits with
// given sum of dits a and sum of square of digits as b
    static int minimumNumberOfDigits(int a, int b) {
        // Invalid condition
        if (a > b || a < 0 || b < 0 || a > 900 || b > 8100) {
            return -1;
        }

        // Number of digits satisfied
        if (a == 0 && b == 0) {
            return 0;
        }

        // Memoization
        if (dp[a][b] != -1) {
            return dp[a][b];
        }

        // Initialize ans as maximum as we have to find the 
        // minimum number of digits
        int ans = 101;

        // Check for all possible combinations of digits
        for (int i = 9; i >= 1; i--) {

            // recurrence call
            int k = minimumNumberOfDigits(a - i, b - (i * i));

            // If the combination of digits cannot give sum as a
            // and sum of square of digits as b
            if (k != -1) {
                ans = Math.min(ans, k + 1);
            }
        }

        // Returns the minimum number of digits
        return dp[a][b] = ans;
    }

// Function to print the digits that gives
// sum as a and sum of square of digits as b
    static void printSmallestNumber(int a, int b) {

        // initialize the dp array as -1
        for (int[] row : dp) {
            Arrays.fill(row, -1);
        }

        // base condition
        dp[0][0] = 0;

        // function call to get the minimum number of digits 
        int k = minimumNumberOfDigits(a, b);

        // When there does not exists any number
        if (k == -1 || k > 100) {
            System.out.println("-1");
        } else {
            // Printing the digits from the most significant digit
            while (a > 0 && b > 0) {

                // Trying all combinations
                for (int i = 1; i <= 9; i++) {
                    // checking conditions for minimum digits
                    if (a >= i && b >= i * i
                            && 1 + dp[a - i][b - i * i] == dp[a][b]) {
                        System.out.print(i);
                        a -= i;
                        b -= i * i;
                        break;
                    }
                }
            }
        }
    }

// Driver Code
    public static void main(String args[]) {
        int a = 18, b = 162;
        // Function call to print the smallest number
        printSmallestNumber(a, b);
    }
}

// This code is contributed by PrinciRaj19992
```

## 蟒蛇 3

```
# Python3 program to find the Smallest number
# with given sum of digits and
# sum of square of digits

dp=[[-1 for i in range(8101)]for i in range(901)]

# Top down dp to find minimum number of digits with
# given sum of dits a and sum of square of digits as b
def minimumNumberOfDigits(a,b):
    # Invalid condition
    if (a > b or a < 0 or b < 0 or a > 900 or b > 8100):
        return -1

    # Number of digits satisfied
    if (a == 0 and b == 0):
        return 0

    # Memoization
    if (dp[a][b] != -1):
        return dp[a][b]

    # Initialize ans as maximum as we have to find the
    # minimum number of digits
    ans = 101

    #Check for all possible combinations of digits
    for i in range(9,0,-1):

        # recurrence call
        k = minimumNumberOfDigits(a - i, b - (i * i))

        # If the combination of digits cannot give sum as a
        # and sum of square of digits as b
        if (k != -1):
            ans = min(ans, k + 1)

    # Returns the minimum number of digits
    dp[a][b] = ans
    return ans

# Function to print the digits that gives
# sum as a and sum of square of digits as b
def printSmallestNumber(a,b):
    # initialize the dp array as
    for i in range(901):
        for j in range(8101):
            dp[i][j]=-1

    # base condition
    dp[0][0] = 0

    # function call to get the minimum number of digits
    k = minimumNumberOfDigits(a, b)

    # When there does not exists any number
    if (k == -1 or k > 100):
        print(-1,end='')
    else:
        # Printing the digits from the most significant digit

        while (a > 0 and b > 0):

            # Trying all combinations
            for i in range(1,10):

                #checking conditions for minimum digits
                if (a >= i and b >= i * i and
                    1 + dp[a - i][b - i * i] == dp[a][b]):
                    print(i,end='')
                    a -= i
                    b -= i * i
                    break
# Driver Code
if __name__=='__main__':
    a = 18
    b = 162
# Function call to print the smallest number
    printSmallestNumber(a,b)

# This code is contributed by sahilshelangia
```

## C#

```
// C# program to find the Smallest number
// with given sum of digits and
// sum of square of digits
using System;
public class GFG {

    static int [,]dp = new int[901,8101];

// Top down dp to find minimum number of digits with
// given sum of dits a and sum of square of digits as b
    static int minimumNumberOfDigits(int a, int b) {
        // Invalid condition
        if (a > b || a < 0 || b < 0 || a > 900 || b > 8100) {
            return -1;
        }

        // Number of digits satisfied
        if (a == 0 && b == 0) {
            return 0;
        }

        // Memoization
        if (dp[a,b] != -1) {
            return dp[a,b];
        }

        // Initialize ans as maximum as we have to find the 
        // minimum number of digits
        int ans = 101;

        // Check for all possible combinations of digits
        for (int i = 9; i >= 1; i--) {

            // recurrence call
            int k = minimumNumberOfDigits(a - i, b - (i * i));

            // If the combination of digits cannot give sum as a
            // and sum of square of digits as b
            if (k != -1) {
                ans = Math.Min(ans, k + 1);
            }
        }

        // Returns the minimum number of digits
        return dp[a,b] = ans;
    }

// Function to print the digits that gives
// sum as a and sum of square of digits as b
    static void printSmallestNumber(int a, int b) {

        // initialize the dp array as -1
        for (int i = 0; i < dp.GetLength(0); i++)
            for (int j = 0; j < dp.GetLength(1); j++)
                   dp[i, j] = -1;

        // base condition
        dp[0,0] = 0;

        // function call to get the minimum number of digits 
        int k = minimumNumberOfDigits(a, b);

        // When there does not exists any number
        if (k == -1 || k > 100) {
            Console.WriteLine("-1");
        } else {
            // Printing the digits from the most significant digit
            while (a > 0 && b > 0) {

                // Trying all combinations
                for (int i = 1; i <= 9; i++) {
                    // checking conditions for minimum digits
                    if (a >= i && b >= i * i
                            && 1 + dp[a - i,b - i * i] == dp[a,b]) {
                        Console.Write(i);
                        a -= i;
                        b -= i * i;
                        break;
                    }
                }
            }
        }
    }

// Driver Code
    public static void Main() {
        int a = 18, b = 162;
        // Function call to print the smallest number
        printSmallestNumber(a, b);
    }
}

// This code is contributed by PrinciRaj19992
```

## java 描述语言

```
<script>

// JavaScript program to find the Smallest number
// with given sum of digits and
// sum of square of digits

  // initialize the dp array as -1
 dp = new Array(901).fill(-1).map(() =>
 new Array(8101).fill(-1));;

// Top down dp to find minimum
// number of digits with
// given sum of dits a and
// sum of square of digits as b
function minimumNumberOfDigits(a, b)
{
    // Invalid condition
    if (a > b || a < 0 || b < 0 || a > 900 || b > 8100)
        return -1;

    // Number of digits satisfied
    if (a == 0 && b == 0)
        return 0;

    // Memoization
    if (dp[a][b] != -1)
        return dp[a][b];

    // Initialize ans as maximum as we have to find the 
    // minimum number of digits
    var ans = 101;

    // Check for all possible combinations of digits
    for (var i = 9; i >= 1; i--) {

        // recurrence call
        var k = minimumNumberOfDigits(a - i, b - (i * i));

        // If the combination of digits cannot give sum as a
        // and sum of square of digits as b
        if (k != -1)
            ans = Math.min(ans, k + 1);
    }

    // Returns the minimum number of digits
    return dp[a][b] = ans;
}

// Function to print the digits that gives
// sum as a and sum of square of digits as b
function printSmallestNumber(a, b)
{  
    // base condition
    dp[0][0] = 0;

    // function call to get the
    // minimum number of digits 
    var k = minimumNumberOfDigits(a, b);

    // When there does not exists any number
    if (k == -1 || k > 100)
        document.write( "-1");
    else {
        // Printing the digits from the
        // most significant digit
        while (a > 0 && b > 0) {

            // Trying all combinations
            for (var i = 1; i <= 9; i++) {
                // checking conditions for minimum digits
                if (a >= i && b >= i * i &&
                    1 + dp[a - i][b - i * i] == dp[a][b]) {
                    document.write( i);
                    a -= i;
                    b -= i * i;
                    break;
                }
            }
        }
    }
}

   var a = 18, b = 162;

    // Function call to print the smallest number
    printSmallestNumber(a,b);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
99
```

**时间复杂度** : O(900*8100*9)
**辅助空间** : O(900*8100)
**注意:**时间复杂度是用数字来表示的，因为我们正在尝试所有可能的数字组合。