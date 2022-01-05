# 找到最后一个能够翻转二进制字符串中一个字符的玩家

> 原文:[https://www . geesforgeks . org/find-最后一个能够翻转二进制字符串中字符的玩家/](https://www.geeksforgeeks.org/find-the-last-player-to-be-able-to-flip-a-character-in-a-binary-string/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是如果两个玩家 **A** 和 **B** 按照以下规则进行最佳游戏，则找到游戏的赢家:

*   玩家 A 总是开始游戏。
*   在玩家的第一回合中，他可以移动到由**“0”**组成的任何索引(*基于 1 的索引*)并使其成为**“1”**。
*   对于随后的回合，如果任何一个玩家在索引 **i** 处，那么他可以移动到它的相邻索引之一，如果它包含 **0** ，并且在移动后将其转换为**‘1’**。
*   如果任何一个玩家在回合中不能移动到任何位置，那么这个玩家就输了。

任务是找到游戏的赢家。

**示例:**

> **输入:** S = "1100011"
> **输出:**选手 A
> **解说:**
> 指数 3、4、5 由 0 组成，指数 1、2、6、7 由 1 组成。
> A 从翻转索引 4 处的字符开始..
> B 翻转指数 3 或 5。
> A 现在只剩下一个与 4 相邻的指标，B 没有选择。在 A 翻转该索引处的字符后，B 没有任何要翻转的字符。因为 B 没有招式，所以 A 赢。
> 因此，打印“玩家 A”。
> 
> **输入:**S =【11111】
> T3】输出:玩家 B

**方法:**想法是将所有[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的长度存储在另一个数组中，比如说 **V[]** ，这些子串仅由给定数组**中的 **0s** 组成。现在，出现了以下情况:**

1.  [**如果 V 的大小为 0**](https://www.geeksforgeeks.org/vectorempty-vectorsize-c-stl/) **:** 在这种情况下，数组不包含任何 **0s** 。因此**玩家 A** 不能有任何举动，输掉游戏。因此，打印**播放器 B** 。
2.  [**如果 V 的大小是 1**](https://www.geeksforgeeks.org/vectorempty-vectorsize-c-stl/) **:** 在这种情况下，有一个子串只由 **0s** 组成，比如长度为 **L** 。[如果 **L** 的值为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则**玩家 A** 获胜。否则**玩家 B** 赢得游戏。
3.  在所有其他情况下:将 **0** s 的最大和第二大连续线段的长度分别存储在**第一**和**第二**中。**如果且仅当**第一**的值为奇数和**(第一+ 1)/2 >第二**时，玩家 A** 才能赢得游戏。否则**玩家 B** 赢得游戏。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if player A wins
// the game or not
void findWinner(string a, int n)
{
    // Stores size of the groups of 0s
    vector<int> v;

    // Stores size of the group of 0s
    int c = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Increment c by 1 if a[i] is 0
        if (a[i] == '0') {
            c++;
        }

        // Otherwise, push the size
        // in array and reset c to 0
        else {
            if (c != 0)
                v.push_back(c);
            c = 0;
        }
    }
    if (c != 0)
        v.push_back(c);

    // If there is no substring of
    // odd length consisting only of 0s
    if (v.size() == 0) {
        cout << "Player B";
        return;
    }

    // If there is only 1 substring of
    // odd length consisting only of 0s
    if (v.size() == 1) {
        if (v[0] & 1)
            cout << "Player A";

        // Otherwise
        else
            cout << "Player B";
        return;
    }

    // Stores the size of the largest
    // and second largest substrings of 0s
    int first = INT_MIN;
    int second = INT_MIN;

    // Traverse the array v[]
    for (int i = 0; i < v.size(); i++) {

        // If current element is greater
        // than first, then update both
        // first and second
        if (a[i] > first) {
            second = first;
            first = a[i];
        }

        // If arr[i] is in between
        // first and second, then
        // update second
        else if (a[i] > second
                 && a[i] != first)
            second = a[i];
    }

    // If the condition is satisfied
    if ((first & 1)
        && (first + 1) / 2 > second)
        cout << "Player A";
    else
        cout << "Player B";
}

// Driver Code
int main()
{
    string S = "1100011";
    int N = S.length();
    findWinner(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to check if player A wins
  // the game or not
  static void findWinner(String a, int n)
  {

    // Stores size of the groups of 0s
    Vector<Integer> v = new Vector<Integer>(); 

    // Stores size of the group of 0s
    int c = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // Increment c by 1 if a[i] is 0
      if (a.charAt(i) == '0')
      {
        c++;
      }

      // Otherwise, push the size
      // in array and reset c to 0
      else
      {
        if (c != 0)
          v.add(c);
        c = 0;
      }
    }
    if (c != 0)
      v.add(c);

    // If there is no substring of
    // odd length consisting only of 0s
    if (v.size() == 0)
    {
      System.out.print("Player B");
      return;
    }

    // If there is only 1 substring of
    // odd length consisting only of 0s
    if (v.size() == 1)
    {
      if ((v.get(0) & 1) != 0)
        System.out.print("Player A");

      // Otherwise
      else
        System.out.print("Player B");
      return;
    }

    // Stores the size of the largest
    // and second largest substrings of 0s
    int first = Integer.MIN_VALUE;
    int second = Integer.MIN_VALUE;

    // Traverse the array v[]
    for (int i = 0; i < v.size(); i++)
    {

      // If current element is greater
      // than first, then update both
      // first and second
      if (a.charAt(i) > first) {
        second = first;
        first = a.charAt(i);
      }

      // If arr[i] is in between
      // first and second, then
      // update second
      else if (a.charAt(i) > second
               && a.charAt(i) != first)
        second = a.charAt(i);
    }

    // If the condition is satisfied
    if ((first & 1) != 0
        && (first + 1) / 2 > second)
      System.out.print("Player A");
    else
      System.out.print("Player B");
  }

  // Driver code
  public static void main(String[] args)
  {
    String S = "1100011";
    int N = S.length();
    findWinner(S, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to check if player A wins
# the game or not
def findWinner(a, n) :

    # Stores size of the groups of 0s
    v = []

    # Stores size of the group of 0s
    c = 0

    # Traverse the array
    for i in range(0, n) :

        # Increment c by 1 if a[i] is 0
        if (a[i] == '0') :
            c += 1

        # Otherwise, push the size
        # in array and reset c to 0
        else :
            if (c != 0) :
                v.append(c)
            c = 0

    if (c != 0) :
        v.append(c)

    # If there is no substring of
    # odd length consisting only of 0s
    if (len(v) == 0) :
        print("Player B", end = "")
        return

    # If there is only 1 substring of
    # odd length consisting only of 0s
    if (len(v) == 1) :
        if ((v[0] & 1) != 0) :
            print("Player A", end = "")

        # Otherwise
        else :
            print("Player B", end = "")
        return

    # Stores the size of the largest
    # and second largest substrings of 0s
    first = sys.minsize
    second = sys.minsize

    # Traverse the array v[]
    for i in range(len(v)) :

        # If current element is greater
        # than first, then update both
        # first and second
        if (a[i] > first) :
            second = first
            first = a[i]

        # If arr[i] is in between
        # first and second, then
        # update second
        elif (a[i] > second and a[i] != first) :
            second = a[i]

    # If the condition is satisfied
    if (((first & 1) != 0) and (first + 1) // 2 > second) :
        print("Player A", end = "")
    else :
        print("Player B", end = "")

S = "1100011"
N = len(S)
findWinner(S, N)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

  // Function to check if player A wins
  // the game or not
  static void findWinner(string a, int n)
  {

    // Stores size of the groups of 0s
    List<int> v = new List<int>(); 

    // Stores size of the group of 0s
    int c = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // Increment c by 1 if a[i] is 0
      if (a[i] == '0')
      {
        c++;
      }

      // Otherwise, push the size
      // in array and reset c to 0
      else
      {
        if (c != 0)
          v.Add(c);
        c = 0;
      }
    }
    if (c != 0)
      v.Add(c);

    // If there is no substring of
    // odd length consisting only of 0s
    if (v.Count == 0)
    {
      Console.Write("Player B");
      return;
    }

    // If there is only 1 substring of
    // odd length consisting only of 0s
    if (v.Count == 1)
    {
      if ((v[0] & 1) != 0)
        Console.Write("Player A");

      // Otherwise
      else
        Console.Write("Player B");
      return;
    }

    // Stores the size of the largest
    // and second largest substrings of 0s
    int first = Int32.MinValue;
    int second = Int32.MinValue;

    // Traverse the array v[]
    for (int i = 0; i < v.Count; i++)
    {

      // If current element is greater
      // than first, then update both
      // first and second
      if (a[i] > first) {
        second = first;
        first = a[i];
      }

      // If arr[i] is in between
      // first and second, then
      // update second
      else if (a[i] > second
               && a[i] != first)
        second = a[i];
    }

    // If the condition is satisfied
    if ((first & 1) != 0
        && (first + 1) / 2 > second)
      Console.Write("Player A");
    else
      Console.Write("Player B");
  }

// Driver Code
public static void Main(String[] args)
{
    string S = "1100011";
    int N = S.Length;
    findWinner(S, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to check if player A wins
    // the game or not
    function findWinner(a, n)
    {

      // Stores size of the groups of 0s
      let v = [];

      // Stores size of the group of 0s
      let c = 0;

      // Traverse the array
      for (let i = 0; i < n; i++)
      {

        // Increment c by 1 if a[i] is 0
        if (a[i] == '0')
        {
          c++;
        }

        // Otherwise, push the size
        // in array and reset c to 0
        else
        {
          if (c != 0)
            v.push(c);
          c = 0;
        }
      }
      if (c != 0)
        v.push(c);

      // If there is no substring of
      // odd length consisting only of 0s
      if (v.length == 0)
      {
        document.write("Player B");
        return;
      }

      // If there is only 1 substring of
      // odd length consisting only of 0s
      if (v.length == 1)
      {
        if ((v[0] & 1) != 0)
          document.write("Player A");

        // Otherwise
        else
          document.write("Player B");
        return;
      }

      // Stores the size of the largest
      // and second largest substrings of 0s
      let first = Number.MIN_VALUE;
      let second = Number.MIN_VALUE;

      // Traverse the array v[]
      for (let i = 0; i < v.length; i++)
      {

        // If current element is greater
        // than first, then update both
        // first and second
        if (a[i] > first) {
          second = first;
          first = a[i];
        }

        // If arr[i] is in between
        // first and second, then
        // update second
        else if (a[i] > second && a[i] != first)
          second = a[i];
      }

      // If the condition is satisfied
      if ((first & 1) != 0 && parseInt((first + 1) / 2, 10) > second)
        document.write("Player A");
      else
        document.write("Player B");
    }

    let S = "1100011";
    let N = S.length;
    findWinner(S, N);

  // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Player A
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*