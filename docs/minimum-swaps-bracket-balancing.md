# 支架平衡的最小互换量

> 原文:[https://www . geesforgeks . org/minimum-互换-括号-平衡/](https://www.geeksforgeeks.org/minimum-swaps-bracket-balancing/)

您将看到一个由 2N 个字符组成的字符串，由 N 个“[”括号和 N 个“]”括号组成。如果一个字符串可以用 for S2[S1]来表示，那么它就被认为是平衡的，在 for[]中，S1 和 S2 是平衡的字符串。我们可以通过交换相邻字符来平衡一个不平衡的字符串。计算使字符串平衡所需的最小交换次数。

**示例:**

```
Input  : []][][
Output : 2
First swap: Position 3 and 4
[][]][
Second swap: Position 5 and 6
[][][]

Input  : [[][]]
Output : 0
The string is already balanced.
```

我们可以通过使用贪婪策略来解决这个问题。如果前 X 个字符组成了一个平衡的字符串，我们可以忽略这些字符并继续。如果我们在所需的“[”之前遇到“]”，那么我们必须开始交换元素来平衡字符串。

**天真方法**
初始化总和= 0，其中**总和**存储结果。遍历字符串，记录遇到的“[”括号的数量**。当我们遇到“]”字符时，请减少此计数。如果计数为负，那么我们必须开始平衡弦。
让指数‘I’代表我们所处的位置。我们现在前进到索引 j 处的下一个“[”。将总和增加 j–I。将位置 j 处的“[”移动到位置 I，并将所有其他字符向右移动。将计数设置回 0，并继续遍历字符串。最终，“sum”将具有所需的值。**

**时间复杂度= O(N^2)
额外空间= O(1)**

****优化方法**
我们可以首先遍历字符串，并在一个矢量中存储“[”的位置，比如说“ **pos** ”。将“p”初始化为 0。我们将使用 p 来遍历向量“pos”。类似于天真的方法，我们维护遇到的“[”括号的计数。当我们遇到“[”时，我们增加计数，并将“p”增加 1。当我们遇到“]”时，我们减少计数。如果计数变成负数，这意味着我们必须开始交换。元素 pos[p]告诉我们下一个“[”的索引。我们通过位置[p]–I 增加总和，其中 I 是当前指数。我们可以交换当前索引和位置[p]中的元素，并将计数重置为 0，并增加 p，使位置[p]指示下一个“[”。
由于我们已经将一个在简单方法中为 O(N)的步骤转换为 O(1)步骤，我们的新时间复杂度降低了。**

**时间复杂度= 0(N)
额外空间= 0(N)**

## **C++**

```
// C++ program to count swaps required to balance string
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// Function to calculate swaps required
long swapCount(string s)
{
    // Keep track of '['
    vector<int> pos;
    for (int i = 0; i < s.length(); ++i)
        if (s[i] == '[')
            pos.push_back(i);

    int count = 0; // To count number of encountered '['
    int p = 0;  // To track position of next '[' in pos
    long sum = 0; // To store result

    for (int i = 0; i < s.length(); ++i)
    {
        // Increment count and move p to next position
        if (s[i] == '[')
        {
            ++count;
            ++p;
        }
        else if (s[i] == ']')
            --count;

        // We have encountered an unbalanced part of string
        if (count < 0)
        {
            // Increment sum by number of swaps required
            // i.e. position of next '[' - current position
            sum += pos[p] - i;
            swap(s[i], s[pos[p]]);
            ++p;

            // Reset count to 1
            count = 1;
        }
    }
    return sum;
}

// Driver code
int main()
{
    string s = "[]][][";
    cout << swapCount(s) << "\n";

    s = "[[][]]";
    cout << swapCount(s) << "\n";
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to count swaps
// required to balance string
import java.util.*;

class GFG{

// Function to calculate swaps required
public static long swapCount(String s)
{

    // Keep track of '['
    Vector<Integer> pos = new Vector<Integer>();
    for(int i = 0; i < s.length(); ++i)
        if (s.charAt(i) == '[')
            pos.add(i);

    // To count number of encountered '['
    int count = 0;

    // To track position of next '[' in pos
    int p = 0; 

    // To store result
    long sum = 0;

    char[] S = s.toCharArray();

    for(int i = 0; i < s.length(); ++i)
    {

        // Increment count and move p
        // to next position
        if (S[i] == '[')
        {
            ++count;
            ++p;
        }
        else if (S[i] == ']')
            --count;

        // We have encountered an
        // unbalanced part of string
        if (count < 0)
        {

            // Increment sum by number of
            // swaps required i.e. position
            // of next '[' - current position
            sum += pos.get(p) - i;
            char temp = S[i];
            S[i] = S[pos.get(p)];
            S[pos.get(p)] = temp;
            ++p;

            // Reset count to 1
            count = 1;
        }
    }
    return sum;
}

// Driver code
public static void main(String[] args)
{
    String s = "[]][][";
    System.out.println(swapCount(s));

    s = "[[][]]";
    System.out.println(swapCount(s));
}
}

// This code is contributed by divyesh072019
```

## **蟒蛇 3**

```
# Python3 Program to count
# swaps required to balance
# string

# Function to calculate
# swaps required
def swapCount(s):

    # Keep track of '['
    pos = []

    for i in range(len(s)):
        if(s[i] == '['):
            pos.append(i)

    # To count number
    # of encountered '['        
    count = 0

    # To track position
    # of next '[' in pos
    p = 0   

    # To store result
    sum = 0       
    s = list(s)

    for i in range(len(s)):

        # Increment count and
        # move p to next position
        if(s[i] == '['):
            count += 1
            p += 1
        elif(s[i] == ']'):
            count -= 1

        # We have encountered an
        # unbalanced part of string
        if(count < 0):

            # Increment sum by number
            # of swaps required
            # i.e. position of next
            # '[' - current position
            sum += pos[p] - i
            s[i], s[pos[p]] = (s[pos[p]],
                               s[i])
            p += 1

            # Reset count to 1
            count = 1
    return sum

# Driver code
s = "[]][]["
print(swapCount(s))

s = "[[][]]"
print(swapCount(s))

# This code is contributed by avanitrachhadiya2155
```

## **C#**

```
// C# program to count swaps
// required to balance string
using System.IO;
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to calculate swaps required
static long swapCount(string s)
{

    // Keep track of '['
    List<int> pos = new List<int>();
    for(int i = 0; i < s.Length; i++)
    {
        if (s[i] == '[')
        {
            pos.Add(i);
        }
    }

    // To count number of encountered '['
    int count = 0;

    // To track position of next '[' in pos
    int p = 0;

    // To store result
    long sum = 0;

    char[] S = s.ToCharArray();

    for(int i = 0; i < S.Length; i++)
    {

        // Increment count and move p
        // to next position
        if (S[i] == '[')
        {
            ++count;
            ++p;
        }
        else if (S[i] == ']')
        {
            --count;
        }

        // We have encountered an
        // unbalanced part of string
        if (count < 0)
        {

            // Increment sum by number of
            // swaps required i.e. position
            // of next '[' - current position
            sum += pos[p]-i;
            char temp = S[i];
            S[i] = S[pos[p]];
            S[pos[p]] = temp;
            ++p;

            // Reset count to 1
            count = 1;
        }
    }
    return sum;
}

// Driver code
static void Main()
{
    string s = "[]][][";
    Console.WriteLine(swapCount(s));

    s = "[[][]]";
    Console.WriteLine(swapCount(s));
}
}

// This code is contributed by rag2127
```

## **java 描述语言**

```
<script>

// JavaScript program to count swaps
// required to balance string

// Function to calculate swaps required
function swapCount(s)
{

    // Keep track of '['
    let pos = [];
    for(let i = 0; i < s.length; ++i)
        if (s[i] == '[')
            pos.push(i);

    // To count number of encountered '['
    let count = 0;

    // To track position of next '[' in pos
    let p = 0; 

    // To store result
    let sum = 0;

    let S = s.split('');

    for(let i = 0; i < s.length; ++i)
    {

        // Increment count and move p
        // to next position
        if (S[i] == '[')
        {
            ++count;
            ++p;
        }
        else if (S[i] == ']')
            --count;

        // We have encountered an
        // unbalanced part of string
        if (count < 0)
        {

            // Increment sum by number of
            // swaps required i.e. position
            // of next '[' - current position
            sum += pos[p] - i;
            let temp = S[i];
            S[i] = S[pos[p]];
            S[pos[p]] = temp;
            ++p;

            // Reset count to 1
            count = 1;
        }
    }
    return sum;
}

// Driver Code

    let s = "[]][][";
    document.write(swapCount(s) + "<br/>");

    s = "[[][]]";
    document.write(swapCount(s));

</script>
```

****输出:****

```
2
0
```

****另一种方法:**
时间复杂度= O(N)
额外空间= O(1)
我们可以不用存储“[”的位置。**

**下面是实现:**

## **C++**

```
// C++ program to count swaps required
// to balance string
#include <bits/stdc++.h>
using namespace std;

long swapCount(string chars)
{

    // Stores total number of Left and
    // Right brackets encountered
    int countLeft = 0, countRight = 0;

    // swap stores the number of swaps
    // required imbalance maintains
    // the number of imbalance pair
    int swap = 0 , imbalance = 0;

    for(int i = 0; i < chars.length(); i++)
    {
        if (chars[i] == '[')
        {

            // Increment count of Left bracket
            countLeft++;

            if (imbalance > 0)
            {

                // swaps count is last swap count + total
                // number imbalanced brackets
                swap += imbalance;

                // imbalance decremented by 1 as it solved
                // only one imbalance of Left and Right
                imbalance--;    
            }
        }
        else if(chars[i] == ']' )
        {

            // Increment count of Right bracket
            countRight++;

            // imbalance is reset to current difference
            // between Left and Right brackets
            imbalance = (countRight - countLeft);
        }
    }
    return swap;
}

// Driver code 
int main()
{
    string s = "[]][][";
    cout << swapCount(s) << endl;

    s = "[[][]]";
    cout << swapCount(s) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to count swaps required to balance string
public class BalanceParan
{

    static long swapCount(String s)
    {
        char[] chars = s.toCharArray();

        // stores total number of Left and Right
        // brackets encountered
        int countLeft = 0, countRight = 0;
                // swap stores the number of swaps required
        //imbalance maintains the number of imbalance pair
        int swap = 0 , imbalance = 0;

        for(int i =0; i< chars.length; i++)
        {
            if(chars[i] == '[')
            {
                // increment count of Left bracket
                countLeft++;
                if(imbalance > 0)
                {
                    // swaps count is last swap count + total
                    // number imbalanced brackets
                    swap += imbalance;
                    // imbalance decremented by 1 as it solved
                    // only one imbalance of Left and Right
                    imbalance--;    
                }
            } else if(chars[i] == ']' )
            {
                // increment count of Right bracket
                countRight++;
                // imbalance is reset to current difference
                // between Left and Right brackets
                imbalance = (countRight-countLeft);
            }
        }
        return swap;
    }

// Driver code
    public static void main(String args[])
    {
        String s = "[]][][";
        System.out.println(swapCount(s) );

        s = "[[][]]";
        System.out.println(swapCount(s) );

    }
}
// This code is contributed by Janmejaya Das.
```

## **蟒蛇 3**

```
# Python3 program to count swaps required to
# balance string
def swapCount(s):

    chars = s

    # Stores total number of left and 
    # right brackets encountered
    countLeft = 0
    countRight = 0

    # Swap stores the number of swaps 
    # required imbalance maintains the
    # number of imbalance pair
    swap = 0
    imbalance = 0;

    for i in range(len(chars)):
        if chars[i] == '[':

            # Increment count of left bracket
            countLeft += 1

            if imbalance > 0:

                # Swaps count is last swap
                # count + total number
                # imbalanced brackets
                swap += imbalance

                # Imbalance decremented by 1
                # as it solved only one
                # imbalance of left and right
                imbalance -= 1

        elif chars[i] == ']':

            # Increment count of right bracket
            countRight += 1

            # Imbalance is reset to current
            # difference between left and
            # right brackets
            imbalance = (countRight - countLeft)

    return swap

# Driver code
s = "[]][][";
print(swapCount(s))

s = "[[][]]";
print(swapCount(s))

# This code is contributed by Prateek Gupta
```

## **C#**

```
// C# Program to count swaps required
// to balance string
using System;

class GFG
{

public static long swapCount(string s)
{
    char[] chars = s.ToCharArray();

    // stores the total number of Left and
    // Right brackets encountered
    int countLeft = 0, countRight = 0;

    // swap stores the number of swaps
    // required imbalance maintains the
    // number of imbalance pair
    int swap = 0, imbalance = 0;

    for (int i = 0; i < chars.Length; i++)
    {
        if (chars[i] == '[')
        {
            // increment count of Left bracket
            countLeft++;
            if (imbalance > 0)
            {
                // swaps count is last swap count + total
                // number imbalanced brackets
                swap += imbalance;

                // imbalance decremented by 1 as it solved
                // only one imbalance of Left and Right
                imbalance--;
            }
        }
        else if (chars[i] == ']')
        {
            // increment count of Right bracket
            countRight++;

            // imbalance is reset to current difference
            // between Left and Right brackets
            imbalance = (countRight - countLeft);
        }
    }
    return swap;
}

// Driver code
public static void Main(string[] args)
{
    string s = "[]][][";
    Console.WriteLine(swapCount(s));

    s = "[[][]]";
    Console.WriteLine(swapCount(s));
}
}

// This code is contributed by Shrikant13
```

## **java 描述语言**

```
<script>
    // Javascript Program to count swaps required
    // to balance string

    function swapCount(s)
    {
        let chars = s.split('');

        // stores the total number of Left and
        // Right brackets encountered
        let countLeft = 0, countRight = 0;

        // swap stores the number of swaps
        // required imbalance maintains the
        // number of imbalance pair
        let swap = 0, imbalance = 0;

        for (let i = 0; i < chars.length; i++)
        {
            if (chars[i] == '[')
            {
                // increment count of Left bracket
                countLeft++;
                if (imbalance > 0)
                {
                    // swaps count is last swap count + total
                    // number imbalanced brackets
                    swap += imbalance;

                    // imbalance decremented by 1 as it solved
                    // only one imbalance of Left and Right
                    imbalance--;
                }
            }
            else if (chars[i] == ']')
            {
                // increment count of Right bracket
                countRight++;

                // imbalance is reset to current difference
                // between Left and Right brackets
                imbalance = (countRight - countLeft);
            }
        }
        return swap;
    }

      let s = "[]][][";
    document.write(swapCount(s) + "</br>");

    s = "[[][]]";
    document.write(swapCount(s));

    // This code is contributed by suresh07.
</script>
```

****输出:****

```
2
0
```

**本文由 **Aditya Kamath** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**