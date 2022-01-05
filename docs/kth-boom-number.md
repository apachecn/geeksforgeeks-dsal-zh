# 第 K 根吊杆编号

> 原文:[https://www.geeksforgeeks.org/kth-boom-number/](https://www.geeksforgeeks.org/kth-boom-number/)

吊杆编号是仅由数字 2 和 3 组成的编号。给定一个整数 k(0)<k display="" the="" k-th="" boom="" number.="">**示例:**</k>

```
Input : k = 2
Output: 3

Input : k = 3
Output: 22

Input : k = 100
Output: 322323

Input: k = 1000000
Output: 3332322223223222223
```

**<u>参考:</u>**[【http://www.spoj.com/problems/TSHOW1/】](http://www.spoj.com/problems/TSHOW1/)
思路很简单就像[生成二进制数](https://www.geeksforgeeks.org/interesting-method-generate-binary-numbers-1-n/)一样。这里我们也使用同样的方法，
我们使用队列数据结构来解决这个问题。首先入队“2”，然后入队“3”这两个分别是第一个和第二个吊杆编号。现在设置 count=2，每次在队列前弹出()并在弹出数中追加“2”并增加计数++ if (count==k)然后打印当前**吊杆号**否则在弹出数中追加“3”并增加计数++ if (count==k)然后打印当前**吊杆号**。重复该过程，直到我们到达第 K 个**动臂编号**。
这种做法可以看作是以根为空弦的树的 BFS。每个节点的左子节点有 2 个附加，右子节点有 3 个附加。

下面是这个想法的实现。

## C++

```
// C++ program to find K'th Boom number
#include<bits/stdc++.h>
using namespace std;
typedef long long int ll;

// This function uses queue data structure to K'th
// Boom number
void  boomNumber(ll k)
{
    // Create an empty queue of strings
    queue<string> q;

    // Enqueue an empty string
    q.push("");

    // counter for K'th element
    ll count = 0;

    // This loop checks the value of count to
    // become equal to K when value of count
    // will be equals to k we will print the
    // Boom number
    while (count <= k)
    {
        // current Boom number
        string s1 = q.front();

        // pop front
        q.pop();

        // Store current Boom number before changing it
        string s2 = s1;

        // Append "2" to string s1 and enqueue it
        q.push(s1.append("2"));
        count++;

        // check if count==k
        if (count==k)
        {
            cout << s1 << endl; // K'th Boom number
            break;
        }

        // Append "3" to string s2 and enqueue it.
        // Note that s2 contains the previous front
        q.push(s2.append("3"));
        count++;

        // check if count==k
        if (count==k)
        {
            cout << s2 << endl; // K'th Boom number
            break;
        }
    }
    return ;
}

// Driver program to test above function
int main()
{
    ll k = 1000000;
    boomNumber(k);
    return 0;
}
```

## C#

```
// C# program to find K'th Boom number
using System;
using System.Collections;

class GFG{

// This function uses queue data structure
// to K'th Boom number
static void boomNumber(long k)
{

    // Create an empty queue of strings
    Queue q = new Queue();

    // Enqueue an empty string
    q.Enqueue("");

    // counter for K'th element
    long count = 0;

    // This loop checks the value of count to
    // become equal to K when value of count
    // will be equals to k we will print the
    // Boom number
    while (count <= k)
    {

        // current Boom number
        string s1 = (string)q.Dequeue();

        // Store current Boom number
        // before changing it
        string s2 = s1;

        // Append "2" to string s1 and
        // enqueue it
        s1 += "2";
        q.Enqueue(s1);
        count++;

        // Check if count==k
        if (count == k)
        {

            // K'th Boom number
            Console.Write(s1);
            break;
        }

        // Append "3" to string s2 and enqueue it.
        // Note that s2 contains the previous front
        s2 += "3";
        q.Enqueue(s2);
        count++;

        // Check if count==k
        if (count == k)
        {

            // K'th Boom number
            Console.Write(s2);
            break;
        }
    }
    return;
}   

// Driver code   
public static void Main(string []arg)
{
    long k = 1000000;

    boomNumber(k);
}
}

// This code is contributed by rutvik_56
```

**输出:**

```
3332322223223222223
```

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。本文由 GeeksforGeeks 团队审阅。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。