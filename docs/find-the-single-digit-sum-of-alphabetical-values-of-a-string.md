# 求字符串字母值的一位数和

> 原文:[https://www . geeksforgeeks . org/find-按字母顺序排列的字符串值总和/](https://www.geeksforgeeks.org/find-the-single-digit-sum-of-alphabetical-values-of-a-string/)

给定大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过给定字符串中所有字母的**顺序之和得到的值的重复位数来[求一位数之和。](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)**

> 字母的顺序是由它们在英语中出现的位置决定的。

**示例:**

> **输入:** S =【极客】
> **输出:** 1
> **解释:**
> 字母的和顺序得到的值是 7 + 5 + 5 + 11 = 28。
> 28 = 2+8 = 10 = 1+0 = 1 相加得到的一位数和。
> 
> **输入:**S = " geeks forgeeks "
> T3】输出: 7

**方法:**给定的问题可以这样解决:如果 **S[i]** 是小写或大写字符，则通过将值**(S[I]–‘A’+1)**或**(S[I]–‘A’+1)**相加，首先找到给定字符串中存在的所有字母的顺序的**和**。找到**和**的值后，使用本文中讨论的方法找到该值的个位数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

int findTheSum(string str)
{
    string alpha;

    // Traverse the given string
    for (int i = 0; i < str.length(); i++) {

        // If character is an alphabet
        if ((str[i] >= 'A' && str[i] <= 'Z')
            || (str[i] >= 'a' && str[i] <= 'z'))
            alpha.push_back(str[i]);
    }

    // Stores the sum of order of values
    int score = 0, n = 0;

    for (int i = 0; i < alpha.length(); i++) {

        // Find the score
        if (alpha[i] >= 'A' && alpha[i] <= 'Z')
            score += alpha[i] - 'A' + 1;
        else
            score += alpha[i] - 'a' + 1;
    }

    // Find the single digit sum
    while (score > 0 || n > 9) {
        if (score == 0) {
            score = n;
            n = 0;
        }
        n += score % 10;
        score /= 10;
    }

    // Return the resultant sum
    return n;
}

// Driver Code
int main()
{
    string S = "GeeksforGeeks";
    cout << findTheSum(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

static int findTheSum(char []str)
{
    String alpha="";

    // Traverse the given String
    for (int i = 0; i < str.length; i++) {

        // If character is an alphabet
        if ((str[i] >= 'A' && str[i] <= 'Z')
            || (str[i] >= 'a' && str[i] <= 'z'))
            alpha+=(str[i]);
    }

    // Stores the sum of order of values
    int score = 0, n = 0;

    for (int i = 0; i < alpha.length(); i++) {

        // Find the score
        if (alpha.charAt(i) >= 'A' && alpha.charAt(i) <= 'Z')
            score += alpha.charAt(i) - 'A' + 1;
        else
            score += alpha.charAt(i) - 'a' + 1;
    }

    // Find the single digit sum
    while (score > 0 || n > 9) {
        if (score == 0) {
            score = n;
            n = 0;
        }
        n += score % 10;
        score /= 10;
    }

    // Return the resultant sum
    return n;
}

// Driver Code
public static void main(String[] args)
{
    String S = "GeeksforGeeks";
    System.out.print(findTheSum(S.toCharArray()));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach
def findTheSum(str):

    alpha = ""

    # Traverse the given string
    for i in range(0, len(str)):

                # If character is an alphabet
        if ((str[i] >= 'A' and str[i] <= 'Z') or (str[i] >= 'a' and str[i] <= 'z')):
            alpha += str[i]

        # Stores the sum of order of values
    score = 0
    n = 0

    for i in range(0, len(alpha)):

                # Find the score
        if (alpha[i] >= 'A' and alpha[i] <= 'Z'):
            score += ord(alpha[i]) - ord('A') + 1

        else:
            score += ord(alpha[i]) - ord('a') + 1

        # Find the single digit sum
    while (score > 0 or n > 9):
        if (score == 0):
            score = n
            n = 0

        n += score % 10
        score = score // 10

        # Return the resultant sum
    return n

# Driver Code
if __name__ == "__main__":

    S = "GeeksforGeeks"
    print(findTheSum(S))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {
    static int findTheSum(string str)
    {
        string alpha = "";

        // Traverse the given string
        for (int i = 0; i < str.Length; i++) {

            // If character is an alphabet
            if ((str[i] >= 'A' && str[i] <= 'Z')
                || (str[i] >= 'a' && str[i] <= 'z'))
                alpha += (str[i]);
        }

        // Stores the sum of order of values
        int score = 0, n = 0;

        for (int i = 0; i < alpha.Length; i++) {

            // Find the score
            if (alpha[i] >= 'A' && alpha[i] <= 'Z')
                score += alpha[i] - 'A' + 1;
            else
                score += alpha[i] - 'a' + 1;
        }

        // Find the single digit sum
        while (score > 0 || n > 9) {
            if (score == 0) {
                score = n;
                n = 0;
            }
            n += score % 10;
            score /= 10;
        }

        // Return the resultant sum
        return n;
    }

    // Driver Code
    public static void Main()
    {
        string S = "GeeksforGeeks";
        Console.WriteLine(findTheSum(S));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

function findTheSum(str) {
  let alpha = [];

  // Traverse the given string
  for (let i = 0; i < str.length; i++) {
    // If character is an alphabet
    if (
      (str[i].charCodeAt(0) >= "A".charCodeAt(0) &&
        str[i].charCodeAt(0) <= "Z".charCodeAt(0)) ||
      (str[i].charCodeAt(0) >= "a".charCodeAt(0) &&
        str[i].charCodeAt(0) <= "z".charCodeAt(0))
    )
      alpha.push(str[i]);
  }

  // Stores the sum of order of values
  let score = 0,
    n = 0;

  for (let i = 0; i < alpha.length; i++) {
    // Find the score
    if (
      alpha[i].charCodeAt(0) >= "A".charCodeAt(0) &&
      alpha[i].charCodeAt(0) <= "Z".charCodeAt(0)
    )
      score += alpha[i].charCodeAt(0) - "A".charCodeAt(0) + 1;
    else score += alpha[i].charCodeAt(0) - "a".charCodeAt(0) + 1;
  }

  // Find the single digit sum
  while (score > 0 || n > 9) {
    if (score == 0) {
      score = n;
      n = 0;
    }
    n += score % 10;
    score = Math.floor(score / 10);
  }

  // Return the resultant sum
  return n;
}

// Driver Code

let S = "GeeksforGeeks";
document.write(findTheSum(S));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)