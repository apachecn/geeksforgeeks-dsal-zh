# 检查一个字符串的所有字符是否可以递增或递减相等

> 原文:[https://www . geesforgeks . org/check-if-all-characters-of-string-can-equal-by-increments-or-increments/](https://www.geeksforgeeks.org/check-if-all-characters-of-a-string-can-be-made-equal-by-increments-or-decrements/)

给定一个由 **N** 小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查是否可以通过将给定字符串中的任意两个字符递增或递减 **1** 来使[字符串的所有字符 **S** 相等](https://www.geeksforgeeks.org/quick-way-check-characters-string/)。如果可以使所有字符相同，则打印**“是”**。否则，打印**“否”**。

> 增加或减少任何字符意味着将字符分别更改为英语字母表中的下一个或上一个字符。如果字符是**‘a’**和**‘z’**，则不能进一步更改。

**示例:**

> **输入:**S =【beb】
> **输出:**是
> **解释:**
> 通过执行以下操作可以使给定字符串 S 的字符相等:
> 
> *   对于字符串“beb”，将“b”增加 1，将“e”减少 1，则该字符串变为“cdb”。
> *   对于字符串“cdb”，将“d”减少 1，将“b”增加 1，则该字符串变为“ccc”。
> 
> **输入:** S = "极客"
> T3】输出:否

**方法:**给定的问题可以基于以下观察来解决:

*   当任意字符同时递增和递减 **1** 时，字符串的 [ASCII 值之和在操作前后保持不变。](https://www.geeksforgeeks.org/python-program-to-find-the-sum-of-characters-ascii-values-in-string-list/)
*   假设任意字符的 ASCII 值为 **X** 。如果所有字符相等，则字符串的 ASCII 值之和为 **N*X** 。因此，可以说总和可以被 **N** 整除。因此，ASCII 值的初始总和需要被 **N** 整除，才能使所有字符相等。

请按照以下步骤解决此问题:

*   初始化一个变量 **sum** ，它存储给定字符串的 ASCII 值的 [sum。](https://www.geeksforgeeks.org/sums-of-ascii-values-of-each-word-in-a-sentence/)
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，对于每个字符**S【I】**将**(S【I】–‘a’+1)**的值加到**和**上。
*   完成上述步骤后，如果**和**的值可被 **N** 整除，则给定字符串的所有字符可以相等。因此，打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is
// possible to make all characters
// of string S same or not
void canMakeEqual(string S)
{
    // Length of string
    int N = S.size();

    // Stores the sum of ASCII value
    int weightOfString = 0;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Update the weightOfString
        weightOfString += S[i] - 'a' + 1;
    }

    // If the sum is divisible by N
    // then print "Yes"
    if (weightOfString % N == 0)
        cout << "Yes";

    // Otherwise print "No"
    else
        cout << "No";
}

// Driver Code
int main()
{
    string S = "beb";
    canMakeEqual(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to check if it is
// possible to make all characters
// of string S same or not
static void canMakeEqual(String S){
   // Length of string
    int N = S.length();

    // Stores the sum of ASCII value
    int weightOfString = 0;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Update the weightOfString
        weightOfString += S.charAt(i) - 'a' + 1;
    }

    // If the sum is divisible by N
    // then print "Yes"
    if (weightOfString % N == 0)
        System.out.println("Yes");

    // Otherwise print "No"
    else
        System.out.println("No");
}

  // Driver Code
    public static void main (String[] args) {
            String S = "beb";
               canMakeEqual(S);
    }
}

// This code is contributed by aadityaburujwale
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is
# possible to make all characters
# of string S same or not
def canMakeEqual(S):

    # Length of string
    N = len(S)

    # Stores the sum of ASCII value
    weightOfString = 0

    # Traverse the string S
    for i in range(N):

        # Update the weightOfString
        weightOfString += ord(S[i]) - ord('a') + 1

    # If the sum is divisible by N
    # then pr "Yes"
    if (weightOfString % N == 0):
        print("Yes")

    # Otherwise pr "No"
    else:
        print("No")

# Driver Code
S = "beb"
canMakeEqual(S)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if it is
// possible to make all characters
// of string S same or not
static void canMakeEqual(String S)
{

    // Length of string
    int N = S.Length;

    // Stores the sum of ASCII value
    int weightOfString = 0;

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Update the weightOfString
        weightOfString += S[i] - 'a' + 1;
    }

    // If the sum is divisible by N
    // then print "Yes"
    if (weightOfString % N == 0)
        Console.WriteLine("Yes");

    // Otherwise print "No"
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main(String[] args)
{
    String S = "beb";
    canMakeEqual(S);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if it is
// possible to make all characters
// of string S same or not
function canMakeEqual(S){
   // Length of string
    var N = S.length;

    // Stores the sum of ASCII value
    var weightOfString = 0;

    // Traverse the string S
    for (var i = 0; i < N; i++) {

        // Update the weightOfString
        weightOfString += S.charAt(i).charCodeAt(0) -
        'a'.charCodeAt(0) + 1;
    }

    // If the sum is divisible by N
    // then print "Yes"
    if (weightOfString % N == 0)
        document.write("Yes");

    // Otherwise print "No"
    else
        document.write("No");
}

// Driver Code
var S = "beb";
canMakeEqual(S);

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)