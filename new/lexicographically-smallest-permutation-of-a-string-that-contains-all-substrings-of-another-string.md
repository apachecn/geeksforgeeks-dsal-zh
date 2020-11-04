# 包含另一个字符串的所有子字符串的字符串的按字典顺序排列的最小排列

> 原文：[https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-a-string-that-contains-all-substrings-of-another-string/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-a-string-that-contains-all-substrings-of-another-string/)

给定两个字符串 **A** 和 **B** ，任务是从字典上找到字符串 **B** 的最小排列，以使其包含字符串 **A 中的每个子字符串** 作为其[子字符串](https://www.geeksforgeeks.org/length-of-the-longest-valid-substring/)。 如果无法进行有效的排列，请打印“ **-1”** 。

**示例**：

> **输入**：A =“ aa”，B =“ ababab”
> **输出**：aaabbb
> **说明**：。
> A 的所有可能子串 是（'a'，'a'，'aa'）。
> 将字符串 B 重新排列为“ aaabb”。
> 现在，在字典上，“ aaabb”是 B 的最小排列，其中包含 A 的所有子串。
> 
> **输入**：A =“ aaa”，B =“ ramialsadaka” 是（'a'，'aa'，'aaa'）。
> 将字符串 B 重新排列为“ aaaaadiklmrs”。
> 现在，“ aaaaadiklmrs”是 B 在字典上的最小排列，其中包含 A 的所有子串。

**朴素的方法**：最简单的方法是[生成字符串 **B**](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/) 的所有可能排列，然后从所有这些排列中，从字典上找到包含所有子串的最小排列 **A** 的组成。

**时间复杂度**：O（N！）

**辅助空间**：`O(1)`

**有效方法**：为优化上述方法，主要观察结果是，包含 **A** 所有子字符串的最小字符串是字符串 **A** 本身。 因此，要对字符串 **B** 重新排序并包含 **A** 的所有子字符串，它必须包含 **A** 作为子字符串。 仅当字符串 **B** 中每个字符的[频率大于或等于**中的频率时，重新排序的字符串 B 才能包含 **A** 作为其子字符串。 A** 。 步骤如下：](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)

1.  计算数组 **freq []** 中字符串 **B** 中每个字符的[频率，然后从中减去字符串 **A 中相应字符的频率** 。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)

2.  为了按字典顺序形成最小的字符串，请初始化一个空字符串**结果**，然后将其追加，其值小于字符串 **A** 的第一个字符的所有剩余字符。

3.  在添加等于第一个字符 **A** 的所有字符之前，请检查是否存在小于字符串 **A** 中第一个字符的字符。 如果是这样，则将 A 附加到第一个结果，然后将所有其余字符都等于 A 的第一个字符，以使重新排序的字符串在字典上最小。

4.  否则，附加所有剩余的 A [0]，然后附加 A。

5.  最后，将其余字符附加到结果中。

6.  完成上述步骤后，打印字符串**结果**。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to reorder the string B
// to contain all the substrings of A
string reorderString(string A, string B)
{
    // Find length of strings
    int size_a = A.length();
    int size_b = B.length();

    // Initialize array to count the
    // frequencies of the character
    int freq[300] = { 0 };

    // Counting frequencies of
    // character in B
    for (int i = 0; i < size_b; i++)
        freq[B[i]]++;

    // Find remaining character in B
    for (int i = 0; i < size_a; i++)
        freq[A[i]]--;

    for (int j = 'a'; j <= 'z'; j++) {
        if (freq[j] < 0)
            return "-1";
    }

    // Declare the reordered string
    string answer;

    for (int j = 'a'; j < A[0]; j++)

        // Loop until freq[j] > 0
        while (freq[j] > 0) {
            answer.push_back(j);

            // Decrement the value
            // from freq array
            freq[j]--;
        }

    int first = A[0];

    for (int j = 0; j < size_a; j++) {

        // Check if A[j] > A[0]
        if (A[j] > A[0])
            break;

        // Check if A[j] < A[0]
        if (A[j] < A[0]) {
            answer += A;
            A.clear();
            break;
        }
    }

    // Append the remaining characters
    // to the end of the result
    while (freq[first] > 0) {
        answer.push_back(first);
        --freq[first];
    }

    answer += A;

    for (int j = 'a'; j <= 'z'; j++)

        // Push all the values from
        // frequency array in the answer
        while (freq[j]--)
            answer.push_back(j);

    // Return the answer
    return answer;
}

// Driver Code
int main()
{
    // Given strings A and B
    string A = "aa";
    string B = "ababab";

    // Function Call
    cout << reorderString(A, B);

    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
class GFG{

// Function to reorder the String B
// to contain all the subStrings of A
static String reorderString(char []A, 
                            char []B)
{
  // Find length of Strings
  int size_a = A.length;
  int size_b = B.length;

  // Initialize array to count the
  // frequencies of the character
  int freq[] = new int[300];

  // Counting frequencies of
  // character in B
  for (int i = 0; i < size_b; i++)
    freq[B[i]]++;

  // Find remaining character in B
  for (int i = 0; i < size_a; i++)
    freq[A[i]]--;

  for (int j = 'a'; j <= 'z'; j++) 
  {
    if (freq[j] < 0)
      return "-1";
  }

  // Declare the reordered String
  String answer = "";

  for (int j = 'a'; j < A[0]; j++)

    // Loop until freq[j] > 0
    while (freq[j] > 0) 
    {
      answer+=j;

      // Decrement the value
      // from freq array
      freq[j]--;
    }

  int first = A[0];

  for (int j = 0; j < size_a; j++) 
  {
    // Check if A[j] > A[0]
    if (A[j] > A[0])
      break;

    // Check if A[j] < A[0]
    if (A[j] < A[0]) 
    {
      answer += String.valueOf(A);
      A = new char[A.length];
      break;
    }
  }

  // Append the remaining characters
  // to the end of the result
  while (freq[first] > 0) 
  {
    answer += String.valueOf((char)first);
    --freq[first];
  }

  answer += String.valueOf(A);

  for (int j = 'a'; j <= 'z'; j++)

    // Push all the values from
    // frequency array in the answer
    while (freq[j]-- > 0)
      answer += ((char)j);

  // Return the answer
  return answer;
}

// Driver Code
public static void main(String[] args)
{
  // Given Strings A and B
  String A = "aa";
  String B = "ababab";

  // Function Call
  System.out.print(reorderString(A.toCharArray(), 
                                 B.toCharArray()));
}
}

// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python3 program for the above approach

# Function to reorder the B
# to contain all the substrings of A
def reorderString(A, B):

    # Find length of strings
    size_a = len(A)
    size_b = len(B)

    # Initialize array to count the
    # frequencies of the character
    freq = [0] * 300

    # Counting frequencies of
    # character in B
    for i in range(size_b):
        freq[ord(B[i])] += 1

    # Find remaining character in B
    for i in range(size_a):
        freq[ord(A[i])] -= 1

    for j in range(ord('a'), ord('z') + 1):
        if (freq[j] < 0):
            return "-1"

    # Declare the reordered string
    answer = []

    for j in range(ord('a'), ord(A[0])):

        # Loop until freq[j] > 0
        while (freq[j] > 0):
            answer.append(j)

            # Decrement the value
            # from freq array
            freq[j] -= 1

    first = A[0]

    for j in range(size_a):

        # Check if A[j] > A[0]
        if (A[j] > A[0]):
            break

        # Check if A[j] < A[0]
        if (A[j] < A[0]):
            answer += A
            A = ""
            break

    # Append the remaining characters
    # to the end of the result
    while (freq[ord(first)] > 0):
        answer.append(first)
        freq[ord(first)] -= 1

    answer += A

    for j in range(ord('a'), ord('z') + 1):

        # Push all the values from
        # frequency array in the answer
        while (freq[j]):
            answer.append(chr(j))
            freq[j] -= 1

    # Return the answer
    return "".join(answer)

# Driver Code
if __name__ == '__main__':

    # Given strings A and B
    A = "aa"
    B = "ababab"

    # Function call
    print(reorderString(A, B))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for 
// the above approach
using System;
class GFG{

// Function to reorder the String B
// to contain all the subStrings of A
static String reorderString(char []A, 
                            char []B)
{
  // Find length of Strings
  int size_a = A.Length;
  int size_b = B.Length;

  // Initialize array to count the
  // frequencies of the character
  int []freq = new int[300];

  // Counting frequencies of
  // character in B
  for (int i = 0; i < size_b; i++)
    freq[B[i]]++;

  // Find remaining character in B
  for (int i = 0; i < size_a; i++)
    freq[A[i]]--;

  for (int j = 'a'; j <= 'z'; j++) 
  {
    if (freq[j] < 0)
      return "-1";
  }

  // Declare the reordered String
  String answer = "";

  for (int j = 'a'; j < A[0]; j++)

    // Loop until freq[j] > 0
    while (freq[j] > 0) 
    {
      answer+=j;

      // Decrement the value
      // from freq array
      freq[j]--;
    }

  int first = A[0];

  for (int j = 0; j < size_a; j++) 
  {
    // Check if A[j] > A[0]
    if (A[j] > A[0])
      break;

    // Check if A[j] < A[0]
    if (A[j] < A[0]) 
    {
      answer += String.Join("", A);
      A = new char[A.Length];
      break;
    }
  }

  // Append the remaining characters
  // to the end of the result
  while (freq[first] > 0) 
  {
    answer += String.Join("", (char)first);
    --freq[first];
  }

  answer += String.Join("", A);

  for (int j = 'a'; j <= 'z'; j++)

    // Push all the values from
    // frequency array in the answer
    while (freq[j]-- > 0)
      answer += ((char)j);

  // Return the answer
  return answer;
}

// Driver Code
public static void Main(String[] args)
{
  // Given Strings A and B
  String A = "aa";
  String B = "ababab";

  // Function Call
  Console.Write(reorderString(A.ToCharArray(), 
                              B.ToCharArray()));
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
aaabbb

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *



