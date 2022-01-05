# 英雄休克的总时间

> 原文:[https://www . geeksforgeeks . org/总时间-哪个英雄会休克/](https://www.geeksforgeeks.org/total-time-for-which-the-hero-will-be-in-shock/)

给定一个包含非递减顺序的 **N** 整数和一个整数 **D** 的数组**攻击**。阵法攻击中的每一个元素都表示英雄在游戏中被攻击的时间，D 表示英雄被震到无法反击的持续时间。任务是找到英雄被电击的总时间。

**示例:**

> **输入:**攻击=【1，4】，d= 2
> **输出:** 4
> **说明:**
> 第 1 秒，Hero 被攻击，保持震荡 1 秒和 2 秒。
> 第 4 秒，Hero 被攻击，持续 4 秒和 5 秒处于休克状态。
> 总共 4 秒。
> 
> **输入:**攻击=【1，2】，d= 2
> **输出:** 3
> **说明:**
> 第 1 秒，Hero 被攻击，保持震荡 1 秒，2 秒。
> 第二秒，英雄被攻击，持续 2 秒和 3 秒处于休克状态。
> 总共 3 秒。

**进场:**用公式计算英雄休克的时间:

> **攻击[i] =(攻击[I]+D)–最大(前一次攻击结束的时间，攻击[i])**

现在要解决这个问题，请按照以下步骤操作:

1.  创建一个变量 **totalTime** ，存储这个问题的答案。
2.  创建一个变量 **prev** 并将其初始化为攻击【0】。该变量将存储每次单独攻击前一次攻击结束的时间。
3.  运行从 **i=0** 到 **i < N** 的循环，在每次迭代中:
    *   将攻击【I】即**(攻击【I】+D)–max(prev，攻击【I】)**的电击时间加到 **totalTime** 上。
    *   将 prev 更改为前一次攻击结束的时间，因此**prev =攻击[i]+D** 。
4.  循环结束后，返回 **totalTime** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total time for
// which hero will be under shock
int heroInShock(vector<int>& attack, int D)
{

    int N = attack.size();
    int totalTime = 0;

    int prev = attack[0];

    for (int i = 0; i < N; i++) {

        // Adding time of attack in total time
        totalTime += (attack[i] + D)
                     - max(prev, attack[i]);

        // Changing prev to the time where
        // the previous attack ends
        prev = attack[i] + D;
    }

    return totalTime;
}

// Driver Code
int main()
{
    vector<int> attack = { 1, 2, 6 };
    int D = 2;
    cout << heroInShock(attack, D);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG{

// Function to find the total time for
// which hero will be under shock
static int heroInShock(ArrayList<Integer> attack, int D)
{
    int N = attack.size();
    int totalTime = 0;
    int prev = (int)attack.get(0);

    for(int i = 0; i < N; i++)
    {

        // Adding time of attack in total time
        totalTime += ((int)attack.get(i) + D) -
                      Math.max(prev, (int)attack.get(i));

        // Changing prev to the time where
        // the previous attack ends
        prev = (int)attack.get(i) + D;
    }
    return totalTime;
}

// Driver code
public static void main(String args[])
{
    ArrayList<Integer> attack = new ArrayList<Integer>();
    attack.add(1);
    attack.add(2);
    attack.add(6);

    int D = 2;
    System.out.println(heroInShock(attack, D));
}
}

// This code is contributed by gfking
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the total time for
# which hero will be under shock
def heroInShock(attack, D):
    N = len(attack)
    totalTime = 0
    prev = attack[0]
    for i in range(N):

        # Adding time of attack in total time
        totalTime += (attack[i] + D) - max(prev, attack[i])

        # Changing prev to the time where
        # the previous attack ends
        prev = attack[i] + D

    return totalTime

# Driver Code
attack = [1, 2, 6]
D = 2
print(heroInShock(attack, D))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code to implement above approach
using System;
using System.Collections;
class GFG {

  // Function to find the total time for
  // which hero will be under shock
  static int heroInShock(ArrayList attack, int D)
  {

    int N = attack.Count;
    int totalTime = 0;

    int prev = (int)attack[0];

    for (int i = 0; i < N; i++) {

      // Adding time of attack in total time
      totalTime += ((int)attack[i] + D)
        - Math.Max(prev, (int)attack[i]);

      // Changing prev to the time where
      // the previous attack ends
      prev = (int)attack[i] + D;
    }

    return totalTime;
  }

  // Driver code
  public static void Main()
  {
    ArrayList attack = new ArrayList();
    attack.Add(1);
    attack.Add(2);
    attack.Add(6);

    int D = 2;
    Console.Write(heroInShock(attack, D));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find the total time for
      // which hero will be under shock
      function heroInShock(attack, D)
      {
          let N = attack.length;
          let totalTime = 0;

          let prev = attack[0];

          for (let i = 0; i < N; i++) {

              // Adding time of attack in total time
              totalTime += (attack[i] + D)
                  - Math.max(prev, attack[i]);

              // Changing prev to the time where
              // the previous attack ends
              prev = attack[i] + D;
          }

          return totalTime;
      }

      // Driver Code
      let attack = [1, 2, 6];
      let D = 2;
      document.write(heroInShock(attack, D));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
5
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)