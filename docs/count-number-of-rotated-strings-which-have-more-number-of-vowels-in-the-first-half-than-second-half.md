# 统计前半部分元音数多于后半部分的旋转字符串数

> 原文:[https://www . geesforgeks . org/count-旋转字符串的数量-前半部分的元音数量比后半部分多/](https://www.geeksforgeeks.org/count-number-of-rotated-strings-which-have-more-number-of-vowels-in-the-first-half-than-second-half/)

给定的偶数大小的字符串由小写英文字母组成。任务是找出在前半部分比后半部分有更多元音的旋转字符串的数量。

**示例:**

> **输入:** str = "abcd"
> **输出:** 2
> **说明:**
> 所有旋转的字符串都是“abcd”、“dabc”、“cdab”、“bcda”。
> 前两个旋转的弦在
> 前半段的元音比后半段多。
> 
> **输入:**str = " abecidft "
> T3】输出: 4
> **解释:**
> 有 4 种可能的旋转字符串，其中前半部分的元音比后半部分多。

**方法:**一个有效的方法是制作字符串 **s = str + str** 那么 **s** 的大小将为 **2 * N** 。现在，制作一个前缀数组来存储从第 0 个索引到第 I 个索引的元音数量。然后从**N–1**到**2 * N–2**循环，得到**弦**的所有旋转弦。查找所需旋转字符串的计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of rotated
// strings which have more number of vowels in
// the first half than the second half
int cntRotations(string s, int n)
{
    // Create a new string
    string str = s + s;

    // Pre array to store count of all vowels
    int pre[2 * n] = { 0 };

    // Compute the prefix array
    for (int i = 0; i < 2 * n; i++) {
        if (i != 0)
            pre[i] += pre[i - 1];

        if (str[i] == 'a' || str[i] == 'e'
            || str[i] == 'i' || str[i] == 'o'
            || str[i] == 'u') {
            pre[i]++;
        }
    }

    // To store the required answer
    int ans = 0;

    // Find all rotated strings
    for (int i = n - 1; i < 2 * n - 1; i++) {

        // Right and left index of the string
        int r = i, l = i - n;

        // x1 stores the number of vowels
        // in the rotated string
        int x1 = pre[r];
        if (l >= 0)
            x1 -= pre[l];
        r = i - n / 2;

        // Left stores the number of vowels
        // in the first half of rotated string
        int left = pre[r];
        if (l >= 0)
            left -= pre[l];

        // Right stores the number of vowels
        // in the second half of rotated string
        int right = x1 - left;

        // If the count of vowels in the first half
        // is greater than the count in the second half
        if (left > right) {
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    string s = "abecidft";
    int n = s.length();

    cout << cntRotations(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of rotated
// Strings which have more number of vowels in
// the first half than the second half
static int cntRotations(String s, int n)
{
    // Create a new String
    String str = s + s;

    // Pre array to store count of all vowels
    int pre[]=new int[2 * n] ;

    // Compute the prefix array
    for (int i = 0; i < 2 * n; i++)
    {
        if (i != 0)
            pre[i] += pre[i - 1];

        if (str.charAt(i) == 'a' || str.charAt(i) == 'e' ||
            str.charAt(i) == 'i' || str.charAt(i) == 'o' ||
            str.charAt(i) == 'u')
        {
            pre[i]++;
        }
    }

    // To store the required answer
    int ans = 0;

    // Find all rotated Strings
    for (int i = n - 1; i < 2 * n - 1; i++)
    {

        // Right and left index of the String
        int r = i, l = i - n;

        // x1 stores the number of vowels
        // in the rotated String
        int x1 = pre[r];
        if (l >= 0)
            x1 -= pre[l];
        r = i - n / 2;

        // Left stores the number of vowels
        // in the first half of rotated String
        int left = pre[r];
        if (l >= 0)
            left -= pre[l];

        // Right stores the number of vowels
        // in the second half of rotated String
        int right = x1 - left;

        // If the count of vowels in the first half
        // is greater than the count in the second half
        if (left > right)
        {
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String args[])
{
    String s = "abecidft";
    int n = s.length();

    System.out.println( cntRotations(s, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of rotated
# strings which have more number of vowels in
# the first half than the second half
def cntRotations(s, n):

    # Create a new string
    str = s + s;

    # Pre array to store count of all vowels
    pre = [0] * (2 * n);

    # Compute the prefix array
    for i in range(2 * n):
        if (i != 0):
            pre[i] += pre[i - 1];

        if (str[i] == 'a' or str[i] == 'e' or
            str[i] == 'i' or str[i] == 'o' or
            str[i] == 'u'):
            pre[i] += 1;

    # To store the required answer
    ans = 0;

    # Find all rotated strings
    for i in range(n - 1, 2 * n - 1, 1):

        # Right and left index of the string
        r = i; l = i - n;

        # x1 stores the number of vowels
        # in the rotated string
        x1 = pre[r];
        if (l >= 0):
            x1 -= pre[l];
        r = (int)(i - n / 2);

        # Left stores the number of vowels
        # in the first half of rotated string
        left = pre[r];
        if (l >= 0):
            left -= pre[l];

        # Right stores the number of vowels
        # in the second half of rotated string
        right = x1 - left;

        # If the count of vowels in the first half
        # is greater than the count in the second half
        if (left > right):
            ans += 1;

    # Return the required answer
    return ans;

# Driver code
s = "abecidft";
n = len(s);

print(cntRotations(s, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of rotated
    // Strings which have more number of vowels in
    // the first half than the second half
    static int cntRotations(string s, int n)
    {
        // Create a new String
        string str = s + s;

        // Pre array to store count of all vowels
        int []pre = new int[2 * n];

        // Compute the prefix array
        for (int i = 0; i < 2 * n; i++)
        {
            if (i != 0)
                pre[i] += pre[i - 1];

            if (str[i] == 'a' || str[i] == 'e' ||
                str[i] == 'i' || str[i] == 'o' ||
                str[i] == 'u')
            {
                pre[i]++;
            }
        }

        // To store the required answer
        int ans = 0;

        // Find all rotated Strings
        for (int i = n - 1; i < 2 * n - 1; i++)
        {

            // Right and left index of the String
            int r = i, l = i - n;

            // x1 stores the number of vowels
            // in the rotated String
            int x1 = pre[r];
            if (l >= 0)
                x1 -= pre[l];
            r = i - n / 2;

            // Left stores the number of vowels
            // in the first half of rotated String
            int left = pre[r];
            if (l >= 0)
                left -= pre[l];

            // Right stores the number of vowels
            // in the second half of rotated String
            int right = x1 - left;

            // If the count of vowels in the first half
            // is greater than the count in the second half
            if (left > right)
            {
                ans++;
            }
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        String s = "abecidft";
        int n = s.Length;

        Console.WriteLine( cntRotations(s, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the count of rotated
    // Strings which have more number of vowels in
    // the first half than the second half
    function cntRotations(s, n)
    {
        // Create a new String
        let str = s + s;

        // Pre array to store count of all vowels
        let pre = new Array(2 * n);
        pre.fill(0);

        // Compute the prefix array
        for (let i = 0; i < 2 * n; i++)
        {
            if (i != 0)
                pre[i] += pre[i - 1];

            if (str[i] == 'a' || str[i] == 'e' ||
                str[i] == 'i' || str[i] == 'o' ||
                str[i] == 'u')
            {
                pre[i]++;
            }
        }

        // To store the required answer
        let ans = 0;

        // Find all rotated Strings
        for (let i = n - 1; i < 2 * n - 1; i++)
        {

            // Right and left index of the String
            let r = i, l = i - n;

            // x1 stores the number of vowels
            // in the rotated String
            let x1 = pre[r];
            if (l >= 0)
                x1 -= pre[l];
            r = i - parseInt(n / 2, 10);

            // Left stores the number of vowels
            // in the first half of rotated String
            let left = pre[r];
            if (l >= 0)
                left -= pre[l];

            // Right stores the number of vowels
            // in the second half of rotated String
            let right = x1 - left;

            // If the count of vowels in the first half
            // is greater than the count in the second half
            if (left > right)
            {
                ans++;
            }
        }

        // Return the required answer
        return ans;
    }

    let s = "abecidft";
    let n = s.length;

    document.write(cntRotations(s, n));

</script>
```

**Output**

```
4
```

***时间复杂度:**O(2 * N)*
T5**辅助空间:** O(2 * N)

**高效方法:**为了将上述方法的空间复杂度降低到常数，将两部分元音的数量存储在**两个变量**中，并通过改变索引来迭代所有旋转。

*   在每次旋转中，前半部分的第一个元素被移除并插入后半部分，如果这个元素是元音，则前半部分的元音数减少 1，后半部分的元音数增加 1。
*   后半部分的第一个元素被移除并插入到前半部分，如果这个元素是元音，那么前半部分的元音数增加 1，后半部分的元音数减少 1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// rotated strings which have more
// number of vowels in the first
// half than the second half
int cntRotations(char s[], int n)
{
    int lh = 0, rh = 0, i, ans = 0;

    // Compute the number of
    // vowels in first-half
    for(i = 0; i < n / 2; ++i)
        if (s[i] == 'a' || s[i] == 'e' ||
            s[i] == 'i' || s[i] == 'o' ||
            s[i] == 'u')
        {
            lh++;
        }

    // Compute the number of
    // vowels in second-half
    for(i = n / 2; i < n; ++i)
        if (s[i] == 'a' || s[i] == 'e' ||
            s[i] == 'i' || s[i] == 'o' ||
            s[i] == 'u')
        {
            rh++;
        }

    // Check if first-half
    // has more vowels
    if (lh > rh)
        ans++;

    // Check for all possible rotations
    for(i = 1; i < n; ++i)
    {
        if (s[i - 1] == 'a' || s[i - 1] == 'e' ||
            s[i - 1] == 'i' || s[i - 1] == 'o' ||
            s[i - 1] == 'u')
        {
            rh++;
            lh--;
        }
        if (s[(i - 1 + n / 2) % n] == 'a' ||
            s[(i - 1 + n / 2) % n] == 'e' ||
            s[(i - 1 + n / 2) % n] == 'i' ||
            s[(i - 1 + n / 2) % n] == 'o' ||
            s[(i - 1 + n / 2) % n] == 'u')
        {
            rh--;
            lh++;
        }
        if (lh > rh)
            ans++;
    }

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    char s[] = "abecidft";

    int n = strlen(s);

    // Function call
    cout << " " << cntRotations(s, n);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C implementation of the approach
#include <stdio.h>
#include <string.h>

// Function to return the count of
// rotated strings which have more
// number of vowels in the first
// half than the second half
int cntRotations(char s[], int n)
{
    int lh = 0, rh = 0, i, ans = 0;

    // Compute the number of
    // vowels in first-half
    for (i = 0; i < n / 2; ++i)
        if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i'
            || s[i] == 'o' || s[i] == 'u')
        {
            lh++;
        }

    // Compute the number of
    // vowels in second-half
    for (i = n / 2; i < n; ++i)
        if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i'
            || s[i] == 'o' || s[i] == 'u') {
            rh++;
        }

    // Check if first-half
    // has more vowels
    if (lh > rh)
        ans++;

    // Check for all possible rotations
    for (i = 1; i < n; ++i) {
        if (s[i - 1] == 'a' || s[i - 1] == 'e'
            || s[i - 1] == 'i' || s[i - 1] == 'o'
            || s[i - 1] == 'u') {
            rh++;
            lh--;
        }
        if (s[(i - 1 + n / 2) % n] == 'a'
            || s[(i - 1 + n / 2) % n] == 'e'
            || s[(i - 1 + n / 2) % n] == 'i'
            || s[(i - 1 + n / 2) % n] == 'o'
            || s[(i - 1 + n / 2) % n] == 'u') {
            rh--;
            lh++;
        }
        if (lh > rh)
            ans++;
    }

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    char s[] = "abecidft";

    int n = strlen(s);

    // Function call
    printf("%d", cntRotations(s, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the approach
class GFG{

// Function to return the count of
// rotated strings which have more
// number of vowels in the first
// half than the second half
public static int cntRotations(char s[],
                               int n)
{
  int lh = 0, rh = 0, i, ans = 0;

  // Compute the number of
  // vowels in first-half
  for (i = 0; i < n / 2; ++i)
    if (s[i] == 'a' || s[i] == 'e' ||
        s[i] == 'i' || s[i] == 'o' ||
        s[i] == 'u')
    {
      lh++;
    }

  // Compute the number of
  // vowels in second-half
  for (i = n / 2; i < n; ++i)
    if (s[i] == 'a' || s[i] == 'e' ||
        s[i] == 'i' || s[i] == 'o' ||
        s[i] == 'u')
    {
      rh++;
    }

  // Check if first-half
  // has more vowels
  if (lh > rh)
    ans++;

  // Check for all possible
  // rotations
  for (i = 1; i < n; ++i)
  {
    if (s[i - 1] == 'a' || s[i - 1] == 'e' ||
        s[i - 1] == 'i' || s[i - 1] == 'o' ||
        s[i - 1] == 'u')
    {
      rh++;
      lh--;
    }
    if (s[(i - 1 + n / 2) % n] == 'a' ||
        s[(i - 1 + n / 2) % n] == 'e' ||
        s[(i - 1 + n / 2) % n] == 'i' ||
        s[(i - 1 + n / 2) % n] == 'o' ||
        s[(i - 1 + n / 2) % n] == 'u')
    {
      rh--;
      lh++;
    }
    if (lh > rh)
      ans++;
  }

  // Return the answer
  return ans;
}

// Driver code
public static void main(String[] args)
{
  char s[] = {'a','b','e','c',
              'i','d','f','t'};
  int n = s.length;

  // Function call
  System.out.println(
         cntRotations(s, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# rotated strings which have more
# number of vowels in the first
# half than the second half
def cntRotations(s, n):

    lh, rh, ans = 0, 0, 0

    # Compute the number of
    # vowels in first-half
    for i in range (n // 2):
        if (s[i] == 'a' or s[i] == 'e' or
            s[i] == 'i' or s[i] == 'o' or
            s[i] == 'u'):
            lh += 1

    # Compute the number of
    # vowels in second-half
    for i in range (n // 2, n):
        if (s[i] == 'a' or s[i] == 'e' or
            s[i] == 'i' or s[i] == 'o' or
            s[i] == 'u'):
            rh += 1

    # Check if first-half
    # has more vowels
    if (lh > rh):
        ans += 1

    # Check for all possible rotations
    for i in range (1, n):
        if (s[i - 1] == 'a' or s[i - 1] == 'e' or
            s[i - 1] == 'i' or s[i - 1] == 'o' or
            s[i - 1] == 'u'):
            rh += 1
            lh -= 1

        if (s[(i - 1 + n // 2) % n] == 'a' or
            s[(i - 1 + n // 2) % n] == 'e' or
            s[(i - 1 + n // 2) % n] == 'i' or
            s[(i - 1 + n // 2) % n] == 'o' or
            s[(i - 1 + n // 2) % n] == 'u'):
            rh -= 1
            lh += 1

        if (lh > rh):
            ans += 1

    # Return the answer
    return ans

# Driver code
if __name__ == "__main__":

    s = "abecidft"
    n = len(s)

    # Function call
    print(cntRotations(s, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of
// the approach
using System;
class GFG
{

    // Function to return the count of
    // rotated strings which have more
    // number of vowels in the first
    // half than the second half
    static int cntRotations(char[] s, int n)
    {
      int lh = 0, rh = 0, i, ans = 0;

      // Compute the number of
      // vowels in first-half
      for (i = 0; i < n / 2; ++i)
        if (s[i] == 'a' || s[i] == 'e' ||
            s[i] == 'i' || s[i] == 'o' ||
            s[i] == 'u')
        {
          lh++;
        }

      // Compute the number of
      // vowels in second-half
      for (i = n / 2; i < n; ++i)
        if (s[i] == 'a' || s[i] == 'e' ||
            s[i] == 'i' || s[i] == 'o' ||
            s[i] == 'u')
        {
          rh++;
        }

      // Check if first-half
      // has more vowels
      if (lh > rh)
        ans++;

      // Check for all possible
      // rotations
      for (i = 1; i < n; ++i)
      {
        if (s[i - 1] == 'a' || s[i - 1] == 'e' ||
            s[i - 1] == 'i' || s[i - 1] == 'o' ||
            s[i - 1] == 'u')
        {
          rh++;
          lh--;
        }
        if (s[(i - 1 + n / 2) % n] == 'a' ||
            s[(i - 1 + n / 2) % n] == 'e' ||
            s[(i - 1 + n / 2) % n] == 'i' ||
            s[(i - 1 + n / 2) % n] == 'o' ||
            s[(i - 1 + n / 2) % n] == 'u')
        {
          rh--;
          lh++;
        }
        if (lh > rh)
          ans++;
      }

      // Return the answer
      return ans;
    }

  // Driver code    
  static void Main()
  {
      char[] s = {'a','b','e','c',
              'i','d','f','t'};
      int n = s.Length;

      // Function call
      Console.WriteLine(cntRotations(s, n));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count of
    // rotated strings which have more
    // number of vowels in the first
    // half than the second half
    function cntRotations(s, n)
    {
      let lh = 0, rh = 0, i, ans = 0;

      // Compute the number of
      // vowels in first-half
      for (i = 0; i < parseInt(n / 2, 10); ++i)
        if (s[i] == 'a' || s[i] == 'e' ||
            s[i] == 'i' || s[i] == 'o' ||
            s[i] == 'u')
        {
          lh++;
        }

      // Compute the number of
      // vowels in second-half
      for (i = parseInt(n / 2, 10); i < n; ++i)
        if (s[i] == 'a' || s[i] == 'e' ||
            s[i] == 'i' || s[i] == 'o' ||
            s[i] == 'u')
        {
          rh++;
        }

      // Check if first-half
      // has more vowels
      if (lh > rh)
        ans++;

      // Check for all possible
      // rotations
      for (i = 1; i < n; ++i)
      {
        if (s[i - 1] == 'a' || s[i - 1] == 'e' ||
            s[i - 1] == 'i' || s[i - 1] == 'o' ||
            s[i - 1] == 'u')
        {
          rh++;
          lh--;
        }
        if (s[(i - 1 + n / 2) % n] == 'a' ||
            s[(i - 1 + n / 2) % n] == 'e' ||
            s[(i - 1 + n / 2) % n] == 'i' ||
            s[(i - 1 + n / 2) % n] == 'o' ||
            s[(i - 1 + n / 2) % n] == 'u')
        {
          rh--;
          lh++;
        }
        if (lh > rh)
          ans++;
      }

      // Return the answer
      return ans;
    }

    // Driver code
    let s = ['a','b','e','c','i','d','f','t'];
    let n = s.length;

    // Function call
    document.write(cntRotations(s, n));

    // This code is contributed by rameshtravel07.
</script>
```

**Output**

```
4
```

***时间复杂度:** O(n)*
***空间复杂度:** O(1)*