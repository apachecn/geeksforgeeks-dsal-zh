# 制作一串 Panagram 的成本|第二套

> 原文:[https://www . geesforgeks . org/制作字符串的成本-panagram-set-2/](https://www.geeksforgeeks.org/cost-to-make-a-string-panagram-set-2/)

给定一个数组**cost【】**包含将来自**(a–z)**的每个字母相加的成本，以及一个由小写英文字母组成的字符串 **str** ，它可以是也可以不是一个 [Panagram](https://www.geeksforgeeks.org/pangram-checking/) 。任务是通过以下操作使给定的字符串成为 Panagram:

1.  在**字符串**中添加一个字符的成本是该字符相关成本的两倍。
2.  从**字符串**中删除一个字符将导致获得与该字符相关的确切成本。

打印使给定字符串成为 Panagram 的成本，如果收益大于成本，则打印 **0** 。

**示例:**

> **输入:** arr[] = {1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1}，
> str = " geeks forgeeks "
> T4】输出: 32
> 字符出现次数如下:
> g = 2，e = 4，k = 2，s = 2，f = 1， o = 1 和 r = 1
> 英文字母中剩余的 19 个字符将按成本 2 相加，即 2 * 19 = 38
> 并且，字符‘g’、‘e’、‘k’和‘s’的 1、3、1 和 1 的出现分别可以换取收益(1 + 3 + 1 + 1)，即 6
> 因此，标准化成本为 38–6 = 32
> 
> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10，11，12，13，14，15，16，17，18，19，20，21，22，23，24，25，26}，
> str = " The quickbrownfoxpjumperserverthelazydog "
> T4】输出: 0
> 给定的字符串已经是 Panagram

**进场:**

*   将每个字符的出现存储在一个数组中**出现次数[]** 。
*   初始化**增益= 0** 并开始遍历数组**事件[]** ，对于每个字符 **ch** :
    *   如果 **ch** 出现不止一次，比如 **x 次**，那么**x–1**可以用它的出现换取一些增益，即**增益=增益+成本【ch】*(x–1)**。
    *   如果 **str** 中没有出现 **ch** ，则必须以两倍的成本添加，即**增益=增益–(2 *成本【ch】)**。
*   如果**增益≥ 0** ，则打印 **0** 。
*   否则打印**增益* -1** ，这是制作**str**Panagram 的成本。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the cost
// to make str a Panagram
int costToPanagram(string str, int cost[])
{

    int i, n = str.length();
    int occurrences[26] = {0};

    // Count the occurrences of
    // each lowercase character
    for (i = 0; i < n; i++)
        occurrences[str[i] - 'a']++;

    // To store the total gain
    int gain = 0;
    for (i = 0; i < 26; i++)
    {

        // If some character is missing,
        // it has to be added at twice the cost
        if (occurrences[i] == 0)
            gain -= (2 * cost[i]);

        // If some character appears more
        // than once, all of its occurrences
        // except 1 can be traded for some gain
        else if (occurrences[i] > 1)
            gain += (cost[i] * (occurrences[i] - 1));
    }

    // If gain is more than the cost
    if (gain >= 0)
        return 0;

    // Return the total cost if gain < 0
    return (gain * -1);
}

// Driver code
int main()
{
    int cost[] = { 1, 1, 1, 1, 1, 1, 1, 1,
                   1, 1, 1, 1, 1, 1, 1, 1,
                   1, 1, 1, 1, 1, 1, 1, 1, 1, 1 };
    string str = "geeksforgeeks";

    cout << costToPanagram(str, cost);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the cost to make str a Panagram
    static int costToPanagram(String str, int cost[])
    {

        int i, n = str.length();
        int occurrences[] = new int[26];

        // Count the occurrences of each lowercase character
        for (i = 0; i < n; i++)
            occurrences[str.charAt(i) - 'a']++;

        // To store the total gain
        int gain = 0;
        for (i = 0; i < 26; i++) {

            // If some character is missing, it has to be added
            // at twice the cost
            if (occurrences[i] == 0)
                gain -= (2 * cost[i]);

            // If some character appears more than once
            // all of its occurrences except 1
            // can be traded for some gain
            else if (occurrences[i] > 1)
                gain += (cost[i] * (occurrences[i] - 1));
        }

        // If gain is more than the cost
        if (gain >= 0)
            return 0;

        // Return the total cost if gain < 0
        return (gain * -1);
    }

    // Driver code
    public static void main(String[] args)
    {
        int cost[] = { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
                       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 };
        String str = "geeksforgeeks";

        System.out.println(costToPanagram(str, cost));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the cost to
# make string a Panagram
def costToPanagram(string, cost):

    n = len(string)
    occurrences = [0] * 26

    # Count the occurrences of each
    # lowercase character
    for i in range(n):
        occurrences[ord(string[i]) - ord('a')] += 1

    # To store the total gain
    gain = 0
    for i in range(26):

        # If some character is missing,
        # it has to be added at twice the cost
        if occurrences[i] == 0:
            gain -= 2 * cost[i]

        # If some character appears more than
        # once all of its occurrences except 1
        # can be traded for some gain
        elif occurrences[i] > 1:
            gain += cost[i] * (occurrences[i] - 1)

    # If gain is more than the cost
    if gain >= 0:
        return 0

    # Return the total cost if gain < 0
    return gain * -1

# Driver code
if __name__ == "__main__":

    cost = [1, 1, 1, 1, 1, 1, 1,
               1, 1, 1, 1, 1, 1,
            1, 1, 1, 1, 1, 1, 1,
               1, 1, 1, 1, 1, 1]

    string = "geeksforgeeks"

    print(costToPanagram(string, cost))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the cost to make str a Panagram
    static int costToPanagram(string str, int []cost)
    {

        int i, n = str.Length ;
        int []occurrences = new int[26];

        // Count the occurrences of each lowercase character
        for (i = 0; i < n; i++)
            occurrences[str[i] - 'a']++;

        // To store the total gain
        int gain = 0;
        for (i = 0; i < 26; i++)
        {

            // If some character is missing, it has to be added
            // at twice the cost
            if (occurrences[i] == 0)
                gain -= (2 * cost[i]);

            // If some character appears more than once
            // all of its occurrences except 1
            // can be traded for some gain
            else if (occurrences[i] > 1)
                gain += (cost[i] * (occurrences[i] - 1));
        }

        // If gain is more than the cost
        if (gain >= 0)
            return 0;

        // Return the total cost if gain < 0
        return (gain * -1);
    }

    // Driver code
    public static void Main()
    {
        int []cost = { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
                    1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 };
        string str = "geeksforgeeks";
        Console.WriteLine(costToPanagram(str, cost));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the cost
// to make str a Panagram
function costToPanagram(str, cost)
{

    var i, n = str.length;
    var occurrences = Array(26).fill(0);

    // Count the occurrences of
    // each lowercase character
    for (i = 0; i < n; i++)
        occurrences[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // To store the total gain
    var gain = 0;
    for (i = 0; i < 26; i++)
    {

        // If some character is missing,
        // it has to be added at twice the cost
        if (occurrences[i] == 0)
            gain -= (2 * cost[i]);

        // If some character appears more
        // than once, all of its occurrences
        // except 1 can be traded for some gain
        else if (occurrences[i] > 1)
            gain += (cost[i] * (occurrences[i] - 1));
    }

    // If gain is more than the cost
    if (gain >= 0)
        return 0;

    // Return the total cost if gain < 0
    return (gain * -1);
}

// Driver code
var cost = [1, 1, 1, 1, 1, 1, 1, 1,
               1, 1, 1, 1, 1, 1, 1, 1,
               1, 1, 1, 1, 1, 1, 1, 1, 1, 1];
var str = "geeksforgeeks";
document.write( costToPanagram(str, cost));

// This code is contributed by importantly.
</script>
```

**Output:** 

```
32
```