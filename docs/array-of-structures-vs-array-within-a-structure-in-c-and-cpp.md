# 结构数组与 C/C++中结构内的数组

> 原文:[https://www . geesforgeks . org/array-of-structures-vs-array-in-a-structure-in-c-and-CPP/](https://www.geeksforgeeks.org/array-of-structures-vs-array-within-a-structure-in-c-and-cpp/)

### [结构内的阵列](https://www.geeksforgeeks.org/flexible-array-members-structure-c/)

结构是 **C/C++** 中的一种数据类型，它允许将一组相关变量视为一个单元，而不是单独的实体。一个结构可能包含不同数据类型的元素——int、char、float、double 等。它还可以包含一个数组作为其成员。这样的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)被称为结构内的阵列。结构中的数组是结构的一个成员，可以像访问结构的其他元素一样被访问。

下面是一个在结构中使用数组概念的程序的演示。程序显示学生的记录，包括各科获得的*卷号*、*年级*和*成绩*。各种主题的标记被存储在一个名为*标记*的数组中。整个记录存储在名为a *候选*的结构下。

## C

```
// C program to demonstrate the
// use of an array within a structure
#include <stdio.h>

// Declaration of the structure candidate
struct candidate {
    int roll_no;
    char grade;

    // Array within the structure
    float marks[4];
};

// Function to displays the content of
// the structure variables
void display(struct candidate a1)
{

    printf("Roll number : %d\n", a1.roll_no);
    printf("Grade : %c\n", a1.grade);
    printf("Marks secured:\n");
    int i;
    int len = sizeof(a1.marks) / sizeof(float);

    // Accessing the contents of the
    // array within the structure
    for (i = 0; i < len; i++) {
        printf("Subject %d : %.2f\n",
               i + 1, a1.marks[i]);
    }
}

// Driver Code
int main()
{
    // Initialize a structure
    struct candidate A
        = { 1, 'A', { 98.5, 77, 89, 78.5 } };

    // Function to display structure
    display(A);
    return 0;
}
```

**Output:**

```
Roll number : 1
Grade : A
Marks secured:
Subject 1 : 98.50
Subject 2 : 77.00
Subject 3 : 89.00
Subject 4 : 78.50

```

### <u>[建筑阵列](https://www.geeksforgeeks.org/structures-c/)</u>

数组是相同类型数据项的集合。数组的每个元素可以是 int、char、float、double，甚至是一个结构。我们已经看到，一个结构允许不同数据类型的元素组合在一个名称下。这种结构本身可以被认为是一种新的数据类型。因此，数组可以包含这种新数据类型的元素。结构数组在将记录分组在一起并提供快速访问方面有其应用。

下面是一系列结构的演示。数组保存了一个班级学生的详细信息。详细信息包括*辊号、等级*、*和标记*，它们被归入一个结构(记录)中。每个学生都有一条记录。这就是如何将一组相关变量组装在一个实体下，以提高代码的清晰度和效率。

## C

```
// C program to demonstrate the
// usage of an array of structures
#include <stdio.h>

// Declaring a structure class
struct class {
    int roll_no;
    char grade;
    float marks;
};

// Function to displays the contents
// of the array of structures
void display(struct class class_record[3])
{
    int i, len = 3;

    // Display the contents of the array
    // of structures here, each element
    // of the array is a structure of class
    for (i = 0; i < len; i++) {
        printf("Roll number : %d\n",
               class_record[i].roll_no);
        printf("Grade : %c\n",
               class_record[i].grade);
        printf("Average marks : %.2f\n",
               class_record[i].marks);
        printf("\n");
    }
}

// Driver Code
int main()
{
    // Initialize of an array of structures
    struct class class_record[3]
        = { { 1, 'A', 89.5f },
            { 2, 'C', 67.5f },
            { 3, 'B', 70.5f } };

    // Function Call to display
    // the class_record
    display(class_record);
    return 0;
}
```

**Output:**

```
Roll number : 1
Grade : A
Average marks : 89.50

Roll number : 2
Grade : C
Average marks : 67.50

Roll number : 3
Grade : B
Average marks : 70.50

```

下面是结构中的数组和结构数组之间的表格差异:

|   | 结构中的数组 | 结构阵列 |
| --- | --- | --- |
| **基本思路** | 结构包含一个数组作为其成员变量 | 每个元素都是类型结构的数组 |
| **进入** | 可以使用点运算符进行访问，就像我们访问结构的其他元素一样 | 可以通过索引来访问，就像我们访问数组一样 |
| **语法** | 

> 朱穆伟{
> 
> int ar[10]；
> 
> } a1′a2′a3；

 | 

> structural class {
> 
> int a, b, c;
> 
> } Students [10];

 |