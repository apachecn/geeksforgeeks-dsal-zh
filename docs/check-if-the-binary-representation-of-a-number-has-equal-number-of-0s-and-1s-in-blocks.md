# 检查一个数的二进制表示在块中是否有相等数量的 0 和 1

> 原文:[https://www . geesforgeks . org/check-如果一个数的二进制表示在块中具有相等的 0 和 1 个数/](https://www.geeksforgeeks.org/check-if-the-binary-representation-of-a-number-has-equal-number-of-0s-and-1s-in-blocks/)

给定一个整数 N，任务是检查它的等价二进制数是否具有 0 和 1 的连续块的相等频率。请注意，0 和全为 1 的数字不被视为具有 0 和 1 的块数。

**示例:**

> **输入:** N = 5
> **输出:**是
> 5 的等价二进制数为 101。
> 第一块是长度为 1 的 1，第二块是长度为 1 的 0
> ，第三块是长度为 1 的 1。所以，0 和 1 的所有块具有相等的频率，即 1。
> 
> **输入:** N = 51
> **输出:**是
> 等效二进制数 51 为 110011。
> 
> **输入:**8
> T3】输出:否
> 
> **输入:**7
> T3】输出:否

**简单方法:**首先将整数转换为其等价的二进制数。从左到右遍历二进制字符串，对于每个 1 或 0 的块，找到它的长度并将其添加到一个集合中。如果器械包长度为 1，则打印“是”，否则打印“否”。

## C++

```
// C++ implementation of the above 
// approach 
#include <bits/stdc++.h>
using namespace std;

// Function to check
void hasEqualBlockFrequency(int N)
{

  // Converting integer to its equivalent 
  // binary number
  string S = bitset<3> (N).to_string();
  set<int> p;
  int c = 1;

  for(int i = 0; i < S.length(); i++)
  {

    // If adjacent character are same 
    // then increase counter
    if (S[i] == S[i + 1])
      c += 1;

    else
    {
      p.insert(c);
      c = 1;
    }
    p.insert(c);
  }

  if (p.size() == 1)
    cout << "Yes" << endl;
  else
    cout << "No" << endl;
}

// Driver code
int main()
{
  int N = 5;
  hasEqualBlockFrequency(N);
  return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above 
// approach 
import java.util.*;

class GFG{

// Function to check
static void hasEqualBlockFrequency(int N)
{

    // Converting integer to its equivalent 
    // binary number
    String S = Integer.toString(N,2);
    HashSet<Integer> p = new HashSet<Integer>();
    int c = 1;

    for(int i = 0; i < S.length() - 1; i++)
    {

        // If adjacent character are same 
        // then increase counter
        if (S.charAt(i) == S.charAt(i + 1))
            c += 1;

        else
        {
            p.add(c);
            c = 1;
        }
        p.add(c);
    }

    if (p.size() == 1)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String []args)
{
    int N = 5;

    hasEqualBlockFrequency(N);
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation of the above
# approach

# Function to check
def hasEqualBlockFrequency(N):

    # Converting integer to its equivalent
    # binary number
    S = bin(N).replace("0b", "")
    p = set()
    c = 1

    for i in range(len(S)-1):

        # If adjacent character are same
        # then increase counter
        if (S[i] == S[i + 1]):
            c += 1

        else:
            p.add(c)
            c = 1

        p.add(c)

    if (len(p) == 1):
        print("Yes")
    else:
        print("No")

# Driver code
N = 5
hasEqualBlockFrequency(N)
```

## C#

```
// C# implementation of the above 
// approach 
using System;
using System.Collections.Generic;

class GFG{

// Function to check
static void hasEqualBlockFrequency(int N)
{

    // Converting integer to its equivalent 
    // binary number
    string S = Convert.ToString(N, 2);
    HashSet<int> p = new HashSet<int>();
    int c = 1;

    for(int i = 0; i < S.Length - 1; i++)
    {

        // If adjacent character are same 
        // then increase counter
        if (S[i] == S[i + 1])
            c += 1;

        else
        {
            p.Add(c);
            c = 1;
        }
        p.Add(c);
    }

    if (p.Count == 1)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
static void Main()
{
    int N = 5;

    hasEqualBlockFrequency(N);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

  // JavaScript implementation of the above approach

  // Function to check
  function hasEqualBlockFrequency(N)
  {

      // Converting integer to its equivalent
      // binary number
      let S = N.toString(2);
      let p = new Set();
      let c = 1;

      for(let i = 0; i < S.length - 1; i++)
      {

          // If adjacent character are same
          // then increase counter
          if (S[i] == S[i + 1])
              c += 1;

          else
          {
              p.add(c);
              c = 1;
          }
          p.add(c);
      }

      if (p.size == 1)
          document.write("Yes");
      else
          document.write("No");
  }

  let N = 5;

  hasEqualBlockFrequency(N);

</script>
```

**Output:** 

```
Yes
```

**优化解:**我们从最后一位开始遍历。我们首先计算最后一个块中的相同位数。然后，我们遍历所有位，对于每个块，我们计算相同位的数量，如果这个计数与第一个计数不同，我们返回 false。如果所有块具有相同的计数，我们返回 true。

## C++

```
// C++ program to check if a number has
// same counts of 0s and 1s in every
// block.

#include <iostream>
using namespace std;

// function to convert decimal to binary
bool isEqualBlock(int n)
{
    // Count same bits in last block
    int first_bit = n % 2;
    int first_count = 1;
    n = n / 2;
    while (n % 2 == first_bit && n > 0) {
        n = n / 2;
        first_count++;
    }

    // If n is 0 or it has all 1s,
    // then it is not considered to
    // have equal number of 0s and
    // 1s in blocks.
    if (n == 0)
        return false;

    // Count same bits in all remaining blocks.
    while (n > 0) {

        int first_bit = n % 2;
        int curr_count = 1;
        n = n / 2;
        while (n % 2 == first_bit) {
            n = n / 2;
            curr_count++;
        }

        if (curr_count != first_count)
            return false;
    }

    return true;
}

// Driver program to test above function
int main()
{
    int n = 51;
    if (isEqualBlock(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number has
// same counts of 0s and 1s in every
// block.
import java.io.*;

class GFG
{

// function to convert decimal to binary
static boolean isEqualBlock(int n)
{
    // Count same bits in last block
    int first_bit = n % 2;
    int first_count = 1;
    n = n / 2;
    while (n % 2 == first_bit && n > 0)
    {
        n = n / 2;
        first_count++;
    }

    // If n is 0 or it has all 1s,
    // then it is not considered to
    // have equal number of 0s and
    // 1s in blocks.
    if (n == 0)
        return false;

    // Count same bits in all remaining blocks.
    while (n > 0)
    {

        first_bit = n % 2;
        int curr_count = 1;
        n = n / 2;
        while (n % 2 == first_bit)
        {
            n = n / 2;
            curr_count++;
        }

        if (curr_count != first_count)
            return false;
    }
    return true;
}

// Driver code
public static void main (String[] args)
{
    int n = 51;
    if (isEqualBlock(n))
        System.out.println( "Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by inder_mca
```

## 蟒蛇 3

```
# Python3 program to check if a number has
# same counts of 0s and 1s in every block.

# Function to convert decimal to binary
def isEqualBlock(n):

    # Count same bits in last block
    first_bit = n % 2
    first_count = 1
    n = n // 2
    while n % 2 == first_bit and n > 0:
        n = n // 2
        first_count += 1

    # If n is 0 or it has all 1s,
    # then it is not considered to
    # have equal number of 0s and
    # 1s in blocks.
    if n == 0:
        return False

    # Count same bits in all remaining blocks.
    while n > 0:

        first_bit = n % 2
        curr_count = 1
        n = n // 2
        while n % 2 == first_bit:
            n = n // 2
            curr_count += 1

        if curr_count != first_count:
            return False

    return True

# Driver Code
if __name__ == "__main__":

    n = 51
    if isEqualBlock(n):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# program to check if a number has
// same counts of 0s and 1s in every
// block.

using System;

class GFG
{

    // function to convert decimal to binary
    static bool isEqualBlock(int n)
    {
        // Count same bits in last block
        int first_bit = n % 2;
        int first_count = 1;
        n = n / 2;
        while (n % 2 == first_bit && n > 0)
        {
            n = n / 2;
            first_count++;
        }

        // If n is 0 or it has all 1s,
        // then it is not considered to
        // have equal number of 0s and
        // 1s in blocks.
        if (n == 0)
            return false;

        // Count same bits in all remaining blocks.
        while (n > 0)
        {

            first_bit = n % 2;
            int curr_count = 1;
            n = n / 2;

            while (n % 2 == first_bit)
            {
                n = n / 2;
                curr_count++;
            }

            if (curr_count != first_count)
                return false;
        }
        return true;
    }

    // Driver code
    public static void Main ()
    {
        int n = 51;

        if (isEqualBlock(n))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number has
// same counts of 0s and 1s in every
// block.

// function to convert decimal to binary
function isEqualBlock($n)
{
    // Count same bits in last block
    $first_bit = $n % 2;
    $first_count = 1;
    $n = (int)($n / 2);
    while ($n % 2 == $first_bit && $n > 0)
    {
        $n = (int)($n / 2);
        $first_count++;
    }

    // If n is 0 or it has all 1s, then
    // it is not considered to have equal
    // number of 0s and 1s in blocks.
    if ($n == 0)
        return false;

    // Count same bits in all remaining blocks.
    while ($n > 0)
    {
        $first_bit = $n % 2;
        $curr_count = 1;
        $n = (int)($n / 2);
        while ($n % 2 == $first_bit)
        {
            $n = (int)($n / 2);
            $curr_count++;
        }

        if ($curr_count != $first_count)
            return false;
    }

    return true;
}

// Driver Code
$n = 51;
if (isEqualBlock($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by
// Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// javascript program to check if a number has
// same counts of 0s and 1s in every
// block.

// function to convert decimal to binary
function isEqualBlock(n)
{
    // Count same bits in last block
    var first_bit = n % 2;
    var first_count = 1;
    n = n / 2;
    while (n % 2 == first_bit && n > 0)
    {
        n = n / 2;
        first_count++;
    }

    // If n is 0 or it has all 1s,
    // then it is not considered to
    // have equal number of 0s and
    // 1s in blocks.
    if (n == 0)
        return false;

    // Count same bits in all remaining blocks.
    while (n > 0)
    {

        first_bit = n % 2;
        var curr_count = 1;
        n = n / 2;
        while (n % 2 == first_bit)
        {
            n = n / 2;
            curr_count++;
        }

        if (curr_count != first_count)
            return false;
    }
    return true;
}

// Driver code
var n = 51;
if (isEqualBlock(n))
    document.write( "Yes");
else
    document.write("No");

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
Yes
```