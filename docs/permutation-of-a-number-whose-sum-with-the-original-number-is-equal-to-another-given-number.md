# 与原数之和等于另一个给定数的数的排列

> 原文:[https://www . geeksforgeeks . org/一个数的排列，其与原始数的和等于另一个给定数/](https://www.geeksforgeeks.org/permutation-of-a-number-whose-sum-with-the-original-number-is-equal-to-another-given-number/)

给定两个整数 **A** 和 **C** ，任务是检查数字 **A** 是否存在排列，使得数字 **A** 与其排列之和等于 **C** 。

**示例:**

> **输入:** A = 133，C = 446
> **输出:**是
> **说明:**A 的一个排列是 313。所以 sum = 133 + 313 = 446，等于 c。
> 
> **输入:** A = 200，C = 201
> T3】输出:否

**天真法:**解决问题最简单的方法是[生成数字**A**T5 的所有排列，并与 **A** 的原值相加。现在，检查它们的总和是否等于 **C** 。](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)

***时间复杂度:** O((日志 <sub>10</sub> A)！)*
***辅助空间:** O(1)*

**高效法:**优化上述方法，思路是从 **C** 中减去 **A** 的值，检查是否存在 **A** 的置换，该置换等于 **C** 和 **A** 的差值。按照以下步骤解决问题:

*   从 **C** 中减去 **A** ，检查 **C** 是否小于 **0** 。如果发现是真的，那么打印“否”。
*   否则，请执行以下步骤:
    *   [将 **A** 转换为它的等价字符串表示](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)并将其存储在一个变量中，比如 **S** 。
    *   将 **C** 转换为其等效的字符串表示形式，并将其存储在一个变量中，比如 **K** 。
    *   [对新生成的字符串](https://www.geeksforgeeks.org/sort-c-stl/) **S** 和 **K** 进行排序。
    *   如果 **S** 等于 **K** ，则随排列打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there
// exists a permutation of a number
// A whose sum with A results to C
void checkPermutation(int a, int c)
{
    // Subtract a from c
    c -= a;

    // Check if c is less than 0
    if (c <= 0) {

        // If true, print "No"
        cout << "No";
        return;
    }

    // Otherwise, convert a to its
    // equivalent string
    string s = to_string(a);

    // convert c to its
    // equivalent string
    string k = to_string(c);

    // Sort string s
    sort(s.begin(), s.end());

    // Sort string k
    sort(k.begin(), k.end());

    // If both strings are equal,
    // then print "Yes"
    if (k == s) {
        cout << "Yes\n"
             << c;
    }

    // Otherwise, print "No"
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int A = 133, C = 446;
    checkPermutation(A, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if there
// exists a permutation of a number
// A whose sum with A results to C
static void checkPermutation(int a, int c)
{

    // Subtract a from c
    c -= a;

    // Check if c is less than 0
    if (c <= 0)
    {

        // If true, print "No"
        System.out.println("No");
        return;
    }

    // Otherwise, convert a to its
    // equivalent string
    String s = sortString(Integer.toString(a));

    // Convert c to its
    // equivalent string
    String k = sortString(Integer.toString(c));

    // If both strings are equal,
    // then print "Yes"
    if (k.equals(s))
    {
        System.out.println("Yes");
        System.out.println(c);
    }

    // Otherwise, print "No"
    else
    {
        System.out.println("No");
    }
}

// Method to sort a string alphabetically
public static String sortString(String inputString)
{

    // Convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Driver code
public static void main(String[] args)
{
    int A = 133, C = 446;

    checkPermutation(A, C);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there
# exists a permutation of a number
# A whose sum with A results to C
def checkPermutation(a, c):
    # Subtract a from c
    c -= a

    # Check if c is less than 0
    if (c <= 0):
        # If true, print "No"
        print("No")
        return

    # Otherwise, convert a to its
    # equivalent string
    s = str(a)

    # convert c to its
    # equivalent string
    k = str(c)

    res = ''.join(sorted(s))

    # Sort string s
    s = str(res)

    # Sort string k
    res = ''.join(sorted(k))
    k = str(res)

    # If both strings are equal,
    # then print "Yes"
    if (k == s):
        print("Yes")
        print(c)

    # Otherwise, print "No"
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    A = 133
    C = 446
    checkPermutation(A, C)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to check if there
  // exists a permutation of a number
  // A whose sum with A results to C
  static void checkPermutation(int a, int c)
  {

    // Subtract a from c
    c -= a;

    // Check if c is less than 0
    if (c <= 0) {

      // If true, print "No"
      Console.Write("No");
      return;
    }

    // Otherwise, convert a to its
    // equivalent string
    string s = a.ToString();

    // convert c to its
    // equivalent string
    string k = c.ToString();

    // Sort string s
    char[] arr = s.ToCharArray();
    Array.Sort(arr);

    // Sort string k
    char[] brr = k.ToCharArray();
    Array.Sort(brr);

    // If both strings are equal,
    // then print "Yes"
    if (String.Join("", brr) == String.Join("", arr)) {
      Console.Write("Yes\n" + c);
    }

    // Otherwise, print "No"
    else {
      Console.WriteLine("No");
    }
  }

  // Driver Code
  public static void Main()
  {
    int A = 133, C = 446;
    checkPermutation(A, C);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if there
// exists a permutation of a number
// A whose sum with A results to C
function checkPermutation(a, c)
{
    // Subtract a from c
    c -= a;

    // Check if c is less than 0
    if (c <= 0) {

        // If true, print "No"
        print("No");
        return;
    }

    // Otherwise, convert a to its
    // equivalent string
    var s = a.toString();

    // convert c to its
    // equivalent string
    var k = c.toString();

    // Sort string s
    s= s.split('').sort((a, b) => a.localeCompare(b)).join('');
   // sort(s);

    // Sort string k
    k = k.split('').sort((a, b) => a.localeCompare(b)).join('');
    //sort(k);

    // If both strings are equal,
    // then print "Yes"
    if (k == s) {
        document.write("Yes" + "<br>" + c);
    }

    // Otherwise, print "No"
    else {
        document.write("No");
    }
}

// Driver Code
    var A = 133, C = 446;
    checkPermutation(A, C);

</script>
```

**Output:** 

```
Yes
313
```

***时间复杂度:**O((log<sub>10</sub>A)* log(log<sub>10</sub>A))*
***辅助空间:** O(log <sub>10</sub> A)*