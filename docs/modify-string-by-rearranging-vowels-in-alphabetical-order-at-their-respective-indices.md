# 通过在各自的索引处按字母顺序重新排列元音来修改字符串

> 原文:[https://www . geeksforgeeks . org/按字母顺序在各自的索引处重新排列元音来修改字符串/](https://www.geeksforgeeks.org/modify-string-by-rearranging-vowels-in-alphabetical-order-at-their-respective-indices/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是按照字母顺序对给定字符串的元音进行排序，并将它们相应地放在各自的索引中。

**示例:**

> **输入:**S = " geeksforgeeks "
> T3】输出:geeksfergoks
> **解释:**
> 字符串中的元音为:e、e、o、e、e
> 按字母顺序排序:e、e、e、e、e、o 并用原字符串中存在的元音替换。
> 
> **输入:** S =【人】
> T3】输出:皮普洛

**方法:**想法是将字符串 **S** 中存在的所有元音存储在另一个字符串中，比如**誓言**。[将绳子**誓言**按字母顺序](https://www.geeksforgeeks.org/check-whether-the-vowels-in-a-string-are-in-alphabetical-order-or-not/)排序。[从头开始遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果**S【I】**是元音，则将**S【I】**替换为**誓言【j】**，并将 **j** 递增 1。按照以下步骤解决问题:

*   初始化一个字符串**发誓**存储字符串中存在的所有元音， **S** 。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 并检查[当前字符 **S[i]** 是否为元音](https://www.geeksforgeeks.org/program-find-character-vowel-consonant/)，如果发现为真，则推 **S[i]** 至**誓言**。
*   [按字母顺序排序字符串](https://www.geeksforgeeks.org/sort-string-characters/) **誓言**并初始化一个变量，比如说 **j** 为 **0** 。
*   再次[使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果当前字符**S【I】**是一个元音，那么将**S【I】**替换为**誓言【j】**，并将 **j** 增加 **1** 。
*   完成上述步骤后，打印字符串 **S** 作为结果。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to arrange the vowels
// in sorted order in the string
// at their respective places
void sortVowels(string S)
{
    // Store the size of the string
    int n = S.size();

    // Stores vowels of string S
    string vow = "";

    // Traverse the string, S and push
    // all the vowels to string vow
    for (int i = 0; i < n; i++) {

        if (S[i] == 'a' || S[i] == 'e'
            || S[i] == 'i' || S[i] == 'o'
            || S[i] == 'u') {
            vow += S[i];
        }
    }

    // If vow is empty, then print S
    // and return
    if (vow.size() == 0) {
        cout << S;
        return;
    }

    // Sort vow in alphabetical order
    sort(vow.begin(), vow.end());

    int j = 0;

    // Traverse the string, S
    for (int i = 0; i < n; i++) {

        // Replace S[i] with vow[j] iif S[i]
        // is a vowel, and increment j by 1
        if (S[i] == 'a' || S[i] == 'e' || S[i] == 'i'
            || S[i] == 'o' || S[i] == 'u') {
            S[i] = vow[j++];
        }
    }

    // Print the string
    cout << S;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    sortVowels(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
class GFG
{

  // Function to arrange the vowels
  // in sorted order in the string
  // at their respective places
  static void sortVowels(String S)
  {

    // Store the size of the string
    int n = S.length();

    // Stores vowels of string S
    String vow = "";

    // Traverse the string, S and push
    // all the vowels to string vow
    for (int i = 0; i < n; i++) {
      if (S.charAt(i) == 'a' || S.charAt(i) == 'e'
          || S.charAt(i) == 'i' || S.charAt(i) == 'o'
          || S.charAt(i) == 'u') {
        vow = vow.substring(0, vow.length())
          + S.charAt(i);
      }
    }

    // If vow is empty, then print S
    // and return
    if (vow.length() == 0) {
      System.out.print(S);
      return;
    }

    // Convert vow to char array
    char tempArray[] = vow.toCharArray();

    // Sort vow in alphabetical order
    Arrays.sort(tempArray);

    int j = 0;

    // Traverse the string, S
    for (int i = 0; i < n; i++) {

      // Replace S[i] with vow[j] iif S[i]
      // is a vowel, and increment j by 1
      if (S.charAt(i) == 'a' || S.charAt(i) == 'e'
          || S.charAt(i) == 'i' || S.charAt(i) == 'o'
          || S.charAt(i) == 'u') {
        S = S.substring(0, i) + tempArray[j++]
          + S.substring(i + 1, n);
      }
    }

    // Print the string
    System.out.print(S);
  }

  // Driver Code
  public static void main(String[] args)
  {
    String S = "geeksforgeeks";
    sortVowels(S);
  }
}

// This code is contributed by subhammahato348.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to arrange the vowels
# in sorted order in the string
# at their respective places
def sortVowels(S) :

    # Store the size of the string
    n = len(S);

    # Stores vowels of string S
    vow = "";

    # Traverse the string, S and push
    # all the vowels to string vow
    for i in range(n) :

        if (S[i] == 'a' or S[i] == 'e'
            or S[i] == 'i' or S[i] == 'o'
            or S[i] == 'u') :
            vow += S[i];

    # If vow is empty, then print S
    # and return
    if len(vow) == 0 :
        print(S,end="");
        return;

    # Sort vow in alphabetical order
    vow = list(vow);
    vow.sort();
    j = 0;

    # Traverse the string, S
    for i in range(n) :

        # Replace S[i] with vow[j] iif S[i]
        # is a vowel, and increment j by 1
        if (S[i] == 'a' or S[i] == 'e' or S[i] == 'i'
            or S[i] == 'o' or S[i] == 'u') :
            S[i] = vow[j];
            j += 1;

    # Print the string
    print("".join(S),end="");

# Driver Code
if __name__ == "__main__" :

    S = "geeksforgeeks";
    sortVowels(list(S));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to arrange the vowels
  // in sorted order in the string
  // at their respective places
  static void sortVowels(string S)
  {

    // Store the size of the string
    int n = S.Length;

    // Stores vowels of string S
    string vow = "";

    // Traverse the string, S and push
    // all the vowels to string vow
    for (int i = 0; i < n; i++) {
      if (S[i] == 'a' || S[i] == 'e'
          || S[i] == 'i' || S[i] == 'o'
          || S[i] == 'u') {
        vow = vow.Substring(0, vow.Length)
          + S[i];
      }
    }

    // If vow is empty, then print S
    // and return
    if (vow.Length == 0) {
      Console.Write(S);
      return;
    }

    // Convert vow to char array
    char []tempArray = vow.ToCharArray();

    // Sort vow in alphabetical order
    Array.Sort(tempArray);
    int j = 0;

    // Traverse the string, S
    for (int i = 0; i < n; i++) {

      // Replace S[i] with vow[j] iif S[i]
      // is a vowel, and increment j by 1
      if (S[i] == 'a' || S[i] == 'e'
          || S[i] == 'i' || S[i] == 'o'
          || S[i] == 'u') {
        S = S.Substring(0, i) + tempArray[j++]
          + S.Substring(i + 1, n - i - 1);
      }
    }

    // Print the string
    Console.Write(S);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    string S = "geeksforgeeks";
    sortVowels(S);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to arrange the vowels
// in sorted order in the string
// at their respective places
function sortVowels(S)
{
    // Store the size of the string
    var n = S.length;

    // Stores vowels of string S
    var vow = "";

    // Traverse the string, S and push
    // all the vowels to string vow
    for (var i = 0; i < n; i++) {

        if (S[i] == 'a' || S[i] == 'e'
            || S[i] == 'i' || S[i] == 'o'
            || S[i] == 'u') {
            vow += S[i];
        }
    }

    // If vow is empty, then print S
    // and return
    if (vow.length == 0) {
        document.write( S);
        return;
    }

    // Sort vow in alphabetical order
    vow = vow.split('').sort();

    var j = 0;

    // Traverse the string, S
    for (var i = 0; i < n; i++) {

        // Replace S[i] with vow[j] iif S[i]
        // is a vowel, and increment j by 1
        if (S[i] == 'a' || S[i] == 'e' || S[i] == 'i'
            || S[i] == 'o' || S[i] == 'u') {
            S[i] = vow[j++];
        }
    }

    // Print the string
    document.write( S.join(''));
}

// Driver Code
var S = "geeksforgeeks".split('');
sortVowels(S);

</script>
```

**Output:** 

```
geeksfergeoks
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*