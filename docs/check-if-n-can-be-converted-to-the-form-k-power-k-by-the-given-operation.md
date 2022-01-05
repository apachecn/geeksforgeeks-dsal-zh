# 检查 N 是否可以通过给定的操作

转换成 K 次方 K 的形式

> 原文:[https://www . geesforgeks . org/check-if-n-can-convert-form-k-power-k-by-then-operation/](https://www.geeksforgeeks.org/check-if-n-can-be-converted-to-the-form-k-power-k-by-the-given-operation/)

给定一个**正数 N** ，我们必须使用以下任意次数的运算，找出 N 是否可以转换成形式 K <sup>K</sup> ，其中 K 也是正整数:

*   选择任何小于当前 N 值的数字，比如 d
*   N = N–d<sup>2</sup>，每次换 N

如果可以在要求的表格中表示数字，则打印“是”，否则打印“否”。
**例:**

> **输入:** N = 13
> **输出:**是
> **解释:**
> 对于整数 13 选择 d = 3:N = 13–3<sup>2</sup>= 4，4 是 2 <sup>2</sup> 的形式。因此，输出为 4。
> 
> **输入:** N = 90
> **输出:**否
> **说明:**
> 无法用要求的形式表示数字 90。

**天真方法:**
为了解决上面提到的问题，我们将使用[递归](https://www.geeksforgeeks.org/recursion/)。在每个递归步骤中，遍历 N 的当前值的所有数字，并选择它作为 d。这样，所有的搜索空间都将被探索，如果其中任何一个 N 的形式为 K <sup>K</sup> 则停止递归并返回 true。要检查数字是否是给定的形式，请将所有这样的数字预先存储在一个集合中。该方法取 *O(D <sup>N</sup> )* ，其中 D 为 N 次的位数，可以进一步优化。

下面是给定方法的实现:

## C++14

```
// C++ implementation to Check whether a given
// number N can be converted to the form K
// power K by the given operation
#include <bits/stdc++.h>
using namespace std;

unordered_set<int> kPowKform;

// Function to check if N can
// be converted to K power K
int func(int n)
{
    if (n <= 0)
        return 0;

    // Check if n is of the form k^k
    if (kPowKform.count(n))
        return 1;

    int answer = 0;
    int x = n;

    // Iterate through each digit of n
    while (x > 0) {
        int d = x % 10;

        if (d != 0) {
            // Check if it is possible to
            // obtain number of given form
            if (func(n - d * d)) {
                answer = 1;
                break;
            }
        }

        // Reduce the number each time
        x /= 10;
    }

    // Return the result
    return answer;
}

// Function to check the above method
void canBeConverted(int n)
{

    // Check if conversion if possible
    if (func(n))
        cout << "Yes";

    else
        cout << "No";
}

// Driver code
int main()
{
    int N = 90;

    // Pre store K power K form of numbers
    // Loop till 8, because 8^8 > 10^7

    for (int i = 1; i <= 8; i++) {
        int val = 1;
        for (int j = 1; j <= i; j++)
            val *= i;

        kPowKform.insert(val);
    }

    canBeConverted(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to 
// Check whether a given
// number N can be converted 
// to the form K power K by 
// the given operation
import java.util.*;
class GFG{

static HashSet<Integer> kPowKform = 
       new HashSet<Integer>();

// Function to check if N can
// be converted to K power K
static int func(int n)
{
  if (n <= 0)
    return 0;

  // Check if n is of the form k^k
  if (kPowKform.contains(n))
    return 1;

  int answer = 0;
  int x = n;

  // Iterate through 
  // each digit of n
  while (x > 0) 
  {
    int d = x % 10;

    if (d != 0) 
    {
      // Check if it is possible to
      // obtain number of given form
      if (func(n - d * d) == 1) 
      {
        answer = 1;
        break;
      }
    }

    // Reduce the number each time
    x /= 10;
  }

  // Return the result
  return answer;
}

// Function to check the above method
static void canBeConverted(int n)
{ 
  // Check if conversion if possible
  if (func(n) == 1)
    System.out.print("Yes");
  else
    System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
  int N = 90;

  // Pre store K power K form of numbers
  // Loop till 8, because 8^8 > 10^7
  for (int i = 1; i <= 8; i++) 
  {
    int val = 1;
    for (int j = 1; j <= i; j++)
      val *= i;

    kPowKform.add(val);
  }
  canBeConverted(N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to Check whether a given
# number N can be converted to the form K
# power K by the given operation

kPowKform=dict()

# Function to check if N can
# be converted to K power K
def func(n):
    global kPowKform
    if (n <= 0):
        return 0

    # Check if n is of the form k^k
    if (n in kPowKform):
        return 1

    answer = 0
    x = n

    # Iterate through each digit of n
    while (x > 0):
        d = x % 10

        if (d != 0):
            # Check if it is possible to
            # obtain number of given form
            if (func(n - d * d)):
                answer = 1
                break

        # Reduce the number each time
        x //= 10

    # Return the result
    return answer

# Function to check the above method
def canBeConverted(n):

    # Check if conversion if possible
    if (func(n)):
        print("Yes")

    else:
        print("No")

# Driver code
if __name__ == '__main__':
    N = 90

    # Pre store K power K form of numbers
    # Loop till 8, because 8^8 > 10^7

    for i in range(1,9):
        val = 1
        for j in range(1,i+1):
            val *= i

        kPowKform[val]=1

    canBeConverted(N)

# This code is contributed by mohit kumar 29 
```

## C#

```
// C# implementation to check whether a given 
// number N can be converted to the form K 
// power K by the given operation 
using System;
using System.Collections.Generic; 

class GFG{ 

static SortedSet<int> kPowKform = new SortedSet<int>(); 

// Function to check if N can 
// be converted to K power K 
static int func(int n) 
{ 
    if (n <= 0) 
        return 0; 

    // Check if n is of the form k^k 
    if (kPowKform.Contains(n)) 
        return 1; 

    int answer = 0; 
    int x = n; 

    // Iterate through each digit of n 
    while (x > 0)
    { 
        int d = x % 10; 

        if (d != 0)
        {

            // Check if it is possible to 
            // obtain number of given form 
            if (func(n - d * d) == 1)
            { 
                answer = 1; 
                break; 
            } 
        } 

        // Reduce the number each time 
        x /= 10; 
    } 

    // Return the result 
    return answer; 
} 

// Function to check the above method 
static void canBeConverted(int n) 
{ 

    // Check if conversion if possible 
    if (func(n) == 1) 
        Console.Write("Yes"); 
    else
        Console.Write("No"); 
} 

// Driver code 
public static void Main() 
{ 
    int N = 90; 

    // Pre store K power K form of numbers 
    // Loop till 8, because 8^8 > 10^7 
    for(int i = 1; i <= 8; i++)
    { 
        int val = 1; 
        for(int j = 1; j <= i; j++) 
            val *= i; 

        kPowKform.Add(val); 
    } 
    canBeConverted(N); 
} 
} 

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript implementation to Check whether a given
// number N can be converted to the form K
// power K by the given operation
var kPowKform = new Set();

// Function to check if N can
// be converted to K power K
function func(n)
{
    if (n <= 0)
        return 0;

    // Check if n is of the form k^k
    if (kPowKform.has(n))
        return 1;

    var answer = 0;
    var x = n;

    // Iterate through each digit of n
    while (x > 0)
    {
        var d = x % 10;

        if (d != 0)
        {

            // Check if it is possible to
            // obtain number of given form
            if (func(n - d * d)) {
                answer = 1;
                break;
            }
        }

        // Reduce the number each time
        x = parseInt(x/10);
    }

    // Return the result
    return answer;
}

// Function to check the above method
function canBeConverted(n)
{

    // Check if conversion if possible
    if (func(n))
        document.write( "Yes");

    else
        document.write( "No");
}

// Driver code
var N = 90;

// Pre store K power K form of numbers
// Loop till 8, because 8^8 > 10^7
for (var i = 1; i <= 8; i++) {
    var val = 1;
    for (var j = 1; j <= i; j++)
        val *= i;
    kPowKform.add(val);
}
canBeConverted(N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
No
```

**高效方法:**
在递归方法中，我们多次求解同一个子问题，即存在[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。因此，我们可以使用动态编程，并使用缓存或记忆表来记忆递归方法。

下面是上述方法的实现:

## C++

```
// C++ implementation to Check whether a given
// number N can be converted to the form K
// power K by the given operation
#include <bits/stdc++.h>
using namespace std;

unordered_set<int> kPowKform;
int dp[100005];

// Function to check if a number is converatable
int func(int n)
{
    if (n <= 0)
        return 0;

    // Check if n is of the form k^k
    if (kPowKform.count(n))
        return 1;

    // Check if the subproblem has been solved before
    if (dp[n] != -1)
        return dp[n];

    int answer = 0;
    int x = n;

    // Iterate through each digit of n
    while (x > 0) {
        int d = x % 10;
        if (d != 0) {
            // Check if it is possible to
            // obtain number of given form
            if (func(n - d * d)) {
                answer = 1;
                break;
            }
        }

        // Reduce the number each time
        x /= 10;
    }

    // Store and return the
    // answer to this subproblem
    return dp[n] = answer;
}

// Function to check the above method
void canBeConverted(int n)
{

    // Initialise the dp table
    memset(dp, -1, sizeof(dp));

    // Check if conversion if possible
    if (func(n))
        cout << "Yes";

    else
        cout << "No";
}

// Driver code
int main()
{
    int N = 13;

    // Pre store K power K form of numbers
    // Loop till 8, because 8^8 > 10^7
    for (int i = 1; i <= 8; i++) {
        int val = 1;

        for (int j = 1; j <= i; j++)
            val *= i;

        kPowKform.insert(val);
    }

    canBeConverted(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// Check whether a given
// number N can be converted 
// to the form K power K by 
// the given operation
import java.util.*;
class GFG{

static HashSet<Integer> kPowKform = 
       new HashSet<>();
static int []dp = new int[100005];

// Function to check if 
// a number is converatable
static int func(int n)
{
  if (n <= 0)
    return 0;

  // Check if n is of the form k^k
  if (kPowKform.contains(n))
    return 1;

  // Check if the subproblem 
  // has been solved before
  if (dp[n] != -1)
    return dp[n];

  int answer = 0;
  int x = n;

  // Iterate through each digit of n
  while (x > 0) 
  {
    int d = x % 10;
    if (d != 0) 
    {
      // Check if it is possible to
      // obtain number of given form
      if (func(n - d * d) != 0) 
      {
        answer = 1;
        break;
      }
    }

    // Reduce the number 
    // each time
    x /= 10;
  }

  // Store and return the
  // answer to this subproblem
  return dp[n] = answer;
}

// Function to check the above method
static void canBeConverted(int n)
{
  // Initialise the dp table
  for (int i = 0; i < n; i++)
    dp[i] = -1;

  // Check if conversion if possible
  if (func(n) == 0)
    System.out.print("Yes");
  else
    System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
  int N = 13;

  // Pre store K power K form of numbers
  // Loop till 8, because 8^8 > 10^7
  for (int i = 1; i <= 8; i++) 
  {
    int val = 1;

    for (int j = 1; j <= i; j++)
      val *= i;

    kPowKform.add(val);
  }
  canBeConverted(N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to check whether 
# a given number N can be converted to
# the form K power K by the given operation
kPowKform = dict()

# Function to check if N can
# be converted to K power K
def func(n, dp):

    global kPowKform
    if (n <= 0):
        return 0

    # Check if n is of the form k^k
    if (n in kPowKform):
        return 1

    if (dp[n] != -1):
        return dp[n]

    answer = 0
    x = n

    # Iterate through each digit of n
    while (x > 0):
        d = x % 10

        if (d != 0):

            # Check if it is possible to
            # obtain number of given form
            if (func(n - d * d, dp)):
                answer = 1
                break

        # Reduce the number each time
        x //= 10

    dp[n] = answer

    # Return the result
    return answer

# Function to check the above method
def canBeConverted(n):

    dp = [-1 for i in range(10001)]

    # Check if conversion if possible
    if (func(n, dp)):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':

    N = 13

    # Pre store K power K form of
    # numbers Loop till 8, because
    # 8^8 > 10^7
    for i in range(1, 9):
        val = 1

        for j in range(1, i + 1):
            val *= i

        kPowKform[val] = 1

    canBeConverted(N)

# This code is contributed by grand_master
```

## C#

```
// C# implementation to check whether a given
// number N can be converted to the form K
// power K by the given operation
using System;
using System.Collections;
using System.Collections.Generic; 

class GFG{

static HashSet<int> kPowKform = new HashSet<int>();
static int []dp = new int[100005];

// Function to check if a number
// is converatable
static int func(int n)
{
    if (n <= 0)
        return 0;

    // Check if n is of the form k^k
    if (kPowKform.Contains(n))
        return 1;

    // Check if the subproblem has
    // been solved before
    if (dp[n] != -1)
        return dp[n];

    int answer = 0;
    int x = n;

    // Iterate through each digit of n
    while (x > 0) 
    {
        int d = x % 10;

        if (d != 0)
        {

            // Check if it is possible to
            // obtain number of given form
            if (func(n - d * d) != 0)
            {
                answer = 1;
                break;
            }
        }

        // Reduce the number each time
        x /= 10;
    }

    // Store and return the
    // answer to this subproblem
    dp[n] = answer;
    return answer;
}

// Function to check the above method
static void canBeConverted(int n)
{

    // Initialise the dp table
    Array.Fill(dp, -1);

    // Check if conversion if possible
    if (func(n) != 0)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(string[] args)
{
   int N = 13;

    // Pre store K power K form of numbers
    // Loop till 8, because 8^8 > 10^7
    for(int i = 1; i <= 8; i++)
    {
        int val = 1;

        for(int j = 1; j <= i; j++)
            val *= i;

        kPowKform.Add(val);
    }
    canBeConverted(N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to Check whether a given
// number N can be converted to the form K
// power K by the given operation
var kPowKform = new Set();
var dp = Array(100005);

// Function to check if a number is converatable
function func(n)
{
    if (n <= 0)
        return 0;

    // Check if n is of the form k^k
    if (kPowKform.has(n))
        return 1;

    // Check if the subproblem has been solved before
    if (dp[n] != -1)
        return dp[n];

    var answer = 0;
    var x = n;

    // Iterate through each digit of n
    while (x > 0) {
        var d = x % 10;
        if (d != 0) {
            // Check if it is possible to
            // obtain number of given form
            if (func(n - d * d)) {
                answer = 1;
                break;
            }
        }

        // Reduce the number each time
        x /= 10;
    }

    // Store and return the
    // answer to this subproblem
    return dp[n] = answer;
}

// Function to check the above method
function canBeConverted(n)
{

    // Initialise the dp table
    dp = Array(100005).fill(-1);

    // Check if conversion if possible
    if (func(n))
        document.write( "Yes");

    else
        document.write( "No");
}

// Driver code
var N = 13;

// Pre store K power K form of numbers
// Loop till 8, because 8^8 > 10^7
for (var i = 1; i <= 8; i++) {
    var val = 1;
    for (var j = 1; j <= i; j++)
        val *= i;
    kPowKform.add(val);
}
canBeConverted(N);

// This code is contributed by famously.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(D * N)* ，其中 D 为 N 中的位数