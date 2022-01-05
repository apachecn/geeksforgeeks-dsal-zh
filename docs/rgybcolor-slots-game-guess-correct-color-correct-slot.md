# RGYB(颜色)吃角子老虎机游戏猜测正确吃角子老虎机的正确颜色

> 原文:[https://www . geesforgeks . org/rgybcolor-slots-game-guess-correct-color-correct-slot/](https://www.geeksforgeeks.org/rgybcolor-slots-game-guess-correct-color-correct-slot/)

假设您有四个插槽，每个插槽将分别包含红色(R)、黄色(Y)、绿色(G)和蓝色(B)。例如，如果选择 YGGR(插槽 1 为黄色，插槽 2 和插槽 3 为绿色，插槽 4 为红色)。槽的颜色事先你是不知道的。你可以猜猜颜色。例如，你可能会猜测 YRGB。
当你为正确的槽猜测正确的颜色时，你得到一个“命中”如果你猜测一个存在但在错误槽中的颜色，你得到一个“伪命中”:注意，一个命中的槽永远不能算作伪命中。
给定一个猜测和一个解决方案，你的任务是编写一个程序来计算命中数和伪命中数。
示例:

```
Input: solution -> RGBY, Guess -> GGRR
Output: hit -> 1, pseudohit -> 1

Input: solution -> RGYB, Guess -> YGRR
Output: hit -> 1, pseudohit -> 2

Input: solution -> RGYB, Guess -> GGYR
Output: hit -> 2, pseudohit -> 1
```

一个简单的解决方案是同时遍历两个字符串并检查两个字符串的字符。如果两个字符串具有相同的字符，那么它是命中，因此增加命中的计数。如果字符串的字符在某个位置不匹配，则再次遍历解决方案字符串，查看猜测中的字符是否出现在解决方案字符串的任何位置，如果是，则增加伪命中的计数。
**时间复杂度** : O(N*N)，其中 N 为弦的长度。
一个**高效的解决方案**是创建一个频率数组，存储每个字符在解决方案中出现的次数，不包括该槽被“命中”的次数。然后，我们通过猜测来计算伪命中的数量。
以下是上述方法的实施:

## C++

```
// CPP code to solve RGYB game
#include<iostream>
#include<string>
using namespace std;
int hits = 0;
int pseudoHits = 0;

// maximum no of colors are 4 RGYB
int MAX_COLORS = 4;

// Function to assign code to a slot
// based on the color they have
int codeOfColor(char c)
{
    switch (c)
        {
        case 'B': return 0;
            case 'G': return 1;
            case 'R': return 2;
            case 'Y': return 3;
            default:
            return -1;
        }
}

// Function to calculate number of hits
// and pseudo hits
void calcResult(string guess, string solution)
{
    hits = 0;
    pseudoHits = 0;

    if(guess.length() != solution.length())
        cout<<"Incorrect Input"<<endl;

    // frequency array to store how many times
    // each character occurs in solution string   
    int frequencies[MAX_COLORS] ={ 0 };

    // Compute hits and build frequency table
    for(int i = 0; i < guess.length() ;i++)
    {
        if(guess[i] == solution[i])
        hits++;

        else
        {
            // Only increment the frequency table (which
            // will be  used for pseudo-hits) if it's not
            // a hit. If it's a hit, the slot has already
            // been "used."
            int codecolor = codeOfColor(solution[i]);
            frequencies[codecolor]++;
        }
    }

   // Compute pseudo-hits
    for (int i = 0; i < guess.length(); i++)
        {
            int codecolor = codeOfColor(guess[i]);

            if (codecolor >= 0 && frequencies[codecolor] > 0
                               && guess[i] != solution[i])
            {
                pseudoHits++;
                frequencies[codecolor]--;
            }
        }

    cout << "hits -> " << hits << " Pseudo hits -> "
                       << pseudoHits << endl;
}

// Driver code to test above function
int main()
{
    string solution = "GGRR";
    string guess = "RGBY";

    calcResult(solution, guess);

    solution = "YGRR";
    guess = "RGYB";

    calcResult(solution, guess);
}
// This code is contributed by Sumit Ghosh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to solve RGYB game

import java.util.*;
import java.lang.*;
import java.io.*;

class CalcRes
{
    static int hits = 0;
    static int pseudoHits = 0;

    // Function to assign code to a slot
    // based on the color they have
    static int codeOfColor(char c)
    {
        switch (c)
        {
        case 'B': return 0;
            case 'G': return 1;
            case 'R': return 2;
            case 'Y': return 3;
            default:
            return -1;
        }
    }

    // maximum no of colors are 4 RGYB
    static int MAX_COLORS = 4;

    // Function to calculate number of hits
    // and pseudo hits
    static void calcResult(String guess, String solution)
    {  
        hits = 0;
        pseudoHits = 0;

        if (guess.length() != solution.length())
            System.out.println("Incorrect Input");

        // frequency array to store how many times
        // each character occurs in solution string
        int[] frequencies = new int[MAX_COLORS];

        // Compute hits and build frequency table
        for (int i = 0; i < guess.length(); i++)
        {
            if (guess.charAt(i) == solution.charAt(i))
            {
                hits++;
            }
            else
            {
                /*
                   Only increment the frequency table (which will be
                   used for pseudo-hits) if it's not a hit. If it's a
                   hit, the slot has already been "used."
                */
                int codeofcolor = codeOfColor(solution.charAt(i));
                frequencies[codeofcolor]++;
            }
        }

        // Compute pseudo-hits
        for (int i = 0; i < guess.length(); i++)
        {
            int codeofcolor = codeOfColor(guess.charAt(i));
            if (codeofcolor >= 0 && frequencies[codeofcolor] > 0 &&
                              guess.charAt(i) != solution.charAt(i))
            {
                pseudoHits++;
                frequencies[codeofcolor]--;
            }
        }

        System.out.println("hits -> " + hits +
                           " Pseudo hits -> " + pseudoHits);
    }

    // Driver Code
    public static void main(String[] args)
    {  
        String solution = "GGRR";
        String guess = "RGBY";

        calcResult(solution, guess);

        solution = "YGRR";
        guess = "RGYB";

        calcResult(solution, guess);
    }
}
```

## 计算机编程语言

```
# Python code to solve RGYB game

hits = 0
pseudoHits = 0

# maximum no of colors are 4 RGYB
MAX_COLORS = 4

# Function to assign code to a slot
# based on the color they have
def codeOfColor(c):
    if c == 'B':
        return 0;
    elif c == 'G':
        return 1;
    elif c == 'R':
        return 2;
    elif c == 'Y':
        return 3;
    else:
        return -1;

# Function to calculate number of hits
# and pseudo hits
def calcResult(guess, solution):
    hits = 0
    pseudoHits = 0
    if (len(guess) != len(solution)):
        print "Incorrect Input"

    # frequency array to store how many times
    # each character occurs in solution string   
    frequencies = [0 for i in range(MAX_COLORS)]

    # Compute hits and build frequency table
    for i in range(len(guess)):
        if (guess[i] == solution[i]):
            hits += 1
        else:

            # Only increment the frequency table (which
            # will be  used for pseudo-hits) if it's not
            # a hit. If it's a hit, the slot has already
            # been "used."
            codecolor = codeOfColor(solution[i])
            frequencies[codecolor] += 1

    # Compute pseudo-hits
    for i in range(len(guess)):
        codecolor = codeOfColor(guess[i])
        if codecolor >= 0 and frequencies[codecolor] > 0 and guess[i] != solution[i]:
                pseudoHits += 1
                frequencies[codecolor] -= 1
    print "hits -> ", hits, " Pseudo hits -> ", pseudoHits

# Driver code to test above function
solution = "GGRR"
guess = "RGBY"
calcResult(solution, guess)

solution = "YGRR"
guess = "RGYB"
calcResult(solution, guess)

#This code is contributed by Sachin Bisht
```

## C#

```
// C# code to solve RGYB game
using System;

class GFG {

    static int hits = 0;
    static int pseudoHits = 0;

    // Function to assign code to a slot
    // based on the color they have
    static int codeOfColor(char c)
    {
        switch (c)
        {
            case 'B': return 0;
            case 'G': return 1;
            case 'R': return 2;
            case 'Y': return 3;
            default: return -1;
        }
    }

    // maximum no of colors are 4 RGYB
    static int MAX_COLORS = 4;

    // Function to calculate number of hits
    // and pseudo hits
    static void calcResult(string guess, string solution)
    {
        hits = 0;
        pseudoHits = 0;

        if (guess.Length != solution.Length)
            Console.Write("Incorrect Input");

        // frequency array to store how many
        // times each character occurs in
        // solution string
        int []frequencies = new int[MAX_COLORS];

        // Compute hits and build frequency table
        for (int i = 0; i < guess.Length; i++)
        {
            if (guess[i] == solution[i])
            {
                hits++;
            }
            else
            {

                /* Only increment the frequency table
                (which will be used for pseudo-hits)
                if it's not a hit. If it's a hit, the
                slot has already been "used." */
                int codeofcolor = codeOfColor(solution[i]);
                frequencies[codeofcolor]++;
            }
        }

        // Compute pseudo-hits
        for (int i = 0; i < guess.Length; i++)
        {
            int codeofcolor = codeOfColor(guess[i]);
            if (codeofcolor >= 0 &&
                        frequencies[codeofcolor] > 0 &&
                                guess[i] != solution[i])
            {
                pseudoHits++;
                frequencies[codeofcolor]--;
            }
        }

        Console.WriteLine("hits -> " + hits +
                     " Pseudo hits -> " + pseudoHits);
    }

    // Driver Code
    public static void Main()
    {
        string solution = "GGRR";
        string guess = "RGBY";

        calcResult(solution, guess);

        solution = "YGRR";
        guess = "RGYB";

        calcResult(solution, guess);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// JavaScript code to solve RGYB game

let hits = 0;
let pseudoHits = 0;

// maximum no of colors are 4 RGYB
let MAX_COLORS = 4;

// Function to assign code to a slot
// based on the color they have
function codeOfColor(c) {
    switch (c) {
        case 'B': return 0;
        case 'G': return 1;
        case 'R': return 2;
        case 'Y': return 3;
        default:
            return -1;
    }
}

// Function to calculate number of hits
// and pseudo hits
function calcResult(guess, solution) {
    hits = 0;
    pseudoHits = 0;

    if (guess.length != solution.length)
        document.write("Incorrect Input<br>");

    // frequency array to store how many times
    // each character occurs in solution string   
    let frequencies = new Array(MAX_COLORS).fill(0);

    // Compute hits and build frequency table
    for (let i = 0; i < guess.length; i++) {
        if (guess[i] == solution[i])
            hits++;

        else {
            // Only increment the frequency table (which
            // will be used for pseudo-hits) if it's not
            // a hit. If it's a hit, the slot has already
            // been "used."
            let codecolor = codeOfColor(solution[i]);
            frequencies[codecolor]++;
        }
    }

    // Compute pseudo-hits
    for (let i = 0; i < guess.length; i++) {
        let codecolor = codeOfColor(guess[i]);

        if (codecolor >= 0 && frequencies[codecolor] > 0
            && guess[i] != solution[i]) {
            pseudoHits++;
            frequencies[codecolor]--;
        }
    }

    document.write("hits -> " + hits + " Pseudo hits -> "
        + pseudoHits + "<br>");
}

// Driver code to test above function

let solution = "GGRR";
let guess = "RGBY";

calcResult(solution, guess);

solution = "YGRR";
guess = "RGYB";

calcResult(solution, guess);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
hits -> 1 Pseudo hits -> 1
hits -> 1 Pseudo hits -> 2
```

**时间复杂度**:O(N)
T3】辅助空间 : O(N)
本文由**Somesh Awasthi 先生**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。