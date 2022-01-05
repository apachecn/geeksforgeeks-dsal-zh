# 检查常规括号序列是否可以由给定字符串的连接形成

> 原文:[https://www . geeksforgeeks . org/check-if-a-regular-括号-sequence-能用给定字符串的串联来形成/](https://www.geeksforgeeks.org/check-if-a-regular-bracket-sequence-can-be-formed-with-concatenation-of-given-strings/)

给定一个由 **N** [字符串](https://www.geeksforgeeks.org/string-data-structure/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，其中每个字符串由**(**和**)**组成，任务是检查给定的[字符串](https://www.geeksforgeeks.org/string-data-structure/)是否可以串联形成[正则括号序列](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/) 。如果发现是真的，则打印**是**。否则打印**否**。

**示例:**

> **输入:** arr[] = {“”、“()(”}
> **输出:**是
> **说明:**有效字符串为 S[1] + S[0] =“()()”。
> 
> **输入:** arr[] = {“”、“()”}
> **输出:**否
> **解释:**不可能有有效的常规括号序列。

**方法:**给定的问题可以借助[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，该方法基于以下观察:

*   如果一个字符串包含一对连续的字母**'('和')'**，那么删除这两个字母不会影响结果。
*   通过重复这个操作，每个 **S[i]** 变成**一个(可能是空的)字符串，由 0 个或多个重复的“)”组成，后面是 0 个或多个重复的“(“**”。
*   那么每一个字符串都可以用两个变量**来表示:A[i] =的个数')'，B[i] =的个数'('**)。
*   保持一对[向量](https://www.geeksforgeeks.org/pair-in-cpp-stl/) r **v[][]** 来存储这些值。
*   现在，将这两个字符串分成两个独立的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**pos【】**和**neg【】**。
*   **pos【】**将存储总和为**正**和**负【】**的字符串，存储总和为**负**的字符串。
*   现在，最佳的方法是先连接正字符串，然后按递增顺序连接负字符串。

按照以下步骤解决问题:

*   维护一个[对向量](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **v[][]** ，该向量将存储值 **{sum，最小前缀}** ，其中总和由 **+1** 为 **'('** )和 **-1** 为 **')'** 计算，最小前缀为字符串中的最大连续 **')'** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0。N)** 使用变量 **i** 并执行以下步骤:
    *   将两个变量**和**以及**预**初始化为 **0** ，以存储给定字符串的和和最小前缀。
    *   [对字符串的每个字符迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，如果当前字符是**(“**)，则按 **1** 递增**和**，否则按 **1** 递减**并在每一步将 **pre** 的值设置为 **pre** 或 **sum** 的最小值。**
    *   将**v【**I**的值设置为 **{ sum，pre }。****
*   **[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0。N)** 对于**v【】**中的元素和每个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)如果总和为正，则将值 **{-min_prefix，sum}** **存储在 pos【】向量**中，否则**{ sum–min _ prefix，-sum}存储在 neg【】向量**中。**
*   **[按照递增顺序对这些向量进行排序](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)。**
*   **初始化变量**打开**为 **0** 。**
*   **[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0。size)** 其中 **size** 是使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)变量 **p** 的向量**pos【**的大小，如果**open–p . first**大于等于 **0** ，那么将 **p.second** 添加到变量 **open** 中。否则，打印**否**并返回。**
*   **将变量**负**初始化为 **0** 。**
*   **[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0。size)** 其中 **size** 是使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)变量 **p** 的向量**neg【】**的大小，如果**为负–p . first**大于等于 **0** ，则将 **p.second** 添加到变量**为负的**中。否则，打印**否**并返回。**
*   **如果**开**的值不等于**负**，则打印**否**。否则，打印**是**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check possible RBS from
// the given strings
int checkRBS(vector<string> S)
{
    int N = S.size();

    // Stores the values {sum, min_prefix}
    vector<pair<int, int> > v(N);

    // Iterate over the range
    for (int i = 0; i < N; ++i) {
        string s = S[i];

        // Stores the total sum
        int sum = 0;

        // Stores the minimum prefix
        int pre = 0;
        for (char c : s) {
            if (c == '(') {
                ++sum;
            }
            else {
                --sum;
            }

            // Check for minimum prefix
            pre = min(sum, pre);
        }

        // Store these values in vector
        v[i] = { sum, pre };
    }

    // Make two pair vectors pos and neg
    vector<pair<int, int> > pos;
    vector<pair<int, int> > neg;

    // Store values according to the
    // mentioned approach
    for (int i = 0; i < N; ++i) {
        if (v[i].first >= 0) {
            pos.push_back(
                { -v[i].second, v[i].first });
        }
        else {
            neg.push_back(
                { v[i].first - v[i].second,
                  -v[i].first });
        }
    }

    // Sort the positive vector
    sort(pos.begin(), pos.end());

    // Stores the extra count of
    // open brackets
    int open = 0;
    for (auto p : pos) {
        if (open - p.first >= 0) {
            open += p.second;
        }

        // No valid bracket sequence
        // can be formed
        else {
            cout << "No"
                 << "\n";
            return 0;
        }
    }

    // Sort the negative vector
    sort(neg.begin(), neg.end());

    // Stores the count of the
    // negative elements
    int negative = 0;
    for (auto p : neg) {

        if (negative - p.first >= 0) {
            negative += p.second;
        }

        // No valid bracket sequence
        // can be formed
        else {
            cout << "No\n";
            return 0;
        }
    }

    // Check if open is equal to negative
    if (open != negative) {
        cout << "No\n";
        return 0;
    }
    cout << "Yes\n";
    return 0;
}

// Driver Code
int main()
{
    vector<string> arr = { ")", "()(" };
    checkRBS(arr);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
// Function to check possible RBS from
// the given Strings
static int checkRBS(String[] S)
{
    int N = S.length;

    // Stores the values {sum, min_prefix}
    pair []v = new pair[N];

    // Iterate over the range
    for (int i = 0; i < N; ++i) {
        String s = S[i];

        // Stores the total sum
        int sum = 0;

        // Stores the minimum prefix
        int pre = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                ++sum;
            }
            else {
                --sum;
            }

            // Check for minimum prefix
            pre = Math.min(sum, pre);
        }

        // Store these values in vector
        v[i] = new pair( sum, pre );
    }

    // Make two pair vectors pos and neg
    Vector<pair> pos = new Vector<pair>();
    Vector<pair > neg = new Vector<pair>();

    // Store values according to the
    // mentioned approach
    for (int i = 0; i < N; ++i) {
        if (v[i].first >= 0) {
            pos.add(
                new pair( -v[i].second, v[i].first ));
        }
        else {
            neg.add(
                    new pair( v[i].first - v[i].second,
                  -v[i].first ));
        }
    }

    // Sort the positive vector
    Collections.sort(pos,(a,b)->a.first-b.first);

    // Stores the extra count of
    // open brackets
    int open = 0;
    for (pair p : pos) {
        if (open - p.first >= 0) {
            open += p.second;
        }

        // No valid bracket sequence
        // can be formed
        else {
            System.out.print("No"
                + "\n");
            return 0;
        }
    }

    // Sort the negative vector
    Collections.sort(neg,(a,b)->a.first-b.first);

    // Stores the count of the
    // negative elements
    int negative = 0;
    for (pair p : neg) {

        if (negative - p.first >= 0) {
            negative += p.second;
        }

        // No valid bracket sequence
        // can be formed
        else {
            System.out.print("No\n");
            return 0;
        }
    }

    // Check if open is equal to negative
    if (open != negative) {
        System.out.print("No\n");
        return 0;

    }
    System.out.print("Yes\n");
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    String []arr = { ")", "()(" };
    checkRBS(arr);

}
}

