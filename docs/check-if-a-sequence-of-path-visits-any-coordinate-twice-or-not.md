# 检查路径序列是否两次访问任意坐标

> 原文:[https://www . geesforgeks . org/check-if-a-sequence-of-path-visitors-any-coordinate-two-or-not/](https://www.geeksforgeeks.org/check-if-a-sequence-of-path-visits-any-coordinate-twice-or-not/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，仅由字符**【N】【S】【E】**或**【W】**组成，每个字符分别代表移动一个单位**北、南、东、**或**西**。一个人从 2D 飞机的原点 **(0，0)** 开始，按照绳子上的方向行走。任务是检查这个人在行走中是否越过了他已经访问过的任何坐标。如果发现是真的，则打印“**划线”**。否则，打印“**未划线”**。

**示例:**

> ***输入:** str = "NESW"*
> ***输出:**穿越*
> ***解释:***
> *人的道路由:*
> *(0，0)—>(0，1)—>(1，1)—>(0，1)—>(0，0)。*
> *此后，坐标(0，0)再次被访问。*
> *因此，印刷体 Crossed 为他已经越过的路径。*
> 
> ***输入:** str = "SESS"*
> ***输出:**未交叉*
> ***解释:***
> *人的道路由:*
> *【0，0】->(0，-1)-(T27)【1，-1)-(T28】(1，-2)-(T29)【1，-3】。*
> *从上面的路径来看，这个人再也没有去过同一个坐标。*
> *故印未划线。*

**方法:**想法是为遇到的坐标保持一个 [**集合**](https://www.geeksforgeeks.org/set-in-java/) ，以检查已经访问的坐标是否出现。以下是步骤:

1.  初始化两个变量 **X** 和 **Y** ，并将数值初始化为**零**。这些变量将表示 **x** 和 **y** 坐标。
2.  在[组](https://www.geeksforgeeks.org/set-in-cpp-stl/)中插入 **X** 和 **Y** 。
3.  在**【0，N)** 范围内循环迭代，按照以下条件增加 X 或 Y 坐标:
    *   如果字符为**‘N’**，则用 **1** 递增 **Y** 。
    *   如果字符是**的**，那么将 **Y** 减 **1** 。
    *   如果字符为**‘E’**，则用 **1** 递增 **X** 。
    *   如果字符为**‘W’**，则以 **1** 递减 **X** 。
4.  为集合中的每个角色插入上一步更新的 **X** 和 **Y** 坐标。
5.  在上述步骤中插入坐标时，如果遇到任何当前坐标，则打印**划线**。
6.  否则，打印**未交叉**，因为所有坐标点都是唯一的。

下面是上述方法的实现

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the man crosses
// previous visited coordinate or not
bool isCrossed(string path)
{
    if (path.size() == 0)
        return false;

    // Stores the count of
    // crossed vertex
    bool ans = false;

    // Stores (x, y) coordinates
    set<pair<int, int> > set;

    // The coordinates for the origin
    int x = 0, y = 0;
    set.insert({ x, y });

    // Iterate over the string
    for (int i = 0; i < path.size(); i++) {

        // Condition to increment X or
        // Y co-ordinates respectively
        if (path[i] == 'N')
            set.insert({ x, y++ });

        if (path[i] == 'S')
            set.insert({ x, y-- });

        if (path[i] == 'E')
            set.insert({ x++, y });

        if (path[i] == 'W')
            set.insert({ x--, y });

        // Check if (x, y) is already
        // visited
        if (set.find({ x, y })
            != set.end()) {

            ans = true;
            break;
        }
    }

    // Print the result
    if (ans)
        cout << "Crossed";
    else
        cout << "Not Crossed";
}

// Driver Code
int main()
{
    // Given string
    string path = "NESW";

    // Function Call
    isCrossed(path);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.awt.Point;
import java.util.HashSet;
class GFG{

// Function to check if the man crosses
// previous visited coordinate or not
static void isCrossed(String path)
{
  if (path.length() == 0)
    return;

  // Stores the count of
  // crossed vertex
  boolean ans = false;

  // Stores (x, y) coordinates
  HashSet<Point> set =
          new HashSet<Point>();

  // The coordinates for the origin
  int x = 0, y = 0;
  set.add(new Point(x, y));

  // Iterate over the String
  for (int i = 0; i < path.length(); i++)
  {
    // Condition to increment X or
    // Y co-ordinates respectively
    if (path.charAt(i) == 'N')
      set.add(new Point(x, y++));

    if (path.charAt(i) == 'S')
      set.add(new Point(x, y--));

    if (path.charAt(i) == 'E')
      set.add(new Point(x++, y));

    if (path.charAt(i) == 'W')
      set.add(new Point(x--, y));

    // Check if (x, y) is already
    // visited
    if (set.contains(new Point(x, y)))
    {
      ans = true;
      break;
    }
  }

  // Print the result
  if (ans)
    System.out.print("Crossed");
  else
    System.out.print("Not Crossed");
}

// Driver Code
public static void main(String[] args)
{
  // Given String
  String path = "NESW";

  // Function Call
  isCrossed(path);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the man crosses
# previous visited coordinate or not
def isCrossed(path):

    if (len(path) == 0):
        return bool(False)

    # Stores the count of
    # crossed vertex
    ans = bool(False)

    # Stores (x, y) coordinates
    Set = set()

    # The coordinates for the origin
    x, y = 0, 0
    Set.add((x, y))

    # Iterate over the string
    for i in range(len(path)):

        # Condition to increment X or
        # Y co-ordinates respectively
        if (path[i] == 'N'):
            Set.add((x, y))
            y = y + 1

        if (path[i] == 'S'):
            Set.add((x, y))
            y = y - 1

        if (path[i] == 'E'):
            Set.add((x, y))
            x = x + 1

        if (path[i] == 'W'):
            Set.add((x, y))
            x = x - 1

        # Check if (x, y) is already visited
        if (x, y) in Set:
            ans = bool(True)
            break

    # Print the result
    if (ans):
        print("Crossed")
    else:
        print("Not Crossed")

# Driver code

# Given string
path = "NESW"

# Function call
isCrossed(path)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if the man crosses
// previous visited coordinate or not
static void isCrossed(String path)
{
    if (path.Length == 0)
        return;

    // Stores the count of
    // crossed vertex
    bool ans = false;

    // Stores (x, y) coordinates
    HashSet<KeyValuePair<int, int>> mySet =
    new HashSet<KeyValuePair<int, int>>();

    // The coordinates for the origin
    int x = 0, y = 0;
    mySet.Add(new KeyValuePair<int, int>(x, y));

    // Iterate over the String
    for(int i = 0; i < path.Length; i++)
    {

        // Condition to increment X or
        // Y co-ordinates respectively
        if (path[i] == 'N')
            mySet.Add(
                new KeyValuePair<int, int>(x, y++));

        if (path[i] == 'S')
            mySet.Add(
                new KeyValuePair<int, int>(x, y--));

        if (path[i] == 'E')
            mySet.Add(
                new KeyValuePair<int, int>(x++, y));

        if (path[i] == 'W')
            mySet.Add(
                new KeyValuePair<int, int>(x--, y));

        // Check if (x, y) is already
        // visited
        if (mySet.Contains(
                new KeyValuePair<int, int>(x, y)))
        {
            ans = true;
            break;
        }
    }

    // Print the result
    if (ans)
        Console.Write("Crossed");
    else
        Console.Write("Not Crossed");
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String path = "NESW";

    // Function call
    isCrossed(path);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if the man crosses
    // previous visited coordinate or not
    function isCrossed(path)
    {
        if (path.length == 0)
            return;

        // Stores the count of
        // crossed vertex
        let ans = false;

        // Stores (x, y) coordinates
        let mySet = new Set();

        // The coordinates for the origin
        let x = 0, y = 0;
        mySet.add([x, y]);

        // Iterate over the String
        for(let i = 0; i < path.length; i++)
        {

            // Condition to increment X or
            // Y co-ordinates respectively
            if (path[i] == 'N')
                mySet.add([x, y++]);

            if (path[i] == 'S')
                mySet.add([x, y--]);

            if (path[i] == 'E')
                mySet.add([x++, y]);

            if (path[i] == 'W')
                mySet.add([x--, y]);

            // Check if (x, y) is already
            // visited
            if (!mySet.has([x, y]))
            {
                ans = true;
                break;
            }
        }

        // Print the result
        if (ans)
            document.write("Crossed");
        else
            document.write("Not Crossed");
    }

    // Given String
    let path = "NESW";

    // Function call
    isCrossed(path);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
Crossed
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*