# 腐烂所有橘子所需的最短时间

> 原文： [https://www.geeksforgeeks.org/minimum-time-required-so-that-all-oranges-become-rotten/](https://www.geeksforgeeks.org/minimum-time-required-so-that-all-oranges-become-rotten/)

给定尺寸为 m * n 的矩阵，其中矩阵中的每个单元格可以具有值 0、1 或 2，其含义如下：

```
0: Empty cell
1: Cells have fresh oranges
2: Cells have rotten oranges 

```

确定什么是最短时间才能使所有橙变烂。 索引为[i，j]的腐烂橙可以腐烂索引为[i-1，j]，[i + 1，j]，[i，j-1]，[i，j + 1]的其他鲜橙（向上 ，向下，向左和向右）。 如果不可能腐烂每个橙色，则只需返回-1。

**范例**：

```
Input:  arr[][C] = { {2, 1, 0, 2, 1},
                     {1, 0, 1, 2, 1},
                     {1, 0, 0, 2, 1}};
Output:
All oranges can become rotten in 2-time frames.
Explanation: 
At 0th time frame:
 {2, 1, 0, 2, 1}
 {1, 0, 1, 2, 1}
 {1, 0, 0, 2, 1}

At 1st time frame:
 {2, 2, 0, 2, 2}
 {2, 0, 2, 2, 2}
 {1, 0, 0, 2, 2}

At 2nd time frame:
 {2, 2, 0, 2, 2}
 {2, 0, 2, 2, 2}
 {2, 0, 0, 2, 2}

Input:  arr[][C] = { {2, 1, 0, 2, 1},
                     {0, 0, 1, 2, 1},
                     {1, 0, 0, 2, 1}};
Output:
All oranges cannot be rotten.
Explanation: 
At 0th time frame:
{2, 1, 0, 2, 1}
{0, 0, 1, 2, 1}
{1, 0, 0, 2, 1}

At 1st time frame:
{2, 2, 0, 2, 2}
{0, 0, 2, 2, 2}
{1, 0, 0, 2, 2}

At 2nd time frame:
{2, 2, 0, 2, 2}
{0, 0, 2, 2, 2}
{1, 0, 0, 2, 2}
...
The 1 at the bottom left corner of the matrix is never rotten.

```

**<u>朴素的解决方案：</u>**

*   **方法**：这个想法很基础。 多轮遍历所有橙子。 在每一轮中，将橙子旋转到上一轮中腐烂的橙子的相邻位置。

*   **算法**：

    1.  创建变量*否= 2* 和*已更改=假*

    2.  循环运行，直到矩阵的任何单元都没有在迭代中更改。

    3.  运行一个嵌套循环并遍历矩阵。 如果矩阵的元素等于*，则不会*，如果相邻元素的值等于 1，即不腐烂，则将相邻元素分配为 no + 1，即更新为 true。

    4.  遍历矩阵并检查是否有任何一个单元格为 1。如果存在 1，则返回-1

    5.  其他返回– 2

*   **实施**：[

## CPP14

```

// C++ program to rot all oranges when u can move
// in all the four direction from a rotten orange
#include <bits/stdc++.h>
using namespace std;

const int R = 3;
const int C = 5;

// Check if i, j is under the array limits of row and column
bool issafe(int i, int j)
{
    if (i >= 0 && i < R && j >= 0 && j < C)
        return true;
    return false;
}

int rotOranges(int v[R][C])
{
    bool changed = false;
    int no = 2;
    while (true) {
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {

                // Rot all other oranges present at
                // (i+1, j), (i, j-1), (i, j+1), (i-1, j)
                if (v[i][j] == no) {
                    if (issafe(i + 1, j) && v[i + 1][j] == 1) {
                        v[i + 1][j] = v[i][j] + 1;
                        changed = true;
                    }
                    if (issafe(i, j + 1) && v[i][j + 1] == 1) {
                        v[i][j + 1] = v[i][j] + 1;
                        changed = true;
                    }
                    if (issafe(i - 1, j) && v[i - 1][j] == 1) {
                        v[i - 1][j] = v[i][j] + 1;
                        changed = true;
                    }
                    if (issafe(i, j - 1) && v[i][j - 1] == 1) {
                        v[i][j - 1] = v[i][j] + 1;
                        changed = true;
                    }
                }
            }
        }

        // if no rotten orange found it means all
        // oranges rottened now
        if (!changed)
            break;
        changed = false;
        no++;
    }

    for (int i = 0; i < R; i++) {
        for (int j = 0; j < C; j++) {

            // if any orange is found to be
            // not rotten then ans is not possible
            if (v[i][j] == 1)
                return -1;
        }
    }

    // Because initial value for a rotten
    // orange was 2
    return no - 2;
}

// Driver function
int main()
{

    int v[R][C] = { { 2, 1, 0, 2, 1 },
                    { 1, 0, 1, 2, 1 },
                    { 1, 0, 0, 2, 1 } };

    cout << "Max time incurred: " << rotOranges(v);

    return 0;
}

```

## Python

```py

# Python3 program to rot all 
# oranges when u can move
# in all the four direction 
# from a rotten orang
R = 3
C = 5

# Check if i, j is under the
# array limits of row and 
# column
def issafe(i, j):

    if (i >= 0 and i < R and
        j >= 0 and j < C):
        return True
    return False

def rotOranges(v):

    changed = False
    no = 2
    while (True):
        for i in range(R):
            for j in range(C):

                # Rot all other oranges
                # present at (i+1, j), 
                # (i, j-1), (i, j+1), 
                # (i-1, j)
                if (v[i][j] == no):
                    if (issafe(i + 1, j) and
                        v[i + 1][j] == 1):
                        v[i + 1][j] = v[i][j] + 1
                        changed = True

                    if (issafe(i, j + 1) and
                        v[i][j + 1] == 1):
                        v[i][j + 1] = v[i][j] + 1
                        changed = True

                    if (issafe(i - 1, j) and
                        v[i - 1][j] == 1):
                        v[i - 1][j] = v[i][j] + 1
                        changed = True

                    if (issafe(i, j - 1) and
                        v[i][j - 1] == 1):
                        v[i][j - 1] = v[i][j] + 1
                        changed = True

        # if no rotten orange found 
        # it means all oranges rottened
        # now
        if (not changed):
           break
        changed = False
        no += 1

    for i in range(R):
        for j in range(C):

            # if any orange is found
            # to be not rotten then 
            # ans is not possible
            if (v[i][j] == 1):
                return -1

    # Because initial value
    # for a rotten orange was 2
    return no - 2

# Driver function
if __name__ == "__main__":

    v = [[2, 1, 0, 2, 1],
         [1, 0, 1, 2, 1],
         [1, 0, 0, 2, 1]]

    print("Max time incurred: ",
           rotOranges(v))

# This code is contributed by Chitranayal

```

**Output:** 

```
Max time incurred: 2

```

*   **复杂度分析**：

    *   **时间复杂度**：O（max（R，C）* R * C）。

        矩阵需要反复遍历，直到矩阵没有变化为止，这可能发生 max（R，C）次。 因此，时间复杂度为 O（max（R，C）* R * C）。

    *   **空间复杂度**：`O(1)`。

        不需要多余的空间。

**<u>有效解决方案</u>**

*   **方法**：的想法是使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)。 橘子变烂的条件是当它们与其他烂橘子接触时。 这类似于广度优先搜索，在该搜索中，图形被分为层或圆，并且搜索从较低或较近的层到较深或较高的层进行。 在以前的方法中，该想法基于 BFS，但实现起来很差且效率低下。 为了找到其值为*而不是*的元素，必须遍历整个矩阵。 因此，使用这种 BFS 的有效方法可以减少时间。

*   **算法**：

    1.  创建一个空队列 *Q* 。

        1.  找到所有烂橙并将其排队到 Q。此外，排队一个定界符以指示下一个时间范围的开始。

        2.  Q 不为空时运行循环

        3.  在未达到 Q 的定界符时执行以下操作

    2.  从队列中取出一个橙色，将所有相邻的橙色腐烂。 在腐烂相邻对象时，请确保时间范围仅增加一次。 如果没有相邻的橙子，则时间范围不会增加。

    3.  使旧的定界符出队，并使新的定界符入队。 在上一个时间范围内烂掉的橙子位于两个定界符之间。

*   **以上方法的空运行**：[

![](img/12c909a5ec6a114a5aff7c3b8cb94792.png)

*   **实施**：[

## C++

```cpp

// C++ program to find minimum time required to make all
// oranges rotten
#include<bits/stdc++.h>
#define R 3
#define C 5
using namespace std;

// function to check whether a cell is valid / invalid
bool isvalid(int i, int j)
{
    return (i >= 0 && j >= 0 && i < R && j < C);
}

// structure for storing coordinates of the cell
struct ele {
    int x, y;
};

// Function to check whether the cell is delimiter
// which is (-1, -1)
bool isdelim(ele temp)
{
    return (temp.x == -1 && temp.y == -1);
}

// Function to check whether there is still a fresh
// orange remaining
bool checkall(int arr[][C])
{
    for (int i=0; i<R; i++)
       for (int j=0; j<C; j++)
          if (arr[i][j] == 1)
             return true;
    return false;
}

// This function finds if it is possible to rot all oranges or not.
// If possible, then it returns minimum time required to rot all,
// otherwise returns -1
int rotOranges(int arr[][C])
{
    // Create a queue of cells
    queue<ele> Q;
    ele temp;
    int ans = 0;

    // Store all the cells having rotten orange in first time frame
    for (int i=0; i<R; i++)
    {
       for (int j=0; j<C; j++)
       {
            if (arr[i][j] == 2)
            {
                temp.x = i;
                temp.y = j;
                Q.push(temp);
            }
        }
    }

    // Separate these rotten oranges from the oranges which will rotten
    // due the oranges in first time frame using delimiter which is (-1, -1)
    temp.x = -1;
    temp.y = -1;
    Q.push(temp);

    // Process the grid while there are rotten oranges in the Queue
    while (!Q.empty())
    {
        // This flag is used to determine whether even a single fresh
        // orange gets rotten due to rotten oranges in current time
        // frame so we can increase the count of the required time.
        bool flag = false;

        // Process all the rotten oranges in current time frame.
        while (!isdelim(Q.front()))
        {
            temp = Q.front();

            // Check right adjacent cell that if it can be rotten
            if (isvalid(temp.x+1, temp.y) && arr[temp.x+1][temp.y] == 1)
            {
                // if this is the first orange to get rotten, increase
                // count and set the flag.
                if (!flag) ans++, flag = true;

                // Make the orange rotten
                arr[temp.x+1][temp.y] = 2;

                // push the adjacent orange to Queue
                temp.x++;
                Q.push(temp);

                temp.x--; // Move back to current cell
            }

            // Check left adjacent cell that if it can be rotten
            if (isvalid(temp.x-1, temp.y) && arr[temp.x-1][temp.y] == 1) {
                if (!flag) ans++, flag = true;
                arr[temp.x-1][temp.y] = 2;
                temp.x--;
                Q.push(temp); // push this cell to Queue
                temp.x++;
            }

            // Check top adjacent cell that if it can be rotten
            if (isvalid(temp.x, temp.y+1) && arr[temp.x][temp.y+1] == 1) {
                if (!flag) ans++, flag = true;
                arr[temp.x][temp.y+1] = 2;
                temp.y++;
                Q.push(temp); // Push this cell to Queue
                temp.y--;
            }

            // Check bottom adjacent cell if it can be rotten
            if (isvalid(temp.x, temp.y-1) && arr[temp.x][temp.y-1] == 1) {
                if (!flag) ans++, flag = true;
                arr[temp.x][temp.y-1] = 2;
                temp.y--;
                Q.push(temp); // push this cell to Queue
            }

            Q.pop();
        }

        // Pop the delimiter
        Q.pop();

        // If oranges were rotten in current frame than separate the
        // rotten oranges using delimiter for the next frame for processing.
        if (!Q.empty()) {
            temp.x = -1;
            temp.y = -1;
            Q.push(temp);
        }

        // If Queue was empty than no rotten oranges left to process so exit
    }

    // Return -1 if all arranges could not rot, otherwise -1.
    return (checkall(arr))? -1: ans;
}

// Driver program
int main()
{
    int arr[][C] = { {2, 1, 0, 2, 1},
                     {1, 0, 1, 2, 1},
                     {1, 0, 0, 2, 1}};
    int ans = rotOranges(arr);
    if (ans == -1)
        cout << "All oranges cannot rotn";
    else
         cout << "Time required for all oranges to rot => " << ans << endl;
    return 0;
}

```

## Java

```java

//Java program to find minimum time required to make all
//oranges rotten

import java.util.LinkedList;
import java.util.Queue;

public class RotOrange 
{
    public final static int R = 3;
    public final static int C = 5;

    // structure for storing coordinates of the cell
    static class Ele
    {
        int x = 0;
        int y = 0;
        Ele(int x,int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // function to check whether a cell is valid / invalid
    static boolean isValid(int i, int j)
    {
        return (i >= 0 && j >= 0 && i < R && j < C);
    }

    // Function to check whether the cell is delimiter
    // which is (-1, -1)
    static boolean isDelim(Ele temp)
    {
        return (temp.x == -1 && temp.y == -1);
    }

    // Function to check whether there is still a fresh
    // orange remaining
    static boolean checkAll(int arr[][])
    {
         for (int i=0; i<R; i++)
               for (int j=0; j<C; j++)
                  if (arr[i][j] == 1)
                     return true;
         return false;
    }

    // This function finds if it is possible to rot all oranges or not.
    // If possible, then it returns minimum time required to rot all,
    // otherwise returns -1
    static int rotOranges(int arr[][])
    {
        // Create a queue of cells
        Queue<Ele> Q=new LinkedList<>();
        Ele temp; 
        int ans = 0;
         // Store all the cells having rotten orange in first time frame
        for (int i=0; i < R; i++)
           for (int j=0; j < C; j++)
               if (arr[i][j] == 2)
                   Q.add(new Ele(i,j));

        // Separate these rotten oranges from the oranges which will rotten
        // due the oranges in first time frame using delimiter which is (-1, -1)
        Q.add(new Ele(-1,-1));

        // Process the grid while there are rotten oranges in the Queue
        while(!Q.isEmpty())
        {
            // This flag is used to determine whether even a single fresh
            // orange gets rotten due to rotten oranges in the current time
            // frame so we can increase the count of the required time.
            boolean flag = false;

            // Process all the rotten oranges in current time frame.
            while(!isDelim(Q.peek()))
            {
                temp = Q.peek();

                // Check right adjacent cell that if it can be rotten
                if(isValid(temp.x+1, temp.y) && arr[temp.x+1][temp.y] == 1)
                {
                    if(!flag)
                    {
                        // if this is the first orange to get rotten, increase
                        // count and set the flag.
                        ans++;
                        flag = true;
                    }
                    // Make the orange rotten
                    arr[temp.x+1][temp.y] = 2;

                    // push the adjacent orange to Queue
                    temp.x++;
                    Q.add(new Ele(temp.x,temp.y));

                    // Move back to current cell
                    temp.x--;
                }

                // Check left adjacent cell that if it can be rotten
                if (isValid(temp.x-1, temp.y) && arr[temp.x-1][temp.y] == 1)
                 {
                        if (!flag)
                        {
                            ans++;
                            flag = true;
                        }
                        arr[temp.x-1][temp.y] = 2;
                        temp.x--;
                        Q.add(new Ele(temp.x,temp.y)); // push this cell to Queue
                        temp.x++;
                 }

                // Check top adjacent cell that if it can be rotten
                 if (isValid(temp.x, temp.y+1) && arr[temp.x][temp.y+1] == 1) {
                        if(!flag)
                        {
                            ans++;
                            flag = true;
                        }
                        arr[temp.x][temp.y+1] = 2;
                        temp.y++;
                        Q.add(new Ele(temp.x,temp.y)); // Push this cell to Queue
                        temp.y--;
                    }

                 // Check bottom adjacent cell if it can be rotten
                 if (isValid(temp.x, temp.y-1) && arr[temp.x][temp.y-1] == 1) 
                 {
                        if (!flag)
                        {
                            ans++;
                            flag = true;
                        }
                        arr[temp.x][temp.y-1] = 2;
                        temp.y--;
                        Q.add(new Ele(temp.x,temp.y)); // push this cell to Queue
                 }
                 Q.remove();

            }
            // Pop the delimiter
            Q.remove();

            // If oranges were rotten in current frame than separate the
            // rotten oranges using delimiter for the next frame for processing.
            if (!Q.isEmpty()) 
            {
                Q.add(new Ele(-1,-1));
            }

            // If Queue was empty than no rotten oranges left to process so exit
        }

        // Return -1 if all arranges could not rot, otherwise -1.s
        return (checkAll(arr))? -1: ans;

    }

    // Driver program
    public static void main(String[] args) 
    {
        int arr[][] = { {2, 1, 0, 2, 1},
                        {1, 0, 1, 2, 1},
                        {1, 0, 0, 2, 1}};
        int ans = rotOranges(arr);
        if(ans == -1)
            System.out.println("All oranges cannot rot");
        else
            System.out.println("Time required for all oranges to rot = " + ans);
    }

}
//This code is contributed by Sumit Ghosh

```

## C#

```cs

// C# program to find minimum time 
// required to make all oranges rotten 
using System;
using System.Collections.Generic;

class GFG
{
    public const int R = 3;
    public const int C = 5;

    // structure for storing 
    // coordinates of the cell 
    public class Ele
    {
        public int x = 0;
        public int y = 0;
        public Ele(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // function to check whether a cell
    // is valid / invalid 
    public static bool isValid(int i, int j)
    {
        return (i >= 0 && j >= 0 && 
                i < R && j < C);
    }

    // Function to check whether the cell 
    // is delimiter which is (-1, -1) 
    public static bool isDelim(Ele temp)
    {
        return (temp.x == -1 && temp.y == -1);
    }

    // Function to check whether there 
    // is still a fresh orange remaining 
    public static bool checkAll(int[][] arr)
    {
        for (int i = 0; i < R; i++)
        {
            for (int j = 0; j < C; j++)
            {
                if (arr[i][j] == 1)
                {
                    return true;
                }
            }
        }
        return false;
    }

    // This function finds if it is possible 
    // to rot all oranges or not. If possible,
    // then it returns minimum time required 
    // to rot all, otherwise returns -1 
    public static int rotOranges(int[][] arr)
    {
        // Create a queue of cells 
        LinkedList<Ele> Q = new LinkedList<Ele>();
        Ele temp;
        int ans = 0;

        // Store all the cells having rotten
        // orange in first time frame 
        for (int i = 0; i < R; i++)
        {
        for (int j = 0; j < C; j++)
        {
            if (arr[i][j] == 2)
            {
                Q.AddLast(new Ele(i, j));
            }
        }
        }

        // Separate these rotten oranges from 
        // the oranges which will rotten 
        // due the oranges in first time frame
        // using delimiter which is (-1, -1) 
        Q.AddLast(new Ele(-1,-1));

        // Process the grid while there are 
        // rotten oranges in the Queue 
        while (Q.Count > 0)
        {
            // This flag is used to determine 
            // whether even a single fresh 
            // orange gets rotten due to rotten 
            // oranges in current time frame so
            // we can increase the count of the 
            // required time. 
            bool flag = false;

            // Process all the rotten oranges
            // in current time frame. 
            while (!isDelim(Q.First.Value))
            {
                temp = Q.First.Value;

                // Check right adjacent cell that
                // if it can be rotten 
                if (isValid(temp.x + 1, temp.y) && 
                        arr[temp.x + 1][temp.y] == 1)
                {
                    if (!flag)
                    {
                        // if this is the first orange 
                        // to get rotten, increase 
                        // count and set the flag. 
                        ans++;
                        flag = true;
                    }

                    // Make the orange rotten 
                    arr[temp.x + 1][temp.y] = 2;

                    // push the adjacent orange to Queue 
                    temp.x++;
                    Q.AddLast(new Ele(temp.x,temp.y));

                    // Move back to current cell 
                    temp.x--;
                }

                // Check left adjacent cell that 
                // if it can be rotten 
                if (isValid(temp.x - 1, temp.y) && 
                        arr[temp.x - 1][temp.y] == 1)
                {
                        if (!flag)
                        {
                            ans++;
                            flag = true;
                        }
                        arr[temp.x - 1][temp.y] = 2;
                        temp.x--;

                        // push this cell to Queue
                        Q.AddLast(new Ele(temp.x,temp.y)); 
                        temp.x++;
                }

                // Check top adjacent cell that 
                // if it can be rotten 
                if (isValid(temp.x, temp.y + 1) && 
                        arr[temp.x][temp.y + 1] == 1)
                {
                        if (!flag)
                        {
                            ans++;
                            flag = true;
                        }
                        arr[temp.x][temp.y + 1] = 2;
                        temp.y++;

                        // Push this cell to Queue
                        Q.AddLast(new Ele(temp.x,temp.y)); 
                        temp.y--;
                }

                // Check bottom adjacent cell
                // if it can be rotten 
                if (isValid(temp.x, temp.y - 1) && 
                        arr[temp.x][temp.y - 1] == 1)
                {
                        if (!flag)
                        {
                            ans++;
                            flag = true;
                        }
                        arr[temp.x][temp.y - 1] = 2;
                        temp.y--;

                        // push this cell to Queue
                        Q.AddLast(new Ele(temp.x,temp.y)); 
                }
                Q.RemoveFirst();

            }

            // Pop the delimiter 
            Q.RemoveFirst();

            // If oranges were rotten in current 
            // frame than separate the rotten 
            // oranges using delimiter for the 
            // next frame for processing. 
            if (Q.Count > 0)
            {
                Q.AddLast(new Ele(-1,-1));
            }

            // If Queue was empty than no rotten 
            // oranges left to process so exit 
        }

        // Return -1 if all arranges could
        // not rot, otherwise -1.s 
        return (checkAll(arr)) ? -1: ans;

    }

    // Driver Code 
    public static void Main(string[] args)
    {
        int[][] arr = new int[][]
        {
            new int[] {2, 1, 0, 2, 1},
            new int[] {1, 0, 1, 2, 1},
            new int[] {1, 0, 0, 2, 1}
        };

        int ans = rotOranges(arr);
        if (ans == -1)
        {
            Console.WriteLine("All oranges cannot rot");
        }
        else
        {
            Console.WriteLine("Time required for all " +
                              "oranges to rot => " + ans);
        }
    }
}

// This code is contributed by Shrikant13

```

*   **输出**：

```
Time required for all oranges to rot => 2

```

*   **复杂度分析**：

    *   **时间复杂度**：O（R * C）。

        矩阵的每个元素只能插入一次队列，因此迭代的上限为 O（R * C），即元素数。 因此，时间复杂度为 O（R * C）。

    *   **空间复杂度**：O（R * C）。

        要将元素存储在队列中，需要 O（R * C）空间。

*感谢 Gaurav Ahirwar 提出上述解决方案。*

如果发现任何不正确的内容，或者想共享有关上述

主题的更多信息，请发表评论

