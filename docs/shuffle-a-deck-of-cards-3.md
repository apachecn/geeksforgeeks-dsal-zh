# 洗牌

> 原文:[https://www.geeksforgeeks.org/shuffle-a-deck-of-cards-3/](https://www.geeksforgeeks.org/shuffle-a-deck-of-cards-3/)

给定一副牌，任务是洗牌。

在[亚马逊采访](https://www.geeksforgeeks.org/amazon-interview-experience-set-145-campus/)中问道

先决条件:[洗牌给定的数组](https://www.geeksforgeeks.org/shuffle-a-given-array/)

**算法:**

```
1\. First, fill the array with the values in order.
2\. Go through the array and exchange each element 
   with the randomly chosen element in the range 
   from itself to the end.

// It is possible that an element will be swap
// with itself, but there is no problem with that. 

```

## C++

```
// C++ program for shuffling desk of cards.
#include <bits/stdc++.h>
using namespace std;

// Function which shuffle and print the array
void shuffle(int card[], int n)
{
    // Initialize seed randomly
    srand(time(0));

    for (int i=0; i<n ;i++)
    {
        // Random for remaining positions.
        int r = i + (rand() % (52 -i));

        swap(card[i], card[r]);
    }
}

// Driver code
int main()
{
    // Array from 0 to 51
    int a[] = {0, 1, 2, 3, 4, 5, 6, 7, 8,
               9, 10, 11, 12, 13, 14, 15,
               16, 17, 18, 19, 20, 21, 22,
               23, 24, 25, 26, 27, 28, 29,
               30, 31, 32, 33, 34, 35, 36,
               37, 38, 39, 40, 41, 42, 43,
               44, 45, 46, 47, 48, 49, 50,
               51};

    shuffle(a, 52);

    // Printing all shuffled elements of cards
    for (int i=0; i<52; i++)
        cout << a[i] << " ";
    cout << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for Shuffle a deck of cards
import java.util.Random;

class GFG {

    // Function which shuffle and print the array
    public static void shuffle(int card[], int n)
    {

        Random rand = new Random();

        for (int i = 0; i < n; i++)
        {
            // Random for remaining positions.
            int r = i + rand.nextInt(52 - i);

             //swapping the elements
             int temp = card[r];
             card[r] = card[i];
             card[i] = temp;

        }
    }

    // Driver code
    public static void main(String[] args) 
    {
        // Array from 0 to 51
        int a[] = {0, 1, 2, 3, 4, 5, 6, 7, 8,
                   9, 10, 11, 12, 13, 14, 15,
                   16, 17, 18, 19, 20, 21, 22,
                   23, 24, 25, 26, 27, 28, 29,
                   30, 31, 32, 33, 34, 35, 36,
                   37, 38, 39, 40, 41, 42, 43,
                   44, 45, 46, 47, 48, 49, 50, 
                   51};

        shuffle(a, 52);

        // Printing all shuffled elements of cards
        for (int i = 0; i < 52; i ++)
           System.out.print(a[i]+" ");

    }
}
// This code is contributed by Arnav Kr. Mandal
```

## 蟒蛇 3

```
# Python3 program for shuffling desk of cards
# Function which shuffle and print the array 

import random
def shuffle(card,n) :

    # Initialize seed randomly
    for i in range(n):

        # Random for remaining positions.
        r = i + (random.randint(0,55) % (52 -i))
        tmp=card[i]
        card[i]=card[r]
        card[r]=tmp
#Driver code
if __name__=='__main__':
    a=[0, 1, 2, 3, 4, 5, 6, 7, 8,
       9, 10, 11, 12, 13, 14, 15,
       16, 17, 18, 19, 20, 21, 22, 
       23, 24, 25, 26, 27, 28, 29,
       30, 31, 32, 33, 34, 35, 36,
       37, 38, 39, 40, 41, 42, 43, 
       44, 45, 46, 47, 48, 49, 50,
       51]
    shuffle(a,52)
    print(a)

#this code is contributed by sahilshelangia
```

## C#

```
// C# Code for Shuffle a deck of cards
using System;

class GFG {

    // Function which shuffle and 
    // print the array
    public static void shuffle(int []card, 
                               int n)
    {

        Random rand = new Random();

        for (int i = 0; i < n; i++)
        {

            // Random for remaining positions.
            int r = i + rand.Next(52 - i);

            //swapping the elements
            int temp = card[r];
            card[r] = card[i];
            card[i] = temp;

        }
    }

    // Driver code
    public static void Main() 
    {
        // Array from 0 to 51
        int []a = {0, 1, 2, 3, 4, 5, 6, 7, 8,
                   9, 10, 11, 12, 13, 14, 15,
                   16, 17, 18, 19, 20, 21, 22,
                   23, 24, 25, 26, 27, 28, 29,
                   30, 31, 32, 33, 34, 35, 36,
                   37, 38, 39, 40, 41, 42, 43,
                   44, 45, 46, 47, 48, 49, 50, 
                   51};

        shuffle(a, 52);

        // Printing all shuffled elements of cards
        for (int i = 0; i < 52; i ++)
        Console.Write(a[i]+" ");

    }
}

// This code is contributed by Nitin Mittal.
```

Output:

```
29 27 20 23 26 21 35 51 15 18 46 32 33 19 
24 30 3 45 40 34 16 11 36 50 17 10 7 5 4 
39 6 47 38 28 13 44 49 1 8 42 43 48 0 12 
37 41 25 2 31 14 22

```

**注意:**由于程序中使用的随机函数，每次输出都会有所不同。
详见[洗牌给定数组](https://www.geeksforgeeks.org/shuffle-a-given-array/)。

本文由 **[萨赫勒拉吉普特](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。