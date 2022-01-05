# C 中的 CHAR _ BIT

> 原文:[https://www.geeksforgeeks.org/char_bit-in-c/](https://www.geeksforgeeks.org/char_bit-in-c/)

**CHAR_BIT :** 是 CHAR 中的位数。如今，几乎所有的架构都使用每字节 8 位(但情况并非总是如此，一些较旧的机器过去使用 7 位字节)。它可以在中找到

让我们看看它的应用。假设我们希望打印一个整数的字节表示。

**示例:**

```
Input  : 4
Output : 00000000 00000000 00000000 00000100

Input  : 12
Output : 00000000 00000000 00000000 00001100 

```

```
// CPP program to print byte by byte presentation
#include <bits/stdc++.h>
using namespace std;

// function in which number and intitally 0 is passed
void printInBinary(int num)
{
    int n = CHAR_BIT*sizeof(num);
    stack<bool> s;
    for (int i=1; i<=n; i++)
    {
        s.push(num%2);
        num = num/2; 
    }     
    for (int i=1; i<=n; i++)
    {
        cout << s.top();
        s.pop();

        // Put a space after every byte. 
        if (i % CHAR_BIT == 0)
        cout << " "; 
    }
}

int main()
{
    int num = 12;
    printInBinary(num);
    return 0;
}
```

**输出:**

```
00000000 00000000 00000000 00001100 

```

本文由 <font color="green">**阿普瓦·阿加瓦尔**</font> 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。