# 小写字母和大写字母数量相等的子字符串数量

> 原文:[https://www . geesforgeks . org/substrings-具有相等数量的小写和大写字母/](https://www.geeksforgeeks.org/number-of-substrings-having-an-equal-number-of-lowercase-and-uppercase-letters/)

给定由小写字母和大写字母组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是找到小写字母和大写字母数量相等的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量。

**示例:**

> **输入:** S = "gEEk"
> **输出:** 3
> **解释:**
> 以下是小写和大写字母数量相等的子字符串:
> 
> 1.  “gE”
> 2.  “极客”
> 3.  “埃克”
> 
> 因此，子字符串的总数是 3。
> 
> **输入:**S = " women day "
> T3】输出: 4

**天真方法:**解决给定问题的最简单方法是[生成给定字符串的所有可能的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **S** 并且如果子串包含相等数量的小写和大写字母，则将该子串的计数增加 **1** 。检查所有子字符串后，打印**计数**的值作为结果。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效的方法:**给定的问题可以通过将每个小写和大写字母分别看作 **1** 和 **-1** 来解决，然后[求具有和 **0**](https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/) 的子阵的个数。按照以下步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，比如说 **M** ，它存储所有前缀总和的频率。
*   初始化一个变量，比如说 **currentSum** 为 **0** 和 **res** 为 **0** ，分别存储每个前缀的总和和结果子串的计数。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并执行以下步骤:
    *   如果当前字符是大写的，那么将 **currentSum** 的值增加 **1** 。否则，将**电流值**减少 **-1** 。
    *   如果**电流**的值为 **0** ，则将 **res** 的值增加 **1** 。
    *   如果地图 **M** 中存在 **currentSum** 的值，则将 **res** 的值增加**M【current sum】**。
    *   将哈希表 **M** 中**电流 m** 的频率增加 **1** 。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// substrings having an equal number
// of uppercase and lowercase characters
int countSubstring(string& S, int N)
{
    // Stores the count of prefixes
    // having sum S considering uppercase
    // and lowercase characters as 1 and -1
    unordered_map<int, int> prevSum;

    // Stores the count of substrings
    // having equal number of lowercase
    // and uppercase characters
    int res = 0;

    // Stores the sum obtained so far
    int currentSum = 0;

    for (int i = 0; i < N; i++) {

        // If the character is uppercase
        if (S[i] >= 'A' and S[i] <= 'Z') {
            currentSum++;
        }

        // Otherwise
        else
            currentSum--;

        // If currsum is o
        if (currentSum == 0)
            res++;

        // If the current sum exists in
        // the HashMap prevSum
        if (prevSum.find(currentSum)
            != prevSum.end()) {

            // Increment the resultant
            // count by 1
            res += (prevSum[currentSum]);
        }

        // Update the frequency of the
        // current sum by 1
        prevSum[currentSum]++;
    }

    // Return the resultant count of
    // the subarrays
    return res;
}

// Driver Code
int main()
{
    string S = "gEEk";
    cout << countSubstring(S, S.length());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;

class GFG{

// Function to find the count of
// substrings having an equal number
// of uppercase and lowercase characters
static int countSubstring(String S, int N)
{

    // Stores the count of prefixes
    // having sum S considering uppercase
    // and lowercase characters as 1 and -1
    HashMap<Integer, Integer> prevSum = new HashMap<>();

    // Stores the count of substrings
    // having equal number of lowercase
    // and uppercase characters
    int res = 0;

    // Stores the sum obtained so far
    int currentSum = 0;

    for(int i = 0; i < N; i++)
    {

        // If the character is uppercase
        if (S.charAt(i) >= 'A' && S.charAt(i) <= 'Z')
        {
            currentSum++;
        }

        // Otherwise
        else
            currentSum--;

        // If currsum is 0
        if (currentSum == 0)
            res++;

        // If the current sum exists in
        // the HashMap prevSum
        if (prevSum.containsKey(currentSum))
        {

            // Increment the resultant
            // count by 1
            res += prevSum.get(currentSum);
        }

        // Update the frequency of the
        // current sum by 1
        prevSum.put(currentSum,
                    prevSum.getOrDefault(currentSum, 0) + 1);
    }

    // Return the resultant count of
    // the subarrays
    return res;
}

// Driver Code
public static void main(String[] args)
{
    String S = "gEEk";
    System.out.println(countSubstring(S, S.length()));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the count of
# substrings having an equal number
# of uppercase and lowercase characters
def countSubstring(S, N):

    # Stores the count of prefixes
    # having sum S considering uppercase
    # and lowercase characters as 1 and -1
    prevSum = {}

    # Stores the count of substrings
    # having equal number of lowercase
    # and uppercase characters
    res = 0

    # Stores the sum obtained so far
    currentSum = 0

    for i in range(N):

        # If the character is uppercase
        if (S[i] >= 'A' and S[i] <= 'Z'):
            currentSum += 1

        # Otherwise
        else:
            currentSum -= 1

        # If currsum is o
        if (currentSum == 0):
            res += 1

        # If the current sum exists in
        # the HashMap prevSum
        if (currentSum in prevSum):

            # Increment the resultant
            # count by 1
            res += (prevSum[currentSum])

        # Update the frequency of the
        # current sum by 1
        if currentSum in prevSum:
            prevSum[currentSum] += 1
        else:
            prevSum[currentSum] = 1

    # Return the resultant count of
    # the subarrays
    return res

# Driver Code
if __name__ == '__main__':

    S = "gEEk"
    print(countSubstring(S, len(S)))

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the count of
// substrings having an equal number
// of uppercase and lowercase characters
static int countSubstring(String S, int N)
{

    // Stores the count of prefixes
    // having sum S considering uppercase
    // and lowercase characters as 1 and -1
    Dictionary<int,
               int> prevSum = new Dictionary<int,
                                             int>();

    // Stores the count of substrings
    // having equal number of lowercase
    // and uppercase characters
    int res = 0;

    // Stores the sum obtained so far
    int currentSum = 0;

    for(int i = 0; i < N; i++)
    {

        // If the character is uppercase
        if (S[i] >= 'A' && S[i] <= 'Z')
        {
            currentSum++;
        }

        // Otherwise
        else
            currentSum--;

        // If currsum is 0
        if (currentSum == 0)
            res++;

        // If the current sum exists in
        // the Dictionary prevSum
        if (prevSum.ContainsKey(currentSum))
        {

            // Increment the resultant
            // count by 1
            res += prevSum[currentSum];
            prevSum[currentSum] = prevSum[currentSum] + 1;
        }
        else
            prevSum.Add(currentSum, 1);
    }

    // Return the resultant count of
    // the subarrays
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "gEEk";
    Console.WriteLine(countSubstring(S, S.Length));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the count of
// substrings having an equal number
// of uppercase and lowercase characters
function countSubstring(S, N)
{
    // Stores the count of prefixes
    // having sum S considering uppercase
    // and lowercase characters as 1 and -1
    var prevSum = new Map();

    // Stores the count of substrings
    // having equal number of lowercase
    // and uppercase characters
    var res = 0;

    // Stores the sum obtained so far
    var currentSum = 0;

    for (var i = 0; i < N; i++) {

        // If the character is uppercase
        if (S[i] >= 'A' && S[i] <= 'Z') {
            currentSum++;
        }

        // Otherwise
        else
            currentSum--;

        // If currsum is o
        if (currentSum == 0)
            res++;

        // If the current sum exists in
        // the HashMap prevSum
        if (prevSum.has(currentSum)) {

            // Increment the resultant
            // count by 1
            res += (prevSum.get(currentSum));
        }

        // Update the frequency of the
        // current sum by 1
        if(prevSum.has(currentSum))
            prevSum.set(currentSum, prevSum.get(currentSum)+1)
        else
            prevSum.set(currentSum, 1)
    }

    // Return the resultant count of
    // the subarrays
    return res;
}

// Driver Code
var S = "gEEk";
document.write( countSubstring(S, S.length));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)