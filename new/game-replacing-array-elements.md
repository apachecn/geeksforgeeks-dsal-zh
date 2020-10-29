# 替换数组元素的游戏

> 原文：[https://www.geeksforgeeks.org/game-replacing-array-elements/](https://www.geeksforgeeks.org/game-replacing-array-elements/)

有两个玩家 A 和 B 对玩数字游戏感兴趣。 玩家在每一步中选择两个不同的数字，例如 *a1* 和 *a2* ，然后将所有 *a2* 替换为 *a1* 或 *a1* 来自 *a2* 。 如果他们中的任何一个无法选择两个数字，而他们又无法选择一个数组中的两个不同的数字，则他们停止游戏。 第一玩家总是先移动，然后再移动。 任务是找到哪个玩家获胜。

例子：

```
Input :  arr[] = { 1, 3, 3, 2,, 2, 1 }
Output : Player 2 wins
Explanation:
First plays always looses irrespective
of the numbers chosen by him. For example,
say first player picks ( 1 & 3) 
replace all 3 by 1  
Now array Become { 1, 1, 1, 2, 2, 1 }
Then second player picks ( 1  2 )
either he replace 1 by 2 or 2 by 1 
Array Become { 1, 1, 1, 1, 1, 1 }
Now first player is not able to choose.

Input  : arr[] = { 1, 2, 1, 2 }
Output : Player 1 wins

```

从上面的示例中，我们可以观察到，如果不同元素的数量为偶数，则第一个玩家总是获胜。 其他第二名获胜。

让我们再举一个例子：

```
  int arr[] =  1, 2, 3, 4, 5, 6 
```

此处，不同元素的数量为偶数（n）。 如果玩家 1 选择任意两个数字，说（4，1），那么我们剩下 n-1 个不同的元素。 因此，玩家以 n-1 个不同的元素排在第二位。 进行此操作直到不同的元素变为 1。这里 **n = 6**

```
Player   :  P1    p2    P1   p2    P1     P2    
distinct : [n, n-1, n-2, n-3, n-4, n-5 ]  

"At this point no distinct element left, 
so p2 is unable to pick two Dis element."
```

以下想法的实现：

## C++

```cpp

// CPP program for Game of Replacement 
#include <bits/stdc++.h> 
using namespace std; 

// Function return which player win the game 
int playGame(int arr[], int n) 
{ 
    // Create hash that will stores 
    // all distinct element 
    unordered_set<int> hash; 

    // Traverse an array element 
    for (int i = 0; i < n; i++) 
        hash.insert(arr[i]); 

    return (hash.size() % 2 == 0 ? 1 : 2); 
} 

// Driver Function 
int main() 
{ 
    int arr[] = { 1, 1, 2, 2, 2, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << "Player " << playGame(arr, n) << " Wins" << endl; 
    return 0; 
} 

```

## Java

```java

// Java program for Game of Replacement  
import java.util.HashSet; 
public class GameOfReplacingArrayElements  
{ 
    // Function return which player win the game  
    public static int playGame(int arr[]) 
    { 
        // Create hash that will stores  
        // all distinct element  
        HashSet<Integer> set=new HashSet<>(); 

        // Traverse an array element  
        for(int i:arr) 
            set.add(i); 
        return (set.size()%2==0)?1:2; 
    } 

    public static void main(String args[]) { 
        int arr[] = { 1, 1, 2, 2, 2, 2 };  
        System.out.print("Player "+playGame(arr)+" wins"); 
    } 
} 
//This code is contributed by Gaurav Tiwari 

```

## Python3

```py

# Python program for Game of Replacement  

# Function return which player win the game  
def playGame(arr, n): 

    # Create hash that will stores  
    # all distinct element  
    s = set() 

    # Traverse an array element  
    for i in range(n): 
        s.add(arr[i]) 
    return 1 if len(s) % 2 == 0 else 2

# Driver code 
arr = [1, 1, 2, 2, 2, 2] 
n = len(arr) 
print("Player",playGame(arr, n),"Wins") 

# This code is contributed by Shrikant13 

```

## C#

```cs

// C# program for Game of Replacement  
using System; 
using System.Collections.Generic; 

public class GameOfReplacingArrayElements  
{ 
    // Function return which player win the game  
    public static int playGame(int []arr) 
    { 
        // Create hash that will stores  
        // all distinct element  
        HashSet<int> set = new HashSet<int>(); 

        // Traverse an array element  
        foreach(int i in arr) 
            set.Add(i); 
        return (set.Count % 2 == 0) ? 1 : 2; 
    } 

    // Driver code 
    public static void Main(String []args) 
    { 
        int []arr = { 1, 1, 2, 2, 2, 2 };  
        Console.Write("Player " + playGame(arr) + " wins"); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Player 1 Wins

```

**时间复杂度**：`O(n)`



* * *

* * *



