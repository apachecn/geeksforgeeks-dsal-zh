# 使用 STL

删除字符串中出现的所有字符

> 原文:[https://www . geesforgeks . org/从字符串中删除所有出现的字符-使用-stl/](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-character-from-a-string-using-stl/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个字符 **C** ，任务是从给定字符串中移除字符 **C** 的所有出现。

**示例:**

> **输入:**vS =“GFG IS FUN”，C =“F”
> **输出:** GG IS UN
> **解释:**
> 移除所有出现的字符‘F’将 S 修改为“GG IS UN”。
> 所以需要的输出是 **GG IS UN**
> 
> **输入:** S =“请移除空格”，C =“”
> **输出:**PLEASE move 空间
> **解释:**
> 移除字符“”的所有出现将 S 修改为“GG IS UN”。

**方法:**思路是从 [C++ STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 中使用 [erase()](https://www.geeksforgeeks.org/stdstringerase-in-cpp/) 方法和 [remove()](https://www.geeksforgeeks.org/list-remove-function-in-c-stl/) 函数。下面是从字符串中删除所有字符的语法。

> S.erase(remove(S.begin()，S.end()，c)，S.end())

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <algorithm>
#include <iostream>
using namespace std;

// Function to remove all occurrences
// of C from the string S
string removeCharacters(string S, char c)
{

    S.erase(remove(
                S.begin(), S.end(), c),
            S.end());

    return S;
}

// Driver Code
int main()
{

    // Given String
    string S = "GFG is Fun";
    char C = 'F';
    cout << "String Before: " << S << endl;

    // Function call
    S = removeCharacters(S, C);

    cout << "String After: " << S << endl;
    return 0;
}
```

**Output:** 

```
String Before: GFG is Fun
String After: GG is un
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)