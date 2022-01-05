# 两人游戏，其中一名玩家可以移除所有出现的数字

> 原文:[https://www . geeksforgeeks . org/两人游戏，其中一名玩家可以移除所有出现的数字/](https://www.geeksforgeeks.org/two-player-game-in-which-a-player-can-remove-all-occurrences-of-a-number/)

两个玩家**玩家 1** 和**玩家 2**在给定的数字序列 **S** 上玩游戏，其中**玩家 1** 首先开始，两个玩家都以最佳状态玩游戏。任务是发现**玩家 1** 是赢还是输。如果他赢了，打印“是”，否则打印“否”。
游戏规则如下:

*   玩家的交替回合。
*   在每一回合中，当前玩家必须选择当前序列 S 的一个或多个元素，使得所有选择的元素的值都相同，并从 S 中擦除这些元素。
*   当一个玩家不能选择任何东西(序列 S 已经是空的)时，这个玩家就输了。

**示例:**

> **输入:** S = {2，1，2，2}
> **输出:**是
> **说明:**
> 第一个玩家可以选择指数为{0，3} {0，2}或{2，3}(在序列中)的元素子集，以确保他未来的胜利。
> 
> **输入:** S = {3，2，2，3，3，5}
> **输出:**否
> **说明:**
> 这个序列第一个玩家不能赢。
> 如果**玩家 1** 选择 2 并从序列中移除所有 2，那么**玩家 2** 将选择两个 3 并仅移除两个 3，因为两个玩家都以最佳方式玩。
> 然后**玩家 1** 移除 3 或 5 个，而**玩家 2** 将移除最后一个元素。所以**玩家 1** 总会输。

**进场:**上述问题的进场可以给出，如果序列中元素总数为偶数，且出现不止一次的元素数也为偶数，那么第一个玩家就不能获胜。如果多次出现的元素个数为奇数，重复出现的元素大于等于 4 且为 2 的倍数，则第一个玩家不能获胜。否则，**玩家 1** 可能是赢家。

下面是上述方法的实现:

## C++

```
// C++ implementation for Two player
// game in which a player can remove
// all occurrences of a number

#include <bits/stdc++.h>
using namespace std;

// Function that print whether
// player1 can wins or loses
void game(int v[], int n)
{
    unordered_map<int, int> m;

    // storing the number of occurrence
    // of elements in unordered map
    for (int i = 0; i < n; i++) {

        if (m.find(v[i]) == m.end())
            m[v[i]] = 1;

        else
            m[v[i]]++;
    }

    int count = 0;

    // variable to check if the
// occurrence of repeated
// elements is >= 4 and
    // multiple of 2 or not
    int check = 0;

    // count elements which
// occur more than once
    for (auto i: m) {
        if (i.second > 1) {

            if (i.second >= 4
&& i.second % 2 == 0)
                check++;

            count++;
        }
    }

    if (check % 2 != 0)
        bool flag = false;

    if (check % 2 != 0)
        cout << "Yes" << endl;

    else if (n % 2 == 0
&& count % 2 == 0)
        cout << "No" << endl;

    else
        cout << "Yes" << endl;
}

// Driver code
int main()
{

    int arr[] = { 3, 2, 2, 3, 3, 5 };

    int size = sizeof(arr)
/ sizeof(arr[0]);

    game(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for Two player
// game in which a player can remove
// all occurrences of a number
import java.util.*;
class GFG{

// Function that print whether
// player1 can wins or loses
public static void game(int[] v,
                        int n)
{
  HashMap<Integer,
          Integer> m = new HashMap<>();

  // Storing the number of occurrence
  // of elements in unordered map
  for (int i = 0; i < n; i++)
  {
    if (!m.containsKey(v[i]))
      m.put(v[i], 1);
    else
      m.replace(v[i], m.get(v[i]) + 1);
  }

  int count = 0;

  // variable to check if the
  // occurrence of repeated
  // elements is >= 4 and
  // multiple of 2 or not
  int check = 0;

  // count elements which
  // occur more than once
  for (Map.Entry<Integer,
                 Integer> i : m.entrySet())
  {
    if(i.getValue() > 1)
    {
      if(i.getValue() >= 4 &&
         i.getValue() % 2 == 0)
        check++;

      count++;
    }
  }

  boolean flag;

  if (check % 2 != 0)
    flag = false;
  if (check % 2 != 0)
    System.out.println("Yes");
  else if (n % 2 == 0  &&
           count % 2 == 0)
    System.out.println("No");
  else
    System.out.println("Yes");
}

public static void main(String[] args)
{
  int[] arr = {3, 2, 2, 3, 3, 5};
  int size = arr.length;
  game(arr, size);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation for two player
# game in which a player can remove
# all occurrences of a number
from collections import defaultdict

# Function that print whether
# player1 can wins or loses
def game(v, n):

    m = defaultdict(int)

    # Storing the number of occurrence
    # of elements in unordered map
    for i in range(n):
        if (v[i] not in m):
            m[v[i]] = 1

        else:
            m[v[i]] += 1

    count = 0

    # Variable to check if the
    # occurrence of repeated
    # elements is >= 4 and
    # multiple of 2 or not
    check = 0

    # Count elements which
    # occur more than once
    for i in m.values():
        if (i > 1):
            if (i >= 4 and i % 2 == 0):
                check += 1
            count += 1

    if (check % 2 != 0):
        flag = False

    if (check % 2 != 0):
        print("Yes")

    elif (n % 2 == 0 and count % 2 == 0):
        print("No")

    else:
        print("Yes")

# Driver code
if __name__ == "__main__":

    arr = [ 3, 2, 2, 3, 3, 5 ]
    size = len(arr)

    game(arr, size)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation for Two player
// game in which a player can remove
// all occurrences of a number
using System;
using System.Collections.Generic;

class GFG{

// Function that print whether
// player1 can wins or loses
public static void game(int[] v,
                        int n)
{
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    // Storing the number of occurrence
    // of elements in unordered map
    for(int i = 0; i < n; i++)
    {
        if (!m.ContainsKey(v[i]))
            m.Add(v[i], 1);
        else
            m[v[i]]= m[v[i]] + 1;
    }

    int count = 0;

    // Variable to check if the
    // occurrence of repeated
    // elements is >= 4 and
    // multiple of 2 or not
    int check = 0;

    // Count elements which
    // occur more than once
    foreach(KeyValuePair<int,
                         int> i in m)
    {
        if (i.Value > 1)
        {
            if (i.Value >= 4 &&
                i.Value % 2 == 0)
                check++;

            count++;
        }
    }

    bool flag;

    if (check % 2 != 0)
        flag = false;
    if (check % 2 != 0)
        Console.WriteLine("Yes");
    else if (n % 2 == 0 &&
         count % 2 == 0)
        Console.WriteLine("No");
    else
        Console.WriteLine("Yes");
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 3, 2, 2, 3, 3, 5 };
    int size = arr.Length;

    game(arr, size);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Java implementation for Two player
// game in which a player can remove
// all occurrences of a number

// Function that print whether
// player1 can wins or loses
function game(v,n)
{
  let m = new Map();

  // Storing the number of occurrence
  // of elements in unordered map
  for (let i = 0; i < n; i++)
  {
    if (!m.has(v[i]))
      m.set(v[i], 1);
    else
      m.set(v[i], m.get(v[i]) + 1);
  }

  let count = 0;

  // variable to check if the
  // occurrence of repeated
  // elements is >= 4 and
  // multiple of 2 or not
  let check = 0;

  // count elements which
  // occur more than once
  for (let [key, value] of m.entries())
  {
    if(value> 1)
    {
      if(value >= 4 &&
         value % 2 == 0)
      check++;

      count++;
    }
  }

  let flag;

  if (check % 2 != 0)
    flag = false;
  if (check % 2 != 0)
    document.write("Yes<br>");
  else if (n % 2 == 0  &&
           count % 2 == 0)
    document.write("No<br>");
  else
    document.write("Yes<br>");
}

let arr=[3, 2, 2, 3, 3, 5];
let size = arr.length;
game(arr, size);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
No
```

***时间复杂度:**的复杂度**上面的做法是 O(N)。*