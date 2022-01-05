# 检查给定的字符串是否是另一个字符串的混洗子字符串

> 原文:[https://www . geeksforgeeks . org/check-如果给定字符串是另一个字符串的混洗子字符串/](https://www.geeksforgeeks.org/check-if-the-given-string-is-shuffled-substring-of-another-string/)

给定字符串 **str1** 和 **str2** 。任务是找出 **str1** 是否是 **str2** 混洗形式的子串。如果 **str1** 是 **str2** 混洗形式的子串，则打印“是”，否则打印“否”。

**例**

> **输入:**str1 =“one two four”，str2 =“hellofourtwoonewworld”
> **输出:** YES
> **解释:** str1 是 str2 的混排形式的子串为
> str 2 =“hello”+“four two one”+“world”
> str 2 =“hello”+str 1+“world”，其中 str 1 =“four two one”(混排形式)
> 因此，str 1 是混排形式的 str 2 的子串。
> 
> **输入:** str1 =“玫瑰黄”，str2 =“黄”
> **输出:**否
> **说明:**由于 str1 的长度大于 str2。因此，str1 不是 str2 的子串。

**逼近:**
设 n = str 1 的长度，m = str 2 的长度。

*   如果 n > m，那么字符串 **str1** 永远不能是 **str2** 的子串。
*   否则排序字符串 **str1** 。
*   遍历字符串 **str2**
    1.  将长度为 n 的 **str2** 的所有字符放入另一个字符串 **str** 中。
    2.  对字符串**进行排序，比较**字符串**和**字符串 1** 。**
    3.  如果 str = str1，则字符串 **str1** 是字符串 **str2** 的混洗子串。
    4.  否则重复上述过程，直到 **str2** 的指数达到(I+n–1>m)(在此指数之后，剩余管柱 **str2** 的长度将小于 **str1** 。
    5.  如果在上述步骤中字符串不等于 str1，那么字符串 **str1** 永远不能是 **str2** 的子字符串。

下面是上述方法的实现:

## C++

```
// C++ program to check if string
// str1 is substring of str2 or not.
#include <bits/stdc++.h>
using namespace std;

// Function two check string A
// is shuffled  substring of B
// or not
bool isShuffledSubstring(string A, string B)
{
    int n = A.length();
    int m = B.length();

    // Return false if length of
    // string A is greater than
    // length of string B
    if (n > m) {
        return false;
    }
    else {

        // Sort string A
        sort(A.begin(), A.end());

        // Traverse string B
        for (int i = 0; i < m; i++) {

            // Return false if (i+n-1 >= m)
            // doesn't satisfy
            if (i + n - 1 >= m)
                return false;

            // Initialise the new string
            string str = "";

            // Copy the characters of
            // string B in str till
            // length n
            for (int j = 0; j < n; j++)
                str.push_back(B[i + j]);

            // Sort the string str
            sort(str.begin(), str.end());

            // Return true if sorted
            // string of "str" & sorted
            // string of "A" are equal
            if (str == A)
                return true;
        }
    }
}

// Driver Code
int main()
{
    // Input str1 and str2
    string str1 = "geekforgeeks";
    string str2 = "ekegorfkeegsgeek";

    // Function return true if
    // str1 is shuffled substring
    // of str2
    bool a = isShuffledSubstring(str1, str2);

    // If str1 is substring of str2
    // print "YES" else print "NO"
    if (a)
        cout << "YES";
    else
        cout << "NO";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if String
// str1 is subString of str2 or not.
import java.util.*;

class GFG
{

// Function two check String A
// is shuffled subString of B
// or not
static boolean isShuffledSubString(String A, String B)
{
    int n = A.length();
    int m = B.length();

    // Return false if length of
    // String A is greater than
    // length of String B
    if (n > m)
    {
        return false;
    }
    else
    {

        // Sort String A
        A = sort(A);

        // Traverse String B
        for (int i = 0; i < m; i++)
        {

            // Return false if (i + n - 1 >= m)
            // doesn't satisfy
            if (i + n - 1 >= m)
                return false;

            // Initialise the new String
            String str = "";

            // Copy the characters of
            // String B in str till
            // length n
            for (int j = 0; j < n; j++)
                str += B.charAt(i + j);

            // Sort the String str
            str = sort(str);

            // Return true if sorted
            // String of "str" & sorted
            // String of "A" are equal
            if (str.equals(A))
                return true;
        }
    }
    return false;
}

// Method to sort a string alphabetically
static String sort(String inputString)
{
    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return String.valueOf(tempArray);
}

// Driver Code
public static void main(String[] args)
{
    // Input str1 and str2
    String str1 = "geekforgeeks";
    String str2 = "ekegorfkeegsgeek";

    // Function return true if
    // str1 is shuffled subString
    // of str2
    boolean a = isShuffledSubString(str1, str2);

    // If str1 is subString of str2
    // print "YES" else print "NO"
    if (a)
        System.out.print("YES");
    else
        System.out.print("NO");
    System.out.println();
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to check if string
# str1 is subof str2 or not.

# Function two check A
# is shuffled subof B
# or not
def isShuffledSubstring(A, B):
    n = len(A)
    m = len(B)

    # Return false if length of
    # A is greater than
    # length of B
    if (n > m):
        return False
    else:

        # Sort A
        A = sorted(A)

        # Traverse B
        for i in range(m):

            # Return false if (i+n-1 >= m)
            # doesn't satisfy
            if (i + n - 1 >= m):
                return False

            # Initialise the new string
            Str = ""

            # Copy the characters of
            # B in str till
            # length n
            for j in range(n):
                Str += (B[i + j])

            # Sort the str
            Str = sorted(Str)

            # Return true if sorted
            # of "str" & sorted
            # of "A" are equal
            if (Str == A):
                return True

# Driver Code
if __name__ == '__main__':

    # Input str1 and str2
    Str1 = "geekforgeeks"
    Str2 = "ekegorfkeegsgeek"

    # Function return true if
    # str1 is shuffled substring
    # of str2
    a = isShuffledSubstring(Str1, Str2)

    # If str1 is subof str2
    # print "YES" else print "NO"
    if (a):
        print("YES")
    else:
        print("NO")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to check if String
// str1 is subString of str2 or not.
using System;

public class GFG
{

// Function two check String A
// is shuffled subString of B
// or not
static bool isShuffledSubString(String A, String B)
{
    int n = A.Length;
    int m = B.Length;

    // Return false if length of
    // String A is greater than
    // length of String B
    if (n > m)
    {
        return false;
    }
    else
    {

        // Sort String A
        A = sort(A);

        // Traverse String B
        for (int i = 0; i < m; i++)
        {

            // Return false if (i + n - 1 >= m)
            // doesn't satisfy
            if (i + n - 1 >= m)
                return false;

            // Initialise the new String
            String str = "";

            // Copy the characters of
            // String B in str till
            // length n
            for (int j = 0; j < n; j++)
                str += B[i + j];

            // Sort the String str
            str = sort(str);

            // Return true if sorted
            // String of "str" & sorted
            // String of "A" are equal
            if (str.Equals(A))
                return true;
        }
    }
    return false;
}

// Method to sort a string alphabetically
static String sort(String inputString)
{
    // convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // sort tempArray
    Array.Sort(tempArray);

    // return new sorted string
    return String.Join("",tempArray);
}

// Driver Code
public static void Main(String[] args)
{
    // Input str1 and str2
    String str1 = "geekforgeeks";
    String str2 = "ekegorfkeegsgeek";

    // Function return true if
    // str1 is shuffled subString
    // of str2
    bool a = isShuffledSubString(str1, str2);

    // If str1 is subString of str2
    // print "YES" else print "NO"
    if (a)
        Console.Write("YES");
    else
        Console.Write("NO");
    Console.WriteLine();
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to check if string
// str1 is substring of str2 or not.

// Function two check string A
// is shuffled  substring of B
// or not
function isShuffledSubstring(A, B)
{
    var n = A.length;
    var m = B.length;

    // Return false if length of
    // string A is greater than
    // length of string B
    if (n > m) {
        return false;
    }
    else {

        // Sort string A
        A = A.split('').sort().join('');

        // Traverse string B
        for (var i = 0; i < m; i++) {

            // Return false if (i+n-1 >= m)
            // doesn't satisfy
            if (i + n - 1 >= m)
                return false;

            // Initialise the new string
            var str = [];

            // Copy the characters of
            // string B in str till
            // length n
            for (var j = 0; j < n; j++)
                str.push(B[i + j]);

            // Sort the string str
            str = str.sort()

            // Return true if sorted
            // string of "str" & sorted
            // string of "A" are equal
            if (str.join('') == A)
                return true;
        }
    }
}

// Driver Code
// Input str1 and str2
var str1 = "geekforgeeks";
var str2 = "ekegorfkeegsgeek";
// Function return true if
// str1 is shuffled substring
// of str2
var a = isShuffledSubstring(str1, str2);
// If str1 is substring of str2
// print "YES" else print "NO"
if (a)
    document.write( "YES");
else
    document.write( "NO");
document.write("<br>");

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(m*n*log(n))，其中 n =字符串 str1 的长度，m =字符串 str2 的长度
**辅助空间:** O(n)

**高效解决方案:**这个问题是一个更简单版本的[字谜搜索](https://www.geeksforgeeks.org/anagram-substring-search-search-permutations/)。利用字符频率计数可以在线性时间内解决。
我们可以在字母表大小固定的假设下实现 O(n)时间复杂度，这通常是真的，因为 ASCII 中最多有 256 个可能的字符。想法是使用两个计数数组:

1)第一计数数组存储模式中字符的频率。
2)第二计数数组存储当前文本窗口中字符的频率。
需要注意的重要一点是，比较两个计数数组的时间复杂度为 O(1)，因为其中的元素数量是固定的(与模式和文本大小无关)。以下是该算法的步骤。
1)在第一计数数组 countP[]中存储模式频率的计数。此外，在数组 countw[]中的第一个文本窗口中存储字符的频率计数。
2)现在运行从 i = M 到 N-1 的循环。循环执行以下操作。
…..a)如果两个计数数组相同，我们发现一个匹配项。
…..b)递增 countw[]
中文本当前字符的计数…..c)countWT[]
中前一个窗口第一个字符的递减计数 3)上一个窗口没有被上面的循环检查，所以明确检查。

以下是上述算法的实现。

## C++

```
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
bool search(char *pat, char *txt)
{
    int M = strlen(pat), N = strlen(txt);

    // countP[]: Store count of all characters of pattern
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
           return true;

        // Add current character to current window
        (countTW[txt[i]])++;

        // Remove the first character of previous window
        countTW[txt[i-M]]--;
    }

    // Check for the last window in text
    if (compare(countP, countTW))
        return true;
        return false;
}

/* Driver program to test above function */
int main()
{
    char txt[] = "BACDGABCDA";
    char pat[] = "ABCD";
    if (search(pat, txt))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

// This function returns true if
// contents of arr1[] and arr2[]
// are same, otherwise false.
static boolean compare(int []arr1, int []arr2)
{
    for(int i = 0; i < 256; i++)
        if (arr1[i] != arr2[i])
            return false;

    return true;
}

// This function search for all
// permutations of pat[] in txt[]
static boolean search(String pat, String txt)
{
    int M = pat.length();
    int N = txt.length();

    // countP[]: Store count of all
    // characters of pattern
    // countTW[]: Store count of
    // current window of text
    int []countP = new int [256];
    int []countTW = new int [256];
    for(int i = 0; i < 256; i++)
    {
        countP[i] = 0;
        countTW[i] = 0;
    }

    for(int i = 0; i < M; i++)
    {
        (countP[pat.charAt(i)])++;
        (countTW[txt.charAt(i)])++;
    }

    // Traverse through remaining
    // characters of pattern
    for(int i = M; i < N; i++)
    {

        // Compare counts of current
        // window of text with
        // counts of pattern[]
        if (compare(countP, countTW))
            return true;

        // Add current character to
        // current window
        (countTW[txt.charAt(i)])++;

        // Remove the first character
        // of previous window
        countTW[txt.charAt(i - M)]--;
    }

    // Check for the last window in text
    if (compare(countP, countTW))
        return true;
        return false;
}

// Driver code
public static void main(String[] args)
{
    String txt = "BACDGABCDA";
    String pat = "ABCD";

    if (search(pat, txt))
        System.out.println("Yes");
    else
        System.out.println("NO");
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
MAX = 256

# This function returns true if contents
# of arr1[] and arr2[] are same,
# otherwise false.
def compare(arr1, arr2):

    global MAX

    for i in range(MAX):
        if (arr1[i] != arr2[i]):
            return False

    return True

# This function search for all permutations
# of pat[] in txt[]
def search(pat, txt):

    M = len(pat)
    N = len(txt)

    # countP[]: Store count of all characters
    #           of pattern
    # countTW[]: Store count of current window
    #            of text
    countP = [0 for i in range(MAX)]
    countTW = [0 for i in range(MAX)]

    for i in range(M):
        countP[ord(pat[i])] += 1
        countTW[ord(txt[i])] += 1

    # Traverse through remaining
    # characters of pattern
    for i in range(M, N):

        # Compare counts of current window
        # of text with counts of pattern[]
        if (compare(countP, countTW)):
            return True

        # Add current character
        # to current window
        countTW[ord(txt[i])] += 1

        # Remove the first character
        # of previous window
        countTW[ord(txt[i - M])] -= 1

    # Check for the last window in text
    if(compare(countP, countTW)):
        return True
        return False

# Driver code
txt = "BACDGABCDA"
pat = "ABCD"

if (search(pat, txt)):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
using System.Collections.Generic;
using System;

class GFG{

// This function returns true if
// contents of arr1[] and arr2[]
// are same, otherwise false.
static bool compare(int []arr1, int []arr2)
{
    for(int i = 0; i < 256; i++)
        if (arr1[i] != arr2[i])
            return false;

    return true;
}

// This function search for all
// permutations of pat[] in txt[]
static bool search(String pat, String txt)
{
    int M = pat.Length;
    int N = txt.Length;

    // countP[]: Store count of all
    // characters of pattern
    // countTW[]: Store count of
    // current window of text
    int []countP = new int [256];
    int []countTW = new int [256];

    for(int i = 0; i < 256; i++)
    {
        countP[i] = 0;
        countTW[i] = 0;
    }

    for(int i = 0; i < M; i++)
    {
        (countP[pat[i]])++;
        (countTW[txt[i]])++;
    }

    // Traverse through remaining
    // characters of pattern
    for(int i = M; i < N; i++)
    {

        // Compare counts of current
        // window of text with
        // counts of pattern[]
        if (compare(countP, countTW))
            return true;

        // Add current character to
        // current window
        (countTW[txt[i]])++;

        // Remove the first character
        // of previous window
        countTW[txt[i - M]]--;
    }

    // Check for the last window in text
    if (compare(countP, countTW))
        return true;
        return false;
}

// Driver code
public static void Main()
{
    string txt = "BACDGABCDA";
    string pat = "ABCD";

    if (search(pat, txt))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// This function returns true if
// contents of arr1[] and arr2[]
// are same, otherwise false.
function compare(arr1,arr2)
{
    for(let i = 0; i < 256; i++)
        if (arr1[i] != arr2[i])
            return false;

    return true;
}

// This function search for all
// permutations of pat[] in txt[]
function search(pat,txt)
{
    let M = pat.length;
    let N = txt.length;

    // countP[]: Store count of all
    // characters of pattern
    // countTW[]: Store count of
    // current window of text
    let countP = new Array(256);
    let countTW = new Array(256);
    for(let i = 0; i < 256; i++)
    {
        countP[i] = 0;
        countTW[i] = 0;
    }
    for(let i = 0; i < 256; i++)
    {
        countP[i] = 0;
        countTW[i] = 0;
    }

    for(let i = 0; i < M; i++)
    {
        (countP[pat[i].charCodeAt(0)])++;
        (countTW[txt[i].charCodeAt(0)])++;
    }

    // Traverse through remaining
    // characters of pattern
    for(let i = M; i < N; i++)
    {

        // Compare counts of current
        // window of text with
        // counts of pattern[]
        if (compare(countP, countTW))
            return true;

        // Add current character to
        // current window
        (countTW[txt[i].charCodeAt(0)])++;

        // Remove the first character
        // of previous window
        countTW[txt[i - M].charCodeAt(0)]--;
    }

    // Check for the last window in text
    if (compare(countP, countTW))
        return true;
        return false;
}

// Driver code
let txt = "BACDGABCDA";
let pat = "ABCD";

if (search(pat, txt))
    document.write("Yes");
else
    document.write("NO");

// This code is contributed by ab2127
</script>
```

**Output:** 

```
Yes
```