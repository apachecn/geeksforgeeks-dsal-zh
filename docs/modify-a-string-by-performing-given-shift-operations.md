# 通过执行给定的换档操作修改字符串

> 原文:[https://www . geesforgeks . org/通过执行给定的移位操作来修改字符串/](https://www.geeksforgeeks.org/modify-a-string-by-performing-given-shift-operations/)

给定一个包含小写英文字母的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，以及一个由成对的形式**{方向，量}** 组成的[矩阵](https://www.geeksforgeeks.org/matrix/)**shift【】【】【】**，其中方向可以是 **0(用于左移位)**或 **1(用于右移位)****量**是字符串 **S** 需要移位的索引数任务是返回执行给定操作后可以获得的修改后的字符串。

***注:**左移 1 是指去掉 **S** 的第一个字符，追加到末尾。同样，右移 1 是指去掉 **S** 的最后一个字符，并在开头插入。*

**示例**

> **输入**:S =“ABC”，shift[][] = {{0，1}，{1，2}}
> **输出:**驾驶室
> **说明:**
> 【0，1】是指将 S[0]向左移动 1。因此，字符串 S 从“abc”修改为“bca”。
> 【1，2】是指将 S[0]向右移动 1。因此，字符串 S 从“bca”修改为“cab”。
> 
> **输入:**S =“abcdefg”，shift[][] = { {1，1}，{1，1}，{0，2}，{1，3} }
> **输出:** efgabcd
> **解释:**
> 【1，1】是指将 S[0]向右移动 1。因此，字符串 S 从“abcdefg”修改为“gabcdef”。
> 【1，1】是指将 S[0]向右移动 1。因此，字符串 S 从“gabcdef”修改为“fgabcde”。
> 【0，2】是指将 S【0】向左移动 2。因此，字符串 S 从“fgabcde”修改为“abcdefg”。
> 【1，3】是指向右移动 S[0]3。因此，字符串 S 从“abcdefg”修改为“efgabcd”。

**天真法:**解决问题最简单的方法是[遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/) **移位【】【】**按指定方向的指数数量移位 S【0】。完成所有移位操作后，打印获得的最终字符串。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**要优化上述方法，请执行以下步骤:

*   初始化一个变量，比如 **val，**来存储有效班次。
*   [遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)**shift【】【】**并在每 i <sup>第</sup>行执行以下操作:
*   如果**档位[i][0] = 0** ( *左档* ) **，**则通过-档位[i][1]降低**值。**
*   否则( *左移*)，通过**移【I】【1】增加**值**。**
*   更新 **val = val % len** (进一步优化有效班次)。
*   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，**结果=“**，存储修改后的字符串。
*   现在，检查**是否值> 0** 。如果发现是真的，则通过**阀**在弦上执行正确的旋转。
*   否则，按 **|val|** 量向左旋转琴弦。
*   打印**结果。**

下面是上述方法的实现:

## C++

```
// C++ implementation
// of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the string obtained
// after performing given shift operations
void stringShift(string s,
                 vector<vector<int> >& shift)
{

    int val = 0;

    for (int i = 0; i < shift.size(); ++i)

        // If shift[i][0] = 0, then left shift
        // Otherwise, right shift
        val += shift[i][0] == 0
                   ? -shift[i][1]
                   : shift[i][1];

    // Stores length of the string
    int len = s.length();

    // Effective shift calculation
    val = val % len;

    // Stores modified string
    string result = "";

    // Right rotation
    if (val > 0)
        result = s.substr(len - val, val)
                 + s.substr(0, len - val);

    // Left rotation
    else
        result
            = s.substr(-val, len + val)
              + s.substr(0, -val);

    cout << result;
}

// Driver Code
int main()
{
    string s = "abc";
    vector<vector<int> > shift = {
        { 0, 1 },
        { 1, 2 }
    };

    stringShift(s, shift);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
import java.io.*;
class GFG
{

  // Function to find the string obtained
  // after performing given shift operations
  static void stringShift(String s, int[][] shift)
  {
    int val = 0;
    for (int i = 0; i < shift.length; ++i)

      // If shift[i][0] = 0, then left shift
      // Otherwise, right shift
      if (shift[i][0] == 0)
        val -= shift[i][1];
    else
      val += shift[i][1];

    // Stores length of the string
    int len = s.length();

    // Effective shift calculation
    val = val % len;

    // Stores modified string
    String result = "";

    // Right rotation
    if (val > 0)
      result = s.substring(len - val, (len - val) + val)
      + s.substring(0, len - val);

    // Left rotation
    else
      result = s.substring(-val, len + val)
      + s.substring(0, -val);

    System.out.println(result);
  }

  // Driver Code
  public static void main(String[] args)
  {
    String s = "abc";
    int[][] shift
      = new int[][] {{ 0, 1 }, { 1, 2 }};

    stringShift(s, shift);
  }
}

// This code is contributed by Dharanendra L V
```

## C#

```
// C# implementation
// of above approach
using System;

public class GFG
{

  // Function to find the string obtained
  // after performing given shift operations
  static void stringShift(String s, int[,] shift)
  {
    int val = 0;
    for (int i = 0; i < shift.GetLength(0); ++i)

      // If shift[i,0] = 0, then left shift
      // Otherwise, right shift
      if (shift[i,0] == 0)
        val -= shift[i, 1];
    else
      val += shift[i, 1];

    // Stores length of the string
    int len = s.Length;

    // Effective shift calculation
    val = val % len;

    // Stores modified string
    String result = "";

    // Right rotation
    if (val > 0)
      result = s.Substring(len - val, val)
      + s.Substring(0, len - val);

    // Left rotation
    else
      result = s.Substring(-val, len)
      + s.Substring(0, -val);

    Console.WriteLine(result);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String s = "abc";
    int[,] shift
      = new int[,] {{ 0, 1 }, { 1, 2 }};

    stringShift(s, shift);
  }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation
// of above approach

// Function to find the string obtained
// after performing given shift operations
function stringShift(s, shift)
{

    var val = 0;

    for (var i = 0; i < shift.length; ++i)

        // If shift[i][0] = 0, then left shift
        // Otherwise, right shift
        val += shift[i][0] == 0
                   ? -shift[i][1]
                   : shift[i][1];

    // Stores length of the string
    var len = s.length;

    // Effective shift calculation
    val = val % len;

    // Stores modified string
    var result = "";

    // Right rotation
    if (val > 0)
        result = s.substring(len - val,len)
                 + s.substring(0, len - val);

    // Left rotation
    else
        result
            = s.substring(-val, len )
              + s.substring(0, -val);

    document.write( result);
}

// Driver Code
var s = "abc";
var shift = [
    [ 0, 1 ],
    [ 1, 2 ]
];
stringShift(s, shift);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
cab
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)