// This code is contributed by shikhasingrajput
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Function to check possible RBS from
# the given strings
def checkRBS(S):

    N = len(S)

    # Stores the values {sum, min_prefix}
    v = [0]*(N)

    # Iterate over the range
    for i in range(N):
        s = S[i]

        # Stores the total sum
        sum = 0

        # Stores the minimum prefix
        pre = 0
        for c in s:
            if (c == '('):
                sum += 1

            else:
                sum -= 1

            # Check for minimum prefix
            pre = min(sum, pre)

        # Store these values in vector
        v[i] = [sum, pre]

    pos = []
    neg = []

    # Store values according to the
    # mentioned approach
    for i in range(N):
        if (v[i][0] >= 0):
            pos.append(
                [-v[i][1], v[i][0]])

        else:
            neg.append(
                [v[i][0] - v[i][1],
                 -v[i][0]])

    # Sort the positive vector
    pos.sort()

    # Stores the extra count of
    # open brackets
    open = 0
    for p in pos:
        if (open - p[0] >= 0):
            open += p[1]

        # No valid bracket sequence
        # can be formed
        else:
            print("No")

            return 0

    # Sort the negative vector
    neg.sort()

    # Stores the count of the
    # negative elements
    negative = 0
    for p in neg:

        if (negative - p[0] >= 0):
            negative += p[1]

        # No valid bracket sequence
        # can be formed
        else:
            print("No")
            return 0

    # Check if open is equal to negative
    if (open != negative):
        print("No")
        return 0

    print("Yes")

