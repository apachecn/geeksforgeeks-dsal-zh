# 找出一个字符到前面位置的出现次数

> 原文:[https://www . geeksforgeeks . org/find-一个字符到前面位置的出现次数/](https://www.geeksforgeeks.org/find-the-number-of-occurrences-of-a-character-upto-preceding-position/)

给定长度为 **N** 的字符串 **S** 和表示字符串中字符位置的整数 **P** (1≤P≤N)。任务是找出出现在 P-1 索引位置的字符的出现次数。

**示例:**

> **输入:** S = "ababababab "，P = 9
> **输出:**4
> P 处的字符为‘a’。到第八个索引的“a”出现次数是 4
> 
> **输入:** S = "geeksforgeeks "，P = 9
> T3】输出: 1

**天真的方法:**天真的方法是迭代字符串，直到位置 1 搜索相似的字符。每当出现类似字符时，将计数器变量递增 1。

下面是上述方法的实现:

## C++

```
// CPP program to find the number of occurrences
// of a character at position P upto p-1
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of occurrences
// of a character at position P upto p-1
int Occurrence(string s, int position)
{
    int count = 0;
    for (int i = 0; i < position - 1; i++)
        if (s[i] == s[position - 1])
            count++;

    // Return the required count
    return count;
}

// Driver code
int main()
{
    string s = "ababababab";

    int p = 9;

    // Function call
    cout << Occurrence(s, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of occurrences
// of a character at position P upto p-1
class GFG
{

// Function to find the number of occurrences
// of a character at position P upto p-1
static int Occurrence(String s, int position)
{
    int count = 0;
    for (int i = 0; i < position - 1; i++)
        if (s.charAt(i) == s.charAt(position - 1))
            count++;

    // Return the required count
    return count;
}

// Driver code
public static void main(String[] args)
{
    String s = "ababababab";

    int p = 9;

    // Function call
    System.out.println(Occurrence(s, p));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the
# number of occurrences of
# a character at position P upto p-1

# Function to find the number of occurrences
# of a character at position P upto p-1
def Occurrence(s, position):
    count = 0
    for i in range(position - 1):
        if (s[i] == s[position - 1]):
            count += 1

    # Return the required count
    return count

# Driver code
s = "ababababab";

p = 9

# Function call
print(Occurrence(s, p))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the number of occurrences
// of a character at position P upto p-1
using System;

class GFG
{

// Function to find the number of occurrences
// of a character at position P upto p-1
static int Occurrence(String s, int position)
{
    int count = 0;
    for (int i = 0; i < position - 1; i++)
        if (s[i] == s[position - 1])
            count++;

    // Return the required count
    return count;
}

// Driver code
public static void Main(String[] args)
{
    String s = "ababababab";

    int p = 9;

    // Function call
    Console.WriteLine(Occurrence(s, p));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find the number of occurrences
// of a character at position P upto p-1

// Function to find the number of occurrences
// of a character at position P upto p-1
function Occurrence(s,position)
{
    let count = 0;
    for (let i = 0; i < position - 1; i++)
        if (s[i] == s[position - 1])
            count++;

    // Return the required count
    return count;
}

// Driver code
let s = "ababababab";

let p = 9;

// Function call
document.write(Occurrence(s, p));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
```

**每个查询的时间复杂度:** **O(N)** 。

**高效方法**:在这种情况下，如果有多个这样的查询，并且每个查询都有一个唯一的索引 P，那么一个高效的方法是使用一个频率数组来存储字符串每次迭代中的字符数。

下面是上述方法的实现:

## C++

```
// CPP program to find the number of occurrences
// of a character at position P upto p-1
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of occurrences
// of a character at position P upto p-1
int countOccurrence(string s, int position)
{
    int alpha[26] = { 0 }, b[s.size()] = { 0 };

    // Iterate over the string
    for (int i = 0; i < s.size(); i++) {
        // Store the Occurrence of same character
        b[i] = alpha[(int)s[i] - 97];

        // Increase its frequency
        alpha[(int)s[i] - 97]++;
    }

    // Return the required count
    return b[position - 1];
}

// Driver code
int main()
{
    string s = "ababababab";

    int p = 9;

    // Function call
    cout << countOccurrence(s, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of occurrences
// of a character at position P upto p-1
import java.util.*;

class GFG
{

// Function to find the number of occurrences
// of a character at position P upto p-1
static int countOccurrence(String s, int position)
{
    int []alpha = new int[26];
    int []b = new int[s.length()];

    // Iterate over the string
    for (int i = 0; i < s.length(); i++)
    {
        // Store the Occurrence of same character
        b[i] = alpha[(int)s.charAt(i) - 97];

        // Increase its frequency
        alpha[(int)s.charAt(i) - 97]++;
    }

    // Return the required count
    return b[position - 1];
}

// Driver code
public static void main(String[] args)
{
    String s = "ababababab";

    int p = 9;

    // Function call
    System.out.println(countOccurrence(s, p));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the number of occurrences
# of a character at position P upto p-1

# Function to find the number of occurrences
# of a character at position P upto p-1
def countOccurrence(s, position):
    alpha = [0] * 26
    b = [0] * len(s)

    # Iterate over the string
    for i in range(0, len(s)):

        # Store the Occurrence of same character
        b[i] = alpha[ord(s[i]) - 97]

        # Increase its frequency
        alpha[ord(s[i]) - 97] = alpha[ord(s[i]) - 97] + 1

    # Return the required count
    return b[position - 1]

# Driver code
s = "ababababab"

p = 9

# Function call
print(countOccurrence(s, p))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find the number of occurrences
// of a character at position P upto p-1
using System;

class GFG
{

// Function to find the number of occurrences
// of a character at position P upto p-1
static int countOccurrence(String s, int position)
{
    int []alpha = new int[26];
    int []b = new int[s.Length];

    // Iterate over the string
    for (int i = 0; i < s.Length; i++)
    {
        // Store the Occurrence of same character
        b[i] = alpha[(int)s[i] - 97];

        // Increase its frequency
        alpha[(int)s[i] - 97]++;
    }

    // Return the required count
    return b[position - 1];
}

// Driver code
public static void Main(String[] args)
{
    String s = "ababababab";

    int p = 9;

    // Function call
    Console.WriteLine(countOccurrence(s, p));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the number of occurrences
// of a character at position P upto p-1

// Function to find the number of occurrences
// of a character at position P upto p-1
function countOccurrence(s, position)
{
    let alpha = new Array(26);
    for(let i = 0; i < 26; i++)
    {
        alpha[i] = 0;
    }
    let b = new Array(s.length);

    // Iterate over the string
    for(let i = 0; i < s.length; i++)
    {

        // Store the Occurrence of same character
        b[i] = alpha[s[i].charCodeAt(0) - 97];

        // Increase its frequency
        alpha[s[i].charCodeAt(0) - 97]++;
    }

    // Return the required count
    return b[position - 1];
}

// Driver code
let s = "ababababab";

p = 9;

// Function call
document.write(countOccurrence(s, p));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4
```