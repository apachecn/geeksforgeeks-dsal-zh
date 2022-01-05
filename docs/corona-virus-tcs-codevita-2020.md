# 冠状病毒| TCS code life 2020

> 哎哎哎::1230【https://www . geeksforgeeks . org/corona 病毒-TCS-code life-2020/

**问题描述:**

城市被表示为二维矩形矩阵。给定矩阵的外墙表示城市的边界。市民分散在城市的不同地点。要么用 **{a，c}** 来描述。冠状病毒已经感染了这座城市。

冠状病毒从坐标 **(0，0)** 进入城市，沿着对角线路径穿越，直到遇到人类。如果它遇到一个人，指定为 **a** ，它的轨迹逆时针(从右到左)旋转 **90 度**。同样，如果它遇到一个人，指定为 **c** ，它的轨迹顺时针(从左到右)旋转 **90 度**。在感染人之后，病毒继续沿着它的对角线路径移动。

在它的穿越过程中，如果第一次碰到城市的边界，它会旋转 **90 度**重新进入城市。然而，如果它第二次击中任何一面边界墙，病毒就会被消灭。

你要计算病毒所走的轨迹，打印出可以找到被感染市民的城市地图，最后报告安全和被感染市民的数量。

**输入:**

由字符“*****、**“a”**、**“c”**、**”组成的 9 行**、 **20 列**的输入矩阵在哪里

*   **“***表示城市边界上的元素
*   **“a”**表示遇到病毒轨迹变化 **90 度**(逆时针方向)的市民
*   **“c”**表示遇到病毒轨迹变化 **90 度**(顺时针方向)的市民
*   **。”**(点)表示城市内的一个空位置

**输出:**

一组随机的线，每条线表示病毒轨迹的坐标。

从下一行开始，输出 9 行和 20 列**的矩阵**，由字符“*****、**、【a】、**、**、【c】、**、**组成。**和**“-”**在哪里

*   **“***表示城市边界上的元素
*   **“a”**表示遇到病毒轨迹变化 **90 度**(逆时针方向)的市民
*   **“c”**表示遇到病毒轨迹变化 **90 度**(顺时针方向)的市民
*   **。”**(点)表示城市中的一个空位置
*   **“-”**表示受感染公民的位置

接下来的两行打印了该市安全和感染的公民人数。

**约束:**

*   0 <= x <= 20
*   0 <= y <= 8
*   病毒无法击中三个角(20，8) (20，0) (0，8)

**示例:**

> **输入:**
> * * * * * * * * * * * * * * * * *
> *…。c……*
> *…c……..*
> *c……..*
> *…………。a…*
> * c . c …………*
> *。a………。*
> *………..c …*
> * * * * * * * * * * * * * * * * * *输出:
> **0 0
> 1 1
> 2 2
> 1 3
> 2 4
> 3 5
> 4 6
> 5
> 6 4
> 7 3
> 8 2
> 9 1
> 10 0
> 11
> 12 2
> 13【3c……*
> *……-………..*
> *c………..*
> *…………。-….*
> *-。c ………*
> *。-…………….*
> *………..c……*
> ****************安全=4
> 感染=4
> **说明:**病毒轨迹从(0，0)开始，穿越(1，1) (2，2)。在(2，2)我们有一个 a 型公民导致病毒轨迹逆时针旋转 90 度。它会移动，直到在 c 型的(1，3)处遇到其路径中的下一个市民，导致病毒轨迹顺时针旋转 90 度。它继续它的路径，直到它到达 c 型病毒轨迹(4，6)的路径中的下一个人。它再次顺时针旋转 90 度，直到它到达(10，0)的边界。由于这是病毒第一次撞击边界，它逆时针旋转 90 度重新进入城市。然后，轨迹继续朝着(11，1) (12，2) (13，3)前进，最后，a 型的公民(14，4)将轨迹逆时针旋转 90 度。从那里，它继续它的轨迹，并在(10，8)处到达边界。
> 由于这是病毒第二次触及边界，病毒被消灭。
> 因此，沿着从(0，0)开始的轨迹，它已经在位置(2，2) (1，3) (4，6) (14，4)感染了 4 名公民。其他 4 名没有进入病毒轨迹的公民被认为是安全的。**
> 
> **输入:**
> * * * * * * * * * * * * * * * * *
> *……………………*
> *..c ………*
> *……。c……*
> *……a……..*
> *………………*
> *……。a……c……*
> *…………*
> * * * * * * * * * * * * * * *输出:
> **输出:**T14】0 0
> 1 1
> 2 2
> 3 3
> 4 4
> 5
> 6 4
> 7 3
> 8 2
> 9 3
> 10 4
> 9 5
> 8 6
> 7
> ..c ………*
> *……。-………….*
> *…………-……..*
> *………………*
> *……。-……c……*
> *……………………*
> * * * * * * * * * * * * * * *安全=2
> 感染=3
> **解释:**病毒轨迹从(0，0)开始，穿过(1，1) (2，2) (5，5)。在(5，5)我们有一个 c 型公民导致病毒轨迹顺时针旋转 90 度。它会移动，直到在 a 型的(8，2)处遇到其路径中的下一个市民，导致病毒轨迹逆时针旋转 90 度。它继续它的路径，直到它到达它的路径中的下一个人。a 型病毒的轨迹再次顺时针旋转 90 度，直到它到达(6，8)处的边界。由于这是病毒第一次撞击边界，它逆时针旋转 90 度重新进入城市。然后，轨迹继续朝着(9，5) (8，6) (7，7) (6，8)移动，并通过逆时针旋转轨迹 90 度来跟随轨迹(5，7) (4，6) (3，5) (2，4) (1，3) (0，2)来租用城市。
> 在(0，2)它再次击中边界，由于这是病毒第二次击中边界，病毒被消灭。所以沿着从(0，0)开始的轨迹，它已经在位置(5，5) (10，4) (8，2)感染了 3 个市民。其他 2 名没有进入病毒轨迹的公民被认为是安全的。

