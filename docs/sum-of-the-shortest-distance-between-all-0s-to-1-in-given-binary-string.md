# 给定二进制字符串中所有 0 到 1 的最短距离之和

> 原文:[https://www . geesforgeks . org/给定二进制字符串中所有 0 到 1 的最短距离之和/](https://www.geeksforgeeks.org/sum-of-the-shortest-distance-between-all-0s-to-1-in-given-binary-string/)

给定一个二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出给定字符串 **S** 中所有 **0s** 到 **1** 的最短距离之和。

**示例:**

> **输入:** S = "100100"
> **输出:** 5
> **解释:**
> 对于索引 1 处的“0”，最近的“1”位于距离 1 处的索引 0 处。
> 对于索引 2 处的“0”，最近的“1”位于距离 1 处的索引 3 处。
> 对于索引 4 处的“0”，最近的“1”位于距离 1 处的索引 3 处。
> 对于索引 5 处的“0”，最近的“1”位于距离 2 处的索引 3 处。
> 因此距离之和为 1 + 1 + 1 + 2 = 5。
> 
> **输入:**S = " 1111 "
> T3】输出: 0

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思想是为从左侧距离其最近的每个'**0′**搜索'**1′**。同样，从右侧开始，为最靠近的每个**“0”**搜索“**1′**”。最后，根据左右两侧的计算值，计算任意'**0′**至'**1′**的最小距离之和。按照以下步骤解决给定的问题。

*   初始化 to 数组**前缀距离(N)** 、**后缀距离(N)** 分别存储左右距离。
*   初始化一个变量，比如说 **cnt = 0** ，它存储任何一个'**0 '**到最近的'**1 '**之间的距离。
*   初始化一个变量，说 **haveOne = false** ，标记字符“**1′**。
*   初始化一个变量，比如说 **sum = 0** ，它存储所有“**0’**到最近的“**1’**之间的总和。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**执行以下步骤:
    *   如果 **S[i]** 的值为“**1′**，则将 **haveOne** 指定为 **true** 、 **cnt** 指定为 **0** 、**prefix distance【I】**指定为 **0** 。
    *   否则，如果**有一个**为**真**，则将 **cnt** 的值增加 **1** ，并将**前缀距离【I】**的值指定为 **cnt** 。
*   使用变量 **i** 迭代范围**【0，N–1】**，执行以下步骤:
    *   如果 **S[i]** 的值为“**1′**，则将 **haveOne** 指定为 **true** 、 **cnt** 指定为 **0** 、**后缀 distance【I】**指定为 **0** 。
    *   否则，如果**有一个**为真，则将 **cnt** 的值增加 **1** ，并将**后缀距离【I】**的值指定为 **cnt** 。
*   使用变量 **i** 迭代范围**【0，N–1】**，如果**S【I】**的值为'**1′**，则将**和**更新为**和+= min(前缀距离[i]，后缀距离[i])** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total sum of
// the shortest distance between every
// 0 to 1 in a given binary string
void findTotalDistance(string S, int N)
{

    // Stores the prefix distance and
    // suffix distance from 0 to 1
    vector<int> prefixDistance(N);
    vector<int> suffixDistance(N);

    // Stores the current distance
    // from 1 to 0
    int cnt = 0;

    // Marks the 1
    bool haveOne = false;
    for (int i = 0; i < N; ++i) {

        // If current character is 1
        if (S[i] == '1') {

            // Mark haveOne to true
            haveOne = true;

            // Assign the cnt to 0
            cnt = 0;

            // Assign prefixDistance[i] as 0
            prefixDistance[i] = 0;
        }

        // If haveOne is true
        else if (haveOne) {

            // Update the cnt
            cnt++;
            // Update prefixDistance[i]
            prefixDistance[i] = cnt;
        }

        // Assign prefixDistance[i]
        // as INT_MAX
        else
            prefixDistance[i] = INT_MAX;
    }

    // Assign haveOne as false
    haveOne = false;
    for (int i = N - 1; i >= 0; --i) {

        // If current character is 1
        if (S[i] == '1') {

            // Mark haveOne to true
            haveOne = true;

            // Assign the cnt to 0
            cnt = 0;

            // Assign the suffixDistance[i]
            // as 0
            suffixDistance[i] = 0;
        }

        // If haveOne is true
        else if (haveOne) {

            // Update the cnt
            cnt++;

            // Update suffixDistance[i]
            // as cnt
            suffixDistance[i] = cnt;
        }
        else
            // Assign suffixDistance[i]
            // as INT_MAX
            suffixDistance[i] = INT_MAX;
    }

    // Stores the total sum of distances
    // between 0 to nearest 1
    int sum = 0;

    for (int i = 0; i < N; ++i) {

        // If current character is 0
        if (S[i] == '0') {

            // Update the value of sum
            sum += min(prefixDistance[i],
                       suffixDistance[i]);
        }
    }

    // Print the value of the sum
    cout << sum << endl;
}

// Driver Code
int main()
{
    string S = "100100";
    int N = S.length();

    findTotalDistance(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

public class GFG{

// Function to find the total sum of
// the shortest distance between every
// 0 to 1 in a given binary string
static void findTotalDistance(String S, int N)
{

    // Stores the prefix distance and
    // suffix distance from 0 to 1
    int []prefixDistance = new int[N];
    int []suffixDistance = new int[N];

    // Stores the current distance
    // from 1 to 0
    int cnt = 0;

    // Marks the 1
    boolean haveOne = false;
    for (int i = 0; i < N; ++i) {

        // If current character is 1
        if (S.charAt(i) == '1') {

            // Mark haveOne to true
            haveOne = true;

            // Assign the cnt to 0
            cnt = 0;

            // Assign prefixDistance[i] as 0
            prefixDistance[i] = 0;
        }

        // If haveOne is true
        else if (haveOne) {

            // Update the cnt
            cnt++;
            // Update prefixDistance[i]
            prefixDistance[i] = cnt;
        }

        // Assign prefixDistance[i]
        // as INT_MAX
        else
            prefixDistance[i] = Integer.MAX_VALUE;
    }

    // Assign haveOne as false
    haveOne = false;
    for (int i = N - 1; i >= 0; --i) {

        // If current character is 1
        if (S.charAt(i) == '1') {

            // Mark haveOne to true
            haveOne = true;

            // Assign the cnt to 0
            cnt = 0;

            // Assign the suffixDistance[i]
            // as 0
            suffixDistance[i] = 0;
        }

        // If haveOne is true
        else if (haveOne) {

            // Update the cnt
            cnt++;

            // Update suffixDistance[i]
            // as cnt
            suffixDistance[i] = cnt;
        }
        else
            // Assign suffixDistance[i]
            // as INT_MAX
            suffixDistance[i] = Integer.MAX_VALUE;
    }

    // Stores the total sum of distances
    // between 0 to nearest 1
    int sum = 0;

    for (int i = 0; i < N; ++i) {

        // If current character is 0
        if (S.charAt(i) == '0') {

            // Update the value of sum
            sum += Math.min(prefixDistance[i],
                       suffixDistance[i]);
        }
    }

    // Print the value of the sum
    System.out.print(sum);
}

// Driver Code
public static void main(String []args)
{
    String S = "100100";
    int N = S.length();

    findTotalDistance(S, N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the total sum of
# the shortest distance between every
# 0 to 1 in a given binary string

INT_MAX = 2147483647

def findTotalDistance(S, N):

    # Stores the prefix distance and
    # suffix distance from 0 to 1
    prefixDistance = [0 for _ in range(N)]
    suffixDistance = [0 for _ in range(N)]

    # Stores the current distance
    # from 1 to 0
    cnt = 0

    # Marks the 1
    haveOne = False
    for i in range(0, N):

        # If current character is 1
        if (S[i] == '1'):

            # // Mark haveOne to true
            haveOne = True

            # Assign the cnt to 0
            cnt = 0

            # Assign prefixDistance[i] as 0
            prefixDistance[i] = 0

        # If haveOne is true
        elif (haveOne):

            # Update the cnt
            cnt = cnt + 1
            # Update prefixDistance[i]
            prefixDistance[i] = cnt

        # Assign prefixDistance[i]
        # as INT_MAX
        else:
            prefixDistance[i] = INT_MAX

    # Assign haveOne as false
    haveOne = False
    for i in range(N-1, -1, -1):

        # If current character is 1
        if (S[i] == '1'):

            # Mark haveOne to true
            haveOne = True

            # Assign the cnt to 0
            cnt = 0

            # Assign the suffixDistance[i]
            # as 0
            suffixDistance[i] = 0

        # If haveOne is true
        elif (haveOne):

            # Update the cnt
            cnt = cnt + 1

            # Update suffixDistance[i]
            # as cnt
            suffixDistance[i] = cnt

        else:
            # // Assign suffixDistance[i]
            # // as INT_MAX
            suffixDistance[i] = INT_MAX

    # Stores the total sum of distances
    # between 0 to nearest 1
    sum = 0

    for i in range(0, N):

        # If current character is 0
        if (S[i] == '0'):

            # Update the value of sum
            sum += min(prefixDistance[i], suffixDistance[i])

    # Print the value of the sum
    print(sum)

# Driver Code
if __name__ == "__main__":

    S = "100100"
    N = len(S)

    findTotalDistance(S, N)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the total sum of
// the shortest distance between every
// 0 to 1 in a given binary string
static void findTotalDistance(string S, int N)
{

    // Stores the prefix distance and
    // suffix distance from 0 to 1
    int []prefixDistance = new int[N];
    int []suffixDistance = new int[N];

    // Stores the current distance
    // from 1 to 0
    int cnt = 0;

    // Marks the 1
    bool haveOne = false;
    for (int i = 0; i < N; ++i) {

        // If current character is 1
        if (S[i] == '1') {

            // Mark haveOne to true
            haveOne = true;

            // Assign the cnt to 0
            cnt = 0;

            // Assign prefixDistance[i] as 0
            prefixDistance[i] = 0;
        }

        // If haveOne is true
        else if (haveOne) {

            // Update the cnt
            cnt++;
            // Update prefixDistance[i]
            prefixDistance[i] = cnt;
        }

        // Assign prefixDistance[i]
        // as INT_MAX
        else
            prefixDistance[i] = Int32.MaxValue;
    }

    // Assign haveOne as false
    haveOne = false;
    for (int i = N - 1; i >= 0; --i) {

        // If current character is 1
        if (S[i] == '1') {

            // Mark haveOne to true
            haveOne = true;

            // Assign the cnt to 0
            cnt = 0;

            // Assign the suffixDistance[i]
            // as 0
            suffixDistance[i] = 0;
        }

        // If haveOne is true
        else if (haveOne) {

            // Update the cnt
            cnt++;

            // Update suffixDistance[i]
            // as cnt
            suffixDistance[i] = cnt;
        }
        else
            // Assign suffixDistance[i]
            // as INT_MAX
            suffixDistance[i] = Int32.MaxValue;
    }

    // Stores the total sum of distances
    // between 0 to nearest 1
    int sum = 0;

    for (int i = 0; i < N; ++i) {

        // If current character is 0
        if (S[i] == '0') {

            // Update the value of sum
            sum += Math.Min(prefixDistance[i],
                       suffixDistance[i]);
        }
    }

    // Print the value of the sum
    Console.Write(sum);
}

// Driver Code
public static void Main()
{
    string S = "100100";
    int N = S.Length;

    findTotalDistance(S, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach
    const INT_MAX = 2147483647

    // Function to find the total sum of
    // the shortest distance between every
    // 0 to 1 in a given binary string
    const findTotalDistance = (S, N) => {

        // Stores the prefix distance and
        // suffix distance from 0 to 1
        let prefixDistance = new Array(N).fill(0);
        let suffixDistance = new Array(N).fill(0);

        // Stores the current distance
        // from 1 to 0
        let cnt = 0;

        // Marks the 1
        let haveOne = false;
        for (let i = 0; i < N; ++i) {

            // If current character is 1
            if (S[i] == '1') {

                // Mark haveOne to true
                haveOne = true;

                // Assign the cnt to 0
                cnt = 0;

                // Assign prefixDistance[i] as 0
                prefixDistance[i] = 0;
            }

            // If haveOne is true
            else if (haveOne) {

                // Update the cnt
                cnt++;
                // Update prefixDistance[i]
                prefixDistance[i] = cnt;
            }

            // Assign prefixDistance[i]
            // as INT_MAX
            else
                prefixDistance[i] = INT_MAX;
        }

        // Assign haveOne as false
        haveOne = false;
        for (let i = N - 1; i >= 0; --i) {

            // If current character is 1
            if (S[i] == '1') {

                // Mark haveOne to true
                haveOne = true;

                // Assign the cnt to 0
                cnt = 0;

                // Assign the suffixDistance[i]
                // as 0
                suffixDistance[i] = 0;
            }

            // If haveOne is true
            else if (haveOne) {

                // Update the cnt
                cnt++;

                // Update suffixDistance[i]
                // as cnt
                suffixDistance[i] = cnt;
            }
            else
                // Assign suffixDistance[i]
                // as INT_MAX
                suffixDistance[i] = INT_MAX;
        }

        // Stores the total sum of distances
        // between 0 to nearest 1
        let sum = 0;

        for (let i = 0; i < N; ++i) {

            // If current character is 0
            if (S[i] == '0') {

                // Update the value of sum
                sum += Math.min(prefixDistance[i], suffixDistance[i]);
            }
        }

        // Print the value of the sum
        document.write(`${sum}<br/>`);
    }

    // Driver Code

    let S = "100100";
    let N = S.length;

    findTotalDistance(S, N);

// This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)