# 从文本文件中排序字符串

> 原文:[https://www . geesforgeks . org/sorting-strings-from-text-file/](https://www.geeksforgeeks.org/sorting-strings-from-the-text-file/)

给定一个由字符串组成的文本文件**“file . txt”**，任务是[在该文本文件中按字母顺序对所有字符串](https://www.geeksforgeeks.org/python-how-to-sort-a-list-of-strings/)进行排序。

[![](img/4eabc570b2c9271188ac12b638474b6a.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200731200026/Web19201.png)

**方法:**思路是使用[文件处理](https://www.geeksforgeeks.org/tag/c-file-handling/)的概念和一个包含所有字符串的文本文件(比如 **file.txt** )。以下是步骤:

*   [使用](https://www.geeksforgeeks.org/c-program-to-create-a-file/) [fopen()](https://www.geeksforgeeks.org/c-fopen-function-with-examples/) 创建文件，并使用 [fprintf()](https://www.geeksforgeeks.org/fprintf-in-c/) 将名称插入文件。
*   使用 [fclose()](https://www.geeksforgeeks.org/php-fclose-function/) 关闭文件。
*   重新打开文件以读取名称。
*   使用 [fscanf()](https://www.geeksforgeeks.org/scanf-and-fscanf-in-c-simple-yet-poweful/) 从文件中读取或扫描名称，并将其存储在字符串的[向量](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)中。
*   使用 [sort()函数](https://www.geeksforgeeks.org/sort-c-stl/)对向量中存储的给定字符串进行排序。
*   现在，将排序后的字符串插入该文件并打印出来。

下面是上述方法的实现:

## C++

```
// C++ program to sort given array
// of string stored in a file
#include <bits/stdc++.h>
#include <cstdlib>
#include <cstring>
#include <fstream>
using namespace std;

// Driver Code
int main()
{
    int N, i, j;

    // File pointer to open file
    FILE* f;

    // fopen() for creating of a file
    f = fopen("file.txt", "w");

    // Input number of strings
    // to be inserted in file
    cin >> n;

    vector<int> name(N);

    // Insert the strings into file
    for (i = 0; i < n; i++) {

        // Insert names in file
        cin >> name[i];

        // Writing into the file
        fprintf(f, "%s", name[i]);
    }

    // Close the file
    fclose(f);

    // Reopening in read mode
    f = fopen("file.txt", "r");

    // Check does file exist or not
    if (f == NULL) {
        cout << "File doesn't exist!";
        return 0;
    }

    // Read the file until it
    // encounters end of line
    while (!feof(f)) {
        fscanf(f, "%s", name[i]);
        i++;
    }
    n = i - 1;

    // Sort the strings
    sort(name.begin(), name.end());

    // Insert the strings into file
    // after sorting
    for (i = 0; i < n; i++) {

        // Write into the file
        fprintf(f, "%s", name[i]);
    }

    // Print the sorted names
    for (i = 0; i < n; i++) {
        cout << name[i] << '\n';
    }

    return 0;
}
```

**输入文件:**

[![](img/e88e677a0405952bd18e20b96b59b34b.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20201123150939/InputFile.png)

**输出文件:**

[![](img/5ec2c7533321a59aae47567e5aa782f0.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20201123151009/OutputFile.png)