# 通过重新排列字符

，从给定字符串中选出最大可能的回文字符串

> 原文:[https://www . geeksforgeeks . org/最大回文字符串-通过重新排列字符从给定字符串中可能得到的字符串/](https://www.geeksforgeeks.org/largest-palindromic-string-possible-from-given-strings-by-rearranging-the-characters/)

给定两个字符串 **S** 和 **P** ，任务是在重新排列字符后，通过从给定的字符串 **S** 和 **P** 中选择字符来找到最大的回文可能字符串。
**注:**如果可能有很多答案，那就找字典上最小的 **T** 最大长度。

**示例:**

> **输入:** S = "abad "，T = "eeff"
> **输出:** aefbfea
> **解释:**
> 来自第一个字符串的“aba”和来自第二个字符串的“effe”都是回文。
> 用这两个做一个新的回文 T“aefbfea”，这个回文在字典上是最小的。
> T 也是可能的最大长度。
> 注:**“ada”，虽然这样会给出同样长度的 T 即 7，但那不会是字典上最小的。**
> 
> ****输入:** S = "aeabb "，T = "dfedf"
> **输出:** abdeffedba
> **解释:**
> 来自第一个字符串“abeba”和来自第二个字符串“dfefd”，都是回文。将两者结合起来得到 T:“abde ffed ba”在字典上是最小的。**

****方法:**思路是从字符串 **S** 和 **P** 中提取所有字符，分别出现**甚至**多次。作为子串，两个串的 **A** 和 **B** 都具有在 **S** 和 **P** 中分别出现偶数次的所有字符，成为来自父串的最大回文。以下是步骤:**

1.  **从字符串 **S** 和 **P** 中提取一个字符，这样它们将分别出现在从每个字符串中提取的回文的中间。将独特的元素放在 **T** 中间。**
2.  **从子串 **A** 和 **B** 中获取唯一元素的可能情况是:

    *   如果在 **A** 和 **B** 中都存在一个独特的元素，那么取两者，因为**会使 T 的长度增加 2** 。
    *   如果在 **S** 和 **P** 中都存在独特的元素，但不是同一个元素，那么取较小的元素，因为这将使字典序上最小的回文 **T** 。
    *   如果两者都没有独特的元素，那么用来自 **A** 和 **B** 的元素制作绳子 **T** 。** 
3.  **使用[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)对父字符串中出现偶数次的字符进行计数。另外，使用另一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来计算制作 **T** 时要使用的字符数。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find largest palindrome
// possible from S and P after rearranging
// characters to make palindromic string T
string mergePalindromes(string S, string P)
{

    // Using unordered_map to store
    // frequency of elements
    // mapT will have freq of elements of T
    unordered_map<char, int> mapS, mapP, mapT;

    // Size of both the strings
    int n = S.size(), m = P.size();

    for (int i = 0; i < n; i++) {
        mapS[S[i]]++;
    }
    for (int i = 0; i < m; i++) {
        mapP[P[i]]++;
    }

    // Take all character in mapT which
    // occur even number of times in
    // respective strings & simultaneously
    // update number of characters left in map
    for (char i = 'a'; i <= 'z'; i++) {

        if (mapS[i] % 2 == 0) {
            mapT[i] += mapS[i];
            mapS[i] = 0;
        }
        else {
            mapT[i] += mapS[i] - 1;
            mapS[i] = 1;
        }

        if (mapP[i] % 2 == 0) {
            mapT[i] += mapP[i];
            mapP[i] = 0;
        }
        else {
            mapT[i] += mapP[i] - 1;
            mapP[i] = 1;
        }
    }

    // Check if a unique character is
    // present in both string S and P
    int check = 0;

    for (char i = 'a'; i <= 'z'; i++) {
        if (mapS[i] > 0 && mapP[i] > 0) {
            mapT[i] += 2;
            check = 1;
            break;
        }
    }

    // Making string T in two halves
    // half1 - first half
    // half2 - second half
    string half1 = "", half2 = "";

    for (char i = 'a'; i <= 'z'; i++) {
        for (int j = 0; (2 * j) < mapT[i]; j++) {
            half1 += i;
            half2 += i;
        }
    }

    // Reverse the half2 to attach with half1
    // to make palindrome T
    reverse(half2.begin(), half2.end());

    // If same unique element is present
    // in both S and P, then taking that only
    // which is already taken through mapT
    if (check) {
        return half1 + half2;
    }

    // If same unique element is not
    // present in S and P, then take
    // characters that make string T
    // lexicographically smallest
    for (char i = 'a'; i <= 'z'; i++) {
        if (mapS[i] > 0 || mapP[i] > 0) {
            half1 += i;
            return half1 + half2;
        }
    }

    // If no unique element is
    // present in both string S and P
    return half1 + half2;
}

// Driver Code
int main()
{
    // Given two strings S and P
    string S = "aeabb";
    string P = "dfedf";

    // Function Call
    cout << mergePalindromes(S, P);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to find largest palindrome
// possible from S and P after rearranging
// characters to make palindromic string T
static String mergePalindromes(StringBuilder S,
                               StringBuilder P)
{
    // Using unordered_map to store
    // frequency of elements
    // mapT will have freq of elements of T
    Map<Character, Integer> mapS = new HashMap<>(),
                            mapP = new HashMap<>(),
                            mapT = new HashMap<>();

    // Size of both the strings
    int n = S.length(), m = P.length();

    for(int i = 0; i < n; i++)
    {
        mapS.put(S.charAt(i),
        mapS.getOrDefault(S.charAt(i), 0) + 1);
    }
    for(int i = 0; i < m; i++)
    {
        mapP.put(P.charAt(i),
        mapP.getOrDefault(P.charAt(i), 0) + 1);
    }

    // Take all character in mapT which
    // occur even number of times in
    // respective strings & simultaneously
    // update number of characters left in map
    for(char i = 'a'; i <= 'z'; i++)
    {
        if (mapS.getOrDefault(i, 0) % 2 == 0)
        {
           mapT.put(i,mapT.getOrDefault(i, 0) +
           mapS.getOrDefault(i, 0));
           mapS.put(i, 0);
        }
        else
        {
            mapT.put(i,mapT.getOrDefault(i, 0) +
            mapS.getOrDefault(i, 0) - 1);
            mapS.put(i, 1);
        }

        if (mapP.getOrDefault(i, 0) % 2 == 0)
        {
            mapT.put(i, mapT.getOrDefault(i, 0) +
            mapP.getOrDefault(i, 0));
            mapP.put(i, 0);
        }
        else
        {
            mapT.put(i, mapT.getOrDefault(i, 0) +
            mapP.getOrDefault(i, 0) - 1);
            mapP.put(i, 1);
        }
    }

    // Check if a unique character is
    // present in both string S and P
    int check = 0;

    for(char i = 'a'; i <= 'z'; i++)
    {
        if (mapS.getOrDefault(i, 0) > 0 &&
            mapP.getOrDefault(i, 0) > 0)
        {
            mapT.put(i, mapT.getOrDefault(i, 0) + 2);
            check = 1;
            break;
        }
    }

    // Making string T in two halves
    // half1 - first half
    // half2 - second half
    StringBuilder half1 = new StringBuilder(),
                  half2 = new StringBuilder();

    for(char i = 'a'; i <= 'z'; i++)
    {
        for(int j = 0;
           (2 * j) < mapT.getOrDefault(i, 0);
                j++)
        {
            half1.append(i);
            half2.append(i);
        }
    }

    // Reverse the half2 to attach with half1
    // to make palindrome T
    StringBuilder tmp = half2.reverse();

    // If same unique element is present
    // in both S and P, then taking that only
    // which is already taken through mapT
    if (check == 1)
    {
        return half1.append(tmp).toString();
    }

    // If same unique element is not
    // present in S and P, then take
    // characters that make string T
    // lexicographically smallest
    for(char i = 'a'; i <= 'z'; i++)
    {
        if (mapS.getOrDefault(i, 0) > 0 ||
            mapP.getOrDefault(i, 0) > 0)
        {
            half1.append(i);
            return half1.append(tmp).toString();
        }
    }

    // If no unique element is
    // present in both string S and P
    return half1.append(tmp).toString();
}

// Driver code
public static void main (String[] args)
{

    // Given two strings S and P
    StringBuilder S = new StringBuilder("aeabb");
    StringBuilder P = new StringBuilder("dfedf");

    // Function call
    System.out.println(mergePalindromes(S, P));
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program for the above approach
from collections import defaultdict

# Function to find largest palindrome
# possible from S and P after rearranging
# characters to make palindromic string T
def mergePalindromes(S, P):

    # Using unordered_map to store
    # frequency of elements
    # mapT will have freq of elements of T
    mapS = defaultdict(lambda : 0)
    mapP = defaultdict(lambda : 0)
    mapT = defaultdict(lambda : 0)

    # Size of both the strings
    n = len(S)
    m = len(P)

    for i in range(n):
        mapS[ord(S[i])] += 1

    for i in range(m):
        mapP[ord(P[i])] += 1

    # Take all character in mapT which
    # occur even number of times in
    # respective strings & simultaneously
    # update number of characters left in map
    for i in range(ord('a'), ord('z') + 1):
        if(mapS[i] % 2 == 0):
            mapT[i] += mapS[i]
            mapS[i] = 0
        else:
            mapT[i] += mapS[i] - 1
            mapS[i] = 1

        if (mapP[i] % 2 == 0):
            mapT[i] += mapP[i]
            mapP[i] = 0
        else:
            mapT[i] += mapP[i] - 1
            mapP[i] = 1

    # Check if a unique character is
    # present in both string S and P
    check = 0

    for i in range(ord('a'), ord('z') + 1):
        if (mapS[i] > 0 and mapP[i] > 0):
            mapT[i] += 2
            check = 1
            break

    # Making string T in two halves
    # half1 - first half
    # half2 - second half
    half1, half2 = "", ""

    for i in range(ord('a'), ord('z') + 1):
        j = 0
        while((2 * j) < mapT[i]):
            half1 += chr(i)
            half2 += chr(i)
            j += 1

    # Reverse the half2 to attach with half1
    # to make palindrome
    half2 = half2[::-1]

    # If same unique element is present
    # in both S and P, then taking that only
    # which is already taken through mapT
    if(check):
        return half1 + half2

    # If same unique element is not
    # present in S and P, then take
    # characters that make string T
    # lexicographically smallest
    for i in range(ord('a'), ord('z') + 1):
        if(mapS[i] > 0 or mapP[i] > 0):
            half1 += chr(i)
            return half1 + half2

    # If no unique element is
    # present in both string S and P
    return half1 + half2

# Driver Code

# Given string S and P
S = "aeabb"
P = "dfedf"

# Function call
print(mergePalindromes(S, P))

# This code is contributed by Shivam Singh
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Text;

class GFG{

// Function to find largest palindrome
// possible from S and P after rearranging
// characters to make palindromic string T
static string mergePalindromes(string S,
                               string P)
{

    // Using unordered_map to store
    // frequency of elements mapT will
    // have freq of elements of T
    Dictionary<char,
               int> mapS = new Dictionary<char,
                                          int>();
    Dictionary<char,
               int> mapP = new Dictionary<char,
                                          int>();
    Dictionary<char,
               int> mapT = new Dictionary<char,
                                          int>();

    // Size of both the strings
    int n = S.Length, m = P.Length;

    for(char i = 'a'; i <= 'z'; i++)
    {
        mapS[i] = 0;
        mapP[i] = 0;
        mapT[i] = 0;
    }

    for(int i = 0; i < n; i++)
    {
        mapS[S[i]]++;
    }

    for(int i = 0; i < m; i++)
    {
        mapP[P[i]]++;
    }

    // Take all character in mapT which
    // occur even number of times in
    // respective strings & simultaneously
    // update number of characters left in map
    for(char i = 'a'; i <= 'z'; i++)
    {
        if (mapS[i] % 2 == 0)
        {
            mapT[i] += mapS[i];
            mapS[i] = 0;
        }
        else
        {
            mapT[i] += mapS[i] - 1;
            mapS[i] = 1;
        }

        if (mapP[i] % 2 == 0)
        {
            mapT[i] += mapP[i];
            mapP[i] = 0;
        }
        else
        {
            mapT[i] += mapP[i] - 1;
            mapP[i] = 1;
        }
    }

    // Check if a unique character is
    // present in both string S and P
    int check = 0;

    for(char i = 'a'; i <= 'z'; i++)
    {
        if (mapS[i] > 0 && mapP[i] > 0)
        {
            mapT[i] += 2;
            check = 1;
            break;
        }
    }

    // Making string T in two halves
    // half1 - first half
    // half2 - second half
    string half1 = "", half2 = "";

    for(char i = 'a'; i <= 'z'; i++)
    {
        for(int j = 0; (2 * j) < mapT[i]; j++)
        {
            half1 += i;
            half2 += i;
        }
    }

    // Reverse the half2 to attach with half1
    // to make palindrome T
    char[] tmp = half2.ToCharArray();
    Array.Reverse(tmp);
    half2 = new string(tmp);

    // If same unique element is present
    // in both S and P, then taking that only
    // which is already taken through mapT
    if (check != 0)
    {
        return half1 + half2;
    }

    // If same unique element is not
    // present in S and P, then take
    // characters that make string T
    // lexicographically smallest
    for(char i = 'a'; i <= 'z'; i++)
    {
        if (mapS[i] > 0 || mapP[i] > 0)
        {
            half1 += i;
            return half1 + half2;
        }
    }

    // If no unique element is
    // present in both string S and P
    return half1 + half2;
}

// Driver Code
public static void Main(string []args)
{

    // Given two strings S and P
    string S = "aeabb";
    string P = "dfedf";

    Console.Write(mergePalindromes(S, P));
}
}

// This code is contributed by rutvik_56
```

****Output:** 

```
abdeffedba

```** 

*****时间复杂度:** O(N)，其中 N 是字符串 S 或 p 的长度*
***辅助空间:** O(N)***