# 检查通过字符交换或替换是否可以使一个字符串等于另一个字符串

> 原文:[https://www . geesforgeks . org/check-if-a-string-to-equal-to-other-string-by-swapping-or-replacement-of-characters/](https://www.geeksforgeeks.org/check-if-a-string-can-be-made-equal-to-another-string-by-swapping-or-replacement-of-characters/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/)**【S1】**和 **S2** ，任务是通过交换任意一对字符来替换字符串 **S1** 中的任意字符，检查字符串 **S1** 是否可以等于字符串 **S2** 。如果可以使字符串 **S1** 等于 **S2** ，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**S1 =“ABC”，S2 =“BCA”
> **输出:**是
> **解释:**
> **操作 1:**“ABC”->“ACB”
> **操作 2:**“ACB”->“BCA”
> 
> **输入:**S1 =“a”，S2 =“aa”
> **输出:**否
> **说明:**不可能让两个字符串相同。

**方法:**解决这个问题的思路是[找到字符串中字符](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/)的频率，检查两个字符串中是否使用了相同的字符。按照以下步骤解决问题:

*   初始化两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**a【】**和**b【】**来存储字符串 **S1** 和 **S2** 的频率。
*   [遍历两个字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S1】**和 **S2** 和[将字符串的频率存储在数组](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) **a[]** 和 **b[]** 中。
*   [对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **a[]** 和 **b[]** 进行排序。
*   [遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果任何元素在任何索引处不相等，则打印**“否”**，因为两个字符串中至少有一个字符不同。
*   经过以上步骤，如果不存在任何不等频，则打印**“是”**作为字符串**【S1】**可以通过给定的操作转换为字符串**【S2】**。

下面是该方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find if given strings
// are same or not
bool sameStrings(string str1,
                 string str2)
{
    int N = str1.length();
    int M = str2.length();

    // Base Condition
    if (N != M) {
        return false;
    }

    // Stores frequency of characters
    // of the string str1 and str2
    int a[256] = { 0 }, b[256] = { 0 };

    // Traverse strings str1 & str2 and
    // store frequencies in a[] and b[]
    for (int i = 0; i < N; i++) {
        a[str1[i] - 'a']++;
        b[str2[i] - 'a']++;
    }

    // Check if both strings have
    // same characters or not
    int i = 0;

    while (i < 256) {

        if ((a[i] == 0 && b[i] == 0)
            || (a[i] != 0 && b[i] != 0)) {
            i++;
        }

        // If a character is present
        // in one string and is not in
        // another string, return false
        else {
            return false;
        }
    }

    // Sort the array a[] and b[]
    sort(a, a + 256);
    sort(b, b + 256);

    // Check arrays a and b contain
    // the same frequency or not
    for (int i = 0; i < 256; i++) {

        // If the frequencies are not
        // the same after sorting
        if (a[i] != b[i])
            return false;
    }

    // At this point, str1 can
    // be converted to str2
    return true;
}
// Driver Code
int main()
{
    string S1 = "cabbba", S2 = "abbccc";
    if (sameStrings(S1, S2))
        cout << "YES" << endl;
    else
        cout << " NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find if given Strings
// are same or not
static boolean sameStrings(String str1,
                 String str2)
{
    int N = str1.length();
    int M = str2.length();

    // Base Condition
    if (N != M)
    {
        return false;
    }

    // Stores frequency of characters
    // of the String str1 and str2
    int []a = new int[256];
    int []b = new int[256];

    // Traverse Strings str1 & str2 and
    // store frequencies in a[] and b[]
    for (int i = 0; i < N; i++)
    {
        a[str1.charAt(i) - 'a']++;
        b[str2.charAt(i) - 'a']++;
    }

    // Check if both Strings have
    // same characters or not
    int i = 0;
    while (i < 256)
    {
        if ((a[i] == 0 && b[i] == 0)
            || (a[i] != 0 && b[i] != 0))
        {
            i++;
        }

        // If a character is present
        // in one String and is not in
        // another String, return false
        else
        {
            return false;
        }
    }

    // Sort the array a[] and b[]
    Arrays.sort(a);
    Arrays.sort(b);

    // Check arrays a and b contain
    // the same frequency or not
    for (i = 0; i < 256; i++)
    {

        // If the frequencies are not
        // the same after sorting
        if (a[i] != b[i])
            return false;
    }

    // At this point, str1 can
    // be converted to str2
    return true;
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "cabbba", S2 = "abbccc";
    if (sameStrings(S1, S2))
        System.out.print("YES" +"\n");
    else
        System.out.print(" NO" +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find if given strings
# are same or not
def sameStrings(str1, str2):
    N = len(str1)
    M = len(str2)

    # Base Condition
    if (N != M):
        return False

    # Stores frequency of characters
    # of the str1 and str2
    a, b = [0]*256, [0]*256

    # Traverse strings str1 & str2 and
    # store frequencies in a[] and b[]
    for i in range(N):
        a[ord(str1[i]) - ord('a')] += 1
        b[ord(str2[i]) - ord('a')] += 1

    # Check if both strings have
    # same characters or not
    i = 0
    while (i < 256):

        if ((a[i] == 0 and b[i] == 0) or (a[i] != 0 and b[i] != 0)):
            i += 1

        # If a character is present
        # in one and is not in
        # another string, return false
        else:
            return False

    # Sort the array a[] and b[]
    a = sorted(a)
    b = sorted(b)

    # Check arrays a and b contain
    # the same frequency or not
    for i in range(256):

        # If the frequencies are not
        # the same after sorting
        if (a[i] != b[i]):
            return False

    # At this point, str1 can
    # be converted to str2
    return True

  # Driver Code
if __name__ == '__main__':

    S1, S2 = "cabbba", "abbccc"
    if (sameStrings(S1, S2)):
        print("YES")
    else:
        print("NO")

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find if given Strings
// are same or not
static bool sameStrings(string str1,
                 string str2)
{
    int N = str1.Length;
    int M = str2.Length;

    // Base Condition
    if (N != M)
    {
        return false;
    }

    // Stores frequency of characters
    // of the String str1 and str2
    int []a = new int[256];
    int []b = new int[256];

    // Traverse Strings str1 & str2 and
    // store frequencies in a[] and b[]
    for (int j = 0; j < N; j++)
    {
        a[str1[j] - 'a']++;
        b[str2[j] - 'a']++;
    }

    // Check if both Strings have
    // same characters or not
    int i = 0 ;
    while (i < 256)
    {
        if ((a[i] == 0 && b[i] == 0)
            || (a[i] != 0 && b[i] != 0))
        {
            i++;
        }

        // If a character is present
        // in one String and is not in
        // another String, return false
        else
        {
            return false;
        }
    }

    // Sort the array a[] and b[]
    Array.Sort(a);
    Array.Sort(b);

    // Check arrays a and b contain
    // the same frequency or not
    for (int j = 0; j < 256; j++)
    {

        // If the frequencies are not
        // the same after sorting
        if (a[j] != b[j])
            return false;
    }

    // At this point, str1 can
    // be converted to str2
    return true;
}

  // Driver Code
  static public void Main()
  {
    string S1 = "cabbba", S2 = "abbccc";
    if (sameStrings(S1, S2))
        Console.Write("YES" +"\n");
    else
        Console.Write(" NO" +"\n");
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find if given Strings
      // are same or not
      function sameStrings(str1, str2) {
        var N = str1.length;
        var M = str2.length;

        // Base Condition
        if (N !== M) {
          return false;
        }

        // Stores frequency of characters
        // of the String str1 and str2
        var a = new Array(256).fill(0);
        var b = new Array(256).fill(0);

        // Traverse Strings str1 & str2 and
        // store frequencies in a[] and b[]
        for (var j = 0; j < N; j++) {
          a[str1[j].charCodeAt(0) - "a".charCodeAt(0)]++;
          b[str2[j].charCodeAt(0) - "a".charCodeAt(0)]++;
        }

        // Check if both Strings have
        // same characters or not
        var i = 0;
        while (i < 256) {
          if ((a[i] === 0 && b[i] === 0) || (a[i] !== 0 && b[i] !== 0)) {
            i++;
          }

          // If a character is present
          // in one String and is not in
          // another String, return false
          else {
            return false;
          }
        }

        // Sort the array a[] and b[]
        a.sort((x, y) => x - y);
        b.sort((x, y) => x - y);

        // Check arrays a and b contain
        // the same frequency or not
        for (var j = 0; j < 256; j++) {
          // If the frequencies are not
          // the same after sorting
          if (a[j] !== b[j]) return false;
        }

        // At this point, str1 can
        // be converted to str2
        return true;
      }

      // Driver Code
      var S1 = "cabbba",
        S2 = "abbccc";
      if (sameStrings(S1, S2)) document.write("YES" + "<br>");
      else document.write(" NO" + "<br>");
    </script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(256)