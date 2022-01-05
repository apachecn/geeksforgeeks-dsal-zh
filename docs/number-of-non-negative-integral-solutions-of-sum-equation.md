# 和方程非负积分解的个数

> 原文:[https://www . geesforgeks . org/非负积分方程解的个数/](https://www.geeksforgeeks.org/number-of-non-negative-integral-solutions-of-sum-equation/)

给定一个数 n(变量数)和 val(变量之和)，找出有多少这样的非负积分解是可能的。

**示例:**

```
Input : n = 5, val = 1
Output : 5
Explanation:
x1 + x2 + x3 + x4 + x5 = 1
Number of possible solution are : 
(0 0 0 0 1), (0 0 0 1 0), (0 0 1 0 0),
(0 1 0 0 0), (1 0 0 0 0)
Total number of possible solutions are 5

Input : n = 5, val = 4
Output : 70
Explanation:
x1 + x2 + x3 + x4 + x5 = 4
Number of possible solution are: 
(1 1 1 1 0), (1 0 1 1 1), (0 1 1 1 1), 
(2 1 0 0 1), (2 2 0 0 0)........ so on......
Total numbers of possible solutions are 70
```

**问于:微软采访**

1.对 countSolutions(int n，int val)
2 进行递归函数调用。调用此 Solution 函数 countSolutions(n-1，val-i)，直到 n = 1，val > =0，然后返回 1。

下面是上述方法的实现:

## C++

```
// CPP program to find the numbers
// of non negative integral solutions
#include<iostream>
using namespace std;

// return number of non negative
// integral solutions
int countSolutions(int n, int val)
{
    // initialize total = 0
    int total = 0;

    // Base Case if n = 1 and val >= 0
    // then it should return 1
    if (n == 1 && val >=0)
        return 1;

    // iterate the loop till equal the val
    for (int i = 0; i <= val; i++){

        // total solution of equations
        // and again call the recursive
        // function Solutions(variable,value)
        total += countSolutions(n-1, val-i);

    }

    // return the total no possible solution
    return total;
}

// driver code
int main(){

    int n = 5;
    int val = 20;

    cout<<countSolutions(n, val);
}

//This code is contributed by Smitha Dinesh Semwal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the numbers
// of non negative integral solutions
class GFG {

  // return number of non negative
  // integral solutions
  static int countSolutions(int n, int val) {

    // initialize total = 0
    int total = 0;

    // Base Case if n = 1 and val >= 0
    // then it should return 1
    if (n == 1 && val >= 0)
      return 1;

    // iterate the loop till equal the val
    for (int i = 0; i <= val; i++) {

      // total solution of equations
      // and again call the recursive
      // function Solutions(variable, value)
      total += countSolutions(n - 1, val - i);
    }

    // return the total no possible solution
    return total;
  }

  // Driver code
  public static void main(String[] args) {
    int n = 5;
    int val = 20;

    System.out.print(countSolutions(n, val));
  }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find the numbers
# of non negative integral solutions

# return number of non negative
# integral solutions
def countSolutions(n, val):

    # initialize total = 0
    total = 0

    # Base Case if n = 1 and val >= 0
    # then it should return 1
    if n == 1 and val >=0:
        return 1

    # iterate the loop till equal the val
    for i in range(val+1):

        # total solution of equations
        # and again call the recursive
        # function Solutions(variable,value)
        total += countSolutions(n-1, val-i)

    # return the total no possible solution
    return total

# driver code
n = 5
val = 20
print(countSolutions(n, val))
```

## C#

```
// C# program to find the numbers
// of non negative integral solutions
using System;

class GFG {

    // return number of non negative
    // integral solutions
    static int countSolutions(int n, int val) {

        // initialize total = 0
        int total = 0;

        // Base Case if n = 1 and val >= 0
        // then it should return 1
        if (n == 1 && val >= 0)
        return 1;

        // iterate the loop till equal the val
        for (int i = 0; i <= val; i++) {

            // total solution of equations
            // and again call the recursive
            // function Solutions(variable, value)
            total += countSolutions(n - 1, val - i);
        }

        // return the total no possible solution
        return total;
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        int val = 20;

        Console.WriteLine(countSolutions(n, val));
    }
}

// This code is contributed by Anant vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the numbers
// of non negative integral solutions

// return number of non negative
// integral solutions
function countSolutions($n, $val)
{
    // initialize total = 0
    $total = 0;

    // Base Case if n = 1 and
    // val >= 0 then it should
    // return 1
    if ($n == 1 && $val >=0)
        return 1;

    // iterate the loop
    // till equal the val
    for ($i = 0; $i <= $val; $i++)
    {

        // total solution of equations
        // and again call the recursive
        // function Solutions(variable,value)
        $total += countSolutions($n - 1,
                                 $val - $i);

    }

    // return the total
    // no possible solution
    return $total;
}

// Driver Code
$n = 5;
$val = 20;

echo countSolutions($n, $val);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the numbers
// of non negative integral solutions

  // return number of non negative
  // integral solutions
  function countSolutions(n, val) {

    // initialize total = 0
    let total = 0;

    // Base Case if n = 1 and val >= 0
    // then it should return 1
    if (n == 1 && val >= 0)
      return 1;

    // iterate the loop till equal the val
    for (let i = 0; i <= val; i++) {

      // total solution of equations
      // and again call the recursive
      // function Solutions(variable, value)
      total += countSolutions(n - 1, val - i);
    }

    // return the total no possible solution
    return total;
  }

// Driver code

        let n = 5;
        let val = 20;

    document.write(countSolutions(n, val));

</script>
```

**输出:**

```
10626
```

**动态规划方法:**

(使用记忆)

## C++

```
// CPP program to find the numbers
// of non negative integral solutions
#include<bits/stdc++.h>
using namespace std;

int dp[1001][1001];

// return number of non negative
// integral solutions
int countSolutions(int n, int val)
{
    // initialize total = 0
    int total = 0;

    // Base Case if n = 1 and val >= 0
    // then it should return 1
    if (n == 1 && val >=0) {
        return 1;
    }

    // If a value already present in dp,
    // return it
    if(dp[n][val] != -1) {
        return dp[n][val];
    }

    // iterate the loop till equal the val
    for (int i = 0; i <= val; i++){

        // total solution of equations
        // and again call the recursive
        // function Solutions(variable,value)
        total += countSolutions(n-1, val-i);

    }

    // Store the value in dp
    dp[n][val] = total;

    // Return dp
    return dp[n][val];
}

// driver code
int main(){

    int n = 5;
    int val = 20;

    memset(dp, -1, sizeof(dp));

    cout << countSolutions(n, val);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the numbers
// of non negative integral solutions
import java.util.*;
public class GFG
{
  static int dp[][] = new int[1001][1001];

  // return number of non negative
  // integral solutions
  static int countSolutions(int n, int val)
  {
    // initialize total = 0
    int total = 0;

    // Base Case if n = 1 and val >= 0
    // then it should return 1
    if (n == 1 && val >=0) {
      return 1;
    }

    // If a value already present in dp,
    // return it
    if(dp[n][val] != -1) {
      return dp[n][val];
    }

    // iterate the loop till equal the val
    for (int i = 0; i <= val; i++){

      // total solution of equations
      // and again call the recursive
      // function Solutions(variable,value)
      total += countSolutions(n-1, val-i);

    }

    // Store the value in dp
    dp[n][val] = total;

    // Return dp
    return dp[n][val];
  }

  // driver code
  public static void main(String args[]){

    int n = 5;
    int val = 20;

    for(int i = 0; i < 1001; i++) {
      for(int j = 0; j < 1001; j++) {
        dp[i][j]=-1;
      }
    }

    System.out.println(countSolutions(n, val));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program to find the numbers
# of non negative integral solutions

# Taking the matrix as globally
dp = [[-1 for i in range(1001)]
          for j in range(1001)]

# Return number of non negative
# integral solutions
def countSolutions(n, val):

    # Initialize total = 0
    total = 0

    # Base Case if n = 1 and val >= 0
    # then it should return 1
    if n == 1 and val >= 0:
        return 1

    # If a value is already present
    # in dp
    if (dp[n][val] != -1):
        return dp[n][val]

    # Iterate the loop till equal the val
    for i in range(val + 1):

        # total solution of equations
        # and again call the recursive
        # function Solutions(variable,value)
        total += countSolutions(n - 1, val - i)

    # Return the total no possible solution
    dp[n][val] = total
    return dp[n][val]

# Driver code
n = 5
val = 20

print(countSolutions(n, val))

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program to find the numbers
// of non negative integral solutions
using System;
class GFG
{
  static int [,]dp = new int[1001, 1001];

  // return number of non negative
  // integral solutions
  static int countSolutions(int n, int val)
  {
    // initialize total = 0
    int total = 0;

    // Base Case if n = 1 and val >= 0
    // then it should return 1
    if (n == 1 && val >=0) {
      return 1;
    }

    // If a value already present in dp,
    // return it
    if(dp[n, val] != -1) {
      return dp[n, val];
    }

    // iterate the loop till equal the val
    for (int i = 0; i <= val; i++){

      // total solution of equations
      // and again call the recursive
      // function Solutions(variable,value)
      total += countSolutions(n-1, val-i);

    }

    // Store the value in dp
    dp[n, val] = total;

    // Return dp
    return dp[n, val];
  }

  // driver code
  public static void Main(){

    int n = 5;
    int val = 20;

    for(int i = 0; i < 1001; i++) {
      for(int j = 0; j < 1001; j++) {
        dp[i, j] = -1;
      }
    }

    Console.Write(countSolutions(n, val));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// JavaScript program to find the numbers
// of non negative integral solutions
  var dp = new Array(1001);

  // Loop to create 2D array using 1D array
  for (var i = 0; i < dp.length; i++) {
      dp[i] = new Array(1001);
  }

  // return number of non negative
  // integral solutions
  function countSolutions(n, val) {

    // initialize total = 0
    let total = 0;

    // Base Case if n = 1 and val >= 0
    // then it should return 1
    if (n == 1 && val >= 0)
      return 1;

    // if a value is already
    // present in dp
    if(dp[n][val] != -1)
        return dp[n][val];

    // iterate the loop till equal the val
    for (let i = 0; i <= val; i++) {

      // total solution of equations
      // and again call the recursive
      // function Solutions(variable, value)
      total += countSolutions(n - 1, val - i);
    }

    // return the total no possible solution
    return dp[n][val] = total;
  }

// Driver code
let n = 5;
let val = 20;

for(let i = 0; i < 1001; i++) {
    for(let j = 0; j < 1001; j++) {
        dp[i][j] = -1;
    }
}
document.write(countSolutions(n, val));

// This code is contributed by Samim Hossain Mondal.  
</script>
```

**Output**

```
10626
```

***时间复杂度:** O(n * val)*

***辅助空间:** O(n * val)*