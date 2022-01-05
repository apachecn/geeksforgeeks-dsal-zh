# 根据给定条件计算欧几里得距离的平方

> 原文:[https://www . geeksforgeeks . org/基于给定条件计算欧几里得距离的平方/](https://www.geeksforgeeks.org/calculate-the-square-of-euclidean-distance-traveled-based-on-given-conditions/)

给定一个数组**命令【】**，该数组由表示沿坐标行进的距离和方向的有符号整数和表示无法访问的坐标的数组**障碍物【】**组成，任务是按照在序列中指定的命令，按照的**命令【】**数组中的顺序，找到可从原点(0，0)开始向北行进的最大 [**欧几里德距离**](https://en.wikipedia.org/wiki/Euclidean_distance#:~:text=In%20mathematics%2C%20the%20Euclidean%20distance, metric%20as%20the%20Pythagorean%20metric.) 的**正方形的正方形**

*   **-2** :左转 90 度。
*   **-1** :右转 90 度。
*   **1 < = X < = 9** :前进 X 个单位。

**示例:**

> **输入:**命令[] = {4，-1，4，-2，4}，障碍物[] = {{ 2，4 }}
> **输出:** 65
> **解释:**
> 第 1 步:(0，0) - > (0，4)
> 第 2 步:(0，4) - > (1，4)
> 第 3 步和第 4 步:
> 障碍物
> 第 5 步:(1，4) - > (1，4)
> 
> **输入:**命令[] = {4，-1，3}，障碍物[] = {}
> **输出:** 25

**方法:**按照以下步骤解决问题:

1.  最初，机器人在 **(0，0)** 朝北。
2.  分配变量以跟踪机器人每一步后的当前位置和方向。
3.  将障碍物的坐标存储在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中。
4.  制作 **2** 阵列 **(dx[]，dy[])** 并根据方向的变化将所有可能的运动存储在 **x** 和 **y** 坐标中。
5.  如果遇到方向改变，参照 2 个阵列改变当前方向。
6.  否则，继续向同一个方向移动，直到遇到方向变化，如果其间没有障碍物。
7.  最后，计算 x 和 y 坐标的平方。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

void robotSim(vector<int> commands,
              vector<pair<int, int>> obstacles)
{

    // Possible movements in x coordinate.
    vector<int> dx = { 0, 1, 0, -1 };

    // Possible movements in y coordinate.
    vector<int> dy = { 1, 0, -1, 0 };

    int x = 0, y = 0;

    int di = 0;

    // Put all obstacles into hashmap.
    map<pair<int, int>, int>obstacleSet;

    for(auto i:obstacles)
        obstacleSet[i] = 1;

    // Maximum distance
    int ans = 0;

    // Iterate commands.
    for(int cmd : commands)
    {

        // Left direction
        if (cmd == -2)
            di = (di-1) % 4;

        // Right direction
        else if (cmd == -1)
            di = (di + 1) % 4;   

        // If no direction changes
        else
        {
            for(int i = 0; i < cmd; i++)
            {

                // Checking for obstacles.
                if (obstacleSet.find({x + dx[di],
                                      y + dy[di]}) ==
                                      obstacleSet.end())
                {

                    // Update x coordinate
                    x += dx[di];

                    // Update y coordinate
                    y += dy[di];

                    // Updating for max distance
                    ans = max(ans, x * x + y * y);
                }
            }
        }
    }
    cout << ans << endl;
}

// Driver Code
int main()
{
    vector<int> commands = { 4, -1, 4, -2, 4 };
    vector<pair<int, int>> obstacles = { { 2, 4 } };

    robotSim(commands, obstacles);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.awt.Point;

class GFG{

static void robotSim(List<Integer> commands,
                     List<Point> obstacles)
{

    // Possible movements in x coordinate.
    List<Integer> dx = Arrays.asList(0, 1, 0, -1);

    // Possible movements in y coordinate.
    List<Integer> dy = Arrays.asList(1, 0, -1, 0);

    int x = 0, y = 0;
    int di = 0;

    // Put all obstacles into hashmap.
    HashMap<Point, Integer> obstacleSet = new HashMap<>();

    for(Point i : obstacles)
        obstacleSet.put(i, 1);

    // Maximum distance
    int ans = 0;

    // Iterate commands.
    for(Integer cmd : commands)
    {

        // Left direction
        if (cmd == -2)
            di = (di - 1) % 4;

        // Right direction
        else if (cmd == -1)
            di = (di + 1) % 4;   

        // If no direction changes
        else
        {
            for(int i = 0; i < cmd; i++)
            {

                // Checking for obstacles.
                if (!obstacleSet.containsKey(
                    new Point(x + dx.get(di),
                              y + dy.get(di))))
                {

                    // Update x coordinate
                    x += dx.get(di);

                    // Update y coordinate
                    y += dy.get(di);

                    // Updating for max distance
                    ans = Math.max(ans, x * x + y * y);
                }
            }
        }
    }
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    List<Integer> commands = Arrays.asList(
        4, -1, 4, -2, 4);
    List<Point> obstacles = new ArrayList<>();
    obstacles.add(new Point(2, 4));

    robotSim(commands, obstacles);
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
def robotSim(commands, obstacles):

    # Possible movements in x coordinate.
    dx = [0, 1, 0, -1]

    # Possible movements in y coordinate.
    dy = [1, 0, -1, 0]

    # Initialise position to (0, 0).
    x, y = 0, 0

    # Initial direction is north.
    di = 0

    # Put all obstacles into hashmap.
    obstacleSet = set(map(tuple, obstacles))

    # maximum distance
    ans = 0

    # Iterate commands.
    for cmd in commands:

        # Left direction
        if cmd == -2:
            di = (di-1) % 4

        # Right direction
        elif cmd == -1:
            di = (di + 1) % 4

        # If no direction changes
        else:
            for i in range(cmd):
                # Checking for obstacles.
                if (x + dx[di], y + dy[di]) \
                not in obstacleSet:

                    # Update x coordinate
                    x += dx[di]

                    # Update y coordinate
                    y += dy[di]

                    # Updating for max distance
                    ans = max(ans, x * x + y * y)
    print(ans)

# Driver Code
if __name__ == "__main__":
    commands = [4, -1, 4, -2, 4]
    obstacles = [[2, 4]]
    robotSim(commands, obstacles)
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;  
class GFG {

  static void robotSim(List<int> commands,
                       List<Tuple<int, int>> obstacles)
  {

    // Possible movements in x coordinate.
    List<int> dx = new List<int>(new int[]{ 0, 1, 0, -1 });

    // Possible movements in y coordinate.
    List<int> dy = new List<int>(new int[]{ 1, 0, -1, 0 });   
    int x = 0, y = 0;    
    int di = 0;

    // Put all obstacles into hashmap.
    Dictionary<Tuple<int, int>, int> obstacleSet =
      new Dictionary<Tuple<int, int>, int>(); 

    foreach(Tuple<int, int> i in obstacles)
      obstacleSet[i] = 1;

    // Maximum distance
    int ans = 0;

    // Iterate commands.
    foreach(int cmd in commands)
    {

      // Left direction
      if (cmd == -2)
        di = (di - 1) % 4;

      // Right direction
      else if (cmd == -1)
        di = (di + 1) % 4;   

      // If no direction changes
      else
      {
        for(int i = 0; i < cmd; i++)
        {

          // Checking for obstacles.
          if (!obstacleSet.ContainsKey(new Tuple<int,int>(x + dx[di],
                                                          y + dy[di])))
          {

            // Update x coordinate
            x += dx[di];

            // Update y coordinate
            y += dy[di];

            // Updating for max distance
            ans = Math.Max(ans, x * x + y * y);
          }
        }
      }
    }
    Console.WriteLine(ans);
  }

  // Driver code
  static void Main()
  {
    List<int> commands = new List<int>(new int[]{ 4, -1, 4, -2, 4 });
    List<Tuple<int, int>> obstacles = new List<Tuple<int, int>>();
    obstacles.Add(new Tuple<int, int>(2,4));   
    robotSim(commands, obstacles);
  }
}

// This code is contributed by divyeshrabadiya07.
```

**Output:** 

```
65
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N + M)，其中 M 是这个*障碍阵的长度。*