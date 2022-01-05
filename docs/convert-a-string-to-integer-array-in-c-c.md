# 在 C/C++中将字符串转换为整数数组

> 原文:[https://www . geesforgeks . org/convert-a-string-to-integer-array-in-c/](https://www.geeksforgeeks.org/convert-a-string-to-integer-array-in-c-c/)

给定一个包含以“，”分隔的数字的字符串**。任务是将其转换成一个整数数组，并找到该数组的和。**

**示例:**

```
Input : str  = "2, 6, 3, 14"
Output : arr[] = {2, 6, 3, 14}
Sum of the array is = 2 + 6 + 3 + 14 = 25

Input : str = "125, 4, 24, 5543, 111"
Output : arr[] = {125, 4, 24, 5543, 111} 

```

**进场:**

*   创建一个空数组，其大小为字符串长度，并将数组的所有元素初始化为零。
*   开始解开绳子。
*   检查字符串中当前索引处的字符是否是逗号(，)。如果是，则增加数组的索引以指向数组的下一个元素。
*   否则，继续遍历字符串，直到找到一个'，'运算符，然后继续将字符转换为数字并存储在当前数组元素中。
    将字符转换为数字:

> arr[j]= arr[j]* 10+(Str[I]–48)

下面是上述想法的实现:

```
// C++ program to convert a string to
// integer array
#include <bits/stdc++.h>
using namespace std;

// Function to convert a string to
// integer array
void convertStrtoArr(string str)
{
    // get length of string str
    int str_length = str.length();

    // create an array with size as string
    // length and initialize with 0
    int arr[str_length] = { 0 };

    int j = 0, i, sum = 0;

    // Traverse the string
    for (i = 0; str[i] != '\0'; i++) {

        // if str[i] is ', ' then split
        if (str[i] == ',')
            continue;
         if (str[i] == ' '){
            // Increment j to point to next
            // array location
            j++;
        }
        else {

            // subtract str[i] by 48 to convert it to int
            // Generate number by multiplying 10 and adding
            // (int)(str[i])
            arr[j] = arr[j] * 10 + (str[i] - 48);
        }
    }

    cout << "arr[] = ";
    for (i = 0; i <= j; i++) {
        cout << arr[i] << " ";
        sum += arr[i]; // sum of array
    }

    // print sum of array
    cout << "\nSum of array is = " << sum << endl;
}

// Driver code
int main()
{
    string str = "2, 6, 3, 14";

    convertStrtoArr(str);

    return 0;
}
```

**Output:**

```
arr[] = 2 6 3 14 
Sum of array is = 25

```

**时间复杂度:** O(N)，其中 N 为字符串的长度。