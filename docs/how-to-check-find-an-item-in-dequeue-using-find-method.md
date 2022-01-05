# 如何使用 find()方法

在出列中检查/查找项目

> 原文:[https://www . geesforgeks . org/如何使用查找方法检查查找出队中的项目/](https://www.geeksforgeeks.org/how-to-check-find-an-item-in-dequeue-using-find-method/)

[**【find()**](https://www.geeksforgeeks.org/stdfind-in-c/)函数查找给定数字范围内的元素。返回范围[第一个，最后一个]中第一个元素的迭代器，该元素与要搜索的值相等。如果没有找到这样的元素，函数返回 last。

**语法:**

> 输入操作符查找(输入操作符第一，输入操作符最后，常量 T&值)

**参数:**

> **第一个，最后一个:**将迭代器输入到序列的初始和最终位置。搜索的范围是[第一个，最后一个]，包含第一个和最后一个之间的所有元素，包括第一个指向的元素，但不包括最后一个指向的元素。
> 
> **值:**要在范围内搜索的值。

**返回值:**

> 范围内第一个元素的迭代器，比较等于 val。
> 如果没有元素匹配，函数返回最后一个。

**示例:**

> **输入:** 10 20 30 40
> **输出:**在位置 2 找到元素 30(从零开始计数)
> 
> **输入:**8 5 9 2 7 1 3 10
> T3】输出:元素 4 未找到。

**例 1:** 下面是在 deque 中实现 find()函数的 C++程序。

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
#include<bits/stdc++.h>
using namespace std;

// Function to find element
// in a deque
void find(deque<int> q)
{
  deque<int>::iterator itr;
  itr = find(q.begin(), q.end(), 2);
  if(itr != q.end())
  {
    cout << "Found";
  }
  else
  {
    cout << "Not Found";
  }
}
// Driver code
int main() 
{
  // Declaring a deque
  deque<int> q;

  // Initializing deque
  q.push_back(1);
  q.push_back(2);
  q.push_back(3);
  q.push_back(4);
  q.push_back(5);

  // Calling function find()
  find(q);
  return 0;
}
```

**输出:**

> 找到

**示例 2:** 下面是一个 C++程序，演示如何在出列中查找元素。

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
#include<bits/stdc++.h>
using namespace std;

// Function to find an element 
// in a deque
void find(deque<string> q)
{
  deque<string>::iterator itr;
  itr = find(q.begin(), q.end(), 
             "Raj");

  if(itr != q.end())
  {
    cout << "Found";
  }
  else
  {
    cout << "Not Found";
  }
}

// Driver code
int main() 
{
  // Declaring a deque
  deque<string> q;

  // Initializing a deque 
  q.push_back("Akshit");
  q.push_back("Nikita");
  q.push_back("Deeksha");
  q.push_back("Nandish");
  q.push_back("Rajat");

  // Calling find() function
  find(q);

  return 0;
}
```

**输出:**

> 未发现

**<u>STD::c++中的 find()vs</u>中的 find**

在 **std::find()中，在 C++** 中，搜索的范围是【第一个，最后一个】，包含第一个和最后一个之间的所有元素，包括第一个指向的元素，但不包括最后一个指向的元素。
在**使用 find()函数在德格**中查找项目的情况下，搜索的范围是【第一个，最后一个】，即包括第一个和最后一个。

下面是 C++程序，演示如何在出列中找到一个项目。

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
#include<bits/stdc++.h>
using namespace std;

void find(deque<int> q)
{
  deque<int>::iterator itr;  
  itr = find(q.begin(), 
             q.end(), 5);
  if(itr != q.end())
  {
    cout << "Found";
  }
  else
  {
    cout << "Not Found";
  }
}

// Driver code
int main() 
{
  // Declaring a deque
  deque<int> q;

  // Initializing deque
  q.push_back(1);
  q.push_back(2);
  q.push_back(3);
  q.push_back(4);
  q.push_back(5);

  // Calling find() function
  find(q);

  return 0;
}
```

**输出:**

> 找到