# 通过将给定字符串的字符增加第二个字符串的相应索引处的数字来生成字符串

> 原文:[https://www . geeksforgeeks . org/按给定字符串的递增字符生成第二个字符串的当前对应索引/](https://www.geeksforgeeks.org/generate-string-by-incrementing-character-of-given-string-by-number-present-at-corresponding-index-of-second-string/)

给定两个相同大小的[字符串](https://www.geeksforgeeks.org/stringstream-c-applications/) **S[]** 和 **N[]** ，任务是通过添加各自索引的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **N[]** 的数字来更新字符串 **S[]** 。

**示例:**

> **输入:** S =“太阳”，N =“966”
> T3】输出:蝙蝠
> 
> **输入:** S = "苹果"，N = " 12580 "
> T3】输出:蛮力

**进场:**思路是[从左到右穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S[]** 。获取字符串 **N[]** 的 ASCII 值，并将其添加到字符串 **S[]** 的 ASCII 值中。如果值超过 **122** ，这是最后一个字母 **'z'** 的 ASCII 值。然后用 **26** 减去该值，即为英文字母总数。用获得的 ASCII 值的字符更新字符串。按照以下步骤解决问题:

*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，S.size())** ，并执行以下任务:
    *   将变量 **a** 和 **b** 初始化为**N【I】**和**S【I】的整数和 ascii 值。**
    *   如果 **b** 大于 **122** ，则从**b**中减去 **26**
    *   将 **S[i]** 设置为 **char(b)。**
*   执行上述步骤后，将**S【】**的值打印为 nswer。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to update string
string updateStr(string S, string N)
{
    for (int i = 0; i < S.size(); i++) {

        // Get ASCII value
        int a = int(N[i]) - '0';
        int b = int(S[i]) + a;

        if (b > 122)
            b -= 26;

        S[i] = char(b);
    }
    return S;
}

// Driver Code
int main()
{
    string S = "sun";
    string N = "966";
    cout << updateStr(S, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
public class GFG {

  // Function to update string
  static String updateStr(String S, String N)
  {
    String t = "";
    for (int i = 0; i < S.length(); i++) {

      // Get ASCII value
      int a = (int)(N.charAt(i) - '0');
      int b = (int)(S.charAt(i) + a);

      if (b > 122)
        b -= 26;

      char x = (char)b;
      t +=x;
    }
    return t;
  }

  // Driver code
  public static void main(String args[])
  {
    String S = "sun";
    String N = "966";
    System.out.println(updateStr(S, N));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to update string
def updateStr(S, N):
    S = list(S)
    for i in range(len(S)):

        # Get ASCII value
        a = ord(N[i]) - ord('0')
        b = ord(S[i]) + a

        if (b > 122):
            b -= 26

        S[i] = chr(b)
    return "".join(S)

# Driver Code

S = "sun"
N = "966"
print(updateStr(S, N))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code to implement above approach
using System;
public class GFG {

  // Function to update string
  static String updateStr(String S, String N)
  {
    String t = "";
    for (int i = 0; i < S.Length; i++) {

      // Get ASCII value
      int a = (int)(N[i] - '0');
      int b = (int)(S[i] + a);

      if (b > 122)
        b -= 26;

      char x = (char)b;
      t +=x;
    }
    return t;
  }

  // Driver code
  public static void Main(String []args)
  {
    String S = "sun";
    String N = "966";
    Console.WriteLine(updateStr(S, N));

  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach

   // Function to update string
   function updateStr(S, N) {
     S = S.split('')
     for (let i = 0; i < S.length; i++) {

       // Get ASCII value
       let a = (N[i].charCodeAt(0) - '0'.charCodeAt(0));
       let b = (S[i].charCodeAt(0)) + a;

       if (b > 122)
         b -= 26;

       S[i] = String.fromCharCode(b);
     }
     return S.join('');
   }

   // Driver Code

   let S = "sun";
   let N = "966";
   document.write(updateStr(S, N));

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
bat
```

***时间复杂度:** O(|S|)*
***辅助空间:** O(1)*