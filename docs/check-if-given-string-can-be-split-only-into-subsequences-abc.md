# 检查给定的字符串是否只能拆分为子序列 ABC

> 原文:[https://www . geesforgeks . org/check-if-给定字符串-只能拆分为子序列-abc/](https://www.geeksforgeeks.org/check-if-given-string-can-be-split-only-into-subsequences-abc/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) **S** ，其中字符串的每个字符或者是“ **A** ”、“ **B** 或者是“ **C** ”。任务是找出是否有可能将字符串拆分为子序列“ **ABC** ”。如果可以拆分，则打印“**是**”。否则，打印“**否**”。

**示例:**

> **输入:** S = "ABABCC"
> **输出:**是
> **解释:**
> 其中一种可能的拆分方式是将字符串拆分为“ABC”的 2 个子序列，如下:
> 
> *   首先通过取索引 0、1 和 4 处的字符来形成子序列“ABC”。
> *   通过取索引 2、3 和 5 处的字符，再次形成子序列“ABC”。
> 
> 因此，该字符串可以被分成“ABC”的两个子序列。
> 
> **输入:** S = "AABBCC"
> **输出:**是
> **解释:**
> 其中一种可能的拆分方式是将字符串拆分为“ABC”的 2 个子序列，如下:
> 
> *   首先通过取索引 0、2 和 4 处的字符来形成子序列“ABC”
> *   通过取索引 1、3 和 5 处的字符，再次形成子序列“ABC”。
> 
> 因此，该字符串可以被分成“ABC”的两个子序列。
> 
> **输入:**S = " BAC "
> T3】输出:否

**方法:**给定的问题可以基于以下观察来解决:

> *   It can be observed that if **n** is not a multiple of 3 or the counts of **a** , **b** and **c** are not equal, then the strings that meet the conditions cannot be split.
> *   Similarly, every **b** must have at least one **a** on the left and one [T4】 C” 【T5] on the right.

按照以下步骤解决问题:

*   初始化 3 个整数的[deq](https://www.geeksforgeeks.org/deque-cpp-stl/)表示 **A、B** 和 **C** ，分别存储字符“ **A** ”、“ **B** ”和“ **C** 的索引。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**S** 的字符，在每次迭代中，如果当前字符是“ **A** ，则将索引 **i** 推入 **A** 。否则，如果当前字符是“ **B** ，则将索引 **i** 推入 **B** 。否则，将索引 **i** 推入 **C** 。
*   如果 **N** 不是 **3** 的倍数，并且字符数“ **A** ”、“ **B** ”和“ **C** 不相等，则打印**“否”**。
*   否则，[使用变量 **i** 迭代德格](https://www.geeksforgeeks.org/deque-cpp-stl/) **B** ，在每次迭代中，如果**B【I】**大于德格 T10】A 的[前元素，则](https://www.geeksforgeeks.org/dequefront-dequeback-c-stl/)[弹出德格](https://www.geeksforgeeks.org/dequepop_front-dequepop_back-c-stl/)T14】A 的前元素。否则打印**否**返回。
*   现在再次[使用变量 **i** 反过来迭代德格](https://www.geeksforgeeks.org/deque-cpp-stl/) **B** ，如果**B【I】**小于德格 **C** 的[最后一个元素，则](https://www.geeksforgeeks.org/dequefront-dequeback-c-stl/)[弹出德格](https://www.geeksforgeeks.org/dequepop_front-dequepop_back-c-stl/) **C** 的最后一个元素。否则打印**否**返回。
*   最后，如果以上情况都不满足，则打印“**是**”作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// string can be splitted into
// subsequences "ABC"
string check(string S)
{
    // Stores the length
    // of the string
    int N = S.length();

    // Stores the indices of 'A'
    deque<int> A;
    // Stores the indices of 'B'
    deque<int> B;
    // Stores the indices of 'C'
    deque<int> C;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If S[i] is equal to 'A'
        if (S[i] == 'A') {
            // Push the index i in A
            A.push_back(i);
        }
        // Else if S[i] is equal
        // to 'B'
        else if (S[i] == 'B') {
            // Push the index i in B
            B.push_back(i);
        }

        // Else if S[i] is equal
        // to 'C'
        else {
            // Push the index i in C
            C.push_back(i);
        }
    }

    // If N is not multiple of 3 or
    // count of characters 'A', 'B'
    // and 'C' are not equal
    if (N % 3 || A.size() != B.size()
        || A.size() != C.size()) {

        // Return "No"
        return "No";
    }
    // Iterate over the deque B
    for (int i = 0; i < B.size(); i++) {

        // If A is not empty and
        // B[i] is greater than
        // A[0]
        if (!A.empty() && B[i] > A[0]) {
            // Removes the front
            // element of A
            A.pop_front();
        }
        // Else return "No"
        else {
            return "No";
        }
    }
    // Iterate over the deque
    // B in reverse
    for (int i = B.size() - 1; i >= 0; i--) {
        // If C is not empty and
        // last element of C is
        // greater thab B[i]
        if (!C.empty() && B[i] < C.back()) {
            // Removes the last
            // element of C
            C.pop_back();
        }
        // Else return "No"
        else {
            return "No";
        }
    }

    // If none of the above
    // cases satisfy return
    //"Yes'
    return "Yes";
}

// Driver Code
int main()
{
    // Input
    string S = "ABABCC";

    // Function call
    cout << check(S) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if the given
// string can be splitted into
// subsequences "ABC"
public static String check(String S)
{

    // Stores the length
    // of the string
    int N = S.length();

    // Stores the indices of 'A'
    Deque<Integer> A = new LinkedList<Integer>();

    // Stores the indices of 'B'
    Deque<Integer> B = new LinkedList<Integer>();

    // Stores the indices of 'C'
    Deque<Integer> C = new LinkedList<Integer>();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // If S[i] is equal to 'A'
        if (S.charAt(i) == 'A')
        {

            // Push the index i in A
            A.addLast(i);
        }

        // Else if S[i] is equal
        // to 'B'
        else if (S.charAt(i) == 'B')
        {

            // Push the index i in B
            B.addLast(i);
        }

        // Else if S[i] is equal
        // to 'C'
        else
        {

            // Push the index i in C
            C.addLast(i);
        }
    }

    // If N is not multiple of 3 or
    // count of characters 'A', 'B'
    // and 'C' are not equal
    if (N % 3 > 0 || A.size() != B.size() ||
        A.size() != C.size())
    {

        // Return "No"
        return "No";
    }

    // Iterate over the deque B
    for(Iterator itr = B.iterator(); itr.hasNext();)
    {
        Integer b = (Integer)itr.next();

        // If A is not empty and
        // curr B is greater than
        // A[0]
        if (A.size() > 0 && b > A.getFirst())
        {

            // Removes the front
            // element of A
            A.pop();
        }

        // Else return "No"
        else
        {
            return "No";
        }
    }

    // Iterate over the deque
    // B in reverse
    for(Iterator itr = B.descendingIterator();
        itr.hasNext();)
    {
        Integer b = (Integer)itr.next();

        // If C is not empty and
        // last element of C is
        // greater thab B[i]
        if (C.size() > 0 && b < C.getLast())
        {

            // Removes the last
            // element of C
            C.pollLast();
        }

        // Else return "No"
        else
        {
            return "No";
        }
    }

    // If none of the above
    // cases satisfy return
    //"Yes'
    return "Yes";
}

// Driver code
public static void main(String[] args)
{

    // Input
    String S = "ABABCC";

    // Function call
    System.out.println(check(S));
}
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to check if the given
# can be splitted into
# subsequences "ABC"
def check(S):

    # Stores the length
    # of the string
    N = len(S)

    # Stores the indices of 'A'
    A = deque()

    # Stores the indices of 'B'
    B = deque()

    # Stores the indices of 'C'
    C = deque()

    # Traverse the S
    for i in range(N):

        # If S[i] is equal to 'A'
        if (S[i] == 'A'):

            # Push the index i in A
            A.append(i)

        # Else if S[i] is equal
        # to 'B'
        elif (S[i] == 'B'):

            # Push the index i in B
            B.append(i)

        # Else if S[i] is equal
        # to 'C'
        else:

            # Push the index i in C
            C.append(i)

    # If N is not multiple of 3 or
    # count of characters 'A', 'B'
    # and 'C' are not equal
    if (N % 3 or len(A) != len(B) or
                 len(A) != len(C)):

        # Return "No"
        return "No"

    # Iterate over the deque B
    for i in range(len(B)):

        # If A is not empty and
        # B[i] is greater than
        # A[0]
        if (len(A) > 0 and B[i] > A[0]):

            # Removes the front
            # element of A
            A.popleft()

        # Else return "No"
        else:
            return "No"

    # Iterate over the deque
    # B in reverse
    for i in range(len(B) - 1, -1, -1):

        # If C is not empty and
        # last element of C is
        # greater thab B[i]
        if (len(C) > 0 and B[i] < C[-1]):

            # Removes the last
            # element of C
            C.popleft()

        # Else return "No"
        else:
            return "No"

    # If none of the above
    # cases satisfy return
    # "Yes'
    return "Yes"

# Driver Code
if __name__ == '__main__':

    # Input
    S = "ABABCC"

    # Function call
    print(check(S))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public static class GFG {

    public static IEnumerable<T> Reverse<T>(this LinkedList<T> list) {
        var el = list.Last;
        while (el != null) {
            yield return el.Value;
            el = el.Previous;
        }
    }

    // Function to check if the given
    // string can be splitted into
    // subsequences "ABC"
    public static string check(string S)
    {

        // Stores the length
        // of the string
        int N = S.Length;

        // Stores the indices of 'A'
        LinkedList<int> A = new LinkedList<int>();

        // Stores the indices of 'B'
        LinkedList<int> B = new LinkedList<int>();

        // Stores the indices of 'C'
        LinkedList<int> C = new LinkedList<int>();

        // Traverse the string S
        for(int i = 0; i < N; i++)
        {

            // If S[i] is equal to 'A'
            if (S[i] == 'A')
            {

                // Push the index i in A
                A.AddLast(i);
            }

            // Else if S[i] is equal
            // to 'B'
            else if (S[i] == 'B')
            {

                // Push the index i in B
                B.AddLast(i);
            }

            // Else if S[i] is equal
            // to 'C'
            else
            {

                // Push the index i in C
                C.AddLast(i);
            }
        }

        // If N is not multiple of 3 or
        // count of characters 'A', 'B'
        // and 'C' are not equal
        if (N % 3 > 0 || A.Count != B.Count ||
            A.Count != C.Count)
        {

            // Return "No"
            return "No";
        }

        // Iterate over the deque B
        foreach(var itr in B)
        {
            int b = itr;

            // If A is not empty and
            // curr B is greater than
            // A[0]
            if (A.Count > 0 && b > A.First.Value)
            {

                // Removes the front
                // element of A
                A.RemoveFirst();
            }

            // Else return "No"
            else
            {
                return "No";
            }
        }

        // Iterate over the deque
        // B in reverse
        foreach(var itr in B.Reverse())
        {
            int b = itr;

            // If C is not empty and
            // last element of C is
            // greater thab B[i]
            if (C.Count > 0 && b < C.Last.Value)
            {

                // Removes the last
                // element of C
                C.RemoveLast();
            }

            // Else return "No"
            else
            {
                return "No";
            }
        }

        // If none of the above
        // cases satisfy return
        //"Yes'
        return "Yes";
    }

    // Driver code
    static public void Main (){

        // Input
        string S = "ABABCC";

        // Function call
        Console.Write(check(S));
    }
}

// This Code is contributed by ShubhamSingh10
```

**Output**

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)