# Driver Code
if __name__ == "__main__":

    arr = [")", "()("]
    checkRBS(arr)

    # This code is contributed by ukasp.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{
 class pair : IComparable<pair>
    {
        public int first,second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }

        public int CompareTo(pair p)
        {
            return this.first - p.first;
        }
    }

// Function to check possible RBS from
// the given Strings
static int checkRBS(String[] S)
{
    int N = S.Length;

    // Stores the values {sum, min_prefix}
    pair []v = new pair[N];

    // Iterate over the range
    for (int i = 0; i < N; ++i) {
        String s = S[i];

        // Stores the total sum
        int sum = 0;

        // Stores the minimum prefix
        int pre = 0;
        foreach (char c in s.ToCharArray()) {
            if (c == '(') {
                ++sum;
            }
            else {
                --sum;
            }

            // Check for minimum prefix
            pre = Math.Min(sum, pre);
        }

        // Store these values in vector
        v[i] = new pair( sum, pre );
    }

    // Make two pair vectors pos and neg
    List<pair> pos = new List<pair>();
    List<pair > neg = new List<pair>();

    // Store values according to the
    // mentioned approach
    for (int i = 0; i < N; ++i) {
        if (v[i].first >= 0) {
            pos.Add(
                new pair( -v[i].second, v[i].first ));
        }
        else {
            neg.Add(
                    new pair( v[i].first - v[i].second,
                  -v[i].first ));
        }
    }

    // Sort the positive vector
    pos.Sort();

    // Stores the extra count of
    // open brackets
    int open = 0;
    foreach (pair p in pos) {
        if (open - p.first >= 0) {
            open += p.second;
        }

        // No valid bracket sequence
        // can be formed
        else {
            Console.Write("No"
                + "\n");
            return 0;
        }
    }

    // Sort the negative vector
    neg.Sort();

    // Stores the count of the
    // negative elements
    int negative = 0;
    foreach (pair p in neg) {

        if (negative - p.first >= 0) {
            negative += p.second;
        }

        // No valid bracket sequence
        // can be formed
        else {
            Console.Write("No\n");
            return 0;
        }
    }

    // Check if open is equal to negative
    if (open != negative) {
        Console.Write("No\n");
        return 0;

    }
    Console.Write("Yes\n");
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = { ")", "()(" };
    checkRBS(arr);

}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to check possible RBS from
// the given strings
function checkRBS(S) {
  let N = S.length;

  // Stores the values {sum, min_prefix}
  let v = new Array(N);

  // Iterate over the range
  for (let i = 0; i < N; ++i) {
    let s = S[i];

    // Stores the total sum
    let sum = 0;

    // Stores the minimum prefix
    let pre = 0;
    for (let c of s) {
      if (c == "(") {
        ++sum;
      } else {
        --sum;
      }

      // Check for minimum prefix
      pre = Math.min(sum, pre);
    }

    // Store these values in vector
    v[i] = [sum, pre];
  }

  // Make two pair vectors pos and neg
  let pos = [];
  let neg = [];

  // Store values according to the
  // mentioned approach
  for (let i = 0; i < N; ++i) {
    if (v[i][0] >= 0) {
      pos.push([-v[i][1], v[i][0]]);
    } else {
      neg.push([v[i][0] - v[i][1], -v[i][0]]);
    }
  }

  // Sort the positive vector
  pos.sort((a, b) => a - b);

  // Stores the extra count of
  // open brackets
  let open = 0;
  for (let p of pos) {
    if (open - p[0] >= 0) {
      open += p[1];
    }

    // No valid bracket sequence
    // can be formed
    else {
      document.write("No" + "<br>");
      return 0;
    }
  }

  // Sort the negative vector
  neg.sort((a, b) => a - b);

  // Stores the count of the
  // negative elements
  let negative = 0;
  for (let p of neg) {
    if (negative - p[0] >= 0) {
      negative += p[1];
    }

    // No valid bracket sequence
    // can be formed
    else {
      document.write("No<br>");
      return 0;
    }
  }

  // Check if open is equal to negative
  if (open != negative) {
    document.write("No<br>");
    return 0;
  }
  document.write("Yes<br>");
  return 0;
}

// Driver Code

let arr = [")", "()("];
checkRBS(arr);

// This code is contributed by gfgking.
</script>
```

****Output:** 

```
Yes
```** 

*****时间复杂度:** O(N*M + N*log(N))，其中 M 是数组 arr[]中字符串的最大长度。*
***辅助空间:** O(N)***