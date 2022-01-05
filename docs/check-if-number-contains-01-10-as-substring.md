# 检查给定的数字在其二进制表示中是否只包含“01”和“10”作为子串

> 原文:[https://www . geesforgeks . org/check-if-number-contains-01-10-as-substring/](https://www.geeksforgeeks.org/check-if-number-contains-01-10-as-substring/)

给定一个数字 **N** ，任务是检查数字 **N** 的二进制表示是否只有**“01”**和**“10”**作为[子串](https://www.geeksforgeeks.org/substring-in-cpp/)。如果发现是真的，则打印**“是”**。否则，打印**“否”**。
**举例:**

> **输入:** N = 5
> **输出:**是
> **解释:**
> (5) <sub>10</sub> 是(101) <sub>2</sub> ，其中只包含“01”和“10”作为子串。
> **输入:** N = 11
> **输出:** No
> **解释:**
> (11) <sub>10</sub> 是(1011) <sub>2</sub> 其中只包含“11”一个子串。

**方法:**给定的问题可以使用以下观察结果来解决:

*   因为[子串](https://www.geeksforgeeks.org/substring-in-cpp/)必须包含**“01”**和**“10”**。因此，二进制表示交替包含 **1** 和 **0** 。
*   对于交替包含 **0** 和 **1** 的二进制表示，可以观察到以下模式:

> 2, 5, 10, 21, …

*   上述模式的形式为 **2 * x** 和 **(4 * x + 1)** ，因此该系列的最后一个术语为 **x** 。

从上面的观察来看，想法是使用上面的模式生成给定的序列，并检查模式中是否存在给定的数字。如果发现为真，则打印**“是”**。否则，打印**“否”**。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

vector<int> Ans;

// Function to generate all numbers
// having "01" and "10" as a substring
void populateNumber()
{
    // Insert 2 and 5
    Ans.push_back(2);
    Ans.push_back(5);

    long long int x = 5;

    // Iterate till x is 10 ^ 15
    while (x < 1000000000001) {

        // Multiply x by 2
        x *= 2;
        Ans.push_back(x);

        // Update x as x*2  + 1
        x = x * 2 + 1;

        Ans.push_back(x);
    }
}

// Function to check if binary representation
// of N contains only "01" and "10" as substring
string checkString(long long int N)
{
    // Function Call to generate all
    // such numbers
    populateNumber();

    // Check if a number N
    // exists in Ans[] or not
    for (auto& it : Ans) {

        // If the number exists
        if (it == N) {
            return "Yes";
        }
    }

    // Otherwise
    return "No";
}

// Driver Code
int main()
{
    long long int N = 5;

    // Function Call
    cout << checkString(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{
  static int N = 200000;

  static long Ans[] = new long [200000];
  static int index = 0;

  // Function to generate all numbers
  // having "01" and "10" as a substring
  static void populateNumber()
  {
    // Insert 2 and 5
    Ans[index++] = (2);
    Ans[index++] = (5);
    long x = 5;
    long inf = 1000000000001L;

    // Iterate till x is 10 ^ 15
    while (x < inf)
    {

      // Multiply x by 2
      x *= 2;
      Ans[index++] = (x);

      // Update x as x*2  + 1
      x = x * 2 + 1;

      Ans[index++] = (x);
    }
  }
  // Function to check if binary representation
  // of N contains only "01" and "10" as substring
  static void checkString(int N)
  {
    // Function Call to generate all
    // such numbers
    populateNumber();

    // Check if a number N
    // exists in Ans[] or not
    for (int i = 0; i < index; i++)
    {

      // If the number exists
      if (Ans[i] == N)
      {
        System.out.println("YES");
        return;
      }
    }
    System.out.println("NO");

  }

  // Driver Code
  public static void main(String[] args)
  {
    N = 5;
    checkString(N);
  }
}

// This code is contributed by amreshkumar3.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
Ans = []

# Function to generate all numbers
# having "01" and "10" as a substring
def populateNumber() :

    # Insert 2 and 5
    Ans.append(2)
    Ans.append(5)
    x = 5

    # Iterate till x is 10 ^ 15
    while (x < 1000000000001) :

        # Multiply x by 2
        x *= 2
        Ans.append(x)

        # Update x as x*2  + 1
        x = x * 2 + 1
        Ans.append(x)

# Function to check if binary representation
# of N contains only "01" and "10" as substring
def checkString(N) :

    # Function Call to generate all
    # such numbers
    populateNumber()

    # Check if a number N
    # exists in Ans[] or not
    for it in Ans :

        # If the number exists
        if (it == N) :
            return "Yes"

    # Otherwise
    return "No"

# Driver Code
N = 5

# Function Call
print(checkString(N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{
  static int N = 200000;
  static long []Ans = new long [200000];
  static int index = 0;

  // Function to generate all numbers
  // having "01" and "10" as a substring
  static void populateNumber()
  {

    // Insert 2 and 5
    Ans[index++] = (2);
    Ans[index++] = (5);
    long x = 5;
    long inf = 1000000000001L;

    // Iterate till x is 10 ^ 15
    while (x < inf)
    {

      // Multiply x by 2
      x *= 2;
      Ans[index++] = (x);

      // Update x as x*2  + 1
      x = x * 2 + 1;
      Ans[index++] = (x);
    }
  }

  // Function to check if binary representation
  // of N contains only "01" and "10" as substring
  static void checkString(int N)
  {

    // Function Call to generate all
    // such numbers
    populateNumber();

    // Check if a number N
    // exists in Ans[] or not
    for (int i = 0; i < index; i++)
    {

      // If the number exists
      if (Ans[i] == N)
      {
        Console.WriteLine("YES");
        return;
      }
    }
    Console.WriteLine("NO");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    N = 5;
    checkString(N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// javascript Program to implement
// the above approach

  var N = 200000;

  var Ans = Array.from({length: N}, (_, i) => 0);
  var index = 0;

  // Function to generate all numbers
  // having "01" and "10" as a substring
  function populateNumber()
  {
    // Insert 2 and 5
    Ans[index++] = (2);
    Ans[index++] = (5);
    var x = 5;
    var inf = 1000000000001;

    // Iterate till x is 10 ^ 15
    while (x < inf)
    {

      // Multiply x by 2
      x *= 2;
      Ans[index++] = (x);

      // Update x as x*2  + 1
      x = x * 2 + 1;

      Ans[index++] = (x);
    }
  }
  // Function to check if binary representation
  // of N contains only "01" and "10" as substring
  function checkString(N)
  {
    // Function Call to generate all
    // such numbers
    populateNumber();

    // Check if a number N
    // exists in Ans or not
    for (i = 0; i < index; i++)
    {

      // If the number exists
      if (Ans[i] == N)
      {
        document.write("YES");
        return;
      }
    }
    document.write("NO");

  }
  // Driver Code
  N = 5;
  checkString(N);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*