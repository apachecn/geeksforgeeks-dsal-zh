# 通过给定操作获得的第 n 个字符串中的第 k 个字符

> 原文:[https://www . geeksforgeeks . org/kth-由给定操作获得的第 n 个字符串字符/](https://www.geeksforgeeks.org/kth-character-from-the-nth-string-obtained-by-the-given-operations/)

给定两个正整数 **N** 和 **K** ，任务是通过对字符串 **S** (最初**“A”**)**N**次执行以下操作得到的字符串的 **K <sup>第</sup>** 个字符。

> 每次 I<sup>操作都会生成以下字符串(S<sub>I</sub>):
> S<sub>I</sub>= S<sub>I–1</sub>+' B '+rev(comp(S<sub>I–1</sub>)
> ，其中，
> **comp()** 表示字符串的补码，即 **A** 改为 **B** 和 **B
> 和 **rev()** 返回字符串的反方向。**</sup>

**示例:**

> **输入:** N = 3，K = 1
> **输出:** A
> **解释:**
> 最初，第一次操作后，S<sub>1</sub>=【A】
> 第二次<sup>操作后，S<sub>2</sub>=【ABB】
> 第三次<sup>第</sup>操作后，S<sub>3</sub>=【ABB baab】【T21
> **输入:** N = 2，K = 3
> **输出:** B</sup>

**方法:**想法是使用[递归](https://www.geeksforgeeks.org/recursion/)从先前生成的字符串生成新的字符串，并重复该过程，直到执行 **N** 操作。以下是步骤:

1.  将两个字符串**初始化为“A”，将**初始化为空字符串。****
2.  如果 **N = 1** 则返回上一步，否则执行以下操作。
3.  循环**(N–1)**次，每次更新 curr 为**prev+“B”**。
4.  反转字符串**上一个**。
5.  再次将字符串 **curr** 更新为 **curr + prev** 。
6.  将字符串**上一个**更新为**当前**。
7.  完成上述步骤后，返回字符串**的第**(K–1)个字符****。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return Kth character
// from recursive string
char findKthChar(int n, int k)
{
    string prev = "A";
    string cur = "";

    // If N is 1 then return A
    if (n == 1) {
        return 'A';
    }

    // Iterate a loop and generate
    // the recursive string
    for (int i = 2; i <= n; i++) {

        // Update current string
        cur = prev + "B";

        // Change A to B and B to A
        for (int i = 0;
             i < prev.length(); i++) {

            if (prev[i] == 'A') {
                prev[i] = 'B';
            }
            else {
                prev[i] = 'A';
            }
        }

        // Reverse the previous string
        reverse(prev.begin(), prev.end());
        cur += prev;
        prev = cur;
    }

    // Return the kth character
    return cur[k - 1];
}

// Driver Code
int main()
{
    int N = 4;
    int K = 3;

    cout << findKthChar(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// String reverse
static String reverse(String input)
{
  char[] a = input.toCharArray();
  int l, r = a.length - 1;
  for (l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.valueOf(a);
}

// Function to return Kth character
// from recursive String
static char findKthChar(int n,
                        int k)
{
  String prev = "A";
  String cur = "";

  // If N is 1 then return A
  if (n == 1)
  {
    return 'A';
  }

  // Iterate a loop and generate
  // the recursive String
  for (int j = 2; j <= n; j++)
  {
    // Update current String
    cur = prev + "B";

    // Change A to B and B to A
    for (int i = 0; i < prev.length(); i++)
    {
      if (prev.charAt(i) == 'A')
      {
        prev.replace(prev.charAt(i), 'B');
      }
      else
      {
        prev.replace(prev.charAt(i), 'A');
      }
    }

    // Reverse the previous String
    prev = reverse(prev);
    cur += prev;
    prev = cur;
  }

  // Return the kth character
  return cur.charAt(k);
}

// Driver Code
public static void main(String[] args)
{
  int N = 4;
  int K = 3;
  System.out.print(findKthChar(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return Kth character
# from recursive string
def findKthChar(n, k):

    prev = "A"
    cur = ""

    # If N is 1 then return A
    if (n == 1):
        return 'A'

    # Iterate a loop and generate
    # the recursive string
    for i in range(2, n + 1):

        # Update current string
        cur = prev + "B"

        # Change A to B and B to A
        temp1 = [y for y in prev]

        for i in range(len(prev)):
            if (temp1[i] == 'A'):
                temp1[i] = 'B'
            else:
                temp1[i] = 'A'

        # Reverse the previous string
        temp1 = temp1[::-1]
        prev = "".join(temp1)
        cur += prev
        prev = cur

    # Return the kth character
    return cur[k - 1]

# Driver Code
if __name__ == '__main__':

    N = 4
    K = 3

    print(findKthChar(N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// String reverse
static String reverse(String input)
{
  char[] a = input.ToCharArray();
  int l, r = a.Length - 1;
  for (l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.Join("", a);
}

// Function to return Kth character
// from recursive String
static char findKthChar(int n,
                        int k)
{
  String prev = "A";
  String cur = "";

  // If N is 1 then return A
  if (n == 1)
  {
    return 'A';
  }

  // Iterate a loop and generate
  // the recursive String
  for (int j = 2; j <= n; j++)
  {
    // Update current String
    cur = prev + "B";

    // Change A to B and B to A
    for (int i = 0; i < prev.Length; i++)
    {
      if (prev[i] == 'A')
      {
        prev.Replace(prev[i], 'B');
      }
      else
      {
        prev.Replace(prev[i], 'A');
      }
    }

    // Reverse the previous String
    prev = reverse(prev);
    cur += prev;
    prev = cur;
  }

  // Return the kth character
  return cur[k];
}

// Driver Code
public static void Main(String[] args)
{
  int N = 4;
  int K = 3;
  Console.Write(findKthChar(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // String reverse
    function reverse(input)
    {
      let a = input.split('');
      let l, r = a.length - 1;
      for (l = 0; l < r; l++, r--)
      {
        let temp = a[l];
        a[l] = a[r];
        a[r] = temp;
      }
      return a.join("");
    }

    // Function to return Kth character
    // from recursive String
    function findKthChar(n, k)
    {
      let prev = "A";
      let cur = "";

      // If N is 1 then return A
      if (n == 1)
      {
        return 'A';
      }

      // Iterate a loop and generate
      // the recursive String
      for (let j = 2; j <= n; j++)
      {
        // Update current String
        cur = prev + "B";

        // Change A to B and B to A
        for (let i = 0; i < prev.length; i++)
        {
          if (prev[i] == 'A')
          {
            prev[prev[i]] = 'B';
          }
          else
          {
            prev[prev[i]] = 'A';
          }
        }

        // Reverse the previous String
        prev = reverse(prev);
        cur += prev;
        prev = cur;
      }

      // Return the kth character
      return cur[k];
    }

    let N = 4;
    let K = 3;
    document.write(findKthChar(N, K));

  // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
B
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*