# 给定动作后机器人的位置

> 原文:[https://www . geeksforgeeks . org/给定动作后机器人的位置/](https://www.geeksforgeeks.org/position-of-robot-after-given-movements/)

给定一个只能在四个方向上移动的机器人，上(U)，下(D)，左(L)，右(R)。给定由移动指令组成的字符串。执行指令后输出机器人的坐标。机器人的初始位置在原点(0，0)。

**示例:**

> **输入:**Move =“udddlrl”
> T3】输出: (-1，-1)
> **解释:**
> Move U : (0，0)–(0，1)
> Move D : (0，1)–(0，0)
> Move D : (0，0)–(0，-1)
> Move L : (0，-1)–(-1，-1)
> Move R : (-1，-1)–(0，-1)
> 
> **输入:**移动=【uddlruuuduuruduulldrrrr】
> 输出: (2，3)

**来源:** [高盛面试经验|第 36 集](https://www.geeksforgeeks.org/goldman-sachs-interview-experience-set-26-experienced/)。

**进场:**
分别计算向上运动(U)、向下运动(D)、向左运动(L)和向右运动(R)的次数为 countUp、倒计时、countLeft 和 countRight。最终 x 坐标为
(count right–count left)，y 坐标为(count up–倒计时)。

下面是上述想法的实现:

## C++

```
// C++ implementation to find  final position of
// robot after the complete movement
#include <bits/stdc++.h>
using namespace std;

// Function to find  final position of
// robot after the complete movement
void finalPosition(string move)
{
    int l = move.size();
    int countUp = 0, countDown = 0;
    int countLeft = 0, countRight = 0;

    // Traverse the instruction string 'move'
    for (int i = 0; i < l; i++)
    {
        // For each movement increment its
        // respective counter
        if (move[i] == 'U')
            countUp++;
        else if (move[i] == 'D')
            countDown++;
        else if (move[i] == 'L')
            countLeft++;
        else if (move[i] == 'R')
            countRight++;
    }

    // Required final position of robot
    cout << "Final Position: ("
         << (countRight - countLeft)
         << ", " << (countUp - countDown)
         << ")" << endl;
}

// Driver code
int main()
{
    string move = "UDDLLRUUUDUURUDDUULLDRRRR";
    finalPosition(move);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find final position
// of robot after the complete movement

import java.io.*;

class GFG {

    // function to find final position of
    // robot after the complete movement
    static void finalPosition(String move)
    {

        int l = move.length();
        int countUp = 0, countDown = 0;
        int countLeft = 0, countRight = 0;

        // traverse the instruction string
        // 'move'
        for (int i = 0; i < l; i++)
        {
            // for each movement increment
            // its respective counter
            if (move.charAt(i) == 'U')
                countUp++;

            else if (move.charAt(i) == 'D')
                countDown++;

            else if (move.charAt(i) == 'L')
                countLeft++;

            else if (move.charAt(i) == 'R')
                countRight++;
        }

        // required final position of robot
        System.out.println("Final Position: ("
                           + (countRight - countLeft) + ", "
                           + (countUp - countDown) + ")");
    }

    // Driver code
    public static void main(String[] args)
    {
        String move = "UDDLLRUUUDUURUDDUULLDRRRR";
        finalPosition(move);
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 implementation to find final position
# of robot after the complete movement

# function to find final position of
# robot after the complete movement

def finalPosition(move):

    l = len(move)
    countUp, countDown = 0, 0
    countLeft, countRight = 0, 0

    # traverse the instruction string
    # 'move'
    for i in range(l):

        # for each movement increment
        # its respective counter
        if (move[i] == 'U'):
            countUp += 1

        elif(move[i] == 'D'):
            countDown += 1

        elif(move[i] == 'L'):
            countLeft += 1

        elif(move[i] == 'R'):
            countRight += 1

    # required final position of robot
    print("Final Position: (", (countRight - countLeft),
          ", ", (countUp - countDown), ")")

# Driver code
if __name__ == '__main__':
    move = "UDDLLRUUUDUURUDDUULLDRRRR"
    finalPosition(move)

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to find final position
// of robot after the complete movement
using System;

class GFG {

    // function to find final position of
    // robot after the complete movement
    static void finalPosition(String move)
    {
        int l = move.Length;
        int countUp = 0, countDown = 0;
        int countLeft = 0, countRight = 0;

        // traverse the instruction string
        // 'move'
        for (int i = 0; i < l; i++)
        {
           // for each movement increment
            // its respective counter
            if (move[i] == 'U')
                countUp++;

            else if (move[i] == 'D')
                countDown++;

            else if (move[i] == 'L')
                countLeft++;

            else if (move[i] == 'R')
                countRight++;
        }

        // required final position of robot
        Console.WriteLine("Final Position: ("
                          + (countRight - countLeft) + ", "
                          + (countUp - countDown) + ")");
    }

    // Driver code
    public static void Main()
    {
        String move = "UDDLLRUUUDUURUDDUULLDRRRR";
        finalPosition(move);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// final position of robot after
// the complete movement

// function to find final position of
// robot after the complete movement
function finalPosition($move)
{
    $l = strlen($move);
    $countUp = 0;
    $countDown = 0;
    $countLeft = 0;
    $countRight = 0;

    // traverse the instruction
    // string 'move'
    for ($i = 0; $i < $l; $i++) {

        // for each movement increment its
        // respective counter
        if ($move[$i] == 'U')
            $countUp++;
        else if ($move[$i] == 'D')
            $countDown++;
        else if ($move[$i] == 'L')
            $countLeft++;
        else if ($move[$i] == 'R')
            $countRight++;
    }

    // required final position of robot
    echo "Final Position: ("
        . ($countRight - $countLeft)
        . ", " , ($countUp - $countDown)
        . ")" ."\n";
}

    // Driver Code
    $move = "UDDLLRUUUDUURUDDUULLDRRRR";
    finalPosition($move);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to find final position
    // of robot after the complete movement

    // function to find final position of
    // robot after the complete movement
    function finalPosition(move)
    {
        let l = move.length;
        let countUp = 0, countDown = 0;
        let countLeft = 0, countRight = 0;

        // traverse the instruction string
        // 'move'
        for (let i = 0; i < l; i++)
        {
           // for each movement increment
            // its respective counter
            if (move[i] == 'U')
                countUp++;

            else if (move[i] == 'D')
                countDown++;

            else if (move[i] == 'L')
                countLeft++;

            else if (move[i] == 'R')
                countRight++;
        }

        // required final position of robot
        document.write("Final Position: ("
                          + (countRight - countLeft) + ", "
                          + (countUp - countDown) + ")");
    }

    let move = "UDDLLRUUUDUURUDDUULLDRRRR";
      finalPosition(move);

</script>
```

**Output**

```
Final Position: (2, 3)
```