# 使用 pthread

的字符串中子字符串的频率

> 原文:[https://www . geesforgeks . org/frequency-of-a-string-in-use-pthread/](https://www.geeksforgeeks.org/frequency-of-a-substring-in-a-string-using-pthread/)

给定输入字符串和子字符串。使用 [pthreads](https://www.geeksforgeeks.org/multithreading-c-2/) 查找给定字符串中子字符串的出现频率。

**示例:**

```
Input: string = "man"
      substring = "dhimanman"
Output: 2

Input: string = "banana"
      substring = "nn"
Output: 0

```

**注意:**建议在基于 Linux 的系统中执行程序。
使用以下代码在 linux 中编译:

```
g++ -pthread program_name.cpp
```

****程序:****

```
// C++ program to find the frequency
// of occurrences of a substring
// in the given string using pthread

#include <iostream>
#include <pthread.h>
#include <stdlib.h>
#include <sys/types.h>
#include <time.h>
#include <unistd.h>
#define max 4
using namespace std;

int count[max] = { 0 };
string str, sub;

void* str_seq_count(void* args)
{
    int value = *(int*)args;
    int i, j, k, l1, l2, flag;

    // calculating length of string 1
    l1 = str.length();

    // calculating length of substring
    l2 = sub.length();

    for (i = 0 + value; i < l1; i = i + max) {

        flag = 0;
        k = i;

        for (j = 0; j < l2; j++) {

            // flag=0;
            if (sub[j] == str[k])
                k++;
            else {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            count[value] += 1;
    }
}

// Driver code
int main()
{
    int sum = 0;
    int x[max];
    for (int a = 0; a < max; a++)
        x[a] = a;

    str = "prrrogramisprrrogramming";
    sub = "rr";

    cout << "Enter the main string: "
         << str << endl;
    cout << "Enter the sequence to search: "
         << sub << endl;

    int i, l1;

    pthread_t tid[max];

    for (i = 0; i < max; i++) {
        pthread_create(&tid[i], NULL,
                       str_seq_count,
                       (void*)&x[i]);
    }
    for (i = 0; i < max; i++)
        pthread_join(tid[i], NULL);
    for (i = 0; i < max; i++)
        sum = sum + count[i];
    cout << "Frequency of substring: "
         << sum;

    return 0;
}
```

****输出:****

```
Enter the main string: prrrogramisprrrogramming
Enter the sequence to search: rr
Frequency of substring: 4 
```

****相关文章:** [字符串中子串的出现频率](https://www.geeksforgeeks.org/frequency-substring-string/)**