# c++中的比较器类，示例

> 原文:[https://www . geesforgeks . org/comparator-class-in-c-with-examples/](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)

比较器类用于比较用户定义类的对象。为了开发一个[通用函数](https://www.geeksforgeeks.org/generics-in-c/)使用[模板](https://www.geeksforgeeks.org/templates-cpp/)，为了使函数更通用，使用[容器](https://www.geeksforgeeks.org/containers-cpp-stl/)，这样可以进行数据之间的比较。

**语法:**

```
class comparator_class {
public:
    // Comparator function
    bool operator(object o1, object o2)
    {

        // There can be any condition
        // implemented as per the need
        // of the problem statement
        return (o1.data_member
                == o2.data_member);
    }
}
```

**解释:**上面的比较器函数**运算符()**类一次取两对对象，如果两个运算符的数据成员相同，则返回 true。根据问题的需要，在比较器函数中可以有任何条件。在上面的例子中，如果数据成员相同，函数返回 true。

**例 1:**
为了在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素上实现[线性搜索](https://www.geeksforgeeks.org/linear-search/)，可以很容易地实现[在给定数组](https://www.geeksforgeeks.org/recursive-c-program-linearly-search-element-given-array/)中搜索整数。但是在[用户定义的数据类型](https://www.geeksforgeeks.org/user-defined-data-types-in-c/)上搜索任何元素都不像数组那样容易实现。在这种情况下，比较器类用于实现它。下面是同样的程序:

## C++

```
// C++ program for the Comparator Class
// for implementing linear search
#include <bits/stdc++.h>
using namespace std;

// Generic function to search for object
template <class ForwardIterator, class T>
ForwardIterator search(
    ForwardIterator start,
    ForwardIterator end, T key)
{
    // Iterate until start equals to end
    while (start != end) {

        // If the value with given key is
        // found the return that index
        if (*start == key) {
            return start;
        }
        start++;
    }
    return end;
}

// Student Class
class student {
public:
    // To store Name and Roll Number
    string name;
    int rollnum;

    // Overloaded Constructor
    student(string name, int rollnum)
    {
        this->name = name;
        this->rollnum = rollnum;
    }
};

// Comparator Class to compare 2 objects
class studentcompare {
public:
    // Comparator function
    bool operator()(student a,
                    student b)
    {
        // If values are the same then
        // return true
        if (a.name == b.name) {
            return true;
        }
        return false;
    }
};

// Driver Code
int main()
{
    // Object of class student
    student s1("Raj", 23);
    student s2("Prerna", 24);

    // List of students
    list<student> s;
    s.push_back(s1);
    s.push_back(s2);

    // Search student("Prerna", 24)
    student searchstudent("Prerna", 24);

    studentcompare cmp;

    // Print if element is found
    if (cmp(s2, searchstudent)) {
        cout << "Student found!";
    }
    else {
        cout << "Not found";
    }

    return 0;
}
```

**Output:**

```
Student found!

```

**说明:**

*   在上面的程序中，创建了一个学生对象列表，其中最初插入了两个学生对象。
*   现在，为了搜索特定的学生，编写了一个模板线性搜索函数，它利用了比较器类。
*   比较器类根据学生的姓名属性比较要从学生列表中搜索的学生。
*   如果要搜索的对象的名称属性等于列表中对象的任何名称属性，则返回 true，否则返回 false。

**例 2:**

我们再举一个使用 comparator 类进行[排序](https://www.geeksforgeeks.org/sorting-algorithms/)的例子，假设任务是根据对象的属性值对对象的[数组](https://www.geeksforgeeks.org/how-to-initialize-array-of-objects-with-parameterized-constructors-in-c/)进行排序，那么想法就是创建一个自定义的 Comparator 类，在这个类中可以提到进行排序的函数。然后可以在 [sort()](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) 函数中作为参数传递。

## C++

```
// C++ program for the Comparator Class
// implementing sorting

#include <bits/stdc++.h>
using namespace std;

// Student Class
class student {
public:
    // To store Name and Roll Number
    string name;
    int rollnum;

    // Overloaded Constructor
    student(string name, int rollnum)
    {
        this->name = name;
        this->rollnum = rollnum;
    }
};

// Comparator Class to compare 2 objects
class studentcompare {
public:
    // Comparator function
    bool operator()(const student& a,
                    const student& b)
    {
        // Compare on basis of roll number
        if (a.rollnum < b.rollnum) {
            return true;
        }
        return false;
    }
};

// Driver Code
int main()
{
    // Object of class student
    student s1("Raj", 23);
    student s2("Prerna", 24);
    student s3("Harshit", 21);

    // List of students
    list<student> s;
    s.push_back(s1);
    s.push_back(s2);
    s.push_back(s3);

    // Creating object of
    // comparator class
    studentcompare cmp;

    // Passing the object of
    // comparator class to sort()
    s.sort(cmp);

    // Printing the list after sorting
    for (auto stu : s) {
        cout << stu.name << " ";
    }

    return 0;
}
```

**Output:**

```
Harshit Raj Prerna

```

**说明:**

*   在上面的程序中，创建了一个学生对象列表，其中最初插入了 3 个学生对象。
*   现在，如果必须根据学生的**rollino**属性对学生列表进行排序，那么必须将一个自定义比较器类作为参数传递给 [sort()](https://www.geeksforgeeks.org/sort-c-stl/) 函数。
*   在比较器类中，必须提到一个谓词逻辑，它返回真或假，列表是根据这个逻辑排序的。