# 将字符串分成两个子字符串，这两个子字符串具有最大数量的常见非重复字符

> 原文:[https://www . geeksforgeeks . org/partition-string-in-two-substrings-具有最大数量的常见非重复字符/](https://www.geeksforgeeks.org/partition-string-into-two-substrings-having-maximum-number-of-common-non-repeating-characters/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是通过将给定的字符串划分为两个非空的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)来找到常见非重复字符的最大数量。

**示例:**

> **输入:** str = "aabbca"
> **输出:** 2
> **解释:**
> 将字符串分成两个子字符串{ { str[0]，… str[2] }，{ str[3]，…，str[5] } }
> 两个子字符串中常见的非重复字符为{ 'a '，' b'}
> 因此，所需的输出为 2。
> 
> **输入:**str = " aaaaaaaaaa "
> T3】输出: 1

**天真方法:**解决这个问题最简单的方法是[迭代字符串的字符](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，在每个可能的索引处将字符串划分为两个非空的子字符串，并计算这两个子字符串中常见重复字符的数量。打印获得的最大计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count maximum common non-repeating
// characters that can be obtained by partitioning
// the string into two non-empty substrings
int countCommonChar(int ind, string& S)
{

    // Stores count of non-repeating characters
    // present in both the substrings
    int cnt = 0;

    // Stores distinct characters
    // in left substring
    set<char> ls;

    // Stores distinct characters
    // in right substring
    set<char> rs;

    // Traverse left substring
    for (int i = 0; i < ind; ++i) {

        // Insert S[i] into ls
        ls.insert(S[i]);
    }

    // Traverse right substring
    for (int i = ind; i < S.length();
         ++i) {

        // Insert S[i] into rs
        rs.insert(S[i]);
    }

    // Traverse distinct characters
    // of left substring
    for (auto v : ls) {

        // If current character is
        // present in right substring
        if (rs.count(v)) {

            // Update cnt
            ++cnt;
        }
    }

    // Return count
    return cnt;
}

// Function to partition the string into
// two non-empty substrings in all possible ways
void partitionStringWithMaxCom(string& S)
{
    // Stores maximum common distinct characters
    // present in both the substring partitions
    int ans = 0;

    // Traverse the string
    for (int i = 1; i < S.length(); ++i) {

        // Update ans
        ans = max(ans,
                  countCommonChar(i, S));
    }

    // Print count of maximum common
    // non-repeating characters
    cout << ans << "\n";
}

// Driver Code
int main()
{
    string str = "aabbca";

    partitionStringWithMaxCom(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count maximum common non-repeating
// characters that can be obtained by partitioning
// the String into two non-empty subStrings
static int countCommonChar(int ind, String S)
{

    // Stores count of non-repeating characters
    // present in both the subStrings
    int cnt = 0;

    // Stores distinct characters
    // in left subString
    HashSet<Character> ls = new HashSet<Character>();

    // Stores distinct characters
    // in right subString
    HashSet<Character> rs = new HashSet<Character>();

    // Traverse left subString
    for (int i = 0; i < ind; ++i) {

        // Insert S[i] into ls
        ls.add(S.charAt(i));
    }

    // Traverse right subString
    for (int i = ind; i < S.length();
         ++i) {

        // Insert S[i] into rs
        rs.add(S.charAt(i));
    }

    // Traverse distinct characters
    // of left subString
    for (char v : ls) {

        // If current character is
        // present in right subString
        if (rs.contains(v)) {

            // Update cnt
            ++cnt;
        }
    }

    // Return count
    return cnt;
}

// Function to partition the String into
// two non-empty subStrings in all possible ways
static void partitionStringWithMaxCom(String S)
{
    // Stores maximum common distinct characters
    // present in both the subString partitions
    int ans = 0;

    // Traverse the String
    for (int i = 1; i < S.length(); ++i) {

        // Update ans
        ans = Math.max(ans,
                  countCommonChar(i, S));
    }

    // Print count of maximum common
    // non-repeating characters
    System.out.print(ans+ "\n");
}

// Driver Code
public static void main(String[] args)
{
    String str = "aabbca";

    partitionStringWithMaxCom(str);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count maximum common 
# non-repeating characters that can 
# be obtained by partitioning the 
# string into two non-empty substrings
def countCommonChar(ind, S):

    # Stores count of non-repeating 
    # characters present in both the 
    # substrings
    cnt = 0

    # Stores distinct characters
    # in left substring
    ls = set()

    # Stores distinct characters
    # in right substring
    rs = set()

    # Traverse left substring
    for i in range(ind):

        # Insert S[i] into ls
        ls.add(S[i])

    # Traverse right substring
    for i in range(ind, len(S)):

        # Insert S[i] into rs
        rs.add(S[i])

    # Traverse distinct characters
    # of left substring
    for v in ls:

        # If current character is
        # present in right substring
        if v in rs:

            # Update cnt
            cnt += 1

    # Return count
    return cnt

# Function to partition the string 
# into two non-empty substrings in 
# all possible ways
def partitionStringWithMaxCom(S):

    # Stores maximum common distinct
    # characters present in both the
    # substring partitions
    ans = 0

    # Traverse the string
    for i in range(1, len(S)):

        # Update ans
        ans = max(ans, countCommonChar(i, S))

    # Print count of maximum common
    # non-repeating characters
    print(ans)

# Driver Code
if __name__ == "__main__": 

    string = "aabbca"

    partitionStringWithMaxCom(string)

# This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count maximum common non-repeating
// characters that can be obtained by partitioning
// the String into two non-empty subStrings
static int countCommonChar(int ind, String S)
{

    // Stores count of non-repeating characters
    // present in both the subStrings
    int cnt = 0;

    // Stores distinct characters
    // in left subString
    HashSet<char> ls = new HashSet<char>();

    // Stores distinct characters
    // in right subString
    HashSet<char> rs = new HashSet<char>();

    // Traverse left subString
    for(int i = 0; i < ind; ++i)
    {

        // Insert S[i] into ls
        ls.Add(S[i]);
    }

    // Traverse right subString
    for(int i = ind; i < S.Length; ++i) 
    {

        // Insert S[i] into rs
        rs.Add(S[i]);
    }

    // Traverse distinct characters
    // of left subString
    foreach(char v in ls) 
    {

        // If current character is
        // present in right subString
        if (rs.Contains(v))
        {

            // Update cnt
            ++cnt;
        }
    }

    // Return count
    return cnt;
}

// Function to partition the String into
// two non-empty subStrings in all possible ways
static void partitionStringWithMaxCom(String S)
{

    // Stores maximum common distinct characters
    // present in both the subString partitions
    int ans = 0;

    // Traverse the String
    for(int i = 1; i < S.Length; ++i) 
    {

        // Update ans
        ans = Math.Max(ans,
                       countCommonChar(i, S));
    }

    // Print count of maximum common
    // non-repeating characters
    Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    String str = "aabbca";

    partitionStringWithMaxCom(str);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to count maximum common non-repeating
// characters that can be obtained by partitioning
// the string into two non-empty substrings
function countCommonChar(ind, S)
{

    // Stores count of non-repeating characters
    // present in both the substrings
    var cnt = 0;

    // Stores distinct characters
    // in left substring
    var ls = new Set();

    // Stores distinct characters
    // in right substring
    var rs = new Set();

    // Traverse left substring
    for (var i = 0; i < ind; ++i) {

        // Insert S[i] into ls
        ls.add(S[i]);
    }

    // Traverse right substring
    for (var i = ind; i < S.length;
         ++i) {

        // Insert S[i] into rs
        rs.add(S[i]);
    }

    // Traverse distinct characters
    // of left substring
    ls.forEach(v => {

        // If current character is
        // present in right substring
        if (rs.has(v)) {

            // Update cnt
            ++cnt;
        }
    });

    // Return count
    return cnt;
}

// Function to partition the string into
// two non-empty substrings in all possible ways
function partitionStringWithMaxCom(S)
{
    // Stores maximum common distinct characters
    // present in both the substring partitions
    var ans = 0;

    // Traverse the string
    for (var i = 1; i < S.length; ++i) {

        // Update ans
        ans = Math.max(ans,
                  countCommonChar(i, S));
    }

    // Print count of maximum common
    // non-repeating characters
    document.write( ans);
}

// Driver Code
var str = "aabbca";
partitionStringWithMaxCom(str);

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)和[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)以排序顺序存储字符串的[不同字符。按照以下步骤解决问题:](https://www.geeksforgeeks.org/print-all-distinct-characters-of-a-string-in-order-3-methods/)

*   初始化一个变量，比如 **res** ，通过将字符串分成两个子字符串来存储两个子字符串中常见的不同字符的最大数量。
*   初始化一个[映射](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，比如说 **mp** ，来存储字符串每个不同字符的[频率。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   初始化一个[有序集](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，比如说 **Q** ，以有序的顺序存储字符串的不同字符。
*   [迭代字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的字符，对于每一个**I<sup>th</sup>T5【字符，递减 **str[i]** 的频率，检查**MP【str[I]】**的频率是否等于 **0** 。如果发现错误，则从**有序集合**中移除**字符串【I】**。**
*   否则，在有序集中插入**str【I】**并更新 **res = max(res，X)** ，其中 **X** 是有序集中的元素计数。
*   最后，打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace std;
using namespace __gnu_cxx;
using namespace __gnu_pbds;
template <typename T>
using ordered_set = tree<T, null_type, less<T>,
                         rb_tree_tag, tree_order_statistics_node_update>;

// Function to count maximum common non-repeating
// characters that can be obtained by partitioning
// the string into two non-empty substrings
int countMaxCommonChar(string& S)
{
    // Stores distinct characters
    // of S in sorted order
    ordered_set<char> Q;

    // Stores maximum common distinct characters
    // present in both the partitions
    int res = 0;

    // Stores frequency of each
    // distinct character n the string S
    map<char, int> freq;

    // Traverse the string
    for (int i = 0; i < S.length(); i++) {

        // Update frequency of S[i]
        freq[S[i]]++;
    }

    // Traverse the string
    for (int i = 0; i < S.length(); i++) {

        // Decreasing frequency of S[i]
        freq[S[i]]--;

        // If the frequency of S[i] is 0
        if (!freq[S[i]]) {

            // Remove S[i] from Q
            Q.erase(S[i]);
        }
        else {

            // Insert S[i] into Q
            Q.insert(S[i]);
        }

        // Stores count of distinct
        // characters in Q
        int curr = Q.size();

        // Update res
        res = max(res, curr);
    }

    cout << res << "\n";
}

// Driver Code
int main()
{
    string str = "aabbca";

    // Function call
    countMaxCommonChar(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count maximum common non-repeating
// characters that can be obtained by partitioning
// the String into two non-empty subStrings
static void countMaxCommonChar(char[] S)
{

    // Stores distinct characters
    // of S in sorted order
    LinkedHashSet<Character> Q = new LinkedHashSet<>();

    // Stores maximum common distinct characters
    // present in both the partitions
    int res = 1;

    // Stores frequency of each
    // distinct character n the String S
    HashMap<Character, Integer> freq = new HashMap<>();

    // Traverse the String
    for(int i = 0; i < S.length; i++)
    {

        // Update frequency of S[i]
        if (freq.containsKey(S[i]))
        {
            freq.put(S[i], freq.get(S[i]) + 1);
        }
        else
        {
            freq.put(S[i], 1);
        }
    }

    // Traverse the String
    for(int i = 0; i < S.length; i++)
    {

        // Decreasing frequency of S[i]
        if (freq.containsKey(S[i]))
        {
            freq.put(S[i], freq.get(S[i]) - 1);
        }

        // If the frequency of S[i] is 0
        if (!freq.containsKey(S[i]))
        {

            // Remove S[i] from Q
            Q.remove(S[i]);
        }
        else
        {

            // Insert S[i] into Q
            Q.add(S[i]);
        }

        // Stores count of distinct
        // characters in Q
        int curr = Q.size() - 1;

        // Update res
        res = Math.max(res, curr);
    }

    System.out.print(res + "\n");
}

// Driver Code
public static void main(String[] args)
{
    String str = "aabbca";

    // Function call
    countMaxCommonChar(str.toCharArray());
}
}

// This code is contributed by aashish1995
```

**Output**

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*