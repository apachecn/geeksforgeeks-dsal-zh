# 找到游戏的赢家

> 原文:[https://www.geeksforgeeks.org/find-the-winner-of-the-game/](https://www.geeksforgeeks.org/find-the-winner-of-the-game/)

两个玩家正在玩一个游戏，游戏中给出了一个字符串**。第一个玩家可以在偶数索引处取字符，第二个玩家可以在奇数索引处取字符。能够比其他玩家构建字典上更小的字符串的玩家赢得游戏。打印游戏的获胜者，如果是平局，则打印玩家 **A** 、 **B** 或打印**平局**。
**举例:**** 

> ****输入:** str = "geeksforgeeks"
> **输出:**B
> “eeggoss”是玩家 A 可以获得的字典上最小的
> 字符串。
> “eefkkr”是玩家 B 可以获得的字典上最小的
> 字符串。
> B 的字符串在词典上更小。
> **输入:** str = "abcdbh"
> **输出:** A**

****进场:**分别为 A、B 玩家创建两个空弦 **str1** 和 **str2** 。逐字符遍历原始字符串，对于索引为偶数的每个字符，在 **str1** 中追加该字符，否则在 **str2** 中追加该字符。最后，对生成的字符串进行排序，以获得字典上最小的字符串，并将它们进行比较，以找到游戏的赢家。
以下是上述方法的实施:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the winner of the game
void find_winner(string str, int n)
{

    // To store the strings for both the players
    string str1 = "", str2 = "";
    for (int i = 0; i < n; i++) {

        // If the index is even
        if (i % 2 == 0) {

            // Append the current character
            // to player A's string
            str1 += str[i];
        }

        // If the index is odd
        else {

            // Append the current character
            // to player B's string
            str2 += str[i];
        }
    }

    // Sort both the strings to get
    // the lexicographically smallest
    // string possible
    sort(str1.begin(), str1.end());
    sort(str2.begin(), str2.end());

    // Copmpare both the strings to
    // find the winner of the game
    if (str1 < str2)
        cout << "A";
    else if (str2 < str1)
        cout << "B";
    else
        cout << "Tie";
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int n = str.length();

    find_winner(str, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function to find the winner of the game
static void find_winner(String str, int n)
{

    // To store the strings for both the players
    String str1 = "", str2 = "";
    for (int i = 0; i < n; i++)
    {

        // If the index is even
        if (i % 2 == 0)
        {

            // Append the current character
            // to player A's string
            str1 += str.charAt(i);
        }

        // If the index is odd
        else
        {

            // Append the current character
            // to player B's string
            str2 += str.charAt(i);
        }
    }

    // Sort both the strings to get
    // the lexicographically smallest
    // string possible
    char a[] = str1.toCharArray();
    Arrays.sort(a);
    char b[] = str2.toCharArray();
    Arrays.sort(b);
    str1 = new String(a);
    str2 = new String(b);

    // Copmpare both the strings to
    // find the winner of the game
    if (str1.compareTo(str2) < 0)
        System.out.print("A");
    else if (str1.compareTo(str2) > 0)
        System.out.print("B");
    else
        System.out.print("Tie");
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int n = str.length();

    find_winner(str, n);
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function to find the winner of the game
def find_winner(string, n) :

    # To store the strings for both the players
    string1= ""; string2 = "";
    for i in range(n) :

        # If the index is even
        if (i % 2 == 0) :

            # Append the current character
            # to player A's string
            string1 += string[i];

        # If the index is odd
        else :

            # Append the current character
            # to player B's string
            string2 += string[i];

    # Sort both the strings to get
    # the lexicographically smallest
    # string possible
    string1 = "".join(sorted(string1))
    string2 = "".join(sorted(string2))

    # Copmpare both the strings to
    # find the winner of the game
    if (string1 < string2) :
        print("A", end = "");

    elif (string2 < string1) :
        print("B", end = "");

    else :
        print("Tie", end = "");

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";
    n = len(string);

    find_winner(string, n);

# This code is contributed by AnkitRai01
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the winner of the game
static void find_winner(String str, int n)
{

    // To store the strings for both the players
    String str1 = "", str2 = "";
    for (int i = 0; i < n; i++)
    {

        // If the index is even
        if (i % 2 == 0)
        {

            // Append the current character
            // to player A's string
            str1 += str[i];
        }

        // If the index is odd
        else
        {

            // Append the current character
            // to player B's string
            str2 += str[i];
        }
    }

    // Sort both the strings to get
    // the lexicographically smallest
    // string possible
    char []a = str1.ToCharArray();
    Array.Sort(a);
    char []b = str2.ToCharArray();
    Array.Sort(b);
    str1 = new String(a);
    str2 = new String(b);

    // Copmpare both the strings to
    // find the winner of the game
    if (str1.CompareTo(str2) < 0)
        Console.Write("A");
    else if (str1.CompareTo(str2) > 0)
        Console.Write("B");
    else
        Console.Write("Tie");
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int n = str.Length;

    find_winner(str, n);
}
}

// This code is contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

// Function to find the winner of the game
function find_winner(str, n)
{

    // To store the strings for both the players
    var str1 = "", str2 = "";
    for (var i = 0; i < n; i++) {

        // If the index is even
        if (i % 2 == 0) {

            // Append the current character
            // to player A's string
            str1 += str[i];
        }

        // If the index is odd
        else {

            // Append the current character
            // to player B's string
            str2 += str[i];
        }
    }

    // Sort both the strings to get
    // the lexicographically smallest
    // string possible
    str1 = str1.split('').sort();
    str2 = str2.split('').sort();

    // Copmpare both the strings to
    // find the winner of the game
    if (str1 < str2)
        document.write( "A");
    else if (str2 < str1)
        document.write( "B");
    else
        document.write( "Tie");
}

// Driver code
var str = "geeksforgeeks";
var n = str.length;
find_winner(str, n);

</script>
```

****Output:** 

```
B
```**