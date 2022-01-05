# 给定按键的唯一 BST 数|动态编程

> 原文:[https://www . geeksforgeeks . org/带有给定密钥的唯一 bst 号动态编程/](https://www.geeksforgeeks.org/number-of-unique-bst-with-a-given-key-dynamic-programming/)

给定 N，用 1 到 N 的值求唯一 BST 的总数。
 **示例:**

```
Input: n = 3 
Output: 5
For n = 3, preorder traversal of Unique BSTs are:
1\. 1 2 3
2\. 1 3 2
3\. 2 1 3
4\. 3 1 2
5\. 3 2 1

Input: 4 
Output: 14

```

在[之前的](https://www.geeksforgeeks.org/total-number-of-possible-binary-search-trees-with-n-keys/)帖子中已经讨论了 O(n)解决方案。在这篇文章中，我们将讨论一个基于动态编程的解决方案。对于 I 的所有可能值，将 I 视为根，然后[1…i-1]数字将落在左子树和[i+1…n]数字将落在右边的子树中。所以，在答案中加上(i-1)*(n-i)。产品的总和将是唯一 BST 数量的答案。

以下是上述方法的实现:

## C++

```
// C++ code to find number of unique BSTs
// Dynamic Programming solution
#include <bits/stdc++.h>
using namespace std;

// Function to find number of unique BST
int numberOfBST(int n)
{

    // DP to store the number of unique BST with key i
    int dp[n + 1];
    fill_n(dp, n + 1, 0);

    // Base case
    dp[0] = 1;
    dp[1] = 1;

    // fill the dp table in top-down approach.
    for (int i = 2; i <= n; i++) {
        for (int j = 1; j <= i; j++) {

            // n-i in right * i-1 in left
            dp[i] = dp[i] + (dp[i - j] * dp[j - 1]);
        }
    }

    return dp[n];
}

// Driver Code
int main()
{
    int n = 3;
    cout << "Number of structurally Unique BST with " << 
    n << " keys are : " << numberOfBST(n) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find number
// of unique BSTs Dynamic 
// Programming solution
import java.io.*;
import java.util.Arrays;

class GFG
{
    static int numberOfBST(int n)
    {

    // DP to store the number 
    // of unique BST with key i
    int dp[] = new int[n + 1];
    Arrays.fill(dp, 0);

    // Base case
    dp[0] = 1;
    dp[1] = 1;

    // fill the dp table in
    // top-down approach.
    for (int i = 2; i <= n; i++) 
    {
        for (int j = 1; j <= i; j++) 
        {

            // n-i in right * i-1 in left
            dp[i] = dp[i] + (dp[i - j] * 
                             dp[j - 1]);
        }
    }

    return dp[n];
}

// Driver Code
public static void main (String[] args) 
{
    int n = 3;
    System.out.println("Number of structurally " + 
                           "Unique BST with "+ n +
                                  " keys are : " + 
                                  numberOfBST(n));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 蟒蛇 3

```
# Python3 code to find number of unique 
# BSTs Dynamic Programming solution 

# Function to find number of unique BST 
def numberOfBST(n): 

    # DP to store the number of unique
    # BST with key i 
    dp = [0] * (n + 1) 

    # Base case 
    dp[0], dp[1] = 1, 1

    # fill the dp table in top-down 
    # approach. 
    for i in range(2, n + 1): 
        for j in range(1, i + 1): 

            # n-i in right * i-1 in left 
            dp[i] = dp[i] + (dp[i - j] *
                             dp[j - 1]) 

    return dp[n] 

# Driver Code 
if __name__ == "__main__": 

    n = 3
    print("Number of structurally Unique BST with", 
                   n, "keys are :", numberOfBST(n)) 

# This code is contributed 
# by Rituraj Jain
```

## C#

```
// C# code to find number
// of unique BSTs Dynamic 
// Programming solution
using System;

class GFG
{
    static int numberOfBST(int n)
    {

    // DP to store the number 
    // of unique BST with key i
    int []dp = new int[n + 1];

    // Base case
    dp[0] = 1;
    dp[1] = 1;

    // fill the dp table in
    // top-down approach.
    for (int i = 2; i <= n; i++) 
    {
        for (int j = 1; j <= i; j++) 
        {

            // n-i in right * i-1 in left
            dp[i] = dp[i] + (dp[i - j] * 
                             dp[j - 1]);
        }
    }
    return dp[n];
}

// Driver Code
public static void Main () 
{
    int n = 3;
    Console.Write("Number of structurally " + 
                      "Unique BST with "+ n +
                             " keys are : " + 
                             numberOfBST(n));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find number 
// of unique BSTs Dynamic
// Programming solution

// Function to find number 
// of unique BST
function numberOfBST($n)
{

    // DP to store the number 
    // of unique BST with key i
    $dp = array($n + 1);
    for($i = 0; $i <= $n + 1; $i++)
    $dp[$i] = 0;

    // Base case
    $dp[0] = 1;
    $dp[1] = 1;

    // fill the dp table 
    // in top-down approach.
    for ($i = 2; $i <= $n; $i++) 
    {
        for ($j = 1; $j <= $i; $j++) 
        {

            // n-i in right * 
            // i-1 in left
            $dp[$i] += (($dp[$i - $j]) * 
                        ($dp[$j - 1]));
        }
    }

    return $dp[$n];
}

// Driver Code
$n = 3;
echo "Number of structurally ". 
           "Unique BST with " , 
          $n , " keys are : " , 
              numberOfBST($n) ;

// This code is contributed
// by shiv_bhakt.
?>
```

**Output:**

```
Number of structurally Unique BST with 3 keys are : 5

```

**时间复杂度:** O(n <sup>2</sup>