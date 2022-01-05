# 根据排名计算学生百分位的程序

> 原文:[https://www . geesforgeks . org/program-to-compute-percent-of-a-student-based-on-rank/](https://www.geeksforgeeks.org/program-to-calculate-percentile-of-a-student-based-on-rank/)

给定学生的**等级**和出现在考试中的**学生总数**，任务是找到学生的百分位数。

> 学生的百分比是分数低于他/她的学生人数的百分比。

**例:**

> **输入:**排名:805，总出场人数:97481
> **输出:** 99.17
> **讲解:**
> ((97481–805)/97481)* 100 = 99.17
> **输入:**排名:65，总出场人数:100
> **输出:**35【T11

**逼近**
给出了学生排名和学生总数出现时的百分位计算公式为:

> ((学生总数-排名)/学生总数)* 100

下面是上面公式的实现:

C++

## C++

```
// C++ program to calculate Percentile
// of a student based on rank

#include <bits/stdc++.h>
using namespace std;

// Program to calculate the percentile
float getPercentile(int rank, int students)
{
    // flat variable to store the result
    float result = float(students - rank)
                / students * 100;

    // calculate and return the percentile
    return result;
}

// Driver Code
int main()
{
    int your_rank = 805;
    int total_students = 97481;

    cout << getPercentile(
        your_rank, total_students);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate Percentile
// of a student based on rank
import java.util.*;

class GFG{

// Program to calculate the percentile
static float getPercentile(int rank, int students)
{
    // flat variable to store the result
    float result = (float)(students - rank)
                   / students * 100;

    // calculate and return the percentile
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int your_rank = 805;
    int total_students = 97481;

    System.out.print(getPercentile(
        your_rank, total_students));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to calculate Percentile
# of a student based on rank

# Program to calculate the percentile
def getPercentile(rank, students) :

    # flat variable to store the result
    result = (students - rank) / students * 100;

    # calculate and return the percentile
    return result;

# Driver Code
if __name__ == "__main__" :

    your_rank = 805;
    total_students = 97481;

    print(getPercentile(your_rank, total_students));

# This code is contributed by Yash_R
```

## C#

```
// C# program to calculate Percentile
// of a student based on rank
using System;

class GFG{

// Program to calculate the percentile
static float getPercentile(int rank, int students)
{
    // flat variable to store the result
    float result = (float)(students - rank)
                   / students * 100;

    // calculate and return the percentile
    return result;
}

// Driver Code
public static void Main(String[] args)
{
    int your_rank = 805;
    int total_students = 97481;

    Console.Write(getPercentile(
        your_rank, total_students));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to calculate Percentile
// of a student based on rank

    // Program to calculate the percentile
    function getPercentile(rank , students)
    {
        // flat variable to store the result
        var result =  (students - rank) / students * 100;

        // calculate and return the percentile
        return result;
    }

    // Driver Code

        var your_rank = 805;
        var total_students = 97481;

        document.write(getPercentile(your_rank, total_students).toFixed(4));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
99.1742
```

**业绩分析** :

*   **时间复杂度**:在上面的方法中，我们可以用一个公式在恒定时间内计算百分位，所以时间复杂度为 **O(1)** 。

*   **辅助空间复杂度**:在上面的方法中，除了几个大小不变的变量，我们没有使用任何额外的空间，所以辅助空间复杂度为 **O(1)** 。