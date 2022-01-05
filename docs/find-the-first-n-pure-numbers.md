# 求前 N 个纯数字

> 原文:[https://www . geesforgeks . org/find-first-n-pure-numbers/](https://www.geeksforgeeks.org/find-the-first-n-pure-numbers/)

给定一个整数 **N** ，任务是先打印第 **N <sup>第</sup>T5】个纯数字。如果一个数**

1.  它有偶数位数。
2.  所有数字要么是 **4** 要么是 **5** 。
3.  数字是回文。

前几个纯数字是 **44，55，4444，4554，5445，5555，…**

**示例:**

> **输入:**N = 4
> T3】输出: 44 55 4444 5445
> 
> **输入:**N = 10
> T3】输出:44 55 4444 4554 5445 5555 44444 454454 454454 544455

**方法:**这个想法类似于这里[讨论的方法](https://www.geeksforgeeks.org/interesting-method-generate-binary-numbers-1-n/)。在队列的每一步，我们可以通过在两边加上 4 和 5 来生成下一个数字，即前一个数字的结束和开始:

```
q.push("4" + temp + "4");
q.push("5" + temp + "5");

```

按照这种方式，我们可以处理回文和偶数长度的数字

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the first n pure numbers
void nPureNumbers(int n)
{

    queue<string> q;
    vector<string> ans;

    // Push the starting two elements
    q.push("44");
    q.push("55");
    int total = 2;

    // While generated numbers are less than n
    while (ans.size() < n) {

        string temp = q.front();
        q.pop();
        ans.push_back(temp);

        q.push("4" + temp + "4");
        q.push("5" + temp + "5");
    }

    // Sorting strings based on their value
    sort(ans.begin(), ans.end(), [](auto s, auto s2) {
        if (s.size() == s2.size())
            return s < s2;
        else
            return s.size() < s2.size();
    });

    // Print first n pure numbers
    for (auto i : ans) {
        cout << i << " ";
    }
}

// Driver code
int main()
{
    int n = 4;

    nPureNumbers(n);

    return 0;
}
```

**Output:**

```
44 55 4444 5445

```

**方法 2:** 该方法将偶数回文数分成两个相等的部分，两者互为镜像。其思想是使用与通过每隔一位翻转来构建二进制计数器相同的方法来构建第一部分；只不过，我们不是翻转 0 和 1，而是翻转 4 和 5。之后，我们使用数字的第一部分和回文属性来创建最终的纯数字。

```
44, 55, 4444, 4554... can be separated out into 
 4 | 4
 5 | 5
44 | 44
45 | 54
54 | 45
55 | 55

```

这些数字模仿了第一个“k”位的二进制数的特性，其中 k = 1、2、3 等等。

```
 0
 1
00
01
10
11

```

因此，我们从每次迭代后翻转最后一位开始，然后移动到每 2 次迭代后翻转的(k-1)位，以此类推。第一次翻转 n 次，第二次翻转 n/2 次，以此类推。

因为 n 是 k 位的所有可能数的和，其中 k= 1，2，3…，我们的数将是 2 + 4 + 8 + …2 <sup>k</sup> 个数的和。我们连续地将 n 除以 2，如果它的值等于零，我们就停止，因为不需要再添加更多的位，也因为在下一次迭代中，这个数字将在两倍于上一次迭代的元素数后翻转。

我们可以使用堆栈来存储值，然后按顺序弹出它们，或者通过将数据存储在字符串中并简单地反转它，这比堆栈占用的空间少。

```
#include <bits/stdc++.h>
using namespace std;

// Creating a function 'pure' that returns the pure number 
// in the form of a string.
string pure(int n)
{
    // initializing string p where the number will be stored
    string p; 

    // It keeps on adding numbers as long as n>0
    while (n > 0) { 

        // To equalize the value of n to the corresponding flips 
        n--; 
        if (n % 2 == 0)
            p.append("4");
        else
            p.append("5");

        // Dividing n by 2 to move to the next bit
        n /= 2; 
    }

    int len = p.length(); // Taking the length of the string
    reverse(p.begin(), p.end()); // Reversing the string

    for (int i = len - 1; i >= 0; i--) // Building the palindrome
        p += p[i];

    return p;
}

int main()
{
    for (int i = 1; i <= 10; i++)
        cout << pure(i) << " "; // Print Ith pure number

    return 0;
}
```

**Output:**

```
44 55 4444 4554 5445 5555 444444 445544 454454 455554
```