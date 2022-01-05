# 字符串中重复之间的曼哈顿距离之和

> 原文:[https://www . geesforgeks . org/sum-Manhattan-字符串中重复之间的距离/](https://www.geeksforgeeks.org/sum-of-manhattan-distances-between-repetitions-in-a-string/)

给定一个由小写字符组成的大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出每对 **(i，j)** 之间的[曼哈顿距离](https://www.geeksforgeeks.org/maximum-manhattan-distance-between-a-distinct-pair-from-n-coordinates/)之和，使得 **i≤j** 和**S【j】= S【I】**。

**示例:**

> **输入:** S =【亚贝巴】
> **输出:** 10
> **说明:**具有相同字符的对是:(1，3)、(1，5)、(2，4)和(3，5)。因此，曼哈顿距离的总和将是| 3–1 |+| 5–1 |+| 4–2 |+| 5–3 | = 10
> 
> **输入:**S = " ABC "
> T3】输出: 0

**天真方法:**最简单的方法是使用两个[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)生成所有对 **(i，j)** ，并检查每对是否满足给定条件。如果发现是真的，把它们的距离加到答案上。检查所有配对后，打印答案。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**该方法类似于求所有点对之间的曼哈顿距离的[和](https://www.geeksforgeeks.org/sum-manhattan-distances-pairs-points/)。按照以下步骤解决问题:

*   将变量**和**初始化为 0，以存储所需的结果。
*   为每个字符创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)、 **V** ，分别存储每个字符的位置。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、 **S** ，并追加每个字符在各自向量中的位置， **V** 。
*   现在，问题简化为求每个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)数组的每对点之间的[曼哈顿距离的和。](https://www.geeksforgeeks.org/sum-manhattan-distances-pairs-points/)
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，25】**中迭代
    *   将向量、**V【I】**中所有元素的[和存储在变量**和**中。](https://www.geeksforgeeks.org/how-to-find-the-sum-of-elements-of-a-vector-using-stl-in-c/)
    *   [使用变量 **j** 遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)、**V【I】**
        *   从**和**中减去**V【I】【j】**的值。
        *   将值**相加–V[I][j]*(V[I]。尺寸()–1–j)**至**和**。
*   打印**和**的值作为结果。

> 设向量的元素为 x1，x2，x3，x4，代表同一字符的索引。
> 该字符将贡献值=**| x2–x1 |+| x3–x1 |+| x4–x1 |+| x3–x2 |+| x4–x2 |+| x4–x3 |**
> 
> 对于排序后的数组，也可以写成**(x2+x3+x4)–3 * x1+(x3+x4)–2 * x2+(x4)–1 * x3**。
> 
> 现在，总和也可以表示为**∑后缀【I+****1】–(n-I)* Xi**为 **i = 1 至 n** 。
> 其中**后缀【I+1】**为**【I+1，n】**的元素之和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of the manhattan
// distances between same characters in string
void SumofDistances(string s)
{
    // Vector to store indices for each
    // unique character of the string
    vector<int> v[26];

    // Append the position of each character
    // in their respective vectors
    for (int i = 0; i < s.size(); i++) {
        v[s[i] - 'a'].push_back(i);
    }

    // Store the required result
    int ans = 0;

    // Iterate over all the characters
    for (int i = 0; i < 26; i++) {
        int sum = 0;

        // Calculate sum of all elements
        // present in the vector
        for (int j = 0; j < v[i].size(); j++) {
            sum += v[i][j];
        }

        // Traverse the current vector
        for (int j = 0; j < v[i].size(); j++) {

            // Find suffix[i+1]
            sum -= v[i][j];

            // Adding distance of all pairs
            // whose first element is i and
            // second element belongs to [i+1, n]
            ans += (sum
                    - (v[i].size() - 1 - j) * (v[i][j]));
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given Input
    string s = "ababa";

    // Function Call
    SumofDistances(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the sum of the manhattan
// distances between same characters in string
static void SumofDistances(String s)
{

    // Vector to store indices for each
    // unique character of the string
    ArrayList<ArrayList<Integer>> v = new ArrayList<>();

    for(int i = 0; i < 26; i++)
        v.add(new ArrayList<>());

    // Append the position of each character
    // in their respective vectors
    for(int i = 0; i < s.length(); i++)
    {
        v.get(s.charAt(i) - 'a').add(i);
    }

    // Store the required result
    int ans = 0;

    // Iterate over all the characters
    for(int i = 0; i < 26; i++)
    {
        int sum = 0;

        // Calculate sum of all elements
        // present in the vector
        for(int j = 0; j < v.get(i).size(); j++)
        {
            sum += v.get(i).get(j);
        }

        // Traverse the current vector
        for(int j = 0; j < v.get(i).size(); j++)
        {

            // Find suffix[i+1]
            sum -= v.get(i).get(j);

            // Adding distance of all pairs
            // whose first element is i and
            // second element belongs to [i+1, n]
            ans += (sum - (v.get(i).size() - 1 - j) *
                          (v.get(i).get(j)));
        }
    }

    // Print the result
   System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    String s = "ababa";

    // Function Call
    SumofDistances(s);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach

#Function to find the sum of the manhattan
#distances between same characters in string
def SumofDistances(s):

    # Vector to store indices for each
    # unique character of the string
    v = [[] for i in range(26)]

    # Append the position of each character
    # in their respective vectors
    for i in range(len(s)):
        v[ord(s[i]) - ord('a')].append(i)

    # Store the required result
    ans = 0

    # Iterate over all the characters
    for i in range(26):
        sum = 0

        # Calculate sum of all elements
        # present in the vector
        for j in range(len(v[i])):
            sum += v[i][j]

        # Traverse the current vector
        for j in range(len(v[i])):
            # Find suffix[i+1]
            sum -= v[i][j]

            # Adding distance of all pairs
            # whose first element is i and
            # second element belongs to [i+1, n]
            ans += (sum - (len(v[i]) - 1 - j) * (v[i][j]))

    # Print the result
    print (ans)

# Driver Code
if __name__ == '__main__':
    # Given Input
    s = "ababa"

    # Function Call
    SumofDistances(s)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the sum of the manhattan
// distances between same characters in string
static void SumofDistances(string s)
{

    // Vector to store indices for each
    // unique character of the string
    List<int>[] v = new List<int>[26];
    for(int i = 0; i < 26; i++)
      v[i] = new List<int>();

    // Append the position of each character
    // in their respective vectors
    for(int i = 0; i < s.Length; i++)
    {
        v[(int)s[i] - 97].Add(i);
    }

    // Store the required result
    int ans = 0;

    // Iterate over all the characters
    for(int i = 0; i < 26; i++)
    {
        int sum = 0;

        // Calculate sum of all elements
        // present in the vector
        for(int j = 0; j < v[i].Count; j++)
        {
            sum += v[i][j];
        }

        // Traverse the current vector
        for(int j = 0; j < v[i].Count; j++)
        {

            // Find suffix[i+1]
            sum -= v[i][j];

            // Adding distance of all pairs
            // whose first element is i and
            // second element belongs to [i+1, n]
            ans += (sum - (v[i].Count - 1 - j) *
                          (v[i][j]));
        }
    }

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main()
{

    // Given Input
    string s = "ababa";

    // Function Call
    SumofDistances(s);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the sum of the manhattan
// distances between same characters in string
function SumofDistances(s)
{
    let v = [];
    for(let i = 0; i < 26; i++)
        v.push([]);

    // Append the position of each character
    // in their respective vectors
    for(let i = 0; i < s.length; i++)
    {
        v[s[i].charCodeAt(0) - 'a'.charCodeAt(0)].push(i);
    }

    // Store the required result
    let ans = 0;

    // Iterate over all the characters
    for(let i = 0; i < 26; i++)
    {
        let sum = 0;

        // Calculate sum of all elements
        // present in the vector
        for(let j = 0; j < v[i].length; j++)
        {
            sum += v[i][j];
        }

        // Traverse the current vector
        for(let j = 0; j < v[i].length; j++)
        {

            // Find suffix[i+1]
            sum -= v[i][j];

            // Adding distance of all pairs
            // whose first element is i and
            // second element belongs to [i+1, n]
            ans += (sum - (v[i].length - 1 - j) *
                          (v[i][j]));
        }
    }

    // Print the result
   document.write(ans);
}

// Driver code
// Given Input
let s = "ababa";

// Function Call
SumofDistances(s);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)