# 确定从字符串中删除字符的游戏的获胜者

> 原文：[https://www.geeksforgeeks.org/determine-the-winner-of-a-game-of-deleting-characters-from-a-string/](https://www.geeksforgeeks.org/determine-the-winner-of-a-game-of-deleting-characters-from-a-string/)

在给定数字字符串 **str** 的情况下，任务是确定当两个玩家根据给定条件使用该字符串以最佳方式玩游戏时，确定游戏的赢家：

*   玩家 1 总是最先开始。

*   一轮回合中，一个玩家可以从字符串中删除连续的元素，并且删除的元素数量将总计为他的分数。 播放器 1 将删除奇数个连续元素，而播放器 1 将删除偶数个连续元素。

*   任何无法采取行动的玩家都会输掉比赛。

*   删除所有字符串后，得分最高的玩家将赢得比赛，如果得分相等，则打印 -1。

**示例**：

> **输入**：`str = "7788"`
>
> **输出**：-1
>
> **说明**：
>
> 播放器 1 的第一个动作是删除 77，然后 玩家 2 的得分为 88。两者的得分均为 2。因此为 -1。
> 
> **输入**：`str = "8822"`
>
> **输出**：`Player 2`
>
> **说明**：
>
> 没有奇数元素，因此玩家 1 不能移动，因此玩家 2 获胜。

**方法**：请按照以下步骤解决问题：

1.  创建大小为 10 的数组`A[]`，以存储给定字符串中所有数字的频率。

2.  迭代给定的字符串，并更新上述数组中每个数字的频率。

3.  遍历数组`A[]`并采用两个变量，例如`sum1 = 0`和`sum2 = 0`，以存储分数总和。

4.  如果索引为奇数，即玩家 1 回合，则递增`sum1`；否则，如果索引为偶数，即玩家 2 回合，则递增`sum2`。

5.  完成上述步骤后，检查`sum1`是否等于`sum2`，然后打印 **-1**，否则打印根据得分赢得比赛的玩家编号。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the winner of the 
// game when both players play optimally 
void determineWinner(string str) 
{ 
    // Stores the frequency of all digit 
    vector<int> A(10); 

    // Stores the scores of player1 
    // and player2 respectively 
    int sum1 = 0, sum2 = 0; 

    // Iterate to store frequencies 
    for (int i = 0; i < str.length(); i++) { 
        A[int(str[i]) - 48]++; 
    } 

    for (int i = 0; i <= 9; i++) { 

        // Turn for the player1 
        if (i % 2 != 0) { 

            // Add score of player1 
            sum1 = sum1 + A[i]; 
        } 
        else { 

            // Add score of player2 
            sum2 = sum2 + A[i]; 
        } 
    } 

    // Check if its a draw 
    if (sum1 == sum2) { 
        cout << "-1"; 
    } 

    // If score of player 1 is greater 
    else if (sum1 > sum2) { 
        cout << "Player 1"; 
    } 

    // Otherwise 
    else { 
        cout << "Player 2"; 
    } 
} 

// Driver Code 
int main() 
{ 
    string str = "78787"; 
    determineWinner(str); 
    return 0; 
} 

```

## Java

```java

// Java program for the above approach  
import java.util.*; 

class GFG{ 

// Function to find the winner of the 
// game when both players play optimally 
static void determineWinner(String str) 
{ 

    // Stores the frequency of all digit 
    int[] A = new int[10]; 

    // Stores the scores of player1 
    // and player2 respectively 
    int sum1 = 0, sum2 = 0; 

    // Iterate to store frequencies 
    for(int i = 0; i < str.length(); i++) 
    { 
        A[(int)str.charAt(i) - 48]++; 
    } 

    for(int i = 0; i <= 9; i++) 
    { 

        // Turn for the player1 
        if (i % 2 != 0)  
        { 

            // Add score of player1 
            sum1 = sum1 + A[i]; 
        } 
        else
        { 

            // Add score of player2 
            sum2 = sum2 + A[i]; 
        } 
    } 

    // Check if its a draw 
    if (sum1 == sum2)  
    { 
        System.out.print("-1"); 
    } 

    // If score of player 1 is greater 
    else if (sum1 > sum2) 
    { 
        System.out.print("Player 1"); 
    } 

    // Otherwise 
    else 
    { 
        System.out.print("Player 2"); 
    } 
} 

// Driver code 
public static void main (String[] args) 
{ 
    String str = "78787"; 

    determineWinner(str); 
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program for the above approach  

# Function to find the winner of the 
# game when both players play optimally 
def determineWinner(str): 

    # Stores the frequency of all digit 
    A = [0 for i in range(9)]; 

    # Stores the scores of player1 
    # and player2 respectively 
    sum1 = 0; sum2 = 0; 

    # Iterate to store frequencies 
    for i in range(0, len(str)): 
        A[int(str[i])] += 1; 

    for i in range(0, 9): 

        # Turn for the player1 
        if (i % 2 != 0): 

            # Add score of player1 
            sum1 = sum1 + A[i]; 
        else: 

            # Add score of player2 
            sum2 = sum2 + A[i]; 

    # Check if its a draw 
    if (sum1 == sum2): 
        print("-1"); 

    # If score of player 1 is greater 
    elif(sum1 > sum2): 
        print("Player 1"); 

    # Otherwise 
    else: 
        print("Player 2"); 

# Driver code 
if __name__ == '__main__': 

    str = "78787"; 

    determineWinner(str); 

# This code is contributed by Amit Katiyar  

```

## C#

```cs

// C# program for the above approach  
using System; 
class GFG{ 

// Function to find the winner of the 
// game when both players play optimally 
static void determineWinner(String str) 
{ 

    // Stores the frequency of all digit 
    int[] A = new int[10]; 

    // Stores the scores of player1 
    // and player2 respectively 
    int sum1 = 0, sum2 = 0; 

    // Iterate to store frequencies 
    for(int i = 0; i < str.Length; i++) 
    { 
        A[(int)str[i] - 48]++; 
    } 

    for(int i = 0; i <= 9; i++) 
    { 

        // Turn for the player1 
        if (i % 2 != 0)  
        { 

            // Add score of player1 
            sum1 = sum1 + A[i]; 
        } 
        else
        { 

            // Add score of player2 
            sum2 = sum2 + A[i]; 
        } 
    } 

    // Check if its a draw 
    if (sum1 == sum2)  
    { 
        Console.Write("-1"); 
    } 

    // If score of player 1 is greater 
    else if (sum1 > sum2) 
    { 
        Console.Write("Player 1"); 
    } 

    // Otherwise 
    else 
    { 
        Console.Write("Player 2"); 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    String str = "78787"; 

    determineWinner(str); 
} 
} 

// This code is contributed by Rohit_ranjan

```

**输出**： 

```
Player 1

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



