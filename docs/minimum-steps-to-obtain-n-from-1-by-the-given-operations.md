# 通过给定操作从 1 获得 N 的最小步骤

> 原文:[https://www . geeksforgeeks . org/按给定操作从 1 获取 n 的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-to-obtain-n-from-1-by-the-given-operations/)

给定一个整数 **N** ，任务是从 **1** 开始，找到获得数字 **N** 所需的最小操作数。以下是操作:

*   在当前数字上加 1。
*   将当前数字乘以 2。
*   将当前数字乘以 3。

打印所需的最小操作次数和相应的顺序，获得 **N** 。

**示例:**

> **输入:** N = 3
> **输出:**
> 1
> 1 3
> **说明:**
> 运算 1:乘 1 * 3 = 3。
> 因此，只需要 1 次操作。
> 
> **输入:** N = 5
> **输出:**
> 3
> 1 2 4 5
> **说明:**
> 最低要求操作如下:
> 1 * 2->2
> 2 * 2->4
> 4+1->5

**递归方法:**递归生成每个可能的组合，将 **N** 减少到 1，并计算所需的运算次数。最后，在用尽所有可能的组合后，打印需要最少操作次数的序列。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

vector<int> find_sequence(int n)
{

    // Base Case
    if (n == 1)
        return {1, -1};

    // Recursive Call for n-1
    auto arr = find_sequence(n - 1);
    vector<int> ans = {arr[0] + 1, n - 1};

    // Check if n is divisible by 2
    if (n % 2 == 0)
    {
        vector<int> div_by_2 = find_sequence(n / 2);

        if (div_by_2[0] < ans[0])
            ans = {div_by_2[0] + 1, n / 2};
    }

    // Check if n is divisible by 3
    if (n % 3 == 0)
    {
        vector<int> div_by_3 = find_sequence(n / 3);

        if (div_by_3[0] < ans[0])
            vector<int> ans = {div_by_3[0] + 1, n / 3};
    }

    // Returns a tuple (a, b), where
    // a: Minimum steps to obtain x from 1
    // b: Previous number
    return ans;
}

// Function that find the optimal
// solution
vector<int> find_solution(int n)
{
    auto a = find_sequence(n);

    // Print the length
    cout << a[0] << endl;

    vector<int> sequence;
    sequence.push_back(n);

    //Exit condition for loop = -1
    //when n has reached 1
    while (a[1] != -1)
    {
        sequence.push_back(a[1]);
        auto arr = find_sequence(a[1]);
        a[1] = arr[1];
    }

    // Return the sequence
    // in reverse order
    reverse(sequence.begin(),
            sequence.end());

    return sequence;
}

// Driver Code
int main()
{

    // Given N
    int n = 5;

    // Function call
    auto i = find_solution(n);

    for(int j : i)
        cout << j << " ";
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.util.Collections;
import java.util.Vector;

//Vector<Integer> v = new Vector<Integer>(n);

class GFG{

static Vector<Integer> find_sequence(int n)
{
    Vector<Integer> temp = new Vector<Integer>();

    temp.add(1);
    temp.add(-1);

    // Base Case
    if (n == 1)
        return temp;

    // Recursive Call for n-1
    Vector<Integer> arr = find_sequence(n - 1);
    Vector<Integer> ans = new Vector<Integer>(n);
    ans.add(arr.get(0) + 1);
    ans.add(n - 1);

    // Check if n is divisible by 2
    if (n % 2 == 0)
    {
        Vector<Integer> div_by_2 = find_sequence(n / 2);

        if (div_by_2.get(0) < ans.get(0))
        {
            ans.clear();
            ans.add(div_by_2.get(0) + 1);
            ans.add(n / 2);
        }
    }

    // Check if n is divisible by 3
    if (n % 3 == 0)
    {
        Vector<Integer> div_by_3 = find_sequence(n / 3);

        if (div_by_3.get(0) < ans.get(0))
        {
            ans.clear();
            ans.add(div_by_3.get(0) + 1);
            ans.add(n / 3);
        }
    }

    // Returns a tuple (a, b), where
    // a: Minimum steps to obtain x from 1
    // b: Previous number
    return ans;
}

// Function that find the optimal
// solution
static Vector<Integer> find_solution(int n)
{
    Vector<Integer> a = find_sequence(n);

    // Print the length
    System.out.println(a.get(0));

    Vector<Integer> sequence = new Vector<Integer>();
    sequence.add(n);

    // Exit condition for loop = -1
    // when n has reached 1
    while (a.get(1) != -1)
    {
        sequence.add(a.get(1));
        Vector<Integer> arr = find_sequence(a.get(1));
        a.set(1, arr.get(1));
    }

    // Return the sequence
    // in reverse order
    Collections.reverse(sequence);

    return sequence;
}

// Driver Code
public static void main(String args[])
{

    // Given N
    int n = 5;

    // Function call
    Vector<Integer> res = find_solution(n);

    for(int i = 0; i < res.size(); i++)
    {
        System.out.print(res.get(i) + " ");
    }
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

def find_sequence(n):

    # Base Case
    if n == 1:
        return 1, -1

    # Recursive Call for n-1
    ans = (find_sequence(n - 1)[0] + 1, n - 1)

    # Check if n is divisible by 2
    if n % 2 == 0:
        div_by_2 = find_sequence(n // 2)

        if div_by_2[0] < ans[0]:
            ans = (div_by_2[0] + 1, n // 2)

    # Check if n is divisible by 3
    if n % 3 == 0:
        div_by_3 = find_sequence(n // 3)

        if div_by_3[0] < ans[0]:
            ans = (div_by_3[0] + 1, n // 3)

    # Returns a tuple (a, b), where
    # a: Minimum steps to obtain x from 1
    # b: Previous number
    return ans

# Function that find the optimal
# solution
def find_solution(n):
    a, b = find_sequence(n)

    # Print the length
    print(a)

    sequence = []
    sequence.append(n)

    # Exit condition for loop = -1
    # when n has reached 1
    while b != -1:
        sequence.append(b)
        _, b = find_sequence(b)

    # Return the sequence
    # in reverse order
    return sequence[::-1]

# Driver Code

# Given N
n = 5

# Function Call
print(*find_solution(n))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static List<int> find_sequence(int n)
{
  List<int> temp = new List<int>();

  temp.Add(1);
  temp.Add(-1);

  // Base Case
  if (n == 1)
    return temp;

  // Recursive Call for n-1
  List<int> arr = find_sequence(n - 1);
  List<int> ans = new List<int>(n);
  ans.Add(arr[0] + 1);
  ans.Add(n - 1);

  // Check if n is divisible by 2
  if (n % 2 == 0)
  {
    List<int> div_by_2 =
         find_sequence(n / 2);

    if (div_by_2[0] < ans[0])
    {
      ans.Clear();
      ans.Add(div_by_2[0] + 1);
      ans.Add(n / 2);
    }
  }

  // Check if n is divisible
  // by 3
  if (n % 3 == 0)
  {
    List<int> div_by_3 =
         find_sequence(n / 3);

    if (div_by_3[0] < ans[0])
    {
      ans.Clear();
      ans.Add(div_by_3[0] + 1);
      ans.Add(n / 3);
    }
  }

  // Returns a tuple (a, b), where
  // a: Minimum steps to obtain x
  // from 1 b: Previous number
  return ans;
}

// Function that find the optimal
// solution
static List<int> find_solution(int n)
{
  List<int> a = find_sequence(n);

  // Print the length
  Console.WriteLine(a[0]);

  List<int> sequence =
       new List<int>();
  sequence.Add(n);

  // Exit condition for loop = -1
  // when n has reached 1
  while (a[1] != -1)
  {
    sequence.Add(a[1]);
    List<int> arr =
         find_sequence(a[1]);
    a.Insert(1, arr[1]);
  }

  // Return the sequence
  // in reverse order
  sequence.Reverse();
  return sequence;
}

// Driver Code
public static void Main(String []args)
{   
  // Given N
  int n = 5;

  // Function call
  List<int> res = find_solution(n);

  for(int i = 0; i < res.Count; i++)
  {
    Console.Write(res[i] + " ");
  }
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

function find_sequence(n)
{

    // Base Case
    if (n == 1)
        return [1, -1];

    // Recursive Call for n-1
    var arr = find_sequence(n - 1);
    var ans = [arr[0] + 1, n - 1];

    // Check if n is divisible by 2
    if (n % 2 == 0)
    {
        var div_by_2 = find_sequence(n / 2);

        if (div_by_2[0] < ans[0])
            ans = [div_by_2[0] + 1, n / 2];
    }

    // Check if n is divisible by 3
    if (n % 3 == 0)
    {
        var div_by_3 = find_sequence(n / 3);

        if (div_by_3[0] < ans[0])
            var ans = [div_by_3[0] + 1, n / 3];
    }

    // Returns a tuple (a, b), where
    // a: Minimum steps to obtain x from 1
    // b: Previous number
    return ans;
}

// Function that find the optimal
// solution
function find_solution(n)
{
    var a = find_sequence(n);

    // Print the length
    document.write( a[0] + "<br>");

    var sequence = [];
    sequence.push(n);

    //Exit condition for loop = -1
    //when n has reached 1
    while (a[1] != -1)
    {
        sequence.push(a[1]);
        var arr = find_sequence(a[1]);
        a[1] = arr[1];
    }

    // Return the sequence
    // in reverse order
    sequence.reverse();

    return sequence;
}

// Driver Code
// Given N
var n = 5;

// Function call
var i = find_solution(n);

i.forEach(j => {
    document.write(j + " ");
});

</script>
```

**Output:** 

```
4
1 2 4 5
```

***时间复杂度:** T(N) = T(N-1) + T(N/2) + T(N/3)，其中 N 为给定整数。该算法导致指数时间复杂度。*

***辅助空间:** O(1)*

**用** [**记忆**](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/) **方法递归:**上述方法可以通过记忆重叠子问题来优化。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the sequence
# with given operations
def find_sequence(n, map):

    # Base Case
    if n == 1:
        return 1, -1

    # Check if the subproblem
    # is already computed or not
    if n in map:
        return map[n]

    # Recursive Call for n-1
    ans = (find_sequence(n - 1, map)[0]\
    + 1, n - 1)

    # Check if n is divisible by 2
    if n % 2 == 0:
        div_by_2 = find_sequence(n // 2, map)

        if div_by_2[0] < ans[0]:
            ans = (div_by_2[0] + 1, n // 2)

    # Check if n is divisible by 3
    if n % 3 == 0:
        div_by_3 = find_sequence(n // 3, map)

        if div_by_3[0] < ans[0]:
            ans = (div_by_3[0] + 1, n // 3)

    # Memoize
    map[n] = ans

    # Returns a tuple (a, b), where
    # a: Minimum steps to obtain x from 1
    # b: Previous state
    return ans

# Function to check if a sequence can
# be obtained with given operations
def find_solution(n):

    # Stores the computed
    # subproblems
    map = {}
    a, b = find_sequence(n, map)

    # Return a sequence in
    # reverse order
    print(a)
    sequence = []
    sequence.append(n)

    # If n has reached 1
    while b != -1:
        sequence.append(b)
        _, b = find_sequence(b, map)

    # Return sequence in reverse order
    return sequence[::-1]

# Driver Code

# Given N
n = 5

# Function Call
print(*find_solution(n))
```

**Output:** 

```
4
1 2 4 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**迭代** [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) **方法:**通过使用迭代 DP 方法可以进一步优化上述方法。按照以下步骤解决问题:

1.  创建一个数组 **dp[]** ，以存储通过三个可用操作计算 1 到 **N** 所需的最小序列长度。
2.  一旦计算出 dp[]数组，通过从 **N** 到 1 遍历 **dp[]** 数组获得序列。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate
// the minimum sequence
void find_sequence(int n)
{

  // Stores the values for the
  // minimum length of sequences
  int dp[n + 1];
  memset(dp, 0, sizeof(dp));

  // Base Case
  dp[1] = 1;

  // Loop to build up the dp[]
  // array from 1 to n
  for(int i = 1; i < n + 1; i++)
  {
    if (dp[i] != 0)
    {

      // If i + 1 is within limits
      if (i + 1 < n + 1 &&
          (dp[i + 1] == 0 ||
           dp[i + 1] > dp[i] + 1))
      {

        // Update the state of i + 1
        // in dp[] array to minimum
        dp[i + 1] = dp[i] + 1;
      }

      // If i * 2 is within limits
      if (i * 2 < n + 1 &&
          (dp[i * 2] == 0 ||
           dp[i * 2] > dp[i] + 1))
      {

        // Update the state of i * 2
        // in dp[] array to minimum
        dp[i * 2] = dp[i] + 1;
      }

      // If i * 3 is within limits
      if (i * 3 < n + 1 &&
          (dp[i * 3] == 0 ||
           dp[i * 3] > dp[i] + 1))
      {

        // Update the state of i * 3
        // in dp[] array to minimum
        dp[i * 3] = dp[i] + 1;
      }
    }
  }

  // Generate the sequence by
  // traversing the array
  vector<int> sequence;
  while (n >= 1)
  {

    // Append n to the sequence
    sequence.push_back(n);

    // If the value of n in dp
    // is obtained from n - 1:
    if (dp[n - 1] == dp[n] - 1)
    {
      n--;
    }

    // If the value of n in dp[]
    // is obtained from n / 2:
    else if (n % 2 == 0 &&
             dp[(int)floor(n / 2)] == dp[n] - 1)
    {
      n = (int)floor(n / 2);
    }

    // If the value of n in dp[]
    // is obtained from n / 3:
    else if (n % 3 == 0 &&
             dp[(int)floor(n / 3)] == dp[n] - 1)
    {
      n = (int)floor(n / 3);
    }
  }

  // Print the sequence
  // in reverse order
  reverse(sequence.begin(), sequence.end());

  // Print the length of
  // the minimal sequence
  cout << sequence.size() << endl;
  for(int i = 0; i < sequence.size(); i++)
  {
    cout << sequence[i] << " ";
  }
}

// Driver code
int main()
{

  // Given Number N
  int n = 5;

  // Function Call
  find_sequence(n);

  return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to generate
// the minimum sequence
public static void find_sequence(int n)
{

    // Stores the values for the
    // minimum length of sequences
    int[] dp = new int[n + 1];
    Arrays.fill(dp, 0);

    // Base Case
    dp[1] = 1;

    // Loop to build up the dp[]
    // array from 1 to n
    for(int i = 1; i < n + 1; i++)
    {
        if (dp[i] != 0)
        {

            // If i + 1 is within limits
            if (i + 1 < n + 1 &&
            (dp[i + 1] == 0 ||
             dp[i + 1] > dp[i] + 1))
            {

                // Update the state of i + 1
                // in dp[] array to minimum
                dp[i + 1] = dp[i] + 1;
            }

            // If i * 2 is within limits
            if (i * 2 < n + 1 &&
            (dp[i * 2] == 0 ||
             dp[i * 2] > dp[i] + 1))
            {

                // Update the state of i * 2
                // in dp[] array to minimum
                dp[i * 2] = dp[i] + 1;
            }

            // If i * 3 is within limits
            if (i * 3 < n + 1 &&
            (dp[i * 3] == 0 ||
             dp[i * 3] > dp[i] + 1))
            {

                // Update the state of i * 3
                // in dp[] array to minimum
                dp[i * 3] = dp[i] + 1;
            }
        }
    }

    // Generate the sequence by
    // traversing the array
    List<Integer> sequence = new ArrayList<Integer>();
    while (n >= 1)
    {

        // Append n to the sequence
        sequence.add(n);

        // If the value of n in dp
        // is obtained from n - 1:
        if (dp[n - 1] == dp[n] - 1)
        {
            n--;
        }

        // If the value of n in dp[]
        // is obtained from n / 2:
        else if (n % 2 == 0 &&
         dp[(int)Math.floor(n / 2)] == dp[n] - 1)
        {
            n = (int)Math.floor(n / 2);
        }

        // If the value of n in dp[]
        // is obtained from n / 3:
        else if (n % 3 == 0 &&
         dp[(int)Math.floor(n / 3)] == dp[n] - 1)
        {
            n = (int)Math.floor(n / 3);
        }
    }

    // Print the sequence
    // in reverse order
    Collections.reverse(sequence);

    // Print the length of
    // the minimal sequence
    System.out.println(sequence.size());
    for(int i = 0; i < sequence.size(); i++)
    {
        System.out.print(sequence.get(i) + " ");
    }
}

// Driver Code
public static void main (String[] args)
{

    // Given Number N
    int n = 5;

    // Function Call
    find_sequence(n);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to generate
# the minimum sequence
def find_sequence(n):

    # Stores the values for the
    # minimum length of sequences
    dp = [0 for _ in range(n + 1)]

    # Base Case
    dp[1] = 1

    # Loop to build up the dp[]
    # array from 1 to n
    for i in range(1, n + 1):

        if dp[i] != 0:

            # If i + 1 is within limits
            if i + 1 < n + 1 and (dp[i + 1] == 0 \
            or dp[i + 1] > dp[i] + 1):

                # Update the state of i + 1
                # in dp[] array to minimum
                dp[i + 1] = dp[i] + 1

            # If i * 2 is within limits
            if i * 2 < n + 1 and (dp[i * 2] == 0 \
            or dp[i * 2] > dp[i] + 1):

                # Update the state of i * 2
                # in dp[] array to minimum
                dp[i * 2] = dp[i] + 1

            # If i * 3 is within limits
            if i * 3 < n + 1 and (dp[i * 3] == 0 \
            or dp[i * 3] > dp[i] + 1):

                # Update the state of i * 3
                # in dp[] array to minimum
                dp[i * 3] = dp[i] + 1

    # Generate the sequence by
    # traversing the array
    sequence = []
    while n >= 1:

        # Append n to the sequence
        sequence.append(n)

        # If the value of n in dp
        # is obtained from n - 1:
        if dp[n - 1] == dp[n] - 1:
            n = n - 1

        # If the value of n in dp[]
        # is obtained from n / 2:
        elif n % 2 == 0 \
        and dp[n // 2] == dp[n] - 1:
            n = n // 2

        # If the value of n in dp[]
        # is obtained from n / 3:
        elif n % 3 == 0 \
        and dp[n // 3] == dp[n] - 1:
            n = n // 3

    # Return the sequence
    # in reverse order
    return sequence[::-1]

# Driver Code

# Given Number N
n = 5

# Function Call
sequence = find_sequence(n)

# Print the length of
# the minimal sequence
print(len(sequence))

# Print the sequence
print(*sequence)
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to generate
  // the minimum sequence
  public static void find_sequence(int n)
  {

    // Stores the values for the
    // minimum length of sequences
    int[] dp = new int[n + 1];
    Array.Fill(dp, 0);

    // Base Case
    dp[1] = 1;

    // Loop to build up the dp[]
    // array from 1 to n
    for(int i = 1; i < n + 1; i++)
    {
      if(dp[i] != 0)
      {

        // If i + 1 is within limits
        if(i + 1 < n + 1 &&
           (dp[i + 1] == 0 ||
            dp[i + 1] > dp[i] + 1))
        {

          // Update the state of i + 1
          // in dp[] array to minimum
          dp[i + 1] = dp[i] + 1;
        }

        // If i * 2 is within limits
        if(i * 2 < n + 1 &&
           (dp[i * 2] == 0 ||
            dp[i * 2] > dp[i] + 1))
        {

          // Update the state of i * 2
          // in dp[] array to minimum
          dp[i * 2] = dp[i] + 1;
        }

        // If i * 3 is within limits
        if(i * 3 < n + 1 &&
           (dp[i * 3] == 0 ||
            dp[i * 3] > dp[i] + 1))
        {

          // Update the state of i * 3
          // in dp[] array to minimum
          dp[i * 3] = dp[i] + 1;
        }       
      }
    }

    // Generate the sequence by
    // traversing the array
    List<int> sequence = new List<int>();
    while(n >= 1)
    {

      // Append n to the sequence
      sequence.Add(n);

      // If the value of n in dp
      // is obtained from n - 1:
      if(dp[n - 1] == dp[n] - 1)
      {
        n--;
      }

      // If the value of n in dp[]
      // is obtained from n / 2:
      else if(n % 2 == 0 &&
              dp[(int)Math.Floor((decimal)n / 2)] ==
              dp[n] - 1)
      {
        n = (int)Math.Floor((decimal)n / 2);
      }

      // If the value of n in dp[]
      // is obtained from n / 3:
      else if(n % 3 == 0 &&
              dp[(int)Math.Floor((decimal)n / 3)] ==
              dp[n] - 1)
      {
        n = (int)Math.Floor((decimal)n / 3);
      }

    }

    // Print the sequence
    // in reverse order
    sequence.Reverse();

    // Print the length of
    // the minimal sequence
    Console.WriteLine(sequence.Count);
    for(int i = 0; i < sequence.Count; i++)
    {
      Console.Write(sequence[i] + " ");
    }
  }

  // Driver Code
  static public void Main ()
  {

    // Given Number N
    int n = 5;

    // Function Call
    find_sequence(n);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to generate
// the minimum sequence
function find_sequence(n)
{
    // Stores the values for the
    // minimum length of sequences
    let dp = new Array(n + 1);
    for(let i=0;i<n+1;i++)
    {
        dp[i]=0;
    }

    // Base Case
    dp[1] = 1;

    // Loop to build up the dp[]
    // array from 1 to n
    for(let i = 1; i < n + 1; i++)
    {
        if (dp[i] != 0)
        {

            // If i + 1 is within limits
            if (i + 1 < n + 1 &&
            (dp[i + 1] == 0 ||
             dp[i + 1] > dp[i] + 1))
            {

                // Update the state of i + 1
                // in dp[] array to minimum
                dp[i + 1] = dp[i] + 1;
            }

            // If i * 2 is within limits
            if (i * 2 < n + 1 &&
            (dp[i * 2] == 0 ||
             dp[i * 2] > dp[i] + 1))
            {

                // Update the state of i * 2
                // in dp[] array to minimum
                dp[i * 2] = dp[i] + 1;
            }

            // If i * 3 is within limits
            if (i * 3 < n + 1 &&
            (dp[i * 3] == 0 ||
             dp[i * 3] > dp[i] + 1))
            {

                // Update the state of i * 3
                // in dp[] array to minimum
                dp[i * 3] = dp[i] + 1;
            }
        }
    }

    // Generate the sequence by
    // traversing the array
    let sequence = [];
    while (n >= 1)
    {

        // Append n to the sequence
        sequence.push(n);

        // If the value of n in dp
        // is obtained from n - 1:
        if (dp[n - 1] == dp[n] - 1)
        {
            n--;
        }

        // If the value of n in dp[]
        // is obtained from n / 2:
        else if (n % 2 == 0 &&
         dp[Math.floor(n / 2)] == dp[n] - 1)
        {
            n = Math.floor(n / 2);
        }

        // If the value of n in dp[]
        // is obtained from n / 3:
        else if (n % 3 == 0 &&
         dp[Math.floor(n / 3)] == dp[n] - 1)
        {
            n = Math.floor(n / 3);
        }
    }

    // Print the sequence
    // in reverse order
    sequence.reverse();

    // Print the length of
    // the minimal sequence
    document.write(sequence.length+"<br>");
    for(let i = 0; i < sequence.length; i++)
    {
        document.write(sequence[i] + " ");
    }
}

// Driver Code
let n = 5;

// Function Call
find_sequence(n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
1 3 4 5
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*