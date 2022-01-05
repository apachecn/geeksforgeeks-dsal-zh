# 为了通过考试找到最大准备题目

> 原文:[https://www . geesforgeks . org/find-最多要准备的主题-为了通过考试/](https://www.geeksforgeeks.org/find-maximum-topics-to-prepare-in-order-to-pass-the-exam/)

给定三个整数 **n** 、 **h** 和 **p** ，其中 **n** 为题目数， **h** 为剩余时间(小时) **p** 为及格分。还给出了两个数组**标记[]** 和**时间[]** ，其中**标记【I】**是 **i <sup>第</sup>T21】题目的标记，**时间【I】**是学习 **i <sup>第</sup>T27】题目所需的时间。任务是通过研究最大数量的题目来找到可以获得的最大分数。
**例:****** 

> **输入:** n = 4，h = 10，p = 10，标记[] = {6，4，2，8}，时间[] = {4，6，2，7}
> **输出:** 10
> 可以准备带标记【2】和标记【3】
> 的题目，也可以准备标记【0】和标记【1】
> 两种情况合计 10 个标记
> ，等于及格分。
> **输入:** n = 5，h = 40，p = 21，mark[]= { 10，10，10，10，3}，time[] = {12，16，20，24，8}
> **输出:** 36

**方法:**给定的问题是 [0/1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)的修改版本，在这个版本中，我们要么考虑拿一个包，要么忽略那个包。
这个问题的变化是给我们一个特定题目所用时间和考试最大剩余时间的约束条件。
**实现:**
按照 0/1 背包问题的相同方式进行，如果在给定的考试剩余时间内可以阅读某个主题，我们将考虑阅读该主题，否则忽略该主题并进入下一个主题。这样，我们将计算学生在给定时间范围内可以得分的最大加权分数总和。

*   **基础条件:**当时间为 **0** 或题目数为 **0** 时，则计算出的分数也为 **0** 。
*   如果剩余时间少于覆盖 **i <sup>th</sup>** 主题所需的时间，则忽略该主题并继续前进。
*   现在出现了两种情况(我们必须找到这两种情况的最大值)
    1.  考虑一下阅读那个主题。
    2.  忽略那个话题。
*   现在，为了找到可以达到的最高分数，我们必须回溯考虑阅读的主题路径。我们将从矩阵的左下方开始循环，如果我们已经在矩阵中考虑了，我们将继续增加主题权重。
*   现在 **T【话题-1 的数量】【总时间-1】**将包含最终标记。
*   如果最终标记小于合格标记，则打印 **-1** ，否则打印计算出的标记。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum marks
// by considering topics which can be
// completed in the given time duration
int MaximumMarks(int marksarr[], int timearr[],
                             int h, int n, int p)
{
    int no_of_topics = n + 1;
    int total_time = h + 1;

    int T[no_of_topics][total_time];

    // Initialization

    // If we are given 0 time
    // then nothing can be done
    // So all values are 0
    for (int i = 0; i < no_of_topics; i++) {
        T[i][0] = 0;
    }

    // If we are given 0 topics
    // then the time required
    // will be 0 for sure
    for (int j = 0; j < total_time; j++) {
        T[0][j] = 0;
    }

    // Calculating the maximum marks
    // that can be achieved under
    // the given time constraints
    for (int i = 1; i < no_of_topics; i++) {

        for (int j = 1; j < total_time; j++) {

            // If time taken to read that topic
            // is more than the time left now at
            // position j then do no read that topic
            if (j < timearr[i]) {

                T[i][j] = T[i - 1][j];
            }
            else {

                /*Two cases arise:
                1) Considering current topic
                2) Ignoring current topic
                We are finding maximum of (current topic weightage
                + topics which can be done in leftover time
                - current topic time)
                and ignoring current topic weightage sum
                */
                T[i][j] = max(marksarr[i]
                                  + T[i - 1][j - timearr[i]],
                              T[i - 1][j]);
            }
        }
    }

    // Moving upwards in table from bottom right
    // to calculate the total time taken to
    // read the topics which can be done in
    // given time and have highest weightage sum
    int i = no_of_topics - 1, j = total_time - 1;

    int sum = 0;

    while (i > 0 && j > 0) {

        // It means we have not considered
        // reading this topic for
        // max weightage sum
        if (T[i][j] == T[i - 1][j]) {

            i--;
        }
        else {

            // Adding the topic time
            sum += timearr[i];

            // Evaluating the left over time after
            // considering this current topic
            j -= timearr[i];

            // One topic completed
            i--;
        }
    }

    // It contains the maximum weightage sum
    // formed by considering the topics
    int marks = T[no_of_topics - 1][total_time - 1];

    // Condition when exam cannot be passed
    if (marks < p)
        return -1;

    // Return the marks that
    // can be obtained after
    // passing the exam
    return sum;
}

// Driver code
int main()
{
    // Number of topics, hours left
    // and the passing marks
    int n = 4, h = 10, p = 10;

    // n+1 is taken for simplicity in loops
    // Array will be indexed starting from 1
    int marksarr[n + 1] = { 0, 6, 4, 2, 8 };
    int timearr[n + 1] = { 0, 4, 6, 2, 7 };

    cout << MaximumMarks(marksarr, timearr, h, n, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the maximum marks
// by considering topics which can be
// completed in the given time duration
static int MaximumMarks(int marksarr[], int timearr[],
                            int h, int n, int p)
{
    int no_of_topics = n + 1;
    int total_time = h + 1;

    int T[][] = new int[no_of_topics][total_time];

    // Initialization

    // If we are given 0 time
    // then nothing can be done
    // So all values are 0
    for (int i = 0; i < no_of_topics; i++)
    {
        T[i][0] = 0;
    }

    // If we are given 0 topics
    // then the time required
    // will be 0 for sure
    for (int j = 0; j < total_time; j++)
    {
        T[0][j] = 0;
    }

    // Calculating the maximum marks
    // that can be achieved under
    // the given time constraints
    for (int i = 1; i < no_of_topics; i++)
    {

        for (int j = 1; j < total_time; j++)
        {

            // If time taken to read that topic
            // is more than the time left now at
            // position j then do no read that topic
            if (j < timearr[i])
            {

                T[i][j] = T[i - 1][j];
            }
            else
            {

                /*Two cases arise:
                1) Considering current topic
                2) Ignoring current topic
                We are finding maximum of (current topic weightage
                + topics which can be done in leftover time
                - current topic time)
                and ignoring current topic weightage sum
                */
                T[i][j] = Math.max(marksarr[i]
                                + T[i - 1][j - timearr[i]],
                            T[i - 1][j]);
            }
        }
    }

    // Moving upwards in table from bottom right
    // to calculate the total time taken to
    // read the topics which can be done in
    // given time and have highest weightage sum
    int i = no_of_topics - 1, j = total_time - 1;

    int sum = 0;

    while (i > 0 && j > 0)
    {

        // It means we have not considered
        // reading this topic for
        // max weightage sum
        if (T[i][j] == T[i - 1][j])
        {

            i--;
        }
        else
        {

            // Adding the topic time
            sum += timearr[i];

            // Evaluating the left over time after
            // considering this current topic
            j -= timearr[i];

            // One topic completed
            i--;
        }
    }

    // It contains the maximum weightage sum
    // formed by considering the topics
    int marks = T[no_of_topics - 1][total_time - 1];

    // Condition when exam cannot be passed
    if (marks < p)
        return -1;

    // Return the marks that
    // can be obtained after
    // passing the exam
    return sum;
}

    // Driver code
    public static void main (String[] args)
    {
        // Number of topics, hours left
        // and the passing marks
        int n = 4, h = 10, p = 10;

        // n+1 is taken for simplicity in loops
        // Array will be indexed starting from 1
        int marksarr[] = { 0, 6, 4, 2, 8 };
        int timearr[] = { 0, 4, 6, 2, 7 };

        System.out.println( MaximumMarks(marksarr, timearr, h, n, p));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

# Function to return the maximum marks
# by considering topics which can be
# completed in the given time duration
def MaximumMarks(marksarr, timearr, h, n, p) :

    no_of_topics = n + 1;
    total_time = h + 1;

    T = np.zeros((no_of_topics, total_time));

    # Initialization

    # If we are given 0 time
    # then nothing can be done
    # So all values are 0
    for i in range(no_of_topics) :
        T[i][0] = 0;

    # If we are given 0 topics
    # then the time required
    # will be 0 for sure
    for j in range(total_time) :
        T[0][j] = 0;

    # Calculating the maximum marks
    # that can be achieved under
    # the given time constraints
    for i in range(1, no_of_topics) :

        for j in range(1, total_time) :

            # If time taken to read that topic
            # is more than the time left now at
            # position j then do no read that topic
            if (j < timearr[i]) :

                T[i][j] = T[i - 1][j];

            else :

                """Two cases arise:
                1) Considering current topic
                2) Ignoring current topic
                We are finding maximum of (current topic weightage
                + topics which can be done in leftover time
                - current topic time)
                and ignoring current topic weightage sum
                """
                T[i][j] = max(marksarr[i] +
                              T[i - 1][j - timearr[i]],
                              T[i - 1][j]);

    # Moving upwards in table from bottom right
    # to calculate the total time taken to
    # read the topics which can be done in
    # given time and have highest weightage sum
    i = no_of_topics - 1; j = total_time - 1;

    sum = 0;

    while (i > 0 and j > 0) :

        # It means we have not considered
        # reading this topic for
        # max weightage sum
        if (T[i][j] == T[i - 1][j]) :

            i -= 1;

        else :

            # Adding the topic time
            sum += timearr[i];

            # Evaluating the left over time after
            # considering this current topic
            j -= timearr[i];

            # One topic completed
            i -= 1;

    # It contains the maximum weightage sum
    # formed by considering the topics
    marks = T[no_of_topics - 1][total_time - 1];

    # Condition when exam cannot be passed
    if (marks < p) :
        return -1;

    # Return the marks that
    # can be obtained after
    # passing the exam
    return sum;

# Driver code
if __name__ == "__main__" :

    # Number of topics, hours left
    # and the passing marks
    n = 4; h = 10; p = 10;

    # n+1 is taken for simplicity in loops
    # Array will be indexed starting from 1
    marksarr = [ 0, 6, 4, 2, 8 ];
    timearr = [ 0, 4, 6, 2, 7 ];

    print(MaximumMarks(marksarr, timearr, h, n, p));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum marks
// by considering topics which can be
// completed in the given time duration
static int MaximumMarks(int []marksarr, int []timearr,
                            int h, int n, int p)
{
    int no_of_topics = n + 1;
    int total_time = h + 1;

    int [,]T = new int[no_of_topics,total_time];
    int i,j;
    // Initialization

    // If we are given 0 time
    // then nothing can be done
    // So all values are 0
    for (i = 0; i < no_of_topics; i++)
    {
        T[i, 0] = 0;
    }

    // If we are given 0 topics
    // then the time required
    // will be 0 for sure
    for (j = 0; j < total_time; j++)
    {
        T[0, j] = 0;
    }

    // Calculating the maximum marks
    // that can be achieved under
    // the given time constraints
    for (i = 1; i < no_of_topics; i++)
    {

        for (j = 1; j < total_time; j++)
        {

            // If time taken to read that topic
            // is more than the time left now at
            // position j then do no read that topic
            if (j < timearr[i])
            {

                T[i, j] = T[i - 1, j];
            }
            else
            {

                /*Two cases arise:
                1) Considering current topic
                2) Ignoring current topic
                We are finding maximum of (current topic weightage
                + topics which can be done in leftover time
                - current topic time)
                and ignoring current topic weightage sum
                */
                T[i, j] = Math.Max(marksarr[i]
                                + T[i - 1, j - timearr[i]],
                            T[i - 1, j]);
            }
        }
    }

    // Moving upwards in table from bottom right
    // to calculate the total time taken to
    // read the topics which can be done in
    // given time and have highest weightage sum
    i = no_of_topics - 1; j = total_time - 1;

    int sum = 0;

    while (i > 0 && j > 0)
    {

        // It means we have not considered
        // reading this topic for
        // max weightage sum
        if (T[i, j] == T[i - 1, j])
        {

            i--;
        }
        else
        {

            // Adding the topic time
            sum += timearr[i];

            // Evaluating the left over time after
            // considering this current topic
            j -= timearr[i];

            // One topic completed
            i--;
        }
    }

    // It contains the maximum weightage sum
    // formed by considering the topics
    int marks = T[no_of_topics - 1, total_time - 1];

    // Condition when exam cannot be passed
    if (marks < p)
        return -1;

    // Return the marks that
    // can be obtained after
    // passing the exam
    return sum;
}

    // Driver code
    public static void Main (String[] args)
    {
        // Number of topics, hours left
        // and the passing marks
        int n = 4, h = 10, p = 10;

        // n+1 is taken for simplicity in loops
        // Array will be indexed starting from 1
        int []marksarr = { 0, 6, 4, 2, 8 };
        int []timearr = { 0, 4, 6, 2, 7 };

        Console.WriteLine( MaximumMarks(marksarr, timearr, h, n, p));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximum marks
    // by considering topics which can be
    // completed in the given time duration
    function MaximumMarks(marksarr, timearr, h, n, p)
    {
        let no_of_topics = n + 1;
        let total_time = h + 1;

        let T = new Array(no_of_topics);
        for (let i = 0; i < no_of_topics; i++)
        {
            T[i] = new Array(total_time);
            for (let j = 0; j < total_time; j++)
            {
                T[i][j] = 0;
            }
        }
        // Initialization

        // If we are given 0 time
        // then nothing can be done
        // So all values are 0
        for (let i = 0; i < no_of_topics; i++)
        {
            T[i][0] = 0;
        }

        // If we are given 0 topics
        // then the time required
        // will be 0 for sure
        for (let j = 0; j < total_time; j++)
        {
            T[0][j] = 0;
        }

        // Calculating the maximum marks
        // that can be achieved under
        // the given time constraints
        for (let i = 1; i < no_of_topics; i++)
        {

            for (let j = 1; j < total_time; j++)
            {

                // If time taken to read that topic
                // is more than the time left now at
                // position j then do no read that topic
                if (j < timearr[i])
                {

                    T[i][j] = T[i - 1][j];
                }
                else
                {

                    /*Two cases arise:
                    1) Considering current topic
                    2) Ignoring current topic
                    We are finding maximum of (current topic weightage
                    + topics which can be done in leftover time
                    - current topic time)
                    and ignoring current topic weightage sum
                    */
                    T[i][j] = Math.max(marksarr[i]
                                    + T[i - 1][j - timearr[i]],
                                T[i - 1][j]);
                }
            }
        }

        // Moving upwards in table from bottom right
        // to calculate the total time taken to
        // read the topics which can be done in
        // given time and have highest weightage sum
        let i = no_of_topics - 1, j = total_time - 1;

        let sum = 0;

        while (i > 0 && j > 0)
        {

            // It means we have not considered
            // reading this topic for
            // max weightage sum
            if (T[i][j] == T[i - 1][j])
            {

                i--;
            }
            else
            {

                // Adding the topic time
                sum += timearr[i];

                // Evaluating the left over time after
                // considering this current topic
                j -= timearr[i];

                // One topic completed
                i--;
            }
        }

        // It contains the maximum weightage sum
        // formed by considering the topics
        let marks = T[no_of_topics - 1][total_time - 1];

        // Condition when exam cannot be passed
        if (marks < p)
            return -1;

        // Return the marks that
        // can be obtained after
        // passing the exam
        return sum;
    }

    // Number of topics, hours left
    // and the passing marks
    let n = 4, h = 10, p = 10;

    // n+1 is taken for simplicity in loops
    // Array will be indexed starting from 1
    let marksarr = [ 0, 6, 4, 2, 8 ];
    let timearr = [ 0, 4, 6, 2, 7 ];

    document.write( MaximumMarks(marksarr, timearr, h, n, p));

</script>
```

**Output:** 

```
10
```

**时间复杂度** **:** O (n*t)(其中 n 为话题数，t 为总耗时)

**空间复杂度:** O (n*t)