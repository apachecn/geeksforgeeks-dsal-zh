# 计算学生百分比的程序

> 原文:[https://www . geesforgeks . org/计算学生百分比的程序/](https://www.geeksforgeeks.org/program-to-calculate-percentile-of-students/)

给定一个包含学生分数的数组，任务是计算学生的百分位数。百分位数按照以下规则计算:

> 学生的百分比是分数低于他/她的学生人数的百分比。

**例:**

> **输入:** arr[] = { 12，60，80，71，30 }
> **输出:** { 0，50，100，75，25 }
> **解释:**
> 学生 1 的百分位数= 0/4*100 = 0(在其他 4 名学生中，没有人的分数低于该学生)
> 学生 2 的百分位数= 2/4*100 = 50(在其他 4 名学生中， 2 名学生的分数低于该学生)
> 学生 3 的百分位数= 4/4*100 = 100(在其他 4 名学生中，所有 4 名学生的分数都低于该学生)
> 学生 4 的百分位数= 3/4*100 = 75(在其他 4 名学生中，3 名学生的分数低于该学生)
> 学生 5 的百分位数= 1/4*100 = 25(在其他 4 名学生中，只有 1 名学生的分数低于该学生)

**进场:**

*   所以基本上，百分位数是一个数字，其中一定百分比的分数低于这个数字。

*   例如:如果在一次考试中，一个学生的百分位数是 75，那么这意味着该学生在参加考试的学生中得分超过 75%。

*   现在，为了计算百分位数，我们有以下公式:
    **百分位数=(得分低于或等于期望学生人数/学生总数-1)* 100**

以下是上述方法的实现:

## C++

```
// C++ program to calculate Percentile of Students

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the percentile
void percentile(int arr[], int n)
{
    int i, j, count, percent;

    // Start of the loop that calculates percentile
    for (i = 0; i < n; i++) {

        count = 0;
        for (int j = 0; j < n; j++) {

            // Comparing the marks of student i
            // with all other students
            if (arr[i] > arr[j]) {
                count++;
            }
        }
        percent = (count * 100) / (n - 1);

        cout << "\nPercentile of Student "
             << i + 1 << " = " << percent;
    }
}

// Driver Code
int main()
{
    int StudentMarks[] = { 12, 60, 80, 71, 30 };
    int n = sizeof(StudentMarks) / sizeof(StudentMarks[0]);
    percentile(StudentMarks, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate Percentile of Students
class GFG
{

    // Function to calculate the percentile
    static void percentile(int arr[], int n)
    {
        int i, count, percent;

        // Start of the loop that calculates percentile
        for (i = 0; i < n; i++)
        {

            count = 0;
            for (int j = 0; j < n; j++)
            {

                // Comparing the marks of student i
                // with all other students
                if (arr[i] > arr[j])
                {
                    count++;
                }
            }
            percent = (count * 100) / (n - 1);

            System.out.print("\nPercentile of Student "
            + (i + 1) + " = " + percent);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] StudentMarks = { 12, 60, 80, 71, 30 };
        int n = StudentMarks.length;
        percentile(StudentMarks, n);
    }
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python3 program to calculate Percentile of Students

# Function to calculate the percentile
def percentile(arr, n):
    i, j = 0, 0
    count, percent = 0, 0

    # Start of the loop that calculates percentile
    while i < n:

        count = 0
        j = 0
        while j < n:

            # Comparing the marks of student i
            # with all other students
            if (arr[i] > arr[j]):
                count += 1
            j += 1
        percent = (count * 100) // (n - 1)

        print("Percentile of Student ", i + 1," = ", percent)
        i += 1

# Driver Code

StudentMarks = [12, 60, 80, 71, 30]
n = len(StudentMarks)
percentile(StudentMarks, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to calculate Percentile of Students
using System;

class GFG
{

    // Function to calculate the percentile
    static void percentile(int []arr, int n)
    {
        int i, count, percent;

        // Start of the loop that calculates percentile
        for (i = 0; i < n; i++)
        {
            count = 0;
            for (int j = 0; j < n; j++)
            {

                // Comparing the marks of student i
                // with all other students
                if (arr[i] > arr[j])
                {
                    count++;
                }
            }
            percent = (count * 100) / (n - 1);

            Console.Write("\nPercentile of Student "
            + (i + 1) + " = " + percent);
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] StudentMarks = {12, 60, 80, 71, 30};
        int n = StudentMarks.Length;
        percentile(StudentMarks, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to calculate
// Percentile of Students

// Function to calculate the percentile
function percentile(arr, n)
{
    var i, count, percent;

    // Start of the loop that calculates percentile
    for (i = 0; i < n; i++)
    {

        count = 0;
        for (var j = 0; j < n; j++)
        {

            // Comparing the marks of student i
            // with all other students
            if (arr[i] > arr[j])
            {
                count++;
            }
        }
        percent = (count * 100) / (n - 1);

        document.write("\nPercentile of Student "
        + (i + 1) + " = " + percent + "<br>");
    }
}

// Driver Code
var StudentMarks = [ 12, 60, 80, 71, 30 ];
var n = StudentMarks.length;

percentile(StudentMarks, n);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
Percentile of Student 1 = 0
Percentile of Student 2 = 50
Percentile of Student 3 = 100
Percentile of Student 4 = 75
Percentile of Student 5 = 25
```