**方法:**解决这个问题的思路是先将输入表示的图进行反求，[根据给定的条件遍历图](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)。按照以下步骤解决问题:

*   首先，将输入数组反转为反转数组。所以最后一行变成第一行，第二行变成最后一行，以此类推。这样做是为了在二维坐标系中查看图形，正 **x** 和 **y** 。
*   遍历图表，跟踪病毒在名为**的变量中到达边界的次数，并运行 while 循环，直到该变量的值小于或等于 **1** 。**
*   初始化一个变量，**指示**，保持运动方向为:
    *   如果 direct 为 1，则方向为东北方向。
    *   如果 direct 为 2，则方向为西北方向。
    *   如果直达是 3，方向是东南。
    *   如果 direct 是 4，方向是西南方向。
*   病毒将有 4 个运动方向。病毒将从顶点 **(0，0)** 开始，运动方向为 **1** (向东北方向移动)。当遇到墙时，变量的方向会改变。
*   此外，当遇到**‘a’**时，将**的值直接**更改为产生的逆时针方向，当遇到**‘c’**时，将**的值直接**更改为与当前方向顺时针 90 度。
*   对于**’”矩阵中的**(点)字符，通过 **1** 继续增加或减少当前位置变量，以沿**方向的对角线移动**变量的描绘方向。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define row 9
#define col 20

