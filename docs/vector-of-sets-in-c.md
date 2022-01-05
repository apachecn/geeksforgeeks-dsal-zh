# c++中集合的向量

> 原文:[https://www.geeksforgeeks.org/vector-of-sets-in-c/](https://www.geeksforgeeks.org/vector-of-sets-in-c/)

**先决条件:**[<u>c++ STL 中的向量</u>](https://www.geeksforgeeks.org/vector-in-cpp-stl/)

[](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**向量被称为[动态数组](https://www.geeksforgeeks.org/how-do-dynamic-arrays-work/)，能够在插入或删除元素时自动调整自身大小，其存储由容器自动处理。**

**[](https://www.geeksforgeeks.org/set-in-cpp-stl/)**集合是一种关联容器，其中每个元素必须是唯一的，因为元素的值标识了它。元素的值一旦添加到集合中就不能修改，尽管可以移除和添加该元素的修改值。****

******集合向量**可以用来设计复杂而高效的数据结构，在本文中，我们将检查集合向量非常有用的一个这样的例子。****

******语法:******

> ****向量<set>> v；</set>****

******<u>插入集合向量</u>******

****可以使用 [C++ STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 的[**<u>push _ back()</u>**](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)功能将元素插入到向量中。首先使用 [**insert()**](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) 将元素插入到集合中。然后使用[**<u>push _ back()</u>**](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)将该集合插入到向量中。****

****下面的例子演示了集合向量的插入操作:****

## ****C++****

```
**// C++ program to demonstrate the
// insertion into a vector of sets
#include <bits/stdc++.h>
using namespace std;

// Defining the number of sets
// in the vector and number of
// elements in each set
#define ROW 4
#define COL 5

// Driver Code
int main()
{
    // Initialize vector of sets
    vector<set<int> > v;

    // Elements to insert
    // in column
    int num = 10;

    // Inserting elements
    // into vector
    for (int i = 0; i < ROW; i++) {

        // Stores the column elements
        set<int> s;

        for (int j = 0; j < COL; j++) {
            s.insert(num);
            num += 5;
        }

        // Push the set in the vector
        v.push_back(s);
    }

    // Display the vector of sets
    for (int i = 0; i < v.size(); i++) {

        for (auto x : v[i])
            cout << x << " ";
        cout << endl;
    }
    return 0;
}**
```

******Output:**

```
10 15 20 25 30 
35 40 45 50 55 
60 65 70 75 80 
85 90 95 100 105

```**** 

******<u>集合向量中的移除或删除</u>******

1.  ****使用 C++ STL 的[**<u>【pop _ back()】</u>**](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)功能，可以从集合向量的末尾移除集合。****

     ****下面的例子演示了从集合向量的末尾移除集合:

    ## C++

    ```
    // C++ program to demonstrate
    // the removal of sets from
    // the end of vector of sets
    #include <bits/stdc++.h>
    using namespace std;

    // Defining the number of sets
    // in the vector and number of
    // elements in each set
    #define ROW 4
    #define COL 5

    // Driver Code
    int main()
    {
        // Initialize the
        // vector of sets
        vector<set<int> > v;

        // Elements to insert
        // in column
        int num = 10;

        // Inserting elements
        // into vector
        for (int i = 0; i < ROW; i++) {

            // Vector to store
            // column elements
            set<int> s;

            for (int j = 0; j < COL; j++) {
                s.insert(num);
                num += 5;
            }

            // Push the set
            // into the vector
            v.push_back(s);
        }

        // Display the vector of sets
        // before removal of sets
        cout << "Before Removal:" << endl;
        for (int i = 0; i < v.size(); i++) {

            for (auto x : v[i])
                cout << x << " ";
            cout << endl;
        }

        // Remove sets from last
        // index of the vector
        v.pop_back();
        v.pop_back();

        // Display the vector of sets
        // after removal of sets
        cout << endl
             << "After Removal:" << endl;

        for (int i = 0; i < v.size(); i++) {

            for (auto x : v[i])
                cout << x << " ";
            cout << endl;
        }
        return 0;
    }
    ```

    **Output:**

    ```
    Before Removal:
    10 15 20 25 30 
    35 40 45 50 55 
    60 65 70 75 80 
    85 90 95 100 105 

    After Removal:
    10 15 20 25 30 
    35 40 45 50 55

    ```**** 
2.  ****元素的值一旦被添加到集合中就不能被修改，尽管可以移除该元素的值。 [erase()](https://www.geeksforgeeks.org/seterase-c-stl/) 函数用于从集合向量的特定集合中移除特定元素。****

    ****下面的例子演示了从集合向量的特定集合中移除给定的集合元素:****

    ## ****C++****

    ```
    **// C++ program to demonstrate
    // the removal of sets from
    // the end of vector of sets
    #include <bits/stdc++.h>
    using namespace std;

    // Defining the number of sets
    // in the vector and number of
    // elements in each set
    #define ROW 4
    #define COL 5

    // Driver Code
    int main()
    {
        // Initialize vector of sets
        vector<set<int> > v;

        // Elements to insert
        // in column
        int num = 10;

        // Inserting elements
        // into vector
        for (int i = 0; i < ROW; i++) {

            // Vector to store
            // column elements
            set<int> s;

            for (int j = 0; j < COL; j++) {
                s.insert(num);
                num += 5;
            }

            // Push the set
            // into the vector
            v.push_back(s);
        }

        // Display the vector of sets
        // before removal of sets
        cout << "Before Removal:" << endl;

        for (int i = 0;
             i < v.size(); i++) {

            for (auto x : v[i])
                cout << x << " ";
            cout << endl;
        }

        // Erase 70 from 3rd set
        v[2].erase(70);

        // Erase 55 from 2nd set
        v[1].erase(55);

        // Display the vector of sets
        // after removal of sets
        cout << endl
             << "After Removal:" << endl;

        for (int i = 0; i < v.size(); i++) {

            for (auto x : v[i])
                cout << x << " ";
            cout << endl;
        }
        return 0;
    }**
    ```

    ******Output:**

    ```
    Before Removal:
    10 15 20 25 30 
    35 40 45 50 55 
    60 65 70 75 80 
    85 90 95 100 105 

    After Removal:
    10 15 20 25 30 
    35 40 45 50 
    60 65 75 80 
    85 90 95 100 105

    ```**** 

****下面的例子演示了集合向量的使用:****

****给定一个字符串 **S** ，任务是将给定的字符串 **S** 分成三组不同的字符，即元音、辅音或一个特殊字符。****

****下面是上述问题的实现:****

## ****C++****

```
**// C++ program to implement vector of sets
#include <bits/stdc++.h>
using namespace std;

// Function to print set
// of different characters
void separateChar(string s)
{
    // Vector of set
    vector<set<char> > v(3);

    // Insert data in vector of set
    for (int i = 0;
         i < s.length(); i++) {

        if (s[i] >= 'a'
            && s[i] <= 'z') {

            // Insert vowels
            if (s[i] == 'a' || s[i] == 'e'
                || s[i] == 'i' || s[i] == 'o'
                || s[i] == 'u')
                v[0].insert(s[i]);

            // Insert consonants
            else
                v[1].insert(s[i]);
        }
        // Insert special characters
        else
            v[2].insert(s[i]);
    }

    // Iterate over all the sets
    for (int i = 0; i < 3; i++) {

        cout << "Elements of set "
             << i + 1 << " :";

        // Print elements of each set
        for (auto it : v[i]) {

            cout << it << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    string s = "geeks@for&geeks@";

    // Function Call
    separateChar(s);
}**
```

******Output:**

```
Elements of set 1 :e o 
Elements of set 2 :f g k r s 
Elements of set 3 :& @

```****