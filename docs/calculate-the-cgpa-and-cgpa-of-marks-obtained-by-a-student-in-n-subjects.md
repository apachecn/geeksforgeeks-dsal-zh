# 计算一个学生在 N 个科目中获得的分数的 CGPA 和 CGPA 百分比

> 原文:[https://www . geeksforgeeks . org/calculate-the-cgpa-and-cgpa-of-marks-由 n 科学生获得/](https://www.geeksforgeeks.org/calculate-the-cgpa-and-cgpa-of-marks-obtained-by-a-student-in-n-subjects/)

给定一个大小为 **N** 的数组 **arr[]** ，该数组包含学生在 **N 个科目**中的分数，任务是计算学生的 CGPA 和 CGPA 百分比。
**注意:**考虑每个科目的所有分数都在 100 分之外。

> **CGPA(累积绩点平均值)**是教育流中获得平均绩点的系统安排。

**示例:**

> **输入:** arr[] = {90，80，70，80，90}
> **输出:** CGPA = 8.2，百分比= 77.89
> **说明:**
> 各科成绩分别满分为 10 分{9，8，7，8，9}。
> CGPA 是所有等级的平均值= (9 + 8 + 7 + 8 + 9) / 5 = 8.2
> 这个 CGPA 的百分比是 77.89。
> 
> **输入:** arr[] = {90，90，90，80，85}
> 输出: CGPA = 8.7，百分比= 82.65

**方法:**在本文中，CGPA 是按 10 分制计算的。

*   从用户输入包含学生在 N 个科目中的分数的数组。
*   因为分数是 10 分，所以把每门课的分数除以 10，就可以得到学生每门课的平均成绩。
*   所有平均绩点的平均值产生学生的总平均绩点。
*   找到 CGPA 后，CGPA 百分比可通过以下公式计算:

```
CGPA% = CGPA * 9.5
```

*   这是 10 分制的通用公式。然而，如果整个计算是以 4 为尺度进行的，则 9.5 乘以 **2.5** ，通过乘以 **23.75** 得到 CGPA 百分比。

下面是上述方法的实现:

## C++

```
// C++ program to calculate the CGPA
// and CGPA percentage of a student
#include<bits/stdc++.h>
using namespace std;

double CgpaCalc(double marks[], int n)
{
    // Variable to store the grades in
    // every subject
    double grade[n];

    // Variables to store CGPA and the
    // sum of all the grades
    double cgpa, sum = 0;

    // Computing the grades
    for(int i = 0; i < n; i++)
    {
       grade[i] = (marks[i] / 10);
    }

    // Computing the sum of grades
    for(int i = 0; i < n; i++)
    {
       sum += grade[i];
    }

    // Computing the CGPA
    cgpa = sum / n;

    return cgpa;
}

// Driver code
int main()
{
    int n = 5;
    double marks[] = { 90, 80, 70, 80, 90 };

    double cgpa = CgpaCalc(marks, n);

    cout << "CGPA = ";
    printf("%.1f\n", cgpa);
    cout << "CGPA Percentage = ";
    printf("%.2f", cgpa * 9.5);
}

// This code is contributed by Bhupendra_Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the CGPA
// and CGPA percentage of a student

import java.util.Scanner;
class CGPA {

    public static double CgpaCalc(double[] marks, int n)
    {
        // Variable to store the grades in
        // every subject
        double grade[] = new double[n];

        // Variables to store CGPA and the
        // sum of all the grades
        double cgpa, sum = 0;

        // Computing the grades
        for (int i = 0; i < n; i++) {
            grade[i] = (marks[i] / 10);
        }

        // Computing the sum of grades
        for (int i = 0; i < n; i++) {
            sum += grade[i];
        }

        // Computing the CGPA
        cgpa = sum / n;

        return cgpa;
    }

    // Driver code
    public static void main(String args[])
    {

        int n = 5;
        double[] marks
            = { 90, 80, 70, 80, 90 };

        double cgpa = CgpaCalc(marks, n);

        System.out.println(
            "CGPA = " + cgpa);
        System.out.println(
            "CGPA Percentage = "
            + String.format("%.2f", cgpa * 9.5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate the CGPA
# and CGPA percentage of a student
def CgpaCalc(marks, n):

    # Variable to store the grades in
    # every subject
    grade = [0] * n

    # Variables to store CGPA and the
    # sum of all the grades
    Sum = 0

    # Computing the grades
    for i in range(n):
       grade[i] = (marks[i] / 10)

    # Computing the sum of grades
    for i in range(n):
       Sum += grade[i]

    # Computing the CGPA
    cgpa = Sum / n

    return cgpa

# Driver code
n = 5
marks = [ 90, 80, 70, 80, 90 ]

cgpa = CgpaCalc(marks, n)

print("CGPA = ", '%.1f' % cgpa)
print("CGPA Percentage = ", '%.2f' % (cgpa * 9.5))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to calculate the CGPA
// and CGPA percentage of a student
using System;

class GFG{

public static double CgpaCalc(double[] marks,
                              int n)
{

    // Variable to store the grades in
    // every subject
    double []grade = new double[n];

    // Variables to store CGPA and the
    // sum of all the grades
    double cgpa, sum = 0;

    // Computing the grades
    for(int i = 0; i < n; i++)
    {
        grade[i] = (marks[i] / 10);
    }

    // Computing the sum of grades
    for(int i = 0; i < n; i++)
    {
        sum += grade[i];
    }

    // Computing the CGPA
    cgpa = sum / n;

    return cgpa;
}

// Driver code
public static void Main(String []args)
{
    int n = 5;
    double[] marks = { 90, 80, 70, 80, 90 };
    double cgpa = CgpaCalc(marks, n);

    Console.WriteLine("CGPA = " + cgpa);
    Console.WriteLine("CGPA Percentage = {0:F2}",
                      cgpa * 9.5);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to calculate the CGPA
// and CGPA percentage of a student

function CgpaCalc( marks, n)
{

    // Variable to store the grades in
    // every subject
    let grade = Array.from({length: n}, (_, i) => 0);

    // Variables to store CGPA and the
    // sum of all the grades
    let cgpa, sum = 0;

    // Computing the grades
    for(let i = 0; i < n; i++)
    {
        grade[i] = (marks[i] / 10);
    }

    // Computing the sum of grades
    for(let i = 0; i < n; i++)
    {
        sum += grade[i];
    }

    // Computing the CGPA
    cgpa = sum / n;

    return cgpa;
}

// Driver Code

    let n = 5;
        let marks
            = [ 90, 80, 70, 80, 90 ];

        let cgpa = CgpaCalc(marks, n);

        document.write(
            "CGPA = " + cgpa + "<br/>");
        document.write(
            "CGPA Percentage = " + (cgpa * 9.5).toFixed(2));

</script>
```

**Output:** 

```
CGPA = 8.2
CGPA Percentage = 77.90
```

时间复杂度:0(n)

辅助空间:O(n)