# 洗牌并回答查询

> 原文:[https://www . geesforgeks . org/shuffle-pack-cards-answer-query/](https://www.geeksforgeeks.org/shuffle-pack-cards-answer-query/)

给定一包 2^N 牌(0…2^n–1)，分 n 步洗牌。在步骤 k(0)< k < N) we divide the deck into 2k equal-sized decks. Each one of those decks is reordered by having all the cards that lie on even positions first, followed by all cards that lie on odd positions (the order is preserved in each one of the two subsequences). Now, we are given a key (index). We have to answer the card on that position (0-based indexing).
示例:

```
Input : N = 3 (Size = 2^N), Key = 3
Output : 6
Explanation : 
Pack :      0 1 2 3 4 5 6 7
Shuffle 1 : 0 2 4 6|1 3 5 7
Shuffle 2 : 0 4|2 6|1 5|3 7
Card at index 3 : 6
```

**方法一:**我们可以简单的模拟整个过程，在 N 次洗牌全部完成后，找出牌的确切顺序。
时间复杂度:O(N * 2^N)
**方法二:**
让我们试着找到关键和最终答案的二进制表示，并尝试在此基础上发现一些观察值。
让 N = 3
下表:
Key ANS
000 000
001 100
010 010
011 110
100 001
101 101
110 011
111 111
很明显，答案是 Key 的二进制表示的反义词。

## C++

```
// C++ program to find the card at given index
// after N shuffles
#include <bits/stdc++.h>
using namespace std;

// function to find card at given index
void shuffle(int N, int key)
{

    // Answer will be reversal of N bits from MSB
    unsigned int NO_OF_BITS = N;
    unsigned int reverse_num = 0, temp;

    // Calculating the reverse binary representation
    for (int i = 0; i < NO_OF_BITS; i++) {
        temp = (key & (1 << i));
        if (temp)
            reverse_num |= (1 << ((NO_OF_BITS - 1) - i));
    }

    // Printing the result
    cout << reverse_num;
}

// driver code
int main()
{
    // No. of Shuffle Steps
    int N = 3;

    // Key position
    unsigned int key = 3;

    shuffle(N, key);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the card at given index
// after N shuffles
class GFG {

    // function to find card at given index
    static void shuffle(int N, int key)
    {

        // Answer will be reversal of N bits from MSB
        int NO_OF_BITS = N;
        int reverse_num = 0, temp;

        // Calculating the reverse binary representation
        for (int i = 0; i < NO_OF_BITS; i++) {
            temp = (key & (1 << i));
            if (temp>0)
                reverse_num |= (1 << ((NO_OF_BITS - 1) - i));
        }

        // Printing the result
        System.out.print(reverse_num);
    }

    //Driver code
    public static void main (String[] args)
    {

        // No. of Shuffle Steps
        int N = 3;

        // Key position
        int key = 3;

        shuffle(N, key);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find the card
# at given index after N shuffles

# Function to find card at given index
def shuffle(N, key):

    # Answer will be reversal
    # of N bits from MSB
    NO_OF_BITS = N
    reverse_num = 0

    # Calculating the reverse binary representation
    for i in range(NO_OF_BITS):
        temp = (key & (1 << i))
        if (temp):
            reverse_num |= (1 << ((NO_OF_BITS - 1) - i))

    # Printing the result
    print(reverse_num)

# Driver code

# No. of Shuffle Steps
N = 3

# Key position
key = 3
shuffle(N, key)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find the card at given index
// after N shuffles
using System;

class GFG {

    // function to find card at given index
    static void shuffle(int N, int key)
    {

        // Answer will be reversal of N bits from MSB
        int NO_OF_BITS = N;
        int reverse_num = 0, temp;

        // Calculating the reverse binary representation
        for (int i = 0; i < NO_OF_BITS; i++) {
            temp = (key & (1 << i));
            if (temp > 0)
                reverse_num |= (1 << ((NO_OF_BITS - 1) - i));
        }

        // Printing the result
        Console.Write(reverse_num);
    }

    //Driver code
    public static void Main()
    {

        // No. of Shuffle Steps
        int N = 3;

        // Key position
        int key = 3;

        shuffle(N, key);
    }
}

// This code is contributed by Anant Agarwal.
```

## java 描述语言

```
<script>

// Javascript program to find the card at given index
// after N shuffles

    // function to find card at given index
    function shuffle(N, key)
    {

        // Answer will be reversal of N bits from MSB
        let NO_OF_BITS = N;
        let reverse_num = 0, temp;

        // Calculating the reverse binary representation
        for (let i = 0; i < NO_OF_BITS; i++) {
            temp = (key & (1 << i));
            if (temp>0)
                reverse_num |= (1 << ((NO_OF_BITS - 1) - i));
        }

        // Printing the result
        document.write(reverse_num);
    }

// driver program

        // No. of Shuffle Steps
        let N = 3;

        // Key position
        let key = 3;

        shuffle(N, key);

</script>
```

**输出:**

```
6
```

本文由**罗希特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。