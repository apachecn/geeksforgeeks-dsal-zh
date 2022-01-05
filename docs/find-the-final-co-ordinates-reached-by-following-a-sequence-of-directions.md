# 按照一系列方向找到最终坐标

> 原文:[https://www . geesforgeks . org/find-the-final-co-coordinates-following-sequence-of-directions/](https://www.geeksforgeeks.org/find-the-final-co-ordinates-reached-by-following-a-sequence-of-directions/)

给定一个分别具有 x 和 y 坐标 SX 和 SY 的起点，以及一个表示要遵循的方向的序列**‘D’**，任务是找到目的地的坐标。字符串 D 由字符 S、N、W 和 E 组成，其中**【S =南(下移一个单位)、N =北(上移一个单位)、W =西(左移一个单位)、E =东(右移一个单位)】**
**示例**。

> **输入:** SX = 2，SY = 3，D = "SEWW"
> **输出:** (1，2)
> **解释:**从给定点开始，会定向
> 到 S(2，2)—>E(3，2)—>W(2，2)—>W(1，2)。因此最终位置为(1，2)
> **输入:** SX = 2，SY = 2，D =【NSSE】
> **输出:** (3，1)

**方法:**遍历字符串 **D** 并相应地增加或减少坐标 **SX** 和 **SY** 并打印它们的最终值。
以下是上述方法的实施:

## C++

```
// C++ implementation of
// the above approach

#include<bits/stdc++.h>
using namespace std;

// Function to print the final position
// of the point after traversing through
// the given directions
void finalCoordinates(int SX, int SY, string D){

    // Traversing through the given directions
    for (int i = 0; i < D.length(); i++){

        // If its north or south the point
        // will move left or right
        if (D[i] == 'N')
            SY += 1;
        else if(D[i] == 'S')
            SY -= 1;

        // If its west or east the point
        // will move upwards or downwards
        else if(D[i] == 'E')
            SX += 1;
        else
            SX -= 1;
    }

    // Returning the final position
    string ans = '(' + to_string(SX) + ',' +
                     to_string(SY) + ')';
    cout<<ans<<endl;
}

// Driver Code
int main(){

    int SX = 2, SY = 2;
    string D = "NSSE";

    finalCoordinates(SX, SY, D);

}
// This code is contributed by Samarth
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to print the final position
// of the point after traversing through
// the given directions
static void finalCoordinates(int SX, int SY,
                             char []D)
{

    // Traversing through the given directions
    for(int i = 0; i < D.length; i++)
    {

       // If its north or south the point
       // will move left or right
       if (D[i] == 'N')
           SY += 1;
       else if(D[i] == 'S')
           SY -= 1;

       // If its west or east the point
       // will move upwards or downwards
       else if(D[i] == 'E')
           SX += 1;
       else
           SX -= 1;
    }

    // Returning the final position
    String ans = '(' + String.valueOf(SX) + ',' +
                       String.valueOf(SY) + ')';
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int SX = 2, SY = 2;
    String D = "NSSE";

    finalCoordinates(SX, SY, D.toCharArray());
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to print the final position
# of the point after traversing through
# the given directions
def finalCoordinates(SX, SY, D):

    # Traversing through the given directions
    for i in range (len(D)):

        # If its north or south the point
        # will move left or right
        if (D[i] == 'N'):
            SY += 1
        elif (D[i] == 'S'):
            SY -= 1

        # If its west or east the point
        # will move upwards or downwards
        elif (D[i] == 'E'):
            SX += 1
        else :
            SX -= 1

    # Returning the final position
    ans = '(' + str(SX) + ',' +  str(SY) + ')'
    print (ans)

# Driver Code
if __name__ == '__main__':
    SX, SY = 2,2 
    D = "NSSE"

    finalCoordinates(SX, SY, D)

# This code is contributed by parna_28
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to print the readonly position
// of the point after traversing through
// the given directions
static void finalCoordinates(int SX, int SY,
                             char []D)
{

    // Traversing through the given directions
    for(int i = 0; i < D.Length; i++)
    {

       // If its north or south the point
       // will move left or right
       if (D[i] == 'N')
       {
           SY += 1;
       }
       else if(D[i] == 'S')
       {
           SY -= 1;
       }

       // If its west or east the point
       // will move upwards or downwards
       else if(D[i] == 'E')
       {
           SX += 1;
       }
       else
       {
           SX -= 1;
       }
    }

    // Returning the readonly position
    String ans = '(' + String.Join("", SX) + ',' +
                       String.Join("", SY) + ')';
    Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{
    int SX = 2, SY = 2;
    String D = "NSSE";

    finalCoordinates(SX, SY, D.ToCharArray());
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to print the final position
// of the point after traversing through
// the given directions
function finalCoordinates(SX,SY,D)
{
    // Traversing through the given directions
    for(let i = 0; i < D.length; i++)
    {

       // If its north or south the point
       // will move left or right
       if (D[i] == 'N')
           SY += 1;
       else if(D[i] == 'S')
           SY -= 1;

       // If its west or east the point
       // will move upwards or downwards
       else if(D[i] == 'E')
           SX += 1;
       else
           SX -= 1;
    }

    // Returning the final position
    let ans = '(' + (SX).toString() + ',' +
                       (SY).toString() + ')';
    document.write(ans);
}

// Driver Code
let SX = 2, SY = 2;
let D = "NSSE";

finalCoordinates(SX, SY, D.split(""));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
(3,1)
```