# c++中的结构排序(按多个规则)

> 原文:[https://www.geeksforgeeks.org/structure-sorting-in-c/](https://www.geeksforgeeks.org/structure-sorting-in-c/)

先决条件:[C 中的结构](https://www.geeksforgeeks.org/structures-c/)
不同科目(物理、化学和数学)的名称和分数是给所有学生的。任务是计算所有学生的总分和排名。最后显示所有按排名排序的学生。
使用以下规则计算学生的等级。

1.  如果总分不同，那么分数越高的学生排名越好。
2.  如果总分相同，那么数学成绩较高的学生排名更好。
3.  如果总成绩相同，数学成绩也相同，那么物理成绩好的学生排名就更好。
4.  如果总分相同，数学和物理的分数也相同，那么化学成绩好的学生排名也就更好。
5.  如果所有的分数(总分、数学、物理和化学)都一样，那么任何学生都可以被分配更高的等级。

我们使用下面的结构来存储学生的详细信息。

```
struct Student 
{
    string name; // Given
    int math;  // Marks in math (Given)
    int phy;   // Marks in Physics (Given)
    int che;   // Marks in Chemistry (Given)
    int total; // Total marks (To be filled)
    int rank;  // Rank of student (To be filled)
};  

```

我们使用 [std::sort()](https://www.geeksforgeeks.org/sort-c-stl/) 进行**结构排序**。在结构排序中，结构对象拥有的所有相应属性都是基于对象的一个(或多个)属性进行排序的。
在本例中，不同科目的学生成绩由用户提供。将各个科目的这些分数相加，计算出学生的总分数，然后根据不同学生的等级对其进行排序(如上所述)。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate structure sorting in C++
#include <bits/stdc++.h>
using namespace std;

struct Student
{
    string name; // Given
    int math; // Marks in math (Given)
    int phy; // Marks in Physics (Given)
    int che; // Marks in Chemistry (Given)
    int total; // Total marks (To be filled)
    int rank; // Rank of student (To be filled)
};

// Function for comparing two students according
// to given rules
bool compareTwoStudents(Student a, Student b)
{
    // If total marks are not same then
    // returns true for higher total
    if (a.total != b.total)
        return a.total > b.total;

    // If marks in Maths are same then
    // returns true for higher marks
    if (a.math != b.math)
        return a.math > b.math;

    if (a.phy != b.phy)
        return a.phy > b.phy;

    return (a.che > b.che);
}

// Fills total marks and ranks of all Students
void computeRanks(Student a[], int n)
{
    // To calculate total marks for all Students
    for (int i = 0; i < n; i++)
        a[i].total = a[i].math + a[i].phy + a[i].che;

    // Sort structure array using user defined
    // function compareTwoStudents()
    sort(a, a + 5, compareTwoStudents);

    // Assigning ranks after sorting
    for (int i = 0; i < n; i++)
        a[i].rank = i + 1;
}

// Driver code
int main()
{
    int n = 5;

    // array of structure objects
    Student a[n];

    // Details of Student 1
    a[0].name = "Bryan";
    a[0].math = 80;
    a[0].phy = 95;
    a[0].che = 85;

    // Details of Student 2
    a[1].name = "Kevin";
    a[1].math = 95;
    a[1].phy = 85;
    a[1].che = 99;

    // Details of Student 3
    a[2].name = "Nicky";
    a[2].math = 95;
    a[2].phy = 85;
    a[2].che = 80;

    // Details of Student 4
    a[3].name = "Steve";
    a[3].math = 80;
    a[3].phy = 70;
    a[3].che = 90;

    // Details of Student 5
    a[4].name = "Rohan";
    a[4].math = 80;
    a[4].phy = 80;
    a[4].che = 80;

    computeRanks(a, n);

    // Column names for displaying data
    cout << "Rank"
         << " "
         << "Name"
         << "     ";
    cout << "Maths"
         << " "
         << "Physics"
         << " "
         << "Chemistry";
    cout << " "
         << "Total\n";

    // Display details of Students
    for (int i = 0; i < n; i++) {
        cout << a[i].rank << "    ";
        cout << a[i].name << "      ";
        cout << a[i].math << "     " << a[i].phy << "     "
             << a[i].che << "       ";
        cout << a[i].total << " ";
        cout << "\n";
    }

    return 0;
}
```

**Output**

```
Rank Name     Maths Physics Chemistry Total
1    Kevin      95     85     99       279 
2    Nicky      95     85     80       260 
3    Bryan      80     95     85       260 
4    Rohan      80     80     80       240 
5    Steve      80     70     90       240 

```

**相关文章:**
[c++ STL](https://www.geeksforgeeks.org/sort-c-stl/)
[C 中 qsort()的比较器函数](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/)
[C qsort()vs c++ Sort()](https://www.geeksforgeeks.org/c-qsort-vs-c-sort/)
[根据设置位的个数对数组进行排序](https://www.geeksforgeeks.org/sort-array-according-count-set-bits/)
本文由[**Abhinav Tiwari**](https://auth.geeksforgeeks.org/profile.php?user=Abhinav%20Tiwari&list=todoDone)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。