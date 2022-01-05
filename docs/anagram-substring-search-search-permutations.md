# 字谜子串搜索(或搜索所有排列)

> 原文:[https://www . geesforgeks . org/anagram-substring-search-search-排列/](https://www.geeksforgeeks.org/anagram-substring-search-search-permutations/)

给定文本 txt[0..n-1]和模式 pat[0..m-1]，编写一个函数搜索(char pat[]，char txt[])，打印 pat[]及其在 txt[]中的所有排列(或字谜)。你可以假设 n > m.
预期时间复杂度为 O(n)
**示例:**

```
1) Input:  txt[] = "BACDGABCDA"  pat[] = "ABCD"
   Output:   Found at Index 0
             Found at Index 5
             Found at Index 6
2) Input: txt[] =  "AAABABAA" pat[] = "AABA"
   Output:   Found at Index 0
             Found at Index 1
             Found at Index 4
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/count-occurences-of-anagrams5839/1)

这个问题与标准模式搜索问题略有不同，这里我们也需要搜索字谜。因此，我们不能直接应用标准的模式搜索算法，如 [KMP](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/) 、[拉宾卡普](https://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/)、[博耶摩尔](https://www.geeksforgeeks.org/pattern-searching-set-7-boyer-moore-algorithm-bad-character-heuristic/)等。
一个简单的想法就是修改[拉宾卡普算法](https://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/)。例如，我们可以将哈希值保留为大素数模下所有字符的 ASCII 值之和。对于文本的每个字符，我们可以将当前字符添加到哈希值中，并减去上一个窗口的第一个字符。这个解决方案看起来不错，但是和标准的 Rabin Karp 一样，这个解决方案的最坏情况时间复杂度是 O(mn)。最坏的情况发生在所有哈希值都匹配，我们一个接一个地匹配所有字符的时候。
我们可以在字母表大小固定的假设下实现 O(n)时间复杂度，这通常是真的，因为 ASCII 中最多有 256 个可能的字符。想法是使用两个计数数组:
1)第一个计数数组存储模式中字符的频率。
2)第二计数数组存储当前文本窗口中字符的频率。
需要注意的重要一点是，比较两个计数数组的时间复杂度为 O(1)，因为其中的元素数量是固定的(与模式和文本大小无关)。以下是该算法的步骤。
1)在第一计数阵列中存储模式频率的计数*计数[]* 。也存储数组中第一个文本窗口的字符频率计数*countw[]*。
2)现在运行一个从 i = M 到 N-1 的循环。循环执行以下操作。
…..a)如果两个计数数组相同，我们发现一个匹配项。
…..b)countw【】
中文本当前字符的增量计数…..c)countWT[]
3)上一个窗口第一个字符的递减计数，上一个窗口没有被上述循环检查，所以明确检查。
以下是上述算法的实现。

## C++

```
// C++ program to search all anagrams of a pattern in a text
#include<iostream>
#include<cstring>
#define MAX 256
using namespace std;

// This function returns true if contents of arr1[] and arr2[]
// are same, otherwise false.
bool compare(char arr1[], char arr2[])
{
    for (int i=0; i<MAX; i++)
        if (arr1[i] != arr2[i])
            return false;
    return true;
}

// This function search for all permutations of pat[] in txt[]
void search(char *pat, char *txt)
{
    int M = strlen(pat), N = strlen(txt);

    // countP[]:  Store count of all characters of pattern
    // countTW[]: Store count of current window of text
    char countP[MAX] = {0}, countTW[MAX] = {0};
    for (int i = 0; i < M; i++)
    {
        (countP[pat[i]])++;
        (countTW[txt[i]])++;
    }

    // Traverse through remaining characters of pattern
    for (int i = M; i < N; i++)
    {
        // Compare counts of current window of text with
        // counts of pattern[]
        if (compare(countP, countTW))
            cout << "Found at Index " << (i - M) << endl;

        // Add current character to current window
        (countTW[txt[i]])++;

        // Remove the first character of previous window
        countTW[txt[i-M]]--;
    }

    // Check for the last window in text
    if (compare(countP, countTW))
        cout << "Found at Index " << (N - M) << endl;
}

/* Driver program to test above function */
int main()
{
    char txt[] = "BACDGABCDA";
    char pat[] = "ABCD";
    search(pat, txt);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to search all anagrams
// of a pattern in a text
public class GFG
{
    static final int MAX = 256;

    // This function returns true if contents
    // of arr1[] and arr2[] are same, otherwise
    // false.
    static boolean compare(char arr1[], char arr2[])
    {
        for (int i = 0; i < MAX; i++)
            if (arr1[i] != arr2[i])
                return false;
        return true;
    }

    // This function search for all permutations
    // of pat[] in txt[]
    static void search(String pat, String txt)
    {
        int M = pat.length();
        int N = txt.length();

        // countP[]:  Store count of all
        // characters of pattern
        // countTW[]: Store count of current
        // window of text
        char[] countP = new char[MAX];
        char[] countTW = new char[MAX];
        for (int i = 0; i < M; i++)
        {
            (countP[pat.charAt(i)])++;
            (countTW[txt.charAt(i)])++;
        }

        // Traverse through remaining characters
        // of pattern
        for (int i = M; i < N; i++)
        {
            // Compare counts of current window
            // of text with counts of pattern[]
            if (compare(countP, countTW))
                System.out.println("Found at Index " +
                                          (i - M));

            // Add current character to current
            // window
            (countTW[txt.charAt(i)])++;

            // Remove the first character of previous
            // window
            countTW[txt.charAt(i-M)]--;
        }

        // Check for the last window in text
        if (compare(countP, countTW))
            System.out.println("Found at Index " +
                                       (N - M));
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
        String txt = "BACDGABCDA";
        String pat = "ABCD";
        search(pat, txt);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python program to search all
# anagrams of a pattern in a text

MAX=256

# This function returns true
# if contents of arr1[] and arr2[]
# are same, otherwise false.
def compare(arr1, arr2):
    for i in range(MAX):
        if arr1[i] != arr2[i]:
            return False
    return True

# This function search for all
# permutations of pat[] in txt[] 
def search(pat, txt):

    M = len(pat)
    N = len(txt)

    # countP[]:  Store count of
    # all characters of pattern
    # countTW[]: Store count of
    # current window of text
    countP = [0]*MAX

    countTW = [0]*MAX

    for i in range(M):
        (countP[ord(pat[i]) ]) += 1
        (countTW[ord(txt[i]) ]) += 1

    # Traverse through remaining
    # characters of pattern
    for i in range(M,N):

        # Compare counts of current
        # window of text with
        # counts of pattern[]
        if compare(countP, countTW):
            print("Found at Index", (i-M))

        # Add current character to current window
        (countTW[ ord(txt[i]) ]) += 1

        # Remove the first character of previous window
        (countTW[ ord(txt[i-M]) ]) -= 1

    # Check for the last window in text   
    if compare(countP, countTW):
        print("Found at Index", N-M)

# Driver program to test above function      
txt = "BACDGABCDA"
pat = "ABCD"      
search(pat, txt)  

# This code is contributed
# by Upendra Singh Bartwal
```

## C#

```
// C# program to search all anagrams
// of a pattern in a text
using System;

class GFG
{
public const int MAX = 256;

// This function returns true if 
// contents of arr1[] and arr2[]
// are same, otherwise false.
public static bool compare(char[] arr1,
                           char[] arr2)
{
    for (int i = 0; i < MAX; i++)
    {
        if (arr1[i] != arr2[i])
        {
            return false;
        }
    }
    return true;
}

// This function search for all
// permutations of pat[] in txt[]
public static void search(string pat,
                          string txt)
{
    int M = pat.Length;
    int N = txt.Length;

    // countP[]: Store count of all
    // characters of pattern
    // countTW[]: Store count of current
    // window of text
    char[] countP = new char[MAX];
    char[] countTW = new char[MAX];
    for (int i = 0; i < M; i++)
    {
        (countP[pat[i]])++;
        (countTW[txt[i]])++;
    }

    // Traverse through remaining
    // characters of pattern
    for (int i = M; i < N; i++)
    {
        // Compare counts of current window
        // of text with counts of pattern[]
        if (compare(countP, countTW))
        {
            Console.WriteLine("Found at Index " +
                             (i - M));
        }

        // Add current character to
        // current window
        (countTW[txt[i]])++;

        // Remove the first character of
        // previous window
        countTW[txt[i - M]]--;
    }

    // Check for the last window in text
    if (compare(countP, countTW))
    {
        Console.WriteLine("Found at Index " +
                         (N - M));
    }
}

// Driver Code
public static void Main(string[] args)
{
    string txt = "BACDGABCDA";
    string pat = "ABCD";
    search(pat, txt);
}
}

// This code is contributed
// by Shrikant1
```

## java 描述语言

```
<script>

      // JavaScript program to search all anagrams
      // of a pattern in a text
      const MAX = 256;

      // This function returns true if
      // contents of arr1[] and arr2[]
      // are same, otherwise false.
      function compare(arr1, arr2) {
        for (var i = 0; i < MAX; i++) {
          if (arr1[i] !== arr2[i]) {
            return false;
          }
        }
        return true;
      }

      // This function search for all
      // permutations of pat[] in txt[]
      function search(pat, txt) {
        var M = pat.length;
        var N = txt.length;

        // countP[]: Store count of all
        // characters of pattern
        // countTW[]: Store count of current
        // window of text
        var countP = new Array(MAX).fill(0);
        var countTW = new Array(MAX).fill(0);
        for (var i = 0; i < M; i++) {
          countP[pat[i].charCodeAt(0)]++;
          countTW[txt[i].charCodeAt(0)]++;
        }

        // Traverse through remaining
        // characters of pattern
        for (var i = M; i < N; i++) {
          // Compare counts of current window
          // of text with counts of pattern[]
          if (compare(countP, countTW)) {
            document.write("Found at Index " + (i - M) + "<br>");
          }

          // Add current character to
          // current window
          countTW[txt[i].charCodeAt(0)]++;

          // Remove the first character of
          // previous window
          countTW[txt[i - M].charCodeAt(0)]--;
        }

        // Check for the last window in text
        if (compare(countP, countTW)) {
          document.write("Found at Index " + (N - M) + "<br>");
        }
      }

      // Driver Code
      var txt = "BACDGABCDA";
      var pat = "ABCD";
      search(pat, txt);

</script>
```

**输出:**

```
Found at Index 0
Found at Index 5
Found at Index 6
```

本文由**比于什·古普塔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息