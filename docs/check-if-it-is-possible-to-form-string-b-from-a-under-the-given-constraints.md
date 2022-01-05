# 检查在给定的约束条件下是否有可能从 A 形成字符串 B

> 原文:[https://www . geesforgeks . org/check-if-it-to-form-string-b-from-a-the-given-constraints/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-form-string-b-from-a-under-the-given-constraints/)

给定两个字符串 **A** 和 **B** 以及两个整数 **b** 和 **m** 。任务是找到是否有可能从 **A** 中形成字符串 **B** ，使得 **A** 被分成除最后一组之外的多组 **b** 字符，该组将具有字符 **≤ b** ，并且您可以从每组中选择 atmat**m**字符，并且 **B** 中的字符顺序必须与**A【T29】中的字符顺序相同如果可能，则打印**是**否则打印**否**。**

**示例:**

> **输入:**A = abcbcdefxyz，B = acdxyz，b = 5，m = 2
> **输出:**是
> 组可以是“abcbb”、“cdefx”和“yz”
> 现在“acdxyz”可以用来挑“ac”，而“dx”可以从“cdefx”中挑。
> 最后，“yz”如果最后一组。
> 
> **输入:**A = abcbcdefxyz，B = baz，b = 3，m = 2
> T3】输出:否

**进场:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。遍历字符串 **A** 并将 **A** 的每个字符的频率存储在向量 **S** 中。现在遍历 **B** ，如果当前字符不在向量中，则打印**否**，因为不可能使用 **A** 形成字符串 **B** 。否则，检查当前字符的第一次出现，从最后选择的字符的索引**低**开始，这表示字符串 **A** 中的起始位置，我们要从该位置匹配字符串 **B** 中的字符。记录每个组中存储的字符数。如果超过当前块中字符的给定限制，我们将指针**更新为低**到下一个块。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it is possible
// to form B from A satisfying the given conditions
bool isPossible(string A, string B, int b, int m)
{

    // Vector to store the frequency
    // of characters in A
    vector<int> S[26];

    // Vector to store the count of characters
    // used from a particular group of characters
    vector<int> box(A.length(), 0);

    // Store the frequency of the characters
    for (int i = 0; i < A.length(); i++) {
        S[A[i] - 'a'].push_back(i);
    }

    int low = 0;

    for (int i = 0; i < B.length(); i++) {
        auto it = lower_bound(S[B[i] - 'a'].begin(),
                              S[B[i] - 'a'].end(), low);

        // If a character in B is not
        // present in A
        if (it == S[B[i] - 'a'].end())
            return false;

        int count = (*it) / b;
        box[count] = box[count] + 1;

        // If count of characters used from
        // a particular group of characters
        // exceeds m
        if (box[count] >= m) {
            count++;

            // Update low to the starting index
            // of the next group
            low = (count)*b;
        }

        // If count of characters used from
        // a particular group of characters
        // has not exceeded m
        else
            low = (*it) + 1;
    }

    return true;
}

// Driver code
int main()
{
    string A = "abcbbcdefxyz";
    string B = "acdxyz";
    int b = 5;
    int m = 2;

    if (isPossible(A, B, b, m))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function that returns true if it is
// possible to form B from A satisfying
// the given conditions
static boolean isPossible(String A, String B,
                          int b, int m)
{

    // List to store the frequency
    // of characters in A
    List<List<Integer>> S = new ArrayList<List<Integer>>();

    for(int i = 0; i < 26; i++)
        S.add(new ArrayList<Integer>());

    // Vector to store the count of characters
    // used from a particular group of characters
    int[] box = new int[A.length()];

    // Store the frequency of the characters
    for(int i = 0; i < A.length(); i++)
    {
        S.get(A.charAt(i) - 'a').add(i);
    }

    int low = 0;

    for(int i = 0; i < B.length(); i++)
    {
        List<Integer> indexes = S.get(
            B.charAt(i) - 'a');

        int it = lower_bound(indexes, low);

        // If a character in B is not
        // present in A
        if (it == indexes.size())
            return false;

        int count = indexes.get(it) / b;
        box[count] = box[count] + 1;

        // If count of characters used from
        // a particular group of characters
        // exceeds m
        if (box[count] >= m)
        {
            count++;

            // Update low to the starting index
            // of the next group
            low = (count) * b;
        }

        // If count of characters used from
        // a particular group of characters
        // has not exceeded m
        else
            low = indexes.get(it) + 1;
    }

    return true;
}

static int lower_bound(List<Integer> indexes, int k)
{
    int low = 0, high = indexes.size() - 1;

    while (low < high)
    {
        int mid = (low + high) / 2;
        if (indexes.get(mid) < k)
            low = mid + 1;
        else
            high = mid;
    }
    return (indexes.get(low) < k) ? low + 1 : low;
}

// Driver code
public static void main(String[] args)
{
    String A = "abcbbcdefxyz";
    String B = "acdxyz";
    int b = 5;
    int m = 2;

    if (isPossible(A, B, b, m))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it is
# possible to form B from A satisfying
# the given conditions
def isPossible(A, B, b, m) :

    # List to store the frequency
    # of characters in A
    S = []

    for i in range(26) :

        S.append([])  

    # Vector to store the count of characters
    # used from a particular group of characters
    box = [0] * len(A)

    # Store the frequency of the characters
    for i in range(len(A)) :

        S[ord(A[i]) - ord('a')].append(i)

    low = 0

    for i in range(len(B)) :

        indexes = S[ord(B[i]) - ord('a')]

        it = lower_bound(indexes, low)

        # If a character in B is not
        # present in A
        if (it == len(indexes)) :
            return False

        count = indexes[it] // b
        box[count] = box[count] + 1

        # If count of characters used from
        # a particular group of characters
        # exceeds m
        if (box[count] >= m) :

            count += 1

            # Update low to the starting index
            # of the next group
            low = (count) * b

        # If count of characters used from
        # a particular group of characters
        # has not exceeded m
        else :
            low = indexes[it] + 1

    return True

def lower_bound(indexes, k) :

    low, high = 0, len(indexes) - 1

    while (low < high) :

        mid = (low + high) // 2
        if (indexes[mid] < k) :
            low = mid + 1
        else :
            high = mid

    if indexes[low] < k :
        return (low + 1)
    else :
        return low

A = "abcbbcdefxyz"
B = "acdxyz"
b = 5
m = 2

if (isPossible(A, B, b, m)) :
    print("Yes")
else :
    print("No")

    # This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG {

    // Function that returns true if it is
    // possible to form B from A satisfying
    // the given conditions
    static bool isPossible(string A, string B, int b, int m)
    {

        // List to store the frequency
        // of characters in A
        List<List<int>> S = new List<List<int>>();

        for(int i = 0; i < 26; i++)
        {
            S.Add(new List<int>());
        }

        // Vector to store the count of characters
        // used from a particular group of characters
        int[] box = new int[A.Length];

        // Store the frequency of the characters
        for(int i = 0; i < A.Length; i++)
        {
            S[A[i] - 'a'].Add(i);
        }

        int low = 0;

        for(int i = 0; i < B.Length; i++)
        {
            List<int> indexes = S[B[i] - 'a'];

            int it = lower_bound(indexes, low);

            // If a character in B is not
            // present in A
            if (it == indexes.Count)
                return false;

            int count = indexes[it] / b;
            box[count] = box[count] + 1;

            // If count of characters used from
            // a particular group of characters
            // exceeds m
            if (box[count] >= m)
            {
                count++;

                // Update low to the starting index
                // of the next group
                low = (count) * b;
            }

            // If count of characters used from
            // a particular group of characters
            // has not exceeded m
            else
                low = indexes[it] + 1;
        }

        return true;
    }

    static int lower_bound(List<int> indexes, int k)
    {
        int low = 0, high = indexes.Count - 1;

        while (low < high)
        {
            int mid = (low + high) / 2;
            if (indexes[mid] < k)
                low = mid + 1;
            else
                high = mid;
        }
        return (indexes[low] < k) ? low + 1 : low;
    }

  static void Main() {

    string A = "abcbbcdefxyz";
    string B = "acdxyz";
    int b = 5;
    int m = 2;

    if (isPossible(A, B, b, m))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
  }
}

// This code is contributed by divyesh072019
```

**Output:** 

```
Yes
```