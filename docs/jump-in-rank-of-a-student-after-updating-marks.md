# 更新分数后学生排名跃升

> 原文:[https://www . geeksforgeeks . org/更新分数后跳入学生行列/](https://www.geeksforgeeks.org/jump-in-rank-of-a-student-after-updating-marks/)

给定三个数组**名称【】**、**标记【】**和**更新【】**其中:

1.  **人名[]** 包含学生的姓名。
2.  **分数[]** 包含同一学生的分数。
3.  **更新[]** 包含更新这些学生分数的整数。

任务是在学生排名上升和跳跃后找到分数最高的学生的名字，即**以前的排名-当前的排名**。

**注意:**学生的详细信息按分数降序排列，如果两个以上的学生得分相同(也是最高的)，那么选择之前排名较低的一个。

**示例:**

> **输入:**Name[]= {“Sam”、“ram”、“geek”、“sonu”}，
> marks[] = {99、75、70、60}，
> updates[] = {-10、5、9、39 }
> T5】输出: Name: sonu，Jump: 3
> Updated marks 为{89、80、79、99}，很明显 sonu 的最高分是跳 3
> 
> **输入:**名称[]= {“Sam”、“ram”、“geek”}，
> 标记[] = {80，79，75}，
> 更新[] = {0，5，-9 }
> T5】输出:名称:ram，跳转:1

**方法:**创建一个结构**结构学生**存储每个学生的信息，每个学生将有 3 个属性**学生的名字**、学生的**标记**、学生的 **prev_rank** 。
现在，根据**更新的内容更新分数【】**然后用数组的单次遍历，找到更新后分数最高的学生。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure to store the information of
// students
struct Student {
    string name;
    int marks = 0;
    int prev_rank = 0;
};

// Function to print the name of student who
// stood first after updation in rank
void nameRank(string names[], int marks[],
                      int updates[], int n)
{
    // Array of students
    Student x[n];

    for (int i = 0; i < n; i++) {

        // Store the name of the student
        x[i].name = names[i];

        // Update the marks of the student
        x[i].marks = marks[i] + updates[i];

        // Store the current rank of the student
        x[i].prev_rank = i + 1;
    }

    Student highest = x[0];
    for (int j = 1; j < n; j++) {
        if (x[j].marks >= highest.marks)
            highest = x[j];
    }

    // Print the name and jump in rank
    cout << "Name: " << highest.name
         << ", Jump: "
         << abs(highest.prev_rank - 1)
         << endl;
}

// Driver code
int main()
{
    // Names of the students
    string names[] = { "sam", "ram", "geek" };

    // Marks of the students
    int marks[] = { 80, 79, 75 };

    // Updates that are to be done
    int updates[] = { 0, 5, -9 };

    // Number of students
    int n = sizeof(marks) / sizeof(marks[0]);

    nameRank(names, marks, updates, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

static class Student
{
    String name;
    int marks, prev_rank;

    Student()
    {
        this.marks = 0;
        this.prev_rank = 0;
    }
}

// Function to print the name of student who
// stood first after updation in rank
static void nameRank(String []names, int []marks,
                      int []updates, int n)
{

    // Array of students
    Student []x = new Student[n];

    for(int i = 0; i < n; i++)
    {
        x[i] = new Student();

        // Store the name of the student
        x[i].name = names[i];

        // Update the marks of the student
        x[i].marks = marks[i] + updates[i];

        // Store the current rank of the student
        x[i].prev_rank = i + 1;
    }

    Student highest = x[0];

    for(int j = 1; j < n; j++)
    {
        if (x[j].marks >= highest.marks)
            highest = x[j];
    }

    // Print the name and jump in rank
    System.out.print("Name: " + highest.name +
                     ", Jump: " +
                     Math.abs(highest.prev_rank - 1));
}

// Driver code 
public static void main(String[] args)
{

    // Names of the students
    String []names = { "sam", "ram", "geek" };

    // Marks of the students
    int []marks = { 80, 79, 75 };

    // Updates that are to be done
    int []updates = { 0, 5, -9 };

    // Number of students
    int n = marks.length;

    nameRank(names, marks, updates, n);
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the name of student who
# stood first after updation in rank
def nameRank(names, marks, updates, n):

    # Array of students
    x = [[0 for j in range(3)] for i in range(n)]
    for i in range(n):

        # Store the name of the student
        x[i][0] = names[i]

        # Update the marks of the student
        x[i][1]= marks[i] + updates[i]

        # Store the current rank of the student
        x[i][2] = i + 1

    highest = x[0]
    for j in range(1, n):
        if (x[j][1] >= highest[1]):
            highest = x[j]

    # Print the name and jump in rank
    print("Name: ", highest[0], ", Jump: ",
            abs(highest[2] - 1), sep="")

# Driver code

# Names of the students
names= ["sam", "ram", "geek"]

# Marks of the students
marks = [80, 79, 75]

# Updates that are to be done
updates = [0, 5, -9]

# Number of students
n = len(marks)

nameRank(names, marks, updates, n)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

public class Student
{
    public string name;
    public int marks, prev_rank;

    public Student()
    {
        this.marks = 0;
        this.prev_rank = 0;
    }
}

// Function to print the name of student who
// stood first after updation in rank
static void nameRank(string []names, int []marks,
                      int []updates, int n)
{

    // Array of students
    Student []x = new Student[n];

    for(int i = 0; i < n; i++)
    {
        x[i] = new Student();

        // Store the name of the student
        x[i].name = names[i];

        // Update the marks of the student
        x[i].marks = marks[i] + updates[i];

        // Store the current rank of the student
        x[i].prev_rank = i + 1;
    }

    Student highest = x[0];

    for(int j = 1; j < n; j++)
    {
        if (x[j].marks >= highest.marks)
            highest = x[j];
    }

    // Print the name and jump in rank
    Console.Write("Name: " + highest.name +
                  ", Jump: " +
                  Math.Abs(highest.prev_rank - 1));
}

// Driver code 
public static void Main(string[] args)
{

    // Names of the students
    string []names = { "sam", "ram", "geek" };

    // Marks of the students
    int []marks = { 80, 79, 75 };

    // Updates that are to be done
    int []updates = { 0, 5, -9 };

    // Number of students
    int n = marks.Length;

    nameRank(names, marks, updates, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the name of student who
// stood first after updation in rank
function nameRank(names, marks, updates, n)
{

    // Array of students
    let x = new Array(n);
    for(let i = 0; i < n; i++)
    {
        x[i] = new Array(3);
        for(let j = 0; j < 3; j++)
        {
            x[i][j] = 0;
        }
    }

    for(let i = 0; i < n; i++)
    {

        // Store the name of the student
        x[i][0] = names[i]

        // Update the marks of the student
        x[i][1] = marks[i] + updates[i]

        // Store the current rank of the student
        x[i][2] = i + 1
    }

    let highest = x[0];

    for(let j = 1; j < n; j++)
    {
        if (x[j][1] >= highest[1])
            highest = x[j]
    }

    // Print the name and jump in rank
    document.write("Name: ", highest[0], ", Jump: ",
                   Math.abs(highest[2] - 1), sep = "")
}

// Driver code

// Names of the students
let names = [ "sam", "ram", "geek" ];

// Marks of the students
let marks = [ 80, 79, 75 ];

// Updates that are to be done
let updates = [ 0, 5, -9 ];

// Number of students
let n = marks.length;

nameRank(names, marks, updates, n)

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Name: ram, Jump: 1
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)