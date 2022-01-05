# 打印最短路径在屏幕上打印字符串

> 原文:[https://www . geesforgeks . org/print-最短路径-print-string-screen/](https://www.geeksforgeeks.org/print-shortest-path-print-string-screen/)

给定一个包含字母 A-Z 的屏幕，我们可以使用遥控器从一个字符切换到另一个字符。遥控器包含左、右、上、下键。
找到最短的可能路径，使用遥控器键入给定字符串的所有字符。初始位置在左上角，输入字符串的所有字符都应该按顺序打印。
**屏幕:**

```
A B C D E
F G H I J
K L M N O
P Q R S T
U V W X Y
Z
```

**例:**

```
Input: “GEEK”
Output: 
Move Down
Move Right
Press OK
Move Up
Move Right
Move Right
Move Right
Press OK
Press OK
Move Left
Move Left
Move Left
Move Left
Move Down
Move Down
Press OK
```

这个想法是将屏幕视为人物的 2D 矩阵。然后我们逐个考虑给定字符串的所有字符，打印出当前字符和矩阵中下一个字符之间的最短路径。为了找到最短路径，我们考虑矩阵中当前字符和下一个字符的坐标。根据当前和下一个角色坐标的 x 和 y 值之间的差异，我们向左、向右、向上或向下移动。即

```
If row difference is negative, we move up
If row difference is positive, we move down
If column difference is negative, we go left
If column difference is positive, we go right
```

以下是上述想法的实现

## C++

```
// C++ program to print shortest possible path to
// type all characters of given string using a remote
#include <iostream>
using namespace std;

// Function to print shortest possible path to
// type all characters of given string using a remote
void printPath(string str)
{
    int i = 0;
    // start from character 'A' present at position (0, 0)
    int curX = 0, curY = 0;
    while (i < str.length())
    {
        // find coordinates of next character
        int nextX = (str[i] - 'A') / 5;
        int nextY = (str[i] - 'B' + 1) % 5;

        // Move Up if destination is above
        while (curX > nextX)
        {
            cout << "Move Up" << endl;
            curX--;
        }

        // Move Left if destination is to the left
        while (curY > nextY)
        {
            cout << "Move Left" << endl;
            curY--;
        }

        // Move down if destination is below
        while (curX < nextX)
        {
            cout << "Move Down" << endl;
            curX++;
        }

        // Move Right if destination is to the right
        while (curY < nextY)
        {
            cout << "Move Right" << endl;
            curY++;
        }

        // At this point, destination is reached
        cout << "Press OK" << endl;
        i++;
    }
}

// Driver code
int main()
{
    string str = "COZY";

    printPath(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print shortest possible path to
// type all characters of given string using a remote

class GFG
{
    // Function to print shortest possible path to
    // type all characters of given string using a remote
    static void printPath(String str)
    {
        int i = 0;
        // start from character 'A' present at position (0, 0)
        int curX = 0, curY = 0;
        while (i < str.length())
        {
            // find coordinates of next character
            int nextX = (str.charAt(i) - 'A') / 5;
            int nextY = (str.charAt(i) - 'B' + 1) % 5;

            // Move Up if destination is above
            while (curX > nextX)
            {
                System.out.println("Move Up");
                curX--;
            }

            // Move Left if destination is to the left
            while (curY > nextY)
            {
                System.out.println("Move Left");
                curY--;
            }

            // Move down if destination is below
            while (curX < nextX)
            {
                System.out.println("Move Down");
                curX++;
            }

            // Move Right if destination is to the right
            while (curY < nextY)
            {
                System.out.println("Move Right");
                curY++;
            }

            // At this point, destination is reached
            System.out.println("Press OK");
            i++;
        }
    }

    // driver program
    public static void main (String[] args)
    {
        String str = "COZY";
        printPath(str);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 program to print shortest possible
# path to type all characters of given string
# using a remote

# Function to print shortest possible path
# to type all characters of given string
# using a remote
def printPath(str):
    i = 0

    # start from character 'A' present
    # at position (0, 0)
    curX = 0
    curY = 0
    while (i < len(str)):

        # find coordinates of next character
        nextX = int((ord(str[i]) - ord('A')) / 5)
        nextY = (ord(str[i]) - ord('B') + 1) % 5

        # Move Up if destination is above
        while (curX > nextX):
            print("Move Up")
            curX -= 1

        # Move Left if destination is to the left
        while (curY > nextY):
            print("Move Left")
            curY -= 1

        # Move down if destination is below
        while (curX < nextX):
            print("Move Down")
            curX += 1

        # Move Right if destination is to the right
        while (curY < nextY):
            print("Move Right")
            curY += 1

        # At this point, destination is reached
        print("Press OK")
        i += 1

# Driver code
if __name__ == '__main__':
    str = "COZY"

    printPath(str)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print shortest
// possible path to type all
// characters of given string
// using a remote
using System;

class GFG {

    // Function to print shortest
    // possible path to type all
    // characters of given string
    // using a remote
    static void printPath(String str)
    {
        int i = 0;

        // start from character 'A'
        // present at position (0, 0)
        int curX = 0, curY = 0;
        while (i < str.Length)
        {

            // find coordinates of
            // next character
            int nextX = (str[i] - 'A') / 5;
            int nextY = (str[i] - 'B' + 1) % 5;

            // Move Up if destination
            // is above
            while (curX > nextX)
            {
                Console.WriteLine("Move Up");
                curX--;
            }

            // Move Left if destination
            // is to the left
            while (curY > nextY)
            {
                Console.WriteLine("Move Left");
                curY--;
            }

            // Move down if destination
            // is below
            while (curX < nextX)
            {
                Console.WriteLine("Move Down");
                curX++;
            }

            // Move Right if destination
            // is to the right
            while (curY < nextY)
            {
                Console.WriteLine("Move Right");
                curY++;
            }

            // At this point, destination
            // is reached
            Console.WriteLine("Press OK");
            i++;
        }
    }

    // Driver Code
    public static void Main ()
    {
        String str = "COZY";
        printPath(str);
    }
}

// This Code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print shortest possible path to
// type all characters of given string using a remote

// Function to print shortest possible path to
// type all characters of given string using a remote
function printPath($str)
{
    $i = 0;
    // start from character 'A' present at position (0, 0)
    $curX = $curY = 0;
    while ($i < strlen($str))
    {
        // find coordinates of next character
        $nextX = (int)((ord($str[$i]) - ord('A')) / 5);
        $nextY = (ord($str[$i]) - ord('B') + 1) % 5;

        // Move Up if destination is above
        while ($curX > $nextX)
        {
            echo "Move Up\n";
            $curX--;
        }

        // Move Left if destination is to the left
        while ($curY > $nextY)
        {
            echo "Move Left\n";
            $curY--;
        }

        // Move down if destination is below
        while ($curX < $nextX)
        {
            echo "Move Down\n";
            $curX++;
        }

        // Move Right if destination is to the right
        while ($curY < $nextY)
        {
            echo "Move Right\n";
            $curY++;
        }

        // At this point, destination is reached
        echo "Press OK\n";
        $i++;
    }
}

// Driver code
    $str = "COZY";

    printPath($str);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

    // JavaScript program to print shortest
    // possible path to type all
    // characters of given string
    // using a remote

    // Function to print shortest
    // possible path to type all
    // characters of given string
    // using a remote
    function printPath(str)
    {
        let i = 0;

        // start from character 'A'
        // present at position (0, 0)
        let curX = 0, curY = 0;
        while (i < str.length)
        {

            // find coordinates of
            // next character
            let nextX = parseInt((str[i].charCodeAt() -
            'A'.charCodeAt()) / 5, 10);
            let nextY = (str[i].charCodeAt() -
            'B'.charCodeAt() + 1) % 5;

            // Move Up if destination
            // is above
            while (curX > nextX)
            {
                document.write("Move Up" + "</br>");
                curX--;
            }

            // Move Left if destination
            // is to the left
            while (curY > nextY)
            {
                document.write("Move Left" + "</br>");
                curY--;
            }

            // Move down if destination
            // is below
            while (curX < nextX)
            {
                document.write("Move Down" + "</br>");
                curX++;
            }

            // Move Right if destination
            // is to the right
            while (curY < nextY)
            {
                document.write("Move Right" + "</br>");
                curY++;
            }

            // At this point, destination
            // is reached
            document.write("Press OK" + "</br>");
            i++;
        }
    }

    let str = "COZY";
      printPath(str);

</script>
```

**输出:**

```
Move Right
Move Right
Press OK
Move Down
Move Down
Move Right
Move Right
Press OK
Move Left
Move Left
Move Left
Move Left
Move Down
Move Down
Move Down
Press OK
Move Up
Move Right
Move Right
Move Right
Move Right
Press OK
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息