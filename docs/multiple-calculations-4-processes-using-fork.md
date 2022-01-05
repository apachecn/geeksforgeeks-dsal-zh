# 使用 fork()

在 4 个进程中进行多次计算

> 原文:[https://www . geeksforgeeks . org/multiple-computing-4-processes-using-fork/](https://www.geeksforgeeks.org/multiple-calculations-4-processes-using-fork/)

编写一个程序创建 4 个进程:执行各种任务的父进程及其子进程:

*   How often the parent process calculates a number.
*   The first child process sort array
*   The second subprocess finds the even total number in the given array.
*   The third subprocess calculates the sum of even numbers in an array.

**示例–**

```
Input :  
2, 4, 6, 7, 9, 0, 1, 5, 8, 3

Output : 
Parent process :
the key to be searched is 7
the frequency of 7 is 1
1st child process :
the sorted array is
0 1 2 3 4 5 6 7 8 9 
2nd child process :
 Total even no are: 5 
3rd child process :
the sum is :45

```

**解释–**这里，我们已经使用了 fork()函数创建了 4 个进程三个子进程和一个父进程。因此，这里我们使用两个 fork()函数来创建 4 个进程 n1=fork()和 n2 = fork()

*   If n1 and n2 are greater than zero, it is the frequency at which the parent process calculates a number.
*   If n1 is equal to zero and n2 is greater than zero, then it is the first subprocess that sorts the given array.
*   If n1 is greater than zero and n2 is equal to zero, the second subprocess will find the even total number in the array.
*   If both n1 and n2 are equal to zero, then it is the third subelement to calculate the sum of all elements in the array.

**代码–**

```
// C++ code to demonstrate the calculation
// in parent and its 3 child processes using fork()
#include <iostream>
#include <unistd.h>

using namespace std;

int main()
{

    int a[10] = { 2, 4, 6, 7, 9, 0, 1, 5, 8, 3 };
    int n1, n2, i, j, key, c, temp;
    n1 = fork();
    n2 = fork();

    // if n1 is greater than zero
    // and n2 is greater than zero
    // then parent process executes
    if (n1 > 0 && n2 > 0) {

        int c = 0;
        cout << "Parent process :" << endl;

        // key to be searched is 7
        key = 7;
        cout << "the key to be searched is " << key << endl;

        for (i = 0; i < 10; i++) {

            if (a[i] == key)
                // frequency of key
                c++;
        }

        cout << "the frequency of " << key << " is " << c << endl;
    }

    // else if n1 is zero
    // and n2 is greater than zero
    // then 1st child process executes
    else if (n1 == 0 && n2 > 0) {

        cout << "1st child process :" << endl;

        for (i = 0; i < 10; i++) {

            for (j = 0; j < 9; j++) {

                if (a[j] > a[j + 1]) {

                    temp = a[j];
                    a[j] = a[j + 1];
                    a[j + 1] = temp;
                }
            }
        }

        cout << "the sorted array is" << endl;

        for (i = 0; i < 10; i++) {

            cout << a[i] << " ";
        }

        cout << endl;
    }

    // else if n1 is greater than zero
    // and n2 is  zero
    // then 2nd child process executes
    else if (n1 > 0 && n2 == 0) {

        int f = 0;
        cout << "2nd child process :" << endl;

        for (i = 0; i < 10; i++) {

            // counting total even numbers
            if (a[i] % 2 == 0) {

                f++;
            }
        }

        cout << " Total even no are: " << f << " ";
        cout << endl;
    }

    // else if n1 is zero
    // and n2 is zero
    // then 3rd child process executes
    else if (n1 == 0 && n2 == 0) {

        cout << "3rd child process :" << endl;

        int sum = 0;
        // summing all given keys
        for (i = 0; i < 10; i++) {

            sum = sum + a[i];
        }

        cout << "the sum is :" << sum << endl;
    }

    return 0;
}
```

**输出–**

```
Parent process :
the key to be searched is 7
the frequency of 7 is 1
1st child process :
the sorted array is
0 1 2 3 4 5 6 7 8 9 
2nd child process :
 Total even no are: 5 
3rd child process :
the sum is :45

```

本文由**希瓦尼·巴盖尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上述话题的信息，请写评论