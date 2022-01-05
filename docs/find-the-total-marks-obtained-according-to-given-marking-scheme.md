# 找出根据给定的评分方案

得到的总分

> 原文:[https://www . geesforgeks . org/find-the-total-marks-根据给定的评分方案获得/](https://www.geeksforgeeks.org/find-the-total-marks-obtained-according-to-given-marking-scheme/)

给出 N . MCQ 的答案键和学生标注的答案。任务是计算学生的分数。

> 评分方案如下:
> 
> *   每一个正确答案+3 分。
> *   -每答错 1 分。
> *   未尝试该问题得 0 分。

**例:**

```
Input:  N = 5
        Answer key =  {1, 2, 1, 3, 1}
        Student answer = {1, 3, 1, 0, 2}
Output: 4 
(Only 1 and 3 questions are correctly marked and 2 and 5 are 
marked wrong and 4 is not attempt so, (2 * 3) + (2 * -1) = 4)

Input:  N = 5
        Answer key =     {1, 2, 3, 4, 1}
        Student answer = {1, 2, 3, 4, 0}
Output: 12
(1, 2, 3, 4 questions are correctly marked and 5 is not attempt 
so, (4 * 3) = 12)
```

**进场:**

1.  开始遍历学生 _ 答案[]。
2.  如果学生答案[]的当前索引值= 0，则不尝试该问题。
3.  否则如果当前索引处的值等于答案关键字[]中相应索引处的值，则递增肯定答案的计数。
4.  否则增加否定答案的数量。
5.  通过计算正分数和负分数来打印总分数。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that calculates marks.
int markingScheme(int N, int answerKey[], int studentAnswer[])
{
    int positive = 0, negative = 0, notattempt = 0;

    for (int i = 0; i < N; i++) {

        // for not attempt score + 0
        if (studentAnswer[i] == 0)
            notattempt++;

        // for each correct answer score + 3
        else if (answerKey[i] == studentAnswer[i])
            positive++;

        // for each wrong answer score - 1
        else if (answerKey[i] != studentAnswer[i])
            negative++;
    }

    // calculate total marks
    return (positive * 3) + (negative * -1);
}

// Driver code
int main()
{
    int answerKey[] = { 1, 2, 3, 4, 1 };
    int studentAnswer[] = { 1, 2, 3, 4, 0 };   
    int N = sizeof(answerKey)/sizeof(answerKey[0]);
    cout << markingScheme(N, answerKey, studentAnswer);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

// Function that calculates marks.
class geeksforgeeks
{
static int markingScheme(int N, int answerKey[], int studentAnswer[])
{
    int positive = 0, negative = 0, notattempt = 0;

    for (int i = 0; i < N; i++) {

        // for not attempt score + 0
        if (studentAnswer[i] == 0)
            notattempt++;

        // for each correct answer score + 3
        else if (answerKey[i] == studentAnswer[i])
            positive++;

        // for each wrong answer score - 1
        else if (answerKey[i] != studentAnswer[i])
            negative++;
    }

    // calculate total marks
    return (positive * 3) + (negative * -1);
}

// Driver code
public static void main(String args[])
{
    int answerKey[] = { 1, 2, 3, 4, 1 };
    int studentAnswer[] = { 1, 2, 3, 4, 0 };
    int N = answerKey.length;
    int marking_Scheme = markingScheme(N, answerKey, studentAnswer); 
    System.out.println(marking_Scheme);
}
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function that calculates marks.
def markingScheme( N, answerKey, studentAnswer):

    positive = 0
    negative = 0
    notattempt = 0

    for i in range (0, N):

        # for not attempt score + 0
        if (studentAnswer[i] == 0):
            notattempt += 1

        # for each correct answer score + 3
        elif (answerKey[i] == studentAnswer[i]):
            positive += 1

        # for each wrong answer score - 1
        elif (answerKey[i] != studentAnswer[i]):
            negative += 1

    # calculate total marks
    return (positive * 3) + (negative * -1)

# Driver code
def main():
    answerKey = [1, 2, 3, 4, 1]
    studentAnswer = [1, 2, 3, 4, 0]
    N = 5
    print (markingScheme(N, answerKey, studentAnswer))
```

## C#

```
// C# implementation of above approach
// Function that calculates marks.
using System;

class GFG
{
static int markingScheme(int N, int []answerKey,
                                int []studentAnswer)
{
    int positive = 0, negative = 0,
                      notattempt = 0;

    for (int i = 0; i < N; i++)
    {

        // for not attempt score + 0
        if (studentAnswer[i] == 0)
            notattempt++;

        // for each correct answer score + 3
        else if (answerKey[i] == studentAnswer[i])
            positive++;

        // for each wrong answer score - 1
        else if (answerKey[i] != studentAnswer[i])
            negative++;
    }

    // calculate total marks
    return (positive * 3) + (negative * -1);
}

// Driver code
static public void Main ()
{
    int []answerKey = { 1, 2, 3, 4, 1 };
    int []studentAnswer = { 1, 2, 3, 4, 0 };
    int N = answerKey.Length;
    int marking_Scheme = markingScheme(N, answerKey,
                                       studentAnswer);
    Console.WriteLine(marking_Scheme);
}
}

// This code is contributed
// by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that calculates marks.
function markingScheme($N, $answerKey,
                           $studentAnswer)
{
    $positive = 0;
    $negative = 0;
    $notattempt = 0;

    for ($i = 0; $i < $N; $i++)
    {

        // for not attempt score + 0
        if ($studentAnswer[$i] == 0)
            $notattempt++;

        // for each correct answer score + 3
        else if ($answerKey[$i] == $studentAnswer[$i])
            $positive++;

        // for each wrong answer score - 1
        else if ($answerKey[$i] != $studentAnswer[$i])
            $negative++;
    }

    // calculate total marks
    return ($positive * 3) +
           ($negative * -1);
}

// Driver code
$answerKey = array( 1, 2, 3, 4, 1 );
$studentAnswer = array( 1, 2, 3, 4, 0 );    
$N = sizeof($answerKey);
echo markingScheme($N, $answerKey,
                       $studentAnswer);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that calculates marks.
function markingScheme(N, answerKey, studentAnswer)
{
    var positive = 0, negative = 0, notattempt = 0;

    for (var i = 0; i < N; i++) {

        // for not attempt score + 0
        if (studentAnswer[i] == 0)
            notattempt++;

        // for each correct answer score + 3
        else if (answerKey[i] == studentAnswer[i])
            positive++;

        // for each wrong answer score - 1
        else if (answerKey[i] != studentAnswer[i])
            negative++;
    }

    // calculate total marks
    return (positive * 3) + (negative * -1);
}

// Driver code
var answerKey = [ 1, 2, 3, 4, 1 ];
var studentAnswer = [ 1, 2, 3, 4, 0 ];   
var N = answerKey.length;
document.write( markingScheme(N, answerKey, studentAnswer));

</script>
```

**Output:** 

```
12
```