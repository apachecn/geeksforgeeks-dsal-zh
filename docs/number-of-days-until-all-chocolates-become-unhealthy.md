# 所有巧克力变得不健康的天数

> 原文:[https://www . geesforgeks . org/直到所有巧克力变得不健康的天数/](https://www.geeksforgeeks.org/number-of-days-until-all-chocolates-become-unhealthy/)

帕布罗有一个 n×n 大小的方形巧克力盒，里面有各种健康的巧克力，最初用“H”表示，但他发现有些巧克力已经腐烂，不健康的用“U”表示。一天之内，这些腐烂的巧克力会让邻近的巧克力变得不健康。这种情况一直持续到巧克力盒子里的所有巧克力都变得不健康。找出整盒巧克力变得不健康的天数。
(注意:保证至少有一块巧克力是不健康的)

**示例:**

```
Input :  n = 3
         H H H
         H U H
         H H H
Output : 1
Only 1 day is required to turn all the
chocolates unhealthy in the chocolate box.

Input :  n = 4
         H H H U
         H H H H
         H U H H
         H H H H
Output : 2
Explanation:
In first day chocolate at (0, 0), (0, 1),
(2, 3), (3, 3) will remain healthy and in
the second day all the chocolates will
become unhealthy.

```

在亚马逊、雅高、Arcesium 询问。

**蛮力方法:**
初始化一个标志= 1。使用 while 循环，在 while 中搜索 h(搜索需要 O(n^2)时间复杂度如果我们在二维字符数组中找不到 h，停止递增日计数器并将标志设置为 0 以中断循环。

下面是上述方法的实现:

## C++

```
// CPP program to find number of days before
// all chocolates become unhealthy.
#include <bits/stdc++.h>
using namespace std;

// Validates out of bounds indexing
bool isValid(int i, int j, int n)
{
    if (i < 0 || j < 0 || i >= n || j >= n)
        return false;
    return true;
}

// function for returning number of days
int numdays(char arr[][4], int n)
{
    int numdays = 0;

    while (true)
    {
        // Traverse matrix to look for unhealthy
        // chocolates and mark their neighbors.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (arr[i][j] == 'U')
                {

                    if (isValid(i - 1, j - 1, n) &&
                        arr[i - 1][j - 1] == 'H')
                        arr[i - 1][j - 1] = 'V';

                    if (isValid(i - 1, j, n) &&
                        arr[i - 1][j] == 'H')
                        arr[i - 1][j] = 'V';

                    if (isValid(i - 1, j + 1, n) &&
                        arr[i - 1][j + 1] == 'H')
                        arr[i - 1][j + 1] = 'V';

                    if (isValid(i, j - 1, n) &&
                        arr[i][j - 1] == 'H')
                        arr[i][j - 1] = 'V';

                    if (isValid(i, j + 1, n) &&
                        arr[i][j + 1] == 'H')
                        arr[i][j + 1] = 'V';

                    if (isValid(i + 1, j - 1, n) &&
                        arr[i + 1][j - 1] == 'H')
                        arr[i + 1][j - 1] = 'V';

                    if (isValid(i + 1, j, n) &&
                            arr[i + 1][j] == 'H')
                        arr[i + 1][j] = 'V';

                    if (isValid(i + 1, j + 1, n) &&
                        arr[i + 1][j + 1] == 'H')
                        arr[i + 1][j + 1] = 'V';
                }

                /*Here we are assigning the neighbours of U
                with the character V because we don't want
                these neighbours to be counted in that
                particular day. If we do not do so, in the
                next iteration that neighbour will also get
                counted which was supposed to be counted in
                the next day. */
            }
        }

        // Mark chocolates unhealthy which are made
        // unhealthy in current day.
        bool Hflag = false;
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (arr[i][j] == 'V')
                {
                    arr[i][j] = 'U';
                    Hflag = true;
                }
            }
        }

        // Check if there was any chocoloate
        // marked unhealthy in current day
        if (Hflag)
            numdays++;
        else
            break;
    }
    return numdays;
}

// Driver function
int main()
{
    int n = 4;
    char arr[4][4] = { 'H', 'H', 'H', 'U',
                       'H', 'H', 'H', 'H',
                       'H', 'U', 'H', 'H',
                       'H', 'H', 'H', 'H'
                     };
    int ans = numdays(arr, n);
    cout << "number of days taken : "
         << ans << "\n";
    return 0;
}
```

## C

```
// C program to find number of days before
// all chocolates become unhealthy.
#include <stdio.h>

// Validates out of bounds indexing
int isValid(int i, int j, int n)
{
    if (i < 0 || j < 0 || i >= n || j >= n)
        return 0;
    return 1;
}

// function for returning number of days
int numdays(char arr[][4], int n)
{
    int numdays = 0;

    while (1)
    {
        // Traverse matrix to look for unhealthy
        // chocolates and mark their neighbors.
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (arr[i][j] == 'U')
                {

                    if (isValid(i - 1, j - 1, n) &&
                        arr[i - 1][j - 1] == 'H')
                        arr[i - 1][j - 1] = 'V';

                    if (isValid(i - 1, j, n) &&
                        arr[i - 1][j] == 'H')
                        arr[i - 1][j] = 'V';

                    if (isValid(i - 1, j + 1, n) &&
                        arr[i - 1][j + 1] == 'H')
                        arr[i - 1][j + 1] = 'V';

                    if (isValid(i, j - 1, n) &&
                        arr[i][j - 1] == 'H')
                        arr[i][j - 1] = 'V';

                    if (isValid(i, j + 1, n) &&
                        arr[i][j + 1] == 'H')
                        arr[i][j + 1] = 'V';

                    if (isValid(i + 1, j - 1, n) &&
                        arr[i + 1][j - 1] == 'H')
                        arr[i + 1][j - 1] = 'V';

                    if (isValid(i + 1, j, n) &&
                            arr[i + 1][j] == 'H')
                        arr[i + 1][j] = 'V';

                    if (isValid(i + 1, j + 1, n) &&
                        arr[i + 1][j + 1] == 'H')
                        arr[i + 1][j + 1] = 'V';
                }

                /*Here we are assigning the neighbours of U
                with the character V because we don't want
                these neighbours to be counted in that
                particular day. If we do not do so, in the
                next iteration that neighbour will also get
                counted which was supposed to be counted in
                the next day. */
            }
        }

        // Mark chocolates unhealthy which are made
        // unhealthy in current day.
        int Hflag = 0;
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (arr[i][j] == 'V')
                {
                    arr[i][j] = 'U';
                    Hflag = 1;
                }
            }
        }

        // Check if there was any chocoloate
        // marked unhealthy in current day
        if (Hflag)
            numdays++;
        else
            break;
    }
    return numdays;
}

// Driver Code
int main()
{
    int n = 4;
    char arr[4][4] = { 'H', 'H', 'H', 'U',
                       'H', 'H', 'H', 'H',
                       'H', 'U', 'H', 'H',
                       'H', 'H', 'H', 'H' };
    int ans = numdays(arr, n);
    printf("number of days taken : %d\n", ans);
    return 0;
}

// This code is contributed by ankush_953
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of days before
// all chocolates become unhealthy.
class GFG
{

    // Validates out of bounds indexing
    static boolean isValid(int i, int j, int n)
    {
        if (i < 0 || j < 0 || i >= n || j >= n)
            return false;
        return true;
    }

    // function for returning number of days
    static int numdays(char [][]arr, int n)
    {
        int numdays = 0;

        while (true)
        {
            // Traverse matrix to look for unhealthy
            // chocolates and mark their neighbors.
            for (int i = 0; i < n; i++)
            {
                for (int j = 0; j < n; j++)
                {
                    if (arr[i][j] == 'U')
                    {

                        if (isValid(i - 1, j - 1, n) &&
                            arr[i - 1][j - 1] == 'H')
                            arr[i - 1][j - 1] = 'V';

                        if (isValid(i - 1, j, n) &&
                            arr[i - 1][j] == 'H')
                            arr[i - 1][j] = 'V';

                        if (isValid(i - 1, j + 1, n) &&
                            arr[i - 1][j + 1] == 'H')
                            arr[i - 1][j + 1] = 'V';

                        if (isValid(i, j - 1, n) &&
                            arr[i][j - 1] == 'H')
                            arr[i][j - 1] = 'V';

                        if (isValid(i, j + 1, n) &&
                            arr[i][j + 1] == 'H')
                            arr[i][j + 1] = 'V';

                        if (isValid(i + 1, j - 1, n) &&
                            arr[i + 1][j - 1] == 'H')
                            arr[i + 1][j - 1] = 'V';

                        if (isValid(i + 1, j, n) &&
                                arr[i + 1][j] == 'H')
                            arr[i + 1][j] = 'V';

                        if (isValid(i + 1, j + 1, n) &&
                            arr[i + 1][j + 1] == 'H')
                            arr[i + 1][j + 1] = 'V';
                    }

                    /*Here we are assigning the neighbours of U
                    with the character V because we don't want
                    these neighbours to be counted in that
                    particular day. If we do not do so, in the
                    next iteration that neighbour will also get
                    counted which was supposed to be counted in
                    the next day. */
                }
            }

            // Mark chocolates unhealthy which are made
            // unhealthy in current day.
            boolean Hflag = false;
            for (int i = 0; i < n; i++)
            {
                for (int j = 0; j < n; j++)
                {
                    if (arr[i][j] == 'V')
                    {
                        arr[i][j] = 'U';
                        Hflag = true;
                    }
                }
            }

            // Check if there was any chocoloate
            // marked unhealthy in current day
            if (Hflag)
                numdays++;
            else
                break;
        }
        return numdays;
    }

    // Driver Code
    public static void main(String []args)
    {
        int n = 4;
        char [][]arr = {{'H', 'H', 'H', 'U'},
                        {'H', 'H', 'H', 'H'},
                        {'H', 'U', 'H', 'H'},
                        {'H', 'H', 'H', 'H'}};
        int ans = numdays(arr, n);
        System.out.println("number of days taken : " + ans);
    }

}

// This code is contributed by ankush_953
```

## 蟒蛇 3

```
# Python3 program to find number of days before
# all chocolates become unhealthy.

# Validates out of bounds indexing
def isValid(i, j, n):
    if (i < 0 or j < 0 or i >= n or j >= n):
        return False
    return True

# function for returning number of days
def numdays(arr, n):
    numdays = 0
    while (True):

        # Traverse matrix to look for unhealthy
        # chocolates and mark their neighbors.
        for i in range(n):
            for j in range(n):
                if (arr[i][j] == 'U'):
                    if (isValid(i - 1, j - 1, n) and\
                        arr[i - 1][j - 1] == 'H'):
                        arr[i - 1][j - 1] = 'V'

                    if (isValid(i - 1, j, n) and\
                        arr[i - 1][j] == 'H'):
                        arr[i - 1][j] = 'V'

                    if (isValid(i - 1, j + 1, n) and\
                        arr[i - 1][j + 1] == 'H'):
                        arr[i - 1][j + 1] = 'V'

                    if (isValid(i, j - 1, n) and\
                        arr[i][j - 1] == 'H'):
                        arr[i][j - 1] = 'V'

                    if (isValid(i, j + 1, n) and\
                        arr[i][j + 1] == 'H'):
                        arr[i][j + 1] = 'V'

                    if (isValid(i + 1, j - 1, n) and\
                        arr[i + 1][j - 1] == 'H'):
                        arr[i + 1][j - 1] = 'V'

                    if (isValid(i + 1, j, n) and\
                        arr[i + 1][j] == 'H'):
                        arr[i + 1][j] = 'V'

                    if (isValid(i + 1, j + 1, n) and\
                        arr[i + 1][j + 1] == 'H'):
                        arr[i + 1][j + 1] = 'V'

                # Here we are assigning the neighbours of U
                # with the character V because we don't want
                # these neighbours to be counted in that
                # particular day. If we do not do so, in the
                # next iteration that neighbour will also get
                # counted which was supposed to be counted in
                # the next day.

        # Mark chocolates unhealthy which are made
        # unhealthy in current day.
        Hflag = False
        for i in range(n):
            for j in range(n):
                if (arr[i][j] == 'V'):
                    arr[i][j] = 'U'
                    Hflag = True

        # Check if there was any chocoloate
        # marked unhealthy in current day
        if (Hflag):
            numdays += 1
        else:
            break

    return numdays

# Driver Code
n = 4
arr = [['H', 'H', 'H', 'U'],
       ['H', 'H', 'H', 'H'],
       ['H', 'U', 'H', 'H'],
       ['H', 'H', 'H', 'H']]
ans = numdays(arr, n)
print("number of days taken :", ans)

# This code is contributed by ankush_953
```

## C#

```
// C# program to find number of days before
// all chocolates become unhealthy.
using System;

class GFG{

    // Validates out of bounds indexing
    static bool isValid(int i, int j, int n)
    {
        if (i < 0 || j < 0 || i >= n || j >= n)
            return false;
        return true;
    }

    // function for returning number of days
    static int numdays(char[][] arr, int n)
    {
        int numdays = 0;

        while (true)
        {
            // Traverse matrix to look for unhealthy
            // chocolates and mark their neighbors.
            for (int i = 0; i < n; i++)
            {
                for (int j = 0; j < n; j++)
                {
                    if (arr[i][j] == 'U')
                    {

                        if (isValid(i - 1, j - 1, n) &&
                            arr[i - 1][j - 1] == 'H')
                            arr[i - 1][j - 1] = 'V';

                        if (isValid(i - 1, j, n) &&
                            arr[i - 1][j] == 'H')
                            arr[i - 1][j] = 'V';

                        if (isValid(i - 1, j + 1, n) &&
                            arr[i - 1][j + 1] == 'H')
                            arr[i - 1][j + 1] = 'V';

                        if (isValid(i, j - 1, n) &&
                            arr[i][j - 1] == 'H')
                            arr[i][j - 1] = 'V';

                        if (isValid(i, j + 1, n) &&
                            arr[i][j + 1] == 'H')
                            arr[i][j + 1] = 'V';

                        if (isValid(i + 1, j - 1, n) &&
                            arr[i + 1][j - 1] == 'H')
                            arr[i + 1][j - 1] = 'V';

                        if (isValid(i + 1, j, n) &&
                                arr[i + 1][j] == 'H')
                            arr[i + 1][j] = 'V';

                        if (isValid(i + 1, j + 1, n) &&
                            arr[i + 1][j + 1] == 'H')
                            arr[i + 1][j + 1] = 'V';
                    }

                    /*Here we are assigning the neighbours of U
                    with the character V because we don't want
                    these neighbours to be counted in that
                    particular day. If we do not do so, in the
                    next iteration that neighbour will also get
                    counted which was supposed to be counted in
                    the next day. */
                }
            }

            // Mark chocolates unhealthy which are made
            // unhealthy in current day.
            bool Hflag = false;
            for (int i = 0; i < n; i++)
            {
                for (int j = 0; j < n; j++)
                {
                    if (arr[i][j] == 'V')
                    {
                        arr[i][j] = 'U';
                        Hflag = true;
                    }
                }
            }

            // Check if there was any chocoloate
            // marked unhealthy in current day
            if (Hflag)
                numdays++;
            else
                break;
        }
        return numdays;
    }

    // Driver function
    static public void Main ()
    {
        int n = 4;
        char[][] arr = new char[][]{"HHHU".ToCharArray(),
                        "HHHH".ToCharArray(),
                        "HUHH".ToCharArray(),
                        "HHHH".ToCharArray()};
        int ans = numdays(arr, n);
        Console.WriteLine("number of days taken : "+ ans);
    }
}

// This code is contributed by shubhamsingh10
```

 **Output:**

```
 number of days taken : 2

```

**高效方法(使用 BFS)**
在这种方法中，声明一个队列，该队列输入对应于不健康巧克力索引的配对，然后一旦索引(-1，-1)达到，我们就递增 numdays 计数器。该解决方案基本上基于计算二叉树的级别顺序遍历(迭代版本)中的级别，其中我们推送不健康巧克力的初始索引而不是根节点，并且一旦达到索引(-1，-1)而不是空值，就递增 numdays 而不是级别计数器。一旦标志的计数器达到 2，我们就中断循环，表示队列已经编码了两个连续的(-1，-1)对。

下面是上述方法的实现:

## C++

```
// CPP program using Efficient approach
// to find number of days
#include <bits/stdc++.h>
using namespace std;

// Validates out of bounds indexing
bool isValid(int i, int j, int n)
{
    if (i < 0 || j < 0 || i >= n || j >= n)
        return false;
    return true;
}

// function for returning number of days
int numdays(char arr[][4], int n)
{
    int numdays = 0;
    int i, j;
    queue<pair<int, int> > q;

    // Initializing queue with initial
    // positions of unhealthy chocolates
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++) {
            if (arr[i][j] == 'U')
                q.push(make_pair(i, j));
        }

    q.push(make_pair(-1, -1));

    // (-1, -1) is used as a checkpoint
    // to count the number of days
    pair<int, int> temp;

    // temporary pair to store the indexes
    int flag = 0;
    while (!q.empty()) {
        temp = q.front();
        i = temp.first;
        j = temp.second;
        q.pop();
        if (i == -1 && j == -1) {
            flag++;
            q.push(make_pair(-1, -1));

            // pushing the respective
           // checkpoint
            if (flag == 2)
                break;
            numdays++;
        }
        else {
            flag = 0;
            if (isValid(i - 1, j - 1, n) &&
                arr[i - 1][j - 1] == 'H') {
                q.push(make_pair(i - 1, j - 1));
                arr[i - 1][j - 1] = 'U';
            }

            if (isValid(i - 1, j, n) &&
                arr[i - 1][j] == 'H') {
                q.push(make_pair(i - 1, j));
                arr[i - 1][j] = 'U';
            }

            if (isValid(i - 1, j + 1, n) &&
                arr[i - 1][j + 1] == 'H') {
                q.push(make_pair(i - 1, j + 1));
                arr[i - 1][j + 1] = 'U';
            }

            if (isValid(i, j - 1, n) &&
                arr[i][j - 1] == 'H') {
                q.push(make_pair(i, j - 1));
                arr[i][j - 1] = 'U';
            }

            if (isValid(i, j + 1, n) &&
                arr[i][j + 1] == 'H') {
                q.push(make_pair(i, j + 1));
                arr[i][j + 1] = 'U';
            }

            if (isValid(i + 1, j - 1, n) &&
                arr[i + 1][j - 1] == 'H') {
                q.push(make_pair(i + 1, j - 1));
                arr[i + 1][j - 1] = 'U';
            }

            if (isValid(i + 1, j, n) &&
                arr[i + 1][j] == 'H') {
                q.push(make_pair(i + 1, j));
                arr[i + 1][j] = 'U';
            }

            if (isValid(i + 1, j + 1, n) &&
                arr[i + 1][j + 1] == 'H') {
                q.push(make_pair(i + 1, j + 1));
                arr[i + 1][j + 1] = 'U';
            }
        }
    }

    return numdays - 1;
}

// Driver function
int main()
{
    int n = 4;
    char arr[4][4] = { 'H', 'H', 'H', 'U',
                       'H', 'H', 'H', 'H',
                       'H', 'H', 'U', 'H',
                       'H', 'H', 'H', 'H' };
    int ans = numdays(arr, n);
    cout << "number of days taken : "
         << ans << "\n";
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program using Efficient approach
# to find number of days

# Validates out of bounds indexing
def isValid(i, j, n):
    if (i < 0 or j < 0 or i >= n or j >= n):
        return False
    return True

# function for returning number of days
def numdays(arr, n):

    numdays = 0
    i = 0
    j = 0
    q = []

    # Initializing queue with initial
    # positions of unhealthy chocolates
    for i in range(n):
        for j in range(n):
            if (arr[i][j] == 'U'):
                q.append([i, j])

    q.append([-1, -1])

    # (-1, -1) is used as a checkpo
    # to count the number of days
    temp = []

    # temporary pair to store the indexes
    flag = 0
    while (len(q)):
        temp = q[0]
        i = temp[0]
        j = temp[1]
        q.pop(0)
        if (i == -1 and j == -1):
            flag += 1
            q.append([-1, -1])

            # appending the respective
            # checkpo
            if (flag == 2):
                break
            numdays += 1
        else:

            flag = 0
            if (isValid(i - 1, j - 1, n) and arr[i - 1][j - 1] == 'H'):
                q.append([i - 1, j - 1])
                arr[i - 1][j - 1] = 'U'

            if (isValid(i - 1, j, n) and arr[i - 1][j] == 'H'):
                q.append([i - 1, j])
                arr[i - 1][j] = 'U'

            if (isValid(i - 1, j + 1, n) and arr[i - 1][j + 1] == 'H'):
                q.append([i - 1, j + 1])
                arr[i - 1][j + 1] = 'U'

            if (isValid(i, j - 1, n) and arr[i][j - 1] == 'H'):
                q.append([i, j - 1])
                arr[i][j - 1] = 'U'

            if (isValid(i, j + 1, n) and arr[i][j + 1] == 'H'):
                q.append([i, j + 1])
                arr[i][j + 1] = 'U'

            if (isValid(i + 1, j - 1, n) and arr[i + 1][j - 1] == 'H'):
                q.append([i + 1, j - 1])
                arr[i + 1][j - 1] = 'U'

            if (isValid(i + 1, j, n) and arr[i + 1][j] == 'H'):
                q.append([i + 1, j])
                arr[i + 1][j] = 'U'

            if (isValid(i + 1, j + 1, n) and arr[i + 1][j + 1] == 'H'):
                q.append([i + 1, j + 1])
                arr[i + 1][j + 1] = 'U'

    return numdays - 1

# Driver function
n = 4
arr = [['H', 'H', 'H', 'U'],['H', 'H', 'H', 'H'],
        ['H', 'H', 'U', 'H'],['H', 'H', 'H', 'H']] 
ans = numdays(arr, n)
print("number of days taken :",ans)

# This code is contributed by shubhamsingh10
```

Output:

```
number of days taken : 2

```