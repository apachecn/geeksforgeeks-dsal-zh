# 一个字符串可以重新排列形成回文所需的最小删除量

> 原文:[https://www . geeksforgeeks . org/minimum-removes-required-so-字符串可以重新排列以形成回文/](https://www.geeksforgeeks.org/minimum-removals-required-such-that-a-string-can-be-rearranged-to-form-a-palindrome/)

给定一个由小写英文字母组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是找到需要删除的最小字符数，这样该字符串的字符可以重新排列形成一个[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

**示例:**

> **输入:**S = " ababccca "
> T3】输出: 1
> **解释:**
> 去掉字符串中出现的‘c’。因此，修改后的字符串为“ababcca”，可以重新排列形成回文字符串“cababac”。
> 因此，只需拆除一次。
> 
> **输入:**S = abcde
> T3】输出: 4

**方法:**根据观察可以解决这个问题，在一个[回文串](https://www.geeksforgeeks.org/string-palindrome/)中，最多一个字符可以出现奇数次。因此，减少除其中一个字符之外的所有奇频字符的频率。
按照以下步骤解决问题:

*   初始化一个大小为 **26** 的数组，用于在 **S** 中存储每个字符[的频率](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)。
*   [穿过绳子](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)
*   更新频率数组中每个字符的[频率。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)
*   计算奇数频率的字符数，并将其存储在一个变量中，例如**计数**。
*   如果**计数**为 **1** 或 **0** ，则打印 **0** 作为答案。否则，打印**计数–1**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of deletions
// required such that characters of the
// string can be rearranged to form a palindrome
int minDeletions(string str)
{
    // Stores frequency of characters
    int fre[26];
    memset(fre, 0, sizeof(fre));

    int n = str.size();
cout<<n;
    // Store the frequency of each
    // character in frequency array
    for (int i = 0; i < n; i++) {
        fre[str[i] - 'a'] += 1;
    }
      for (int i = 0; i < n; i++) {
        cout<<fre[i];
    }

    int count = 0;

    // Count number of characters
    // with odd frequency
    for (int i = 0; i < 26; i++) {
        if (fre[i] % 2) {
            count += 1;
        }
    }

    // If count is 1 or 0, return 0
    if (count == 0 || count == 1) {
        return 0;
    }

    // Otherwise, return count - 1
    else {
        return count - 1;
    }
}

// Driver Code
int main()
{
    string str = "ababbccca";

    // Function call to find minimum
    // number of deletions required
    cout << minDeletions(str) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

  // Function to find the number of deletions
  // required such that characters of the
  // string can be rearranged to form a palindrome
  static int minDeletions(String str)
  {
    // Stores frequency of characters
    int fre[] = new int[26];

    int n = str.length();

    // Store the frequency of each
    // character in frequency array
    for (int i = 0; i < n; i++) {
      fre[str.charAt(i) - 'a'] += 1;
    }

    int count = 0;

    // Count number of characters
    // with odd frequency
    for (int i = 0; i < 26; i++) {
      if (fre[i] % 2 == 1) {
        count += 1;
      }
    }

    // If count is 1 or 0, return 0
    if (count == 0 || count == 1) {
      return 0;
    }

    // Otherwise, return count - 1
    else {
      return count - 1;
    }
  }

  // Driver Code
  public static void main (String[] args)
  {
    String str = "ababbccca";

    // Function call to find minimum
    // number of deletions required
    System.out.println(minDeletions(str)) ;
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the number of deletions
# required such that characters of the
# string can be rearranged to form a palindrome
def minDeletions(str):

    # Stores frequency of characters
    fre = [0]*26

    # memset(fre, 0, sizeof(fre));
    n = len(str)

    # Store the frequency of each
    # character in frequency array
    for i in range(n):
        fre[ord(str[i]) - ord('a')] += 1

    count = 0

    # Count number of characters
    # with odd frequency
    for i in range(26):
        if (fre[i] % 2):
            count += 1

    # If count is 1 or 0, return 0
    if (count == 0 or count == 1):
        return 0

    # Otherwise, return count - 1
    else:
        return count - 1

# Driver Code
if __name__ == '__main__':
    str = "ababbccca"

    # Function call to find minimum
    # number of deletions required
    print (minDeletions(str))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the number of deletions
  // required such that characters of the
  // string can be rearranged to form a palindrome
  static int minDeletions(string str)
  {

    // Stores frequency of characters
    int []fre = new int[26];
    int n = str.Length;

    // Store the frequency of each
    // character in frequency array
    for (int i = 0; i < n; i++)
    {
      fre[str[i] - 'a'] += 1;
    }

    int count = 0;

    // Count number of characters
    // with odd frequency
    for (int i = 0; i < 26; i++) {
      if (fre[i] % 2 == 1) {
        count += 1;
      }
    }

    // If count is 1 or 0, return 0
    if (count == 0 || count == 1) {
      return 0;
    }

    // Otherwise, return count - 1
    else {
      return count - 1;
    }
  }

  // Driver Code
  public static void Main(string[] args)
  {
    string str = "ababbccca";

    // Function call to find minimum
    // number of deletions required
    Console.WriteLine(minDeletions(str)) ;
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
//Javascript program for
// the above approach

// Function to find the number of deletions
// required such that characters of the
// string can be rearranged to form a palindrome
function minDeletions(str)
{
    // Stores frequency of characters
    var fre = new Array(26);
    fre.fill(0);

    var n = str.length;

    // Store the frequency of each
    // character in frequency array
    for (var i = 0; i < n; i++) {
        //let a = parseInt(str[i] - 97);
        fre[str[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;

    }
    var count = 0;

    // Count number of characters
    // with odd frequency
    for (var i = 0; i < 26; i++) {
        if (fre[i] % 2) {
            count += 1;
        }
    }

    // If count is 1 or 0, return 0
    if (count == 0 || count == 1) {
        return 0;
    }

    // Otherwise, return count - 1
    else {
        return count - 1;
    }
}

    var str = "ababbccca";

    // Function call to find minimum
    // number of deletions required
    document.write( minDeletions(str)+"<br>");

    // This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)