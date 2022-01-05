# 洗牌问题| TCS 数字高级编码问题

> 原文:[https://www . geesforgeks . org/card-shuffle-problem-TCS-digital-advanced-coding-question/](https://www.geeksforgeeks.org/card-shuffle-problem-tcs-digital-advanced-coding-question/)

你有 100 张牌，从 1 到 100。你把它们分成 k 堆，然后按顺序收集回来。例如，如果您将它们分成 4 堆，那么第一堆将包含编号为 1、5、9、…的卡片，第四堆将包含编号为 4、8、12、…在收集您首先收集的卡片时，将最后一堆从下往上翻，然后拿起第三堆，从下往上翻，将卡片放在第四堆的上面，以此类推。下一轮，你将牌分发到另一组牌堆中，并以同样的方式收集(最后一堆先，第一堆后)。

如果我们有 10 张牌，并把它们分成 2 堆，牌堆中的牌的顺序(从上到下)将是 9、7、5、3、1 和 10、8、6、4、2
我们翻转牌堆，得到顺序 1、3、5、7、9 和 2、4、6、8、10
我们把第二堆放在底部，第一堆放在顶部，得到一副牌 1、3、5、7、9、2、4， 6、8、10
给定回合数(m)，每回合的桩数(ki)，你需要写一个程序，在最后一轮结束时从顶部找到第 n 张牌。

**输入:**一个数组**arr【】**代表每轮的桩数。
**输出:**一个整数，代表所有回合打完之后的**第 n 张**牌。

**约束条件:**回合数≤ 10，每回合桩数≤ 13。

**示例:**

> **输入:** arr[] = {2，2}，N = 4
> **输出:** 13
> 我们还有两回合。第一轮有两堆。
> 回合结束时，副牌的顺序为:1、3、5、…、99、2、4、6、…、100
> 下一回合也有 2 堆，第二轮后，牌的顺序为 1、5、9、13、…
> 从上往下的第四张牌有 13 号。
> 
> **输入:** arr[] = {2，2，3，8}，N = 18
> T3】输出: 100

**方法:**每轮为每堆创建空的[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)，然后按照问题中的描述在这些列表中插入号码(卡号)，然后在每轮后更新原始的卡号列表。最后一轮结束时，打印原始(更新)列表中的第 n 个整数。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

    // Total cards
    static final int CARDS = 100;

    // Function to perform the current round
    static void currentRound(List<Integer> list, int totalPiles)
    {

        // Create the required empty piles
        List<List<Integer> > piles = new ArrayList<>();
        for (int i = 0; i < totalPiles; i++)
            piles.add(new ArrayList<Integer>());

        // Add cards to the piles one by one
        int j = 0;
        for (int i = 0; i < CARDS; i++) {
            piles.get(j).add(list.get(i));
            j = (j + 1) % totalPiles;
        }

        // After all the piles have been reversed
        // the new order will be first card of the
        // first pile, second card of the first
        // pile, ..., last pile of the last pile
        // (from top to bottom)
        int pileNo = 0, i = 0;
        j = 0;
        while (i < CARDS) {
            list.set(i, piles.get(pileNo).get(j));
            j++;
            if (j >= piles.get(pileNo).size()) {
                pileNo++;
                j = 0;
            }
            i++;
        }
    }

    // Function to perform all the rounds
    static int performRounds(int piles[], int rounds, int n)
    {

        // Create the initial list with all the cards
        List<Integer> list = new ArrayList<>();
        for (int i = 1; i <= CARDS; i++)
            list.add(i);

        // Perform all the rounds
        for (int i = 0; i < rounds; i++)
            currentRound(list, piles[i]);

        // Return the nth card
        return list.get(n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int piles[] = { 2, 2 };
        int rounds = piles.length;
        int n = 4;

        // nth card will be at (n - 1)th index
        n--;
        System.out.print(performRounds(piles, rounds, n));
    }
}
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;             

class GFG 
{

    // Total cards
    static int CARDS = 100;

    // Function to perform the current round
    static void currentRound(List<int> list, 
                                  int totalPiles)
    {
        int i;

        // Create the required empty piles
        List<List<int> > piles = new List<List<int>>();
        for (i = 0; i < totalPiles; i++)
            piles.Add(new List<int>());

        // Add cards to the piles one by one
        int j = 0;
        for (i = 0; i < CARDS; i++) 
        {
            piles[j].Add(list[i]);
            j = (j + 1) % totalPiles;
        }

        // After all the piles have been reversed
        // the new order will be first card of the
        // first pile, second card of the first
        // pile, ..., last pile of the last pile
        // (from top to bottom)
        int pileNo = 0; i = 0;
        j = 0;
        while (i < CARDS)
        {
            list.Insert(i, piles[pileNo][j]);
            j++;
            if (j >= piles[pileNo].Count) 
            {
                pileNo++;
                j = 0;
            }
            i++;
        }
    }

    // Function to perform all the rounds
    static int performRounds(int []piles, 
                             int rounds, int n)
    {

        // Create the initial list with all the cards
        List<int> list = new List<int>();
        for (int i = 1; i <= CARDS; i++)
            list.Add(i);

        // Perform all the rounds
        for (int i = 0; i < rounds; i++)
            currentRound(list, piles[i]);

        // Return the nth card
        return list[n];
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []piles = { 2, 2 };
        int rounds = piles.Length;
        int n = 4;

        // nth card will be at (n - 1)th index
        n--;
        Console.WriteLine(performRounds(piles, rounds, n));
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
13

```