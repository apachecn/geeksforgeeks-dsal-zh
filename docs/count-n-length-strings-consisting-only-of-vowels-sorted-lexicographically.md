# 统计仅由按照字典顺序排序的元音组成的 N 长度字符串

> 原文:[https://www . geesforgeks . org/count-n-length-strings-仅由元音组成-按字典顺序排序/](https://www.geeksforgeeks.org/count-n-length-strings-consisting-only-of-vowels-sorted-lexicographically/)

给定一个整数 **N** ，任务是统计所有可能的长度字符串 **N** 由元音 **{a，e，I，o，u}** 组成，这些元音可以形成为每个[字符串按照词典顺序](https://www.geeksforgeeks.org/sort-words-lexicographical-order-python/)排序。

**示例:**

> **输入:** N = 2
> **输出:** 15
> **说明:**长度为 2 的字符串按字典顺序排序为[“aa”“AE”“ai”“ao”“au”“ee”“ei”“EO”“eu”“ii”“io”“iu”“oo”“ou”“uu”]。
> 
> **输入:** N = 1
> **输出:** 5
> **说明:**长度为 1 的字符串按字典顺序排序为[“a”、“e”、“I”、“o”、“u”]。

**天真方法:**最简单的方法是[生成所有可能长度的字符串**N**T5【这样每个字符串都按照字典顺序排序。打印完成步骤后获得的计数。](https://www.geeksforgeeks.org/print-all-combinations-of-given-length/)

**递归方法:**跟踪添加到字符串中的元音，以便添加到字符串中的下一个元音在词典学上总是更大。

## C++

```
// C++ program to illustrate Count of N-length strings
// consisting only of vowels sorted lexicographically

#include <iostream>
using namespace std;
// to keep the string in lexicographically sorted order use
// start index
// to add the vowels starting the from that index
int countstrings(int n, int start)
{
    // base case: if string length is 0 add to the count
    if (n == 0) {
        return 1;
    }
    int cnt = 0;
    // if last character in string is 'e'
    // add vowels starting from  'e'
    // i.e    'e','i','o','u'
    for (int i = start; i < 5; i++) {
        // decrease the length of string
        cnt += countstrings(n - 1, i);
    }
    return cnt;
}
int countVowelStrings(int n)
{
    //  char arr[5]={'a','e','i','o','u'};
    // starting from index 0 add the vowels to strings
    return countstrings(n, 0);
}
int main()
{
    int n = 2;
    cout << countVowelStrings(n);
    return 0;
}
// This code is contributed by Deepak Chowdary
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate Count of N-length strings
// consisting only of vowels sorted lexicographically
import java.util.*;
public class Main
{

    // to keep the string in lexicographically sorted order use
    // start index
    // to add the vowels starting the from that index
    static int countstrings(int n, int start)
    {

        // base case: if string length is 0 add to the count
        if (n == 0) {
            return 1;
        }
        int cnt = 0;

        // if last character in string is 'e'
        // add vowels starting from  'e'
        // i.e    'e','i','o','u'
        for (int i = start; i < 5; i++)
        {

            // decrease the length of string
            cnt += countstrings(n - 1, i);
        }
        return cnt;
    }
    static int countVowelStrings(int n)
    {

        //  char arr[5]={'a','e','i','o','u'};
        // starting from index 0 add the vowels to strings
        return countstrings(n, 0);
    }

    public static void main(String[] args) {
        int n = 2;
        System.out.print(countVowelStrings(n));
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program to illustrate Count of N-length strings
# consisting only of vowels sorted lexicographically

# to keep the string in lexicographically sorted order use
# start index
# to add the vowels starting the from that index
def countstrings(n, start):

    # base case: if string length is 0 add to the count
    if n == 0:
        return 1
    cnt = 0

    # if last character in string is 'e'
    # add vowels starting from  'e'
    # i.e    'e','i','o','u'
    for i in range(start, 5):

        # decrease the length of string
        cnt += countstrings(n - 1, i)
    return cnt

def countVowelStrings(n):

    #  char arr[5]={'a','e','i','o','u'};
    # starting from index 0 add the vowels to strings
    return countstrings(n, 0)

n = 2
print(countVowelStrings(n))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to illustrate Count of N-length strings
// consisting only of vowels sorted lexicographically
using System;
using System.Collections.Generic;
class GFG {

    // to keep the string in lexicographically sorted order use
    // start index
    // to add the vowels starting the from that index
    static int countstrings(int n, int start)
    {

        // base case: if string length is 0 add to the count
        if (n == 0) {
            return 1;
        }
        int cnt = 0;

        // if last character in string is 'e'
        // add vowels starting from  'e'
        // i.e    'e','i','o','u'
        for (int i = start; i < 5; i++)
        {

            // decrease the length of string
            cnt += countstrings(n - 1, i);
        }
        return cnt;
    }
    static int countVowelStrings(int n)
    {

        //  char arr[5]={'a','e','i','o','u'};
        // starting from index 0 add the vowels to strings
        return countstrings(n, 0);
    }

  static void Main() {
    int n = 2;
    Console.Write(countVowelStrings(n));
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript program to illustrate Count of N-length strings
    // consisting only of vowels sorted lexicographically

    // to keep the string in lexicographically sorted order use
    // start index
    // to add the vowels starting the from that index
    function countstrings(n, start)
    {

        // base case: if string length is 0 add to the count
        if (n == 0) {
            return 1;
        }
        let cnt = 0;

        // if last character in string is 'e'
        // add vowels starting from  'e'
        // i.e    'e','i','o','u'
        for (let i = start; i < 5; i++)
        {

            // decrease the length of string
            cnt += countstrings(n - 1, i);
        }
        return cnt;
    }
    function countVowelStrings(n)
    {

        //  char arr[5]={'a','e','i','o','u'};
        // starting from index 0 add the vowels to strings
        return countstrings(n, 0);
    }

    let n = 2;
    document.write(countVowelStrings(n));

 // This code is contributed by suresh07.
</script>
```

**Output**

```
15
```

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。以下是解决给定问题的一些观察结果:

*   从字符 **a、e、I、o 和 u** 开始的长度为 **1** 的按词典排序的字符串计数为 **1** 。
*   从字符 **a、e、I、o 和 u** 开始按字典顺序排列的长度为 **2** 的字符串的计数由下式给出:
    *   从字符 **a** 开始的长度为 **2** 的词典排序字符串的计数由从大于或等于 **a** 的字符开始的长度为 **1** 的词典排序字符串的计数给出。所以计数为 **5** 。
    *   从字符 **e** 开始的长度为 **2** 的词典排序字符串的计数由从大于或等于 **e** 的字符开始的长度为 **1** 的词典排序字符串的计数给出。所以计数为 **4** 。
    *   从字符 **i** 开始的长度为 **2** 的词典排序字符串的计数由从大于或等于 **i** 的字符开始的长度为 **1** 的词典排序字符串的计数给出。所以计数为 **3** 。
    *   从字符 **o** 开始的长度为 **2** 的词典排序字符串的计数由从大于或等于字符 **o** 开始的长度为 **1** 的词典排序字符串的计数给出。所以计数为 **2** 。
    *   从字符 **u** 开始的长度为 **2** 的词典排序字符串的计数由从大于或等于 **u** 的字符开始的长度为 **1** 的词典排序字符串的计数给出。所以计数为 **1** 。
*   因此，弦长 **2** 的总计数由下式给出: **5 + 4 + 3 + 2 + 1 = 15** 。
*   通过观察上述模式，从每个元音字符 **ch** 开始的长度为 **N** 的字符串的计数由从大于或等于 **ch** 的字符开始的长度为**(N–1)**的词典字符串的计数之和给出。

按照以下步骤解决问题:

*   创建一个 2D 数组， **dp[N + 1][6]** ，其中 **dp[i][j]** 表示长度为 **i** 的按词典排序的字符串的数量，这些字符串可以使用第一个 **j** 元音构建，并用 **1** 初始化 **dp[1][1]** 。
*   使用变量 **j、**迭代第一行，将**DP[1][j]= DP[1][j–1]+1**设置为长度字符串 **1** 总是按字典顺序排序。
*   [遍历 2D 数组](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/) **dp[][]** 并将每个 dp 状态更新为**DP[I][j]= DP[I][j–1]+DP[I–1][j]**，其中**DP[I][j–1]**将给出词典字符串长度的计数 **N** ，**DP[I–1][j]**将给出词典字符串长度的计数**(N–1)**
*   完成上述步骤后，打印 **dp[N][5]** 的值作为结果字符串的总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
int findNumberOfStrings(int n)
{
    // Stores count of strings consisting
    // of vowels sorted lexicographically
    // of all possible lengths
    vector<vector<int> > DP(n + 1,
                            vector<int>(6));

    // Initialize DP[1][1]
    DP[1][1] = 1;

    // Traverse the matrix row-wise
    for (int i = 1; i < n + 1; i++) {

        for (int j = 1; j < 6; j++) {

            // Base Case
            if (i == 1) {
                DP[i][j] = DP[i][j - 1] + 1;
            }

            else {
                DP[i][j] = DP[i][j - 1]
                           + DP[i - 1][j];
            }
        }
    }

    // Return the result
    return DP[n][5];
}

// Driver Code
int main()
{
    int N = 2;

    // Function Call
    cout << findNumberOfStrings(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
static int findNumberOfStrings(int n)
{
  // Stores count of strings consisting
  // of vowels sorted lexicographically
  // of all possible lengths
  int DP[][] = new int [n + 1][6];

  // Initialize DP[1][1]
  DP[1][1] = 1;

  // Traverse the matrix row-wise
  for (int i = 1; i < n + 1; i++)
  {
    for (int j = 1; j < 6; j++)
    {
      // Base Case
      if (i == 1)
      {
        DP[i][j] = DP[i][j - 1] + 1;
      }

      else
      {
        DP[i][j] = DP[i][j - 1] +
                   DP[i - 1][j];
      }
    }
  }

  // Return the result
  return DP[n][5];
}

// Driver Code
public static void main(String[] args)
{
  int N = 2;

  // Function Call
  System.out.print(findNumberOfStrings(N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to count N-length
# strings consisting of vowels
# only sorted lexicographically
def findNumberOfStrings(n):

    # Stores count of strings
    # consisting of vowels
    # sorted lexicographically
    # of all possible lengths
    DP = [[0 for i in range(6)]
             for i in range(n + 1)]

    # Initialize DP[1][1]
    DP[1][1] = 1

    # Traverse the matrix row-wise
    for i in range(1, n + 1):
        for j in range(1, 6):

            #Base Case
            if (i == 1):
                DP[i][j] = DP[i][j - 1] + 1
            else:
                DP[i][j] = DP[i][j - 1]+ DP[i - 1][j]

    # Return the result
    return DP[n][5]

# Driver Code
if __name__ == '__main__':

    N = 2

    # Function Call
    print(findNumberOfStrings(N))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
static int findNumberOfStrings(int n)
{
  // Stores count of strings consisting
  // of vowels sorted lexicographically
  // of all possible lengths
  int[,] DP = new int [n + 1, 6];

  // Initialize DP[1][1]
  DP[1, 1] = 1;

  // Traverse the matrix row-wise
  for (int i = 1; i < n + 1; i++)
  {
    for (int j = 1; j < 6; j++)
    {
      // Base Case
      if (i == 1)
      {
        DP[i, j] = DP[i, j - 1] + 1;
      }

      else
      {
        DP[i, j] = DP[i, j - 1] +
                   DP[i - 1, j];
      }
    }
  }

  // Return the result
  return DP[n, 5];
}

// Driver Code
public static void Main(string[] args)
{
  int N = 2;

  // Function Call
  Console.Write(findNumberOfStrings(N));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
function findNumberOfStrings(n)
{
  // Stores count of strings consisting
  // of vowels sorted lexicographically
  // of all possible lengths
  let DP = new Array(n + 1);

  // Loop to create 2D array using 1D array
    for (var i = 0; i < DP.length; i++) {
    DP[i] = new Array(2);
    }

    for (var i = 0; i < DP.length; i++) {
        for (var j = 0; j < DP.length; j++) {
        DP[i][j] = 0;
    }
    }

  // Initialize DP[1][1]
  DP[1][1] = 1;

  // Traverse the matrix row-wise
  for (let i = 1; i < n + 1; i++)
  {
    for (let j = 1; j < 6; j++)
    {
      // Base Case
      if (i == 1)
      {
        DP[i][j] = DP[i][j - 1] + 1;
      }

      else
      {
        DP[i][j] = DP[i][j - 1] +
                   DP[i - 1][j];
      }
    }
  }

  // Return the result
  return DP[n][5];
}

// Driver Code

  let N = 2;

  // Function Call
  document.write(findNumberOfStrings(N));

</script>
```

**Output**

```
15
```

**时间复杂度:**O(N * 5)
T3】辅助空间: O(N*5)

**高效逼近**:上述逼近可以进一步简化为**线性时间**和**恒定空间。**

以下是对不同长度弦的一些观察:-

<figure class="table">

| **N** | **以**开始的字符串数 | **总可能字符串** |
| **‘a’** | **‘e’** | **‘I’** | **'o'** | **‘u’** |
| one | one | one | one | one | one | five |
| Two | five | four | three | Two | one | Fifteen |
| three | Fifteen | Ten | six | three | one | Thirty-five |
| four | Thirty-five | Twenty | Ten | four | one | Seventy |

可以看出，对于 **N** 的每个值，可能的字符串数量取决于 **N (N-1)** 的先前值。

**第 N 行**中任意一列的值是 **(N-1)行**中所有列的总和，从右侧开始直到该列号。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
int findNumberOfStrings(int N)
{
    // Initializing vector to store count of strings.
    vector<int> counts(5, 1);

    for (int i = 2; i <= N; i++) {
        for (int j = 3; j >= 0; j--)
            counts[j] += counts[j + 1];
    }

    int ans = 0;

    // Summing up the total number of combinations.
    for (auto c : counts)
        ans += c;

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    int N = 2;

    // Function Call
    cout << findNumberOfStrings(N);

    return 0;
}

// This code is contributed by Sarvesh Roshan.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Function to count N-length strings
    // consisting of vowels only sorted
    // lexicographically
    static int findNumberOfStrings(int N)
    {
        // Initializing vector to store count of strings.
        Vector<Integer> counts = new Vector<Integer>();
        for(int i = 0; i < 5; i++)
        {
            counts.add(1);
        }

        for (int i = 2; i <= N; i++) {
            for (int j = 3; j >= 0; j--)
                counts.set(j, counts.get(j) + counts.get(j + 1));
        }

        int ans = 0;

        // Summing up the total number of combinations.
        for(Integer c : counts)
            ans += c;

        // Return the result
        return ans;
    }

    public static void main(String[] args) {
        int N = 2;

        // Function Call
        System.out.print(findNumberOfStrings(N));
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count N-length strings
# consisting of vowels only sorted
# lexicographically
def findNumberOfStrings(N):
    # Initializing vector to store count of strings.
    counts = []
    for i in range(5):
        counts.append(1)

    for i in range(2, N + 1):
        for j in range(3, -1, -1):
            counts[j] += counts[j + 1]

    ans = 0

    # Summing up the total number of combinations.
    for c in counts:
        ans += c

    # Return the result
    return ans

N = 2

# Function Call
print(findNumberOfStrings(N))

# This code is contributed by decode2207.
```

**Output**

```
15
```

**时间复杂度:**O(5 * N)
T3】空间复杂度: O(1)

**高效方式:**上述 **dp** 方式的相同思路可以在**恒定时间**和**恒定空间**中实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
int findNumberOfStrings(int n)
{
    return (n+1)*(n+2)*(n+3)*(n+4)/24;
}

// Driver Code
int main()
{
    int N = 2;

    // Function Call
    cout << findNumberOfStrings(N);

    return 0;
}
// This code is contributed by Kartik Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
static int findNumberOfStrings(int n)
{
 return (n+1)*(n+2)*(n+3)*(n+4)/24;
}

// Driver Code
public static void main(String[] args)
{
  int N = 2;

  // Function Call
  System.out.print(findNumberOfStrings(N));
}
}

// This code is contributed by Kartik Singh
```

## 计算机编程语言

```
# Python3 program for the
# above approach

# Function to count N-length
# strings consisting of vowels
# only sorted lexicographically
def findNumberOfStrings(n):
    return int((n+1)*(n+2)*(n+3)*(n+4)/24)

# Driver Code
if __name__ == '__main__':

    N = 2

    # Function Call
    print(findNumberOfStrings(N))

# This code is contributed by Kartik Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
static int findNumberOfStrings(int n)
{
  return (n+1)*(n+2)*(n+3)*(n+4)/24;
}

// Driver Code
public static void Main(string[] args)
{
  int N = 2;

  // Function Call
  Console.Write(findNumberOfStrings(N));
}
}

// This code is contributed by Kartik Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count N-length strings
// consisting of vowels only sorted
// lexicographically
function findNumberOfStrings(n)
{
    return (n+1)*(n+2)*(n+3)*(n+4)/24;
}

// Driver Code

  let N = 2;

  // Function Call
  document.write(findNumberOfStrings(N));

</script>
```

**Output**

```
15
```

**时间复杂度** : O(1)

**辅助空间** : O(1)

</figure>