// Function to print trajectory of the virus
// and safe and infected citizens
void coronaVirus(char arr[row][col])
{

    // To store Inverted Array
    char inverted[9][20];

    // Temporary array to store
    // original array
    char temp[9][20];

    // To store number of infected citizens
    int count = 0;

    // To store total number of citizens ('a', 'c')
    int total = 0;

    // To invert the array
    for (int i = 0; i <= 8; i++) {
        for (int j = 0; j < 20; j++) {

            // Invert the array row wise
            inverted[i][j] = arr[8 - i][j];
        }
    }

    // Count the number of citiens
    for (int i = 0; i <= 8; i++) {
        for (int j = 0; j < 20; j++) {

            // Count total number of citizens.
            if (inverted[i][j] == 'a'
                || inverted[i][j] == 'c') {
                total++;
            }

            // Copy inverted array in temp
            temp[i][j] = inverted[i][j];
        }
    }

    // To store number of times,
    // virus encountered a boundary
    int bound = 0;

    // Variable for row-wise traversal
    int i = 1;

    // Variable for column-wise traversal
    int j = 1;

    // Variable to store direction
    int direct = 1;

    // The virus starts from (0, 0) always
    cout << "0 0" << endl;

    // To break infinite looping
    int flag = 0;

    // Finding trajectory and safe
    // and infected citizens
    while (bound <= 1 && flag < 1000) {
        flag++;
        cout << i << " " << j << endl;

        // Virus has striked the boundary twice.
        // Therefore, end loop
        if (inverted[j][i] == '*' && bound == 1) {
            break;
        }

        // Virus striked the corners, end loop
        if (inverted[j][i] == '*') {
            if (i == 0 && j == 8 || i == 20 && j == 8
                || i == 20 && j == 0) {
                break;
            }
        }

        // First time for the virus
        // to hit the boundary
        if (inverted[j][i] == '*' && bound == 0) {

            // Increment bound variable
            bound++;

            // Srikes the left wall
            if (i == 0 && j != 8 && j != 0) {

                // Turns 90 degree clockwise
                if (direct == 2) {
                    direct = 1;
                    i++;
                    j++;
                }

                // Else turns 90 degree anticlockwise
                else if (direct == 4) {
                    direct = 3;
                    j--;
                    i++;
                }
            }

            // Strikes the right wall
            else if (i == 20 && j != 0 && j != 8) {

                // Turns 90 degree anticlockwise
                if (direct == 1) {
                    direct = 2;
                    i--;
                    j++;
                }

                // Else turns 90 degree clockwise
                else if (direct == 3) {
                    direct = 4;
                    i--;
                    j--;
                }
            }

            // Strikes the upper wall
            else if (j == 8 && i != 0 && i != 20) {

                // Turns 90 degree anticlockwise
                if (direct == 2) {
                    direct = 4;
                    i--;
                    j--;
                }
                // Else turns 90 degree clockwise
                else if (direct == 1) {
                    direct = 3;
                    j--;
                    i++;
                }
            }

            // Strikes the lower wall
            else if (j == 0 && i != 0 && i != 20) {

                // Turns 90 degree clockwise
                if (direct == 4) {
                    direct = 2;
                    i--;
                    j++;
                }

                // Else turns 90 degree anticlockwise
                else if (direct == 3) {
                    direct = 1;
                    i++;
                    j++;
                }
            }
            continue;
        }

        // Make 'c' visited by replacing it by'-'
        if (inverted[j][i] == 'c') {
            temp[j][i] = '-';

            // Turns all directions 90
            // degree clockwise
            if (direct == 1) {
                direct = 3;
                j--;
                i++;
            }
            else if (direct == 2) {
                direct = 1;
                i++;
                j++;
            }
            else if (direct == 3) {
                direct = 4;
                i--;
                j--;
            }
            else if (direct == 4) {
                direct = 2;
                i--;
                j++;
            }

            // Increment count of infected citizens
            count++;
            continue;
        }

        // Make 'a' visited by replacing it by'-'
        if (inverted[j][i] == 'a') {
            temp[j][i] = '-';

            // Turns all directions by 90 degree
            // anticlockwise
            if (direct == 1) {
                direct = 2;
                i--;
                j++;
            }
            else if (direct == 2) {
                direct = 4;
                i--;
                j--;
            }
            else if (direct == 3) {
                direct = 1;
                i++;
                j++;
            }
            else if (direct == 4) {
                direct = 3;
                j--;
                i++;
            }

            // Increment count of
            // infected citizens
            count++;
            continue;
        }

        // Increment the counter diagonally
        // in the given direction.
        if (inverted[j][i] == '.') {
            if (direct == 1) {
                i++;
                j++;
            }
            else if (direct == 2) {
                i--;
                j++;
            }
            else if (direct == 3) {
                j--;
                i++;
            }
            else if (direct == 4) {
                i--;
                j--;
            }
            continue;
        }
    }

    // Print the mirror of the array
    // i.e. last row must be printed first.
    for (int i = 0; i <= 8; i++) {
        for (int j = 0; j < 20; j++) {
            cout << temp[8 - i][j];
        }
        cout << endl;
    }

    // Print safe and infected citizens
    cout << "safe=" << (total - count) << endl;
    cout << "infected=" << (count) << endl;
}

// Driver Code
int main()
{

    // Given 2D array
    char arr[row][col]
        = { { '*', '*', '*', '*', '*', '*', '*',
              '*', '*', '*', '*', '*', '*', '*',
              '*', '*', '*', '*', '*', '*' },
            { '*', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '*' },
            { '*', '.', '.', 'c', '.', '.', '.',
              '.', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '*' },
            { '*', '.', '.', '.', '.', 'c', '.',
              '.', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '*' },
            { '*', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', 'a', '.', '.', '.',
              '.', '.', '.', '.', '.', '*' },
            { '*', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '*' },
            { '*', '.', '.', '.', '.', '.', '.',
              '.', 'a', '.', '.', '.', '.', '.',
              '.', 'c', '.', '.', '.', '*' },
            { '*', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '.', '.',
              '.', '.', '.', '.', '.', '*' },
            { '*', '*', '*', '*', '*', '*', '*',
              '*', '*', '*', '*', '*', '*', '*',
              '*', '*', '*', '*', '*', '*' } };

    // Function Call
    coronaVirus(arr);
    return 0;
}
```

**Output:** 

```
0 0
1 1
2 2
3 3
4 4
5 5
6 4
7 3
8 2
9 3
10 4
9 5
8 6
7 7
6 8
5 7
4 6
3 5
2 4
1 3
0 2
********************
*..................*
*..c...............*
*....-.............*
*.........-........*
*..................*
*.......-......c...*
*..................*
********************
safe=2
infected=3
```

***时间复杂度:** O(R*C)其中 R 为行数，C 为列数*
***辅助空间:** O(R*C)*