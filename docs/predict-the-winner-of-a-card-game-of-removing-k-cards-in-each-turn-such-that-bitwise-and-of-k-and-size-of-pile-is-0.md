# 预测每回合移除 K 张牌的卡牌游戏的赢家，使得 K 与牌堆大小的位与为 0

> 原文:[https://www . geeksforgeeks . org/predict-每回合移除 k 张牌游戏的赢家，即 k 位和牌堆大小为 0/](https://www.geeksforgeeks.org/predict-the-winner-of-a-card-game-of-removing-k-cards-in-each-turn-such-that-bitwise-and-of-k-and-size-of-pile-is-0/)

有两个玩家 **A** 和 **B** 和一堆 **N** 牌叠在一起。任务是找到游戏的赢家，假设两个玩家都按照以下指导方针进行最佳游戏:

*   玩家 **A** 总是开始游戏，随后玩家轮流。
*   在每一回合中，如果 **K & n** = 0，玩家可以移除 **K** ( 1 ≤ K ≤ N)张牌，其中 **n** 是当前牌堆的大小。
*   如果一个玩家在游戏中的任何一点都不能移动，那么这个玩家就输了，游戏就结束了。

**示例:**

> **输入:** N = 1
> **输出:** B
> **说明:**
> A 只能移除 1 张牌，但 1 & 1 = 1，所以 A 无法移动。
> 于是，乙赢了比赛。
> 
> **输入:** N = 4
> **输出:** A
> **说明:**
> A 将移除 3 张牌作为 3 & 4 = 0，现在只剩下 1 张牌，B 无法移动。
> 于是，甲赢了比赛。

**进场:**这个想法是基于这样的观察:如果 **N** 的二进制表示中 **1s** 的[计数在遇到一个 **0** 之前是奇数，那么 **A** 赢得比赛。如果整个二进制字符串中不存在 **1s** 和 **0s** 的组合，则 **B** 获胜。按照以下步骤解决问题:](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)

*   初始化一个变量 **countOne** 来存储 **1** 的计数。
*   将 **N** 转换为其[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)并存储在一个字符串中， **binString** 。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **binString** 并执行以下操作:
    *   如果遇到“ **1** ，增加**计数**。
    *   如果遇到“ **0** ”，检查 **countOne** 是奇数还是偶数，如果 **countOne** 是奇数 **A** 获胜，[破环](https://www.geeksforgeeks.org/break-statement-cc/)，否则将 **countOne** 复位为**0**[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)穿越。
*   如果整条线穿越而不断裂，则 **B** 获胜。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the winner of the
// game if both player plays optimally
void findWinner(int N)
{

    // Stores the count of 1s
    int onesBeforeZero = 0;
    int flag = 1;

    // Convert N to binary representation
    int binString[32];

    int i = 0;

    while (N > 0)
    {

        // Storing remainder in binary array
        binString[i] = N % 2;
        N = N / 2;
        i++;
    }

    int l = sizeof(binString) /
            sizeof(binString[0]);

    // Traverse the binary string
    for(int j = 0; j < l; j++)
    {

        // If 1 is encountered,
        // increment count of 1s
        if (binString[j] == 1)
        {
            onesBeforeZero += 1;
        }

        // If 0 is encountered, check
        // if count of 1s is odd
        else
        {

            // If count of 1s is odd,
            // then winner is A
            if (onesBeforeZero & 1)
            {
                cout << "A";
                flag = 0;
                break;
            }

            // If count of 1s is even,
            // reset it to 0
            else
                onesBeforeZero = 0;
        }    
    }

    // If entire loop is traversed
    // without breaking, then
    // B is the winner
    if (flag == 1)
        cout << "B";
}

// Driver Code
int main()
{
    int N = 4;

    // Function Call
    findWinner(N);

    return 0;
}

// This code is contributed by jana_sayantan
```

## C

```
// C program for the above approach
#include <stdio.h>

// Function to find the winner of the
// game if both player plays optimally
void findWinner(unsigned long long N)
{
    // Stores the count of 1s
    int onesBeforeZero = 0;
    int flag = 1, j = 0;
    char binString[32];

    // Converting N into a binary string
    for(int i = 31; i >= 0; i--)
    {
        unsigned long long temp = N >> i;

        if (temp & 1)
            binString[j] = '1';
        else
            binString[j] = '0';

        j += 1;
    }

    // Traverse the binary string
    for(int i = 0; i < 32; i++)
    {
        if (binString[i] == '1')

            // If 1 is encountered
            // increment ones count
            onesBeforeZero += 1;
        else
        {

            // If 0 is encountered check
            // if ones count is odd
            if (onesBeforeZero & 1)
            {

                // If ones count is odd
                // winner is A break
                printf("A");
                flag = 0;
                break;
            }
            else
                // If ones count is even
                // reset it to 0 and continue
                onesBeforeZero = 0;
        }
    }

    // If entire loop is traversed
    // without breaking, then
    // B is the winner
    if (flag == 1)
        printf("B");
}   

// Driver code
int main()
{
    unsigned long long N = 4;

    // Function Call
    findWinner(N);

    return 0;
}

// This code is contributed by Praneeth Kapila
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the winner
static void findWinner(long N)
{
    // Stores the count of 1s
    int onesBeforeZero = 0, flag = 1, j = 0;

    String[] binString = new String[32];

    // Converting N into a binary string
    for(int i = 31; i >= 0; i--)
    {
        long temp = N >> i;

        if ((temp & 1) == 1)
            binString[j] = "1";
        else
            binString[j] = "0";

        j += 1;
    }

    for(int i = 0; i < 32; i++)
    {
        if (binString[i] == "1")

            // If 1 is encountered
            // increment ones count
            onesBeforeZero += 1;
        else
        {

            // If 0 is encountered check
            //if ones count is odd
            if ((onesBeforeZero & 1) == 1)
            {

                // If ones count is odd winner
                // is A break
                System.out.println("A");
                flag = 0;
                break;
            }
            else
                // If ones count is even
                // reset it to 0 and continue
                onesBeforeZero = 0;
        }
    }

    // If entire loop is traversed
    // without breaking, then
    // B is the winner
    if (flag == 1)
        System.out.println("B");
}

// Driver code
public static void main(String[] args)
{
    long N = 4;

    // Function Call
    findWinner(N);
}
}

// This code is contributed by Praneeth Kapila
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the winner of the
# game if both player plays optimally
def findWinner(N):

    # Stores the count of 1s
    onesBeforeZero = 0
    flag = 1

    # Convert N to binary representation
    binString = bin(N).replace("0b", "")

    l = len(binString)

    # Traverse the binary string
    for j in range(l):

        # If 1 is encountered,
        # increment count of 1s
        if binString[j] == '1':
            onesBeforeZero += 1

        # If 0 is encountered, check
        # if count of 1s is odd
        else:

            # If count of 1s is odd,
            # then winner is A
            if onesBeforeZero & 1:
                print("A")
                flag = 0
                break

            # If count of 1s is even,
            # reset it to 0
            else:
                onesBeforeZero = 0

    # If entire loop is traversed
    # without breaking, then
    # B is the winner
    if flag == 1:
        print("B")

# Driver Code
N = 4

# Function Call
findWinner(N)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the winner
static void findWinner(long N)
{

    // Stores the count of 1s
    int onesBeforeZero = 0, flag = 1, j = 0;

    String[] binString = new String[32];

    // Converting N into a binary string
    for(int i = 31; i >= 0; i--)
    {
        long temp = N >> i;

        if ((temp & 1) == 1)
            binString[j] = "1";
        else
            binString[j] = "0";

        j += 1;
    }

    for(int i = 0; i < 32; i++)
    {
        if (binString[i] == "1")

            // If 1 is encountered
            // increment ones count
            onesBeforeZero += 1;
        else
        {

            // If 0 is encountered check
            //if ones count is odd
            if ((onesBeforeZero & 1) == 1)
            {

                // If ones count is odd winner
                // is A break
                Console.WriteLine("A");
                flag = 0;
                break;
            }
            else

                // If ones count is even
                // reset it to 0 and continue
                onesBeforeZero = 0;
        }
    }

    // If entire loop is traversed
    // without breaking, then
    // B is the winner
    if (flag == 1)
        Console.WriteLine("B");
}

// Driver code
public static void Main(String[] args)
{
    long N = 4;

    // Function Call
    findWinner(N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the winner
function findWinner(N)
{

    // Stores the count of 1s
    let onesBeforeZero = 0, flag = 1, j = 0;

    let binString = [];

    // Converting N into a binary string
    for(let i = 31; i >= 0; i--)
    {
        let temp = N >> i;

        if ((temp & 1) == 1)
            binString[j] = "1";
        else
            binString[j] = "0";

        j += 1;
    }

    for(let i = 0; i < 32; i++)
    {
        if (binString[i] == "1")

            // If 1 is encountered
            // increment ones count
            onesBeforeZero += 1;
        else
        {

            // If 0 is encountered check
            //if ones count is odd
            if ((onesBeforeZero & 1) == 1)
            {

                // If ones count is odd winner
                // is A break
                document.write("A");
                flag = 0;
                break;
            }
            else

                // If ones count is even
                // reset it to 0 and continue
                onesBeforeZero = 0;
        }
    }

    // If entire loop is traversed
    // without breaking, then
    // B is the winner
    if (flag == 1)
        document.write("B");
}

// Driver code
let N = 4;

// Function Call
findWinner(N);

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
A
```

***时间复杂度:** O(log N)*
***辅助空间:** O(log N)*