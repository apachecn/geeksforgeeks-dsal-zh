# 三科平均分最高的学生

> 原文:[https://www . geesforgeks . org/三科最高平均分学生/](https://www.geeksforgeeks.org/students-with-maximum-average-score-of-three-subjects/)

给定一个文件，其中包含学生姓名和他/她在 3 个科目中得分的数据。任务是找到平均分数最高的学生名单。
**注意:**如果超过一个学生的平均分最高，按照文件中的顺序打印。
**示例:**

> **输入:**文件[]= {“Shrikanth”“20”“30”“10”“Ram”“100”“50”“10”}
> **输出:**Ram 53
> Shrikanth、Ram 平均成绩分别为 20 和 53。所以拉姆的最高平均分是 53 分。
> **输入:**文件[]= {“Ramesh”、“90”、“70”、“40”、“Adam”、“50”、“10”、
> “40”、“Suresh”、“22”、“1”、“56”、“Rocky”、“100”、“90”、“10”}
> **输出:**Ramesh Rocky 66
> Ramesh、Adam、Suresh、Rocky 平均成绩分别为 66、33、26、66。所以 Ramesh 和 Rocky 的最高平均分都是 66 分。

**进场:**

1.  遍历文件数据并存储每个学生的平均分数。
2.  现在，找到最高平均分，搜索所有有这个最高平均分的学生。
3.  根据文件中的顺序打印最高平均分和姓名。

以下是上述方法的实现:

## C++

```
// C++ program to find the
// list of students having maximum average score
#include<bits/stdc++.h>
using namespace std;

// Function to find the
// list of students having maximum average score
// Driver code
void getStudentsList(string file[],int n)
{
    // Variables to store average score of a student
    // and maximum average score
    int avgScore;
    int maxAvgScore = INT_MIN;

    // List to store names of students
    // having maximum average score
    vector<string> names;

    // Traversing the file data
    for (int i = 0; i < n; i += 4) {

        // finding average score of a student
        avgScore = (stoi(file[i + 1]) +
                    stoi(file[i + 2]) +
                stoi(file[i + 3])) / 3;

        if (avgScore > maxAvgScore) {
            maxAvgScore = avgScore;

            // Clear the list and add name of student
            // having current maximum average score in the list
            names.clear();
            names.push_back(file[i]);
        }

        else if (avgScore == maxAvgScore)
            names.push_back(file[i]);
    }

    // Printing the maximum average score and names
    // of students having this maximum average score
    // as per the order in the file.
    for (int i = 0; i < names.size(); i++) {
        cout <<names[i] + " ";
    }

    cout << maxAvgScore;
}

// Driver code
int main()
{
    string file[] = { "Shrikanth", "20", "30",
                    "10", "Ram", "100", "50", "10" };

    // Number of elements in string array               
    int n= sizeof(file)/sizeof(file[0]);

    getStudentsList(file,n);
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// list of students having maximum average score

import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    // Function to find the
    // list of students having maximum average score
    // Driver code
    static void getStudentsList(String[] file)
    {
        // Variables to store average score of a student
        // and maximum average score
        int avgScore;
        int maxAvgScore = Integer.MIN_VALUE;

        // List to store names of students
        // having maximum average score
        ArrayList<String> names = new ArrayList<>();

        // Traversing the file data
        for (int i = 0; i < file.length; i += 4) {

            // finding average score of a student
            avgScore = (Integer.parseInt(file[i + 1]) +
                        Integer.parseInt(file[i + 2]) +
                       Integer.parseInt(file[i + 3])) / 3;

            if (avgScore > maxAvgScore) {
                maxAvgScore = avgScore;

                // Clear the list and add name of student
                // having current maximum average score in the list
                names.clear();
                names.add(file[i]);
            }

            else if (avgScore == maxAvgScore)
                names.add(file[i]);
        }

        // Printing the maximum average score and names
        // of students having this maximum average score
        // as per the order in the file.
        for (int i = 0; i < names.size(); i++) {
            System.out.print(names.get(i) + " ");
        }

        System.out.print(maxAvgScore);
    }

    // Driver code
    public static void main(String args[])
    {
        String[] file = { "Shrikanth", "20", "30",
                        "10", "Ram", "100", "50", "10" };
        getStudentsList(file);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the list of
# students having maximum average score

# Function to find the list of students
# having maximum average score
def getStudentsList(file):

    # Variables to store maximum
    # average score
    maxAvgScore = 0

    # List to store names of students
    # having maximum average score
    names = []

    # Traversing the file data
    for i in range(0, len(file), 4):

        # finding average score
        # of a student
        avgScore = (int(file[i + 1]) +
                    int(file[i + 2]) +
                    int(file[i + 3])) // 3

        if avgScore > maxAvgScore:
            maxAvgScore = avgScore

            # Clear the list and add name
            # of student having current
            # maximum average score in the list
            names.clear()
            names.append(file[i])

        elif avgScore == maxAvgScore:
            names.add(file[i])

    # Printing the maximum average score and names
    # of students having this maximum average score
    # as per the order in the file.
    for i in range(len(names)):
        print(names[i], end = " ")

    print(maxAvgScore)

# Driver Code
if __name__ == "__main__":

    file = ["Shrikanth", "20", "30", "10",
            "Ram", "100", "50", "10"]

    getStudentsList(file)

# This code is contributed
# by rituraj_jain
```

## C#

```
// C# program to find the
// list of students having maximum average score

using System;
using System.Collections.Generic;
class GFG {

    // Function to find the
    // list of students having maximum average score
    // Driver code
    static void getStudentsList(string [] file)
    {
        // Variables to store average score of a student
        // and maximum average score
        int avgScore;
        int maxAvgScore = Int32.MinValue;

        // List to store names of students
        // having maximum average score
        List<string> names = new List<string>();

        // Traversing the file data
        for (int i = 0; i < file.Length; i += 4) {

            // finding average score of a student
            avgScore = (Int32.Parse(file[i + 1]) +
                        Int32.Parse(file[i + 2]) +
                    Int32.Parse(file[i + 3])) / 3;

            if (avgScore > maxAvgScore) {
                maxAvgScore = avgScore;

                // Clear the list and add name of student
                // having current maximum average score in the list
                names.Clear();
                names.Add(file[i]);
            }

            else if (avgScore == maxAvgScore)
                names.Add(file[i]);
        }

        // Printing the maximum average score and names
        // of students having this maximum average score
        // as per the order in the file.
        for (int i = 0; i < names.Count; i++) {
            Console.Write(names[i] + " ");
        }

        Console.WriteLine(maxAvgScore);
    }

    // Driver code
    public static void Main()
    {
        string[] file = { "Shrikanth", "20", "30",
                        "10", "Ram", "100", "50", "10" };
        getStudentsList(file);
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the list of students
// having maximum average score

// Function to find the list of students
// having maximum average score
function getStudentsList($file, $n)
{
    // Variables to store average score of
    // a student and maximum average score
    $maxAvgScore = PHP_INT_MIN;

    // List to store names of students
    // having maximum average score
    $names = array();
    $avgScore = 0;

    // Traversing the file data
    for ($i = 0; $i < $n; $i += 4)
    {

        // finding average score of a student
        $avgScore = (int)((intval($file[$i + 1]) +
                           intval($file[$i + 2]) +
                           intval($file[$i + 3])) / 3);

        if ($avgScore > $maxAvgScore)
        {
            $maxAvgScore = $avgScore;

            // Clear the list and add name of
            // student having current maximum
            // average score in the list
            unset($names);
            $names = array();
            array_push($names, $file[$i]);
        }

        else if ($avgScore == $maxAvgScore)
            array_push($names, $file[$i]);
    }

    // Printing the maximum average score
    // and names of students having this
    // maximum average score as per the
    // order in the file.
    for ($i = 0; $i < count($names); $i++)
    {
        echo $names[$i] . " ";
    }

    echo $maxAvgScore;
}

// Driver code
$file = array( "Shrikanth", "20", "30", "10",
               "Ram", "100", "50", "10" );

// Number of elements in string array        
$n = count($file);

getStudentsList($file, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find the
// list of students having maximum average score

// Function to find the
// list of students having maximum average score
// Driver code
function getStudentsList(file, n)
{

    // Variables to store average score of a student
    // and maximum average score
    let avgScore;
    let maxAvgScore = Number.MIN_SAFE_INTEGER;

    // List to store names of students
    // having maximum average score
    let names = [];

    // Traversing the file data
    for (let i = 0; i < n; i += 4)
    {

        // finding average score of a student
        avgScore = Math.floor((Number(file[i + 1]) + Number(file[i + 2]) + Number(file[i + 3])) / 3);

        if (avgScore > maxAvgScore)
        {
            maxAvgScore = avgScore;

            // Clear the list and add name of student
            // having current maximum average score in the list
            names = [];
            names.push(file[i]);
        }

        else if (avgScore == maxAvgScore)
            names.push(file[i]);
    }

    // Printing the maximum average score and names
    // of students having this maximum average score
    // as per the order in the file.
    for (let i = 0; i < names.length; i++) {
        document.write(names[i] + " ");
    }

    document.write(maxAvgScore);
}

// Driver code

let file = ["Shrikanth", "20", "30",
    "10", "Ram", "100", "50", "10"];

// Number of elements in string array               
let n = file.length;

getStudentsList(file, n);

// This code is contributed by gfgking.

</script>
```

**Output:** 

```
Ram 53
```