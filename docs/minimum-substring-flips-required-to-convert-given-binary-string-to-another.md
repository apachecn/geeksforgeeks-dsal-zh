# 将给定的二进制字符串转换为另一个

所需的最小子字符串翻转

> 原文:[https://www . geesforgeks . org/minimum-substring-flips-required-convert-给定-binary-string-to-other/](https://www.geeksforgeeks.org/minimum-substring-flips-required-to-convert-given-binary-string-to-another/)

给定两个[二进制字符串](https://www.geeksforgeeks.org/generate-all-binary-strings-from-given-pattern/) **A** 和 **B** ，任务是找出从 A 的第一个字符开始的一个[子串](https://www.geeksforgeeks.org/substring-in-cpp/)需要翻转的最小次数，即将 **1** s 转换为 **0** s 和 **0** s 转换为 **1** s，将 **A** 转换为 **B** 。

**示例:**

> **输入:**A =“0010”，B =“1011”
> 输出； 3
> **说明:**
> 第一步:翻转整个弦 A，因此 A 变成“1101”。
> 第二步:翻转子串{A[0]，A[2]}。因此，A 变成了“0011”。
> 第三步:翻转 A[0]。因此，A 变为“1011”，等于 b。
> 因此，所需的最小操作数为 3。
> 
> **输入:**A =“1010101”，B =“0011100”
> **输出:** 5
> **解释:**
> 第一步:翻转 entiThehrefore，A 变成“0101010”
> 第二步:翻转子串{A[0]，A[5]}。因此，A 变成了“1010100”
> 第三步:翻转子串{A[0]，A[3]}。因此，A 变成了“0101100”
> 第四步:翻转子串{A[0]，A[2]}。因此，A 变成“1011100”
> 第五步:翻转 A[0]。因此，A 变为“0011100”，等于 b。
> 因此，所需的最小操作数为 5。

**方法:**想法是初始化一个**变量**，该变量保存最后一个索引，在该索引处，A 处的**字符不同于 B** 处的**字符。然后从第一个指标到最后一个指标否定 **A** 。重复，直到两个字符串相等。按照以下步骤解决问题:**

*   初始化一个变量 **last_index** ，该变量保存最后一个索引，在该索引处字符在 **A** 和 **B** 中不同。
*   对从**第一个索引**到**最后一个索引**的字符串 **A** 求反，并增加步数。
*   重复以上步骤，直到弦 **A** 变为等于弦 **B** 。
*   执行操作后，在两个字符串相同的情况下打印步数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds the minimum
// number of operations required such
// that string A and B are the same
void findMinimumOperations(string a,
                           string b)
{

    // Stores the count of steps
    int step = 0;

    // Stores the last index whose
    // bits are not same
    int last_index;

    // Iterate until both string
    // are unequal
    while (a != b) {

        // Check till end of string to
        // find rightmost unequals bit
        for (int i = 0;
             i < a.length(); i++) {

            // Update the last index
            if (a[i] != b[i]) {
                last_index = i;
            }
        }

        // Flipping characters up
        // to the last index
        for (int i = 0;
             i <= last_index; i++) {

            // Flip the bit
            a[i] = (a[i] == '0') ? '1' : '0';
        }

        // Increasing steps by one
        step++;
    }

    // Print the count of steps
    cout << step;
}

// Driver Code
int main()
{
    // Given strings A and B
    string A = "101010", B = "110011";

    // Function Call
    findMinimumOperations(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function that finds the minimum
// number of operations required such
// that String A and B are the same
static void findMinimumOperations(char[] a,
                                  char[] b)
{
  // Stores the count of steps
  int step = 0;

  // Stores the last index whose
  // bits are not same
  int last_index = 0;

  // Iterate until both String
  // are unequal
  while (!Arrays.equals(a, b))
  {
    // Check till end of String to
    // find rightmost unequals bit
    for (int i = 0;
             i < a.length; i++)
    {
      // Update the last index
      if (a[i] != b[i])
      {
        last_index = i;
      }
    }

    // Flipping characters up
    // to the last index
    for (int i = 0;
             i <= last_index; i++)
    {

      // Flip the bit
      a[i] = (a[i] == '0') ?
              '1' : '0';
    }
    // Increasing steps by one
    step++;
  }

  // Print the count of steps
  System.out.print(step);
}

// Driver Code
public static void main(String[] args)
{
    // Given Strings A and B
    String A = "101010",
           B = "110011";

    // Function Call
    findMinimumOperations(A.toCharArray(),
                          B.toCharArray());
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the minimum
# number of operations required such
# that string A and B are the same
def findMinimumOperations(a, b):

    # Stores the count of steps
    step = 0

    # Stores the last index whose
    # bits are not same
    last_index = 0

    # Iterate until both string
    # are unequal
    while (a != b):
        a = [i for i in a]

        # Check till end of string to
        # find rightmost unequals bit
        for i in range(len(a)):

            # Update the last index
            if (a[i] != b[i]):
                last_index = i

        # Flipping characters up
        # to the last index
        for i in range(last_index + 1):

            # Flip the bit
            if (a[i] == '0'):
                a[i] = '1'
            else:
                a[i] = '0'

        a = "".join(a)       

        # Increasing steps by one
        step += 1

    # Print the count of steps
    print(step)

# Driver Code
if __name__ == '__main__':

    # Given strings A and B
    A = "101010"
    B = "110011"

    # Function Call
    findMinimumOperations(A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function that finds the minimum
// number of operations required such
// that string A and B are the same
static void findMinimumOperations(string a,
                                  string b)
{

  // Stores the count of steps
  int step = 0;

  // Stores the last index whose
  // bits are not same
  int last_index = 0;

  // Iterate until both string
  // are unequal
  while (a.Equals(b) == false)
  {

    // Check till end of string to
    // find rightmost unequals bit
    for(int i = 0; i < a.Length; i++)
    {

      // Update the last index
      if (a[i] != b[i])
      {
        last_index = i;
      }
    }

    // Flipping characters up
    // to the last index
    char[] ch = a.ToCharArray();
    for(int i = 0;
            i <= last_index; i++)
    {

      // Flip the bit
      if (ch[i] == '0')
      {
        ch[i] = '1';
      }
      else
      {
        ch[i] = '0';
      }
    }
    a = new string(ch);

    // Increasing steps by one
    step++;
  }

  // Print the count of steps
  Console.WriteLine(step);
}

// Driver Code
public static void Main()
{

  // Given strings A and B
  string A = "101010";
  string B = "110011";

  // Function Call
  findMinimumOperations(A,B);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the
// above approach

// Function that finds the minimum
// number of operations required such
// that string A and B are the same
function findMinimumOperations(a, b)
{

    // Stores the count of steps
    var step = 0;

    // Stores the last index whose
    // bits are not same
    var last_index = 0;

    // Iterate until both string
    // are unequal
    while (a !== b)
    {

        // Check till end of string to
        // find rightmost unequals bit
        for (var i = 0; i < a.length; i++)
        {

            // Update the last index
            if (a[i] !== b[i])
            {
                last_index = i;
            }
        }

        // Flipping characters up
        // to the last index
        var ch = a.split("");
        for(var i = 0; i <= last_index; i++)
        {

            // Flip the bit
            if (ch[i] === "0")
            {
                ch[i] = "1";
            }
            else
            {
                ch[i] = "0";
            }
        }
        a = ch.join("");

        // Increasing steps by one
        step++;
    }

    // Print the count of steps
    document.write(step);
}

// Driver Code

// Given strings A and B
var A = "101010";
var B = "110011";

// Function Call
findMinimumOperations(A, B);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*