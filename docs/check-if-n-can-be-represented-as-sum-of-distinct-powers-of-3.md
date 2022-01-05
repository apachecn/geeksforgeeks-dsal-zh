# 检查 N 是否可以表示为 3 的不同幂的和

> 原文:[https://www . geesforgeks . org/check-if-n-可以表示为 3 的不同幂的和/](https://www.geeksforgeeks.org/check-if-n-can-be-represented-as-sum-of-distinct-powers-of-3/)

给定一个正整数 **N** ，任务是检查给定的数字 **N** 是否可以表示为 **3** 的**相异**T6】次幂的和。如果发现是真的，则打印**“是”**。否则，**“否”**。

**示例:**

> **输入:** N = 28
> **输出:** *是*
> **说明:**
> 数字 N(= 28)可以表示为(1 + 7) = (3 <sup>0</sup> + 3 <sup>3</sup> ，是一个完美的幂 2。
> 
> **输入:**N = 6
> T3】输出:否

**方法:**解决给定问题的最简单方法是[生成所有**不同幂 **3** 的所有可能排列**](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，如果存在这样的组合，其和是 **3** 的[完美幂。正如**3<sup>15</sup>>10<sup>7</sup>**一样，也只有 **16** 两种截然不同的权力，即**【0，15】**。](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to try all permutations
// of distinct powers
bool PermuteAndFind(vector<long> power, int idx,
                    long SumSoFar, int target)
{
    // Base Case
    if (idx == power.size()) {

        // If the distinct powers
        // sum is obtained
        if (SumSoFar == target)
            return true;

        // Otherwise
        return false;
    }

    // If current element not selected
    // in power[]
    bool select
        = PermuteAndFind(power, idx + 1, SumSoFar, target);

    // If current element selected in
    // power[]
    bool notselect = PermuteAndFind(
        power, idx + 1, SumSoFar + power[idx], target);

    // Return 1 if any permutation
    // found
    return (select || notselect);
}

// Function to check the N can be
// represented as the sum of the
// distinct powers of 3
void DistinctPowersOf3(int N)
{
    // Stores the all distincts powers
    // of three to [0, 15]
    vector<long> power(16);
    power[0] = 1;
    for (int i = 1; i < 16; i++)
        power[i] = 3 * power[i - 1];

    // Function Call
    bool found = PermuteAndFind(power, 0, 0L, N);

    // print
    if (found == true) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driven Code
int main()
{
    int N = 91;
    DistinctPowersOf3(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to try all permutations
    // of distinct powers
    public static boolean PermuteAndFind(int[] power, int idx,
                                         int SumSoFar, int target)
    {
        // Base Case
        if (idx == power.length)
        {

            // If the distinct powers
            // sum is obtained
            if (SumSoFar == target)
                return true;

            // Otherwise
            return false;
        }

        // If current element not selected
        // in power[]
        boolean select = PermuteAndFind(power, idx + 1, SumSoFar, target);

        // If current element selected in
        // power[]
        boolean notselect = PermuteAndFind(power, idx + 1, SumSoFar + power[idx], target);

        // Return 1 if any permutation
        // found
        return (select || notselect);
    }

    // Function to check the N can be
    // represented as the sum of the
    // distinct powers of 3
    public static void DistinctPowersOf3(int N)
    {

        // Stores the all distincts powers
        // of three to [0, 15]
        int[] power = new int[16];
        power[0] = 1;
        for (int i = 1; i < 16; i++)
            power[i] = 3 * power[i - 1];

        // Function Call
        boolean found = PermuteAndFind(power, 0, 0, N);

        // print
        if (found == true) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }

    // Driven Code
    public static void main(String args[]) {
        int N = 91;
        DistinctPowersOf3(N);
    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to try all permutations
# of distinct powers
def PermuteAndFind(power, idx, SumSoFar, target):

    # Base Case
    if (idx == len(power)):

        # If the distinct powers
        # sum is obtained
        if (SumSoFar == target):
            return True

        # Otherwise
        return False

    # If current element not selected
    # in power[]
    select = PermuteAndFind(power, idx + 1,
                            SumSoFar, target)

    # If current element selected in
    # power[]
    notselect = PermuteAndFind(power, idx + 1,
                                 SumSoFar + power[idx],
                                 target)

    # Return 1 if any permutation
    # found
    return(select or notselect)

# Function to check the N can be
# represented as the sum of the
# distinct powers of 3
def DistinctPowersOf3(N):

    # Stores the all distincts powers
    # of three to[0, 15]
    power = [0 for x in range(16)]
    power[0] = 1

    for i in range(1, 16):
        power[i] = 3 * power[i - 1]

    # Function Call
    found = PermuteAndFind(power, 0, 0, N)

    # Print
    if (found == True):
        print("Yes")
    else:
        print("No")

# Driver Code
N = 91

DistinctPowersOf3(N)

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to try all permutations
    // of distinct powers
    public static bool PermuteAndFind(int[] power, int idx,
                                         int SumSoFar, int target)
    {
        // Base Case
        if (idx == power.Length)
        {

            // If the distinct powers
            // sum is obtained
            if (SumSoFar == target)
                return true;

            // Otherwise
            return false;
        }

        // If current element not selected
        // in power[]
        bool select = PermuteAndFind(power, idx + 1, SumSoFar, target);

        // If current element selected in
        // power[]
        bool notselect = PermuteAndFind(power, idx + 1, SumSoFar + power[idx], target);

        // Return 1 if any permutation
        // found
        return (select || notselect);
    }

    // Function to check the N can be
    // represented as the sum of the
    // distinct powers of 3
    public static void DistinctPowersOf3(int N)
    {

        // Stores the all distincts powers
        // of three to [0, 15]
        int[] power = new int[16];
        power[0] = 1;
        for (int i = 1; i < 16; i++)
            power[i] = 3 * power[i - 1];

        // Function Call
        bool found = PermuteAndFind(power, 0, 0, N);

        // print
        if (found == true) {
            Console.Write("Yes");
        } else {
            Console.Write("No");
        }
    }

// Driver Code
public static void Main()
{
    int N = 91;
    DistinctPowersOf3(N);
}
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to try all permutations
// of distinct powers
function PermuteAndFind(power, idx, SumSoFar, target) {
  // Base Case
  if (idx == power.length) {
    // If the distinct powers
    // sum is obtained
    if (SumSoFar == target) return true;

    // Otherwise
    return false;
  }

  // If current element not selected
  // in power[]
  let select = PermuteAndFind(power, idx + 1, SumSoFar, target);

  // If current element selected in
  // power[]
  let notselect = PermuteAndFind(power, idx + 1, SumSoFar + power[idx], target);

  // Return 1 if any permutation
  // found
  return select || notselect;
}

// Function to check the N can be
// represented as the sum of the
// distinct powers of 3
function DistinctPowersOf3(N) {
  // Stores the all distincts powers
  // of three to [0, 15]
  let power = new Array(16);
  power[0] = 1;
  for (let i = 1; i < 16; i++) power[i] = 3 * power[i - 1];

  // Function Call
  let found = PermuteAndFind(power, 0, 0, N);

  // print
  if (found == true) {
    document.write("Yes");
  } else {
    document.write("No");
  }
}

// Driven Code

let N = 91;
DistinctPowersOf3(N);

</script>
```

**Output**

```
Yes
```

***时间复杂度:**T3】O(2<sup>N</sup>)
*T8】辅助空间:T10】O(2<sup>N</sup>**

**另一种方法:**通过观察**三元**中的 **N** 形成( **基 3** )也可以优化上述方法。每个数字是 **3 <sup>i</sup>** ，**三进制数(N)** 是它们的和。

要拥有 **3** 的**不同**次方，以三进制形式总结为 **N、**，则 **i <sup>th</sup>** 数字可以是 **0，1 或 2** (二进制为 0 和 1)。因此，在**和**位置 **:** 每个数字可以有三种情况

*   数字**可以是 **0** 即 **N** 中有**无**T6】3<sup>I</sup>T9】号。**
*   数字**可以是 **1** 即 **N** 中有**一**T6】3<sup>I</sup>T9】号。**
*   数字**不能是 **2** ，因为 3 <sup>中有**2**</sup>和**，所以**不是截然不同的**。

按照以下步骤解决问题:

*   重复直到 **N** 变为 **0** 并执行以下步骤:
    *   如果 **N%3** 的值为 **2** ，则打印**“否”**。
    *   否则，用 **3** 除 **N** 。
*   完成上述步骤后，如果 **N** 的值为 **0** ，则打印**“是”**。否则，**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether the given
// N can be represented as the sum of
// the distinct powers of 3
void DistinctPowersOf3(int N)
{
    // Iterate until N is non-zero
    while (N > 0) {

        // Termination Condition
        if (N % 3 == 2) {
            cout << "No";
            return;
        }

        // Right shift ternary bits
        // by 1 for the next digit
        N /= 3;
    }

    // If N can be expressed as the
    // sum of perfect powers of 3
    cout << "Yes";
}

// Driver Code
int main()
{
    int N = 91;

    DistinctPowersOf3(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to check whether the given
// N can be represented as the sum of
// the distinct powers of 3
public static void DistinctPowersOf3(int N)
{

    // Iterate until N is non-zero
    while (N > 0) {

        // Termination Condition
        if (N % 3 == 2) {
            System.out.println("No");
            return;
        }

        // Right shift ternary bits
        // by 1 for the next digit
        N /= 3;
    }

    // If N can be expressed as the
    // sum of perfect powers of 3
    System.out.println("Yes");
}

// Driver Code
public static void main(String args[])
{
    int N = 91;

    DistinctPowersOf3(N);
}
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check whether the given
# N can be represented as the sum of
# the distinct powers of 3
def DistinctPowersOf3(N):

    # Iterate until N is non-zero
    while (N > 0):

        # Termination Condition
        if (N % 3 == 2):
            cout << "No"
            return

        # Right shift ternary bits
        # by 1 for the next digit
        N //= 3

    # If N can be expressed as the
    # sum of perfect powers of 3
    print ("Yes")

# Driver Code
if __name__ == '__main__':
    N = 91

    DistinctPowersOf3(N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to check whether the given
// N can be represented as the sum of
// the distinct powers of 3
static void DistinctPowersOf3(int N)
{

    // Iterate until N is non-zero
    while (N > 0) {

        // Termination Condition
        if (N % 3 == 2) {
            Console.Write("No");
            return;
        }

        // Right shift ternary bits
        // by 1 for the next digit
        N /= 3;
    }

    // If N can be expressed as the
    // sum of perfect powers of 3
    Console.Write("Yes");
}

// Driver Code
public static void Main()
{
    int N = 91;
    DistinctPowersOf3(N);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check whether the given
// N can be represented as the sum of
// the distinct powers of 3
function DistinctPowersOf3(N)
{

    // Iterate until N is non-zero
    while (N > 0) {

        // Termination Condition
        if (N % 3 == 2)
        {
            document.write("No");
            return;
        }

        // Right shift ternary bits
        // by 1 for the next digit
        N = Math.floor(N/ 3);
    }

    // If N can be expressed as the
    // sum of perfect powers of 3
    document.write("Yes");
}

// Driver Code
let N = 91;
DistinctPowersOf3(N);

// This code is contributed by patel2127
</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(log<sub>3</sub>N)*
*T8】辅助空间: O(1)*