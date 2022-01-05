# 找到最后一个能够从一个数组中移除字符串的玩家，该字符串尚未从其他数组中移除

> 原文:[https://www . geesforgeks . org/find-最后一个能够从其他阵列中移除字符串的玩家/](https://www.geeksforgeeks.org/find-the-last-player-to-be-able-to-remove-a-string-from-an-array-which-is-not-already-removed-from-other-array/)

给定两个大小分别为 **N** 和 **M** 的[弦阵列](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)**arr【】**和**brr【】**，任务是当两个玩家按照以下规则进行最佳游戏时，找到游戏的赢家:

*   **玩家 1** 开始游戏。
*   **玩家 1** 从阵列中移除一个字符串 **arr[]** 如果它还没有从阵列中移除 **brr[]** 。
*   **玩家 2** 从阵列中移除一个字符串 **brr[]** 如果它还没有从阵列中移除 **arr[]** 。
*   不能从数组中移除字符串的玩家将输掉游戏。

**示例:**

> **输入:** arr[] = {“极客”、“极客”}，brr[] = {“极客”、“极客暴客”}
> **输出:**玩家 1
> **解释:**
> **回合 1:** 玩家 1 从 arr[]中移除了“极客”。
> **第二回合:**玩家 2 从 brr[]移除“极客”
> **第三回合:**玩家 1 从 brr[]移除“极客”。
> 现在，玩家 2 不能移除任何弦。
> 因此，需要的输出是播放器 1。
> 
> **输入:**arr[]= {“a”、“b”}，brr[]= {“a”、“b”}
> **输出:**玩家 2
> **解释:**
> **回合 1:** 玩家 1 从 arr[]**移除“a”。
> **第二回合:**玩家 2 从 brr[]中移除了“b”。
> 因此，需要的输出是播放器 2**

**方法:**这个想法是基于这样一个事实，即两个数组中的公共字符串只能从其中一个数组中移除。按照以下步骤解决问题:

*   如果两个数组中公共字符串的计数都是奇数，那么从数组中移除一个字符串 **brr[]** ，因为**玩家 1** 开始游戏，第一个公共字符串被**玩家 1** 移除。
*   如果 **arr[]** 中的字符串数大于 **brr[]** 中的字符串数，则从两个数组中删除公共字符串，然后打印**“玩家 1”**。
*   否则，打印**“玩家 2”**。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find last player to be
// able to remove a string from one array
// which has not been removed from the other array
void lastPlayer(int n, int m, vector<string> arr,
                       vector<string> brr)
{

    // Stores common strings
    // from both the array
   set<string> common;

    for (int i = 0; i < arr.size(); i++)
    {
        for (int j = 0; j < brr.size(); j++)
        {
            if (arr[i] == brr[j])
            {

                // add common elements
                common.insert(arr[i]);
                break;
            }
        }
    }

    // Removing common strings from arr[]
    set<string> a;
    bool flag;
    for (int i = 0; i < arr.size(); i++)
    {
        flag = false;
        for (auto value : common)
        {
            if (value == arr[i])
            {

                // add common elements
                flag = true;
                break;
            }
        }
        if (flag)
            a.insert(arr[i]);
    }

    // Removing common elements from B
    set<string> b;
    for (int i = 0; i < brr.size(); i++)
    {
        flag = false;
        for (auto value : common)
        {
            if (value == brr[i])
            {

                // add common elements
                flag = true;
                break;
            }
        }

        if (flag)
            b.insert(brr[i]);
    }

    // Stores strings in brr[] which
    // is not common in arr[]
    int LenBrr = b.size();
    if ((common.size()) % 2 == 1)
    {

        // Update LenBrr
        LenBrr -= 1;
    }

    if (a.size() > LenBrr)
    {
        cout<<("Player 1")<<endl;
    }
    else
    {
        cout<<("Player 2")<<endl;
    }
}

// Driver Code
int main()
{

    // Set of strings for player A
    vector<string> arr{ "geeks", "geek" };

    // Set of strings for player B
    vector<string> brr{ "geeks", "geeksforgeeks" };
    int n = arr.size();
    int m = brr.size();
    lastPlayer(n, m, arr, brr);
}

// This code is contributed by SURENDRA_GANGWAR.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;
import java.util.*;
class GFG
{
    // Function to find last player to be
    // able to remove a string from one array
    // which has not been removed from the other array
    static void lastPlayer(int n, int m, String[] arr,
                           String[] brr)
    {

        // Stores common strings
        // from both the array
        Set<String> common = new HashSet<>();

        for (int i = 0; i < arr.length; i++)
        {
            for (int j = 0; j < brr.length; j++)
            {
                if (arr[i] == brr[j])
                {

                    // add common elements
                    common.add(arr[i]);
                    break;
                }
            }
        }

        // Removing common strings from arr[]
        Set<String> a = new HashSet<>();
        boolean flag;
        for (int i = 0; i < arr.length; i++)
        {
            flag = false;
            for (String value : common)
            {
                if (value == arr[i])
                {

                    // add common elements
                    flag = true;
                    break;
                }
            }
            if (flag)
                a.add(arr[i]);
        }

        // Removing common elements from B
        Set<String> b = new HashSet<>();
        for (int i = 0; i < brr.length; i++)
        {
            flag = false;
            for (String value : common)
            {
                if (value == brr[i])
                {

                    // add common elements
                    flag = true;
                    break;
                }
            }

            if (flag)
                b.add(brr[i]);
        }

        // Stores strings in brr[] which
        // is not common in arr[]
        int LenBrr = b.size();
        if ((common.size()) % 2 == 1)
        {

            // Update LenBrr
            LenBrr -= 1;
        }

        if (a.size() > LenBrr)
        {
            System.out.print("Player 1");
        }
        else
        {
            System.out.print("Player 2");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Set of strings for player A
        String[] arr = { "geeks", "geek" };

        // Set of strings for player B
        String[] brr = { "geeks", "geeksforgeeks" };
        int n = arr.length;
        int m = brr.length;
        lastPlayer(n, m, arr, brr);
    }
}

// This code is contributed by Dharanendra L V.
```

## 计算机编程语言

```
# Python Program for the above approach

# Function to find last player to be
# able to remove a string from one array
# which has not been removed from the other array
def lastPlayer(n, m, arr, brr):

    # Stores common strings
    # from both the array
    common = list(set(arr) & set(brr))

    # Removing common strings from arr[]
    a = list(set(arr) ^ set(common))

    # Removing common elements from B
    b = list(set(brr) ^ set(common))

    # Stores strings in brr[] which
    # is not common in arr[]
    LenBrr = len(b)

    if len(common) % 2 == 1:

        # Update LenBrr
        LenBrr -= 1

    if len(a) > LenBrr:
        print("Player 1")
    else:
        print("Player 2")

# Driver Code
if __name__ == '__main__':

    # Set of strings for player A
    arr = ["geeks", "geek"]

    # Set of strings for player B
    brr = ["geeks", "geeksforgeeks"]

    n = len(arr)
    m = len(brr)

    lastPlayer(n, m, arr, brr)
```

## C#

```
// C# Program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

    // Function to find last player to be
    // able to remove a string from one array
    // which has not been removed from the other array
    static void lastPlayer(int n, int m, String[] arr,
                           String[] brr)
    {

        // Stores common strings
        // from both the array
        HashSet<String> common = new HashSet<String>();
        for (int i = 0; i < arr.Length; i++)
        {
            for (int j = 0; j < brr.Length; j++)
            {
                if (arr[i] == brr[j])
                {

                    // add common elements
                    common.Add(arr[i]);
                    break;
                }
            }
        }

        // Removing common strings from []arr
        HashSet<String> a = new HashSet<String>();
        bool flag;
        for (int i = 0; i < arr.Length; i++)
        {
            flag = false;
            foreach (String value in common)
            {
                if (value == arr[i])
                {

                    // add common elements
                    flag = true;
                    break;
                }
            }
            if (flag)
                a.Add(arr[i]);
        }

        // Removing common elements from B
        HashSet<String> b = new HashSet<String>();
        for (int i = 0; i < brr.Length; i++)
        {
            flag = false;
            foreach (String value in common)
            {
                if (value == brr[i])
                {

                    // add common elements
                    flag = true;
                    break;
                }
            }

            if (flag)
                b.Add(brr[i]);
        }

        // Stores strings in brr[] which
        // is not common in []arr
        int LenBrr = b.Count;
        if ((common.Count) % 2 == 1)
        {

            // Update LenBrr
            LenBrr -= 1;
        }

        if (a.Count > LenBrr)
        {
            Console.Write("Player 1");
        }
        else
        {
            Console.Write("Player 2");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Set of strings for player A
        String[] arr = { "geeks", "geek" };

        // Set of strings for player B
        String[] brr = { "geeks", "geeksforgeeks" };
        int n = arr.Length;
        int m = brr.Length;
        lastPlayer(n, m, arr, brr);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript Program for the above approach
      // Function to find last player to be
      // able to remove a string from one array
      // which has not been removed from the other array
      function lastPlayer(n, m, arr, brr)
      {

        // Stores common strings
        // from both the array
        var common = [];
        for (var i = 0; i < arr.length; i++)
        {
          for (var j = 0; j < brr.length; j++)
          {
            if (arr[i] === brr[j])
            {

              // add common elements
              common.push(arr[i]);
              j = brr.length;
            }
          }
        }

        // Removing common strings from []arr
        var a = [];
        var flag;
        for (var i = 0; i < arr.length; i++) {
          flag = false;
          common.forEach((value) => {
            if (value === arr[i])
            {

              // add common elements
              flag = true;
              i = arr.length;
            }
          });
          if (flag) a.push(arr[i]);
        }

        // Removing common elements from B
        var b = [];
        for (var i = 0; i < brr.length; i++) {
          flag = false;
          common.forEach((value) => {
            if (value === brr[i]) {
              // add common elements
              flag = true;
              i = brr.length;
            }
          });

          if (flag) b.push(brr[i]);
        }

        // Stores strings in brr[] which
        // is not common in []arr
        var LenBrr = b.length;
        if (common.length % 2 === 1) {
          // Update LenBrr
          LenBrr -= 1;
        }

        if (a.length > LenBrr) {
          document.write("Player 1");
        } else {
          document.write("Player 2");
        }
      }

      // Driver Code
      // Set of strings for player A
      var arr = ["geeks", "geek"];

      // Set of strings for player B
      var brr = ["geeks", "geeksforgeeks"];
      var n = arr.length;
      var m = brr.length;
      lastPlayer(n, m, arr, brr);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
Player 1
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N + M)*