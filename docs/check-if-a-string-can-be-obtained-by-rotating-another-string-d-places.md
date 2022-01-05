# 检查一根弦是否可以通过旋转另一根弦 d 个位置获得

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-by-rotation-other-string-d-places/](https://www.geeksforgeeks.org/check-if-a-string-can-be-obtained-by-rotating-another-string-d-places/)

给定两个字符串 **str1** 和 **str2** 以及一个整数 **d** ，任务是检查 **str2** 是否可以通过将 **str1** 旋转 **d** 个位置(向左或向右)来获得。

**示例:**

> **输入:**str 1 =“abcdefg”，str 2 =“cdefgab”，d = 2
> T3】输出:是
> 向左旋转 str1 2 位。
> 
> **输入:**str 1 =“abcdefg”，str 2 =“cdfdawb”，d = 6
> T3】输出:否

**方法:**已经讨论了解决相同问题的方法[这里](https://www.geeksforgeeks.org/check-string-can-obtained-rotating-another-string-2-places/)。在本文中，[反转算法](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)用于在 O(n)中向左和向右旋转字符串。如果 **str1** 的任意一个旋转等于 **str2** ，则打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to reverse an array from left
// index to right index (both inclusive)
void ReverseArray(string& arr, int left, int right)
{
    char temp;
    while (left < right) {
        temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}

// Function that returns true if str1 can be
// made equal to str2 by rotating either
// d places to the left or to the right
bool RotateAndCheck(string& str1, string& str2, int d)
{

    if (str1.length() != str2.length())
        return false;

    // Left Rotation string will contain
    // the string rotated Anti-Clockwise
    // Right Rotation string will contain
    // the string rotated Clockwise
    string left_rot_str1, right_rot_str1;
    bool left_flag = true, right_flag = true;
    int str1_size = str1.size();

    // Copying the str1 string to left rotation string
    // and right rotation string
    for (int i = 0; i < str1_size; i++) {
        left_rot_str1.push_back(str1[i]);
        right_rot_str1.push_back(str1[i]);
    }

    // Rotating the string d positions to the left
    ReverseArray(left_rot_str1, 0, d - 1);
    ReverseArray(left_rot_str1, d, str1_size - 1);
    ReverseArray(left_rot_str1, 0, str1_size - 1);

    // Rotating the string d positions to the right
    ReverseArray(right_rot_str1, 0, str1_size - d - 1);
    ReverseArray(right_rot_str1, str1_size - d, str1_size - 1);
    ReverseArray(right_rot_str1, 0, str1_size - 1);

    // Compairing the rotated strings
    for (int i = 0; i < str1_size; i++) {

        // If cannot be made equal with left rotation
        if (left_rot_str1[i] != str2[i]) {
            left_flag = false;
        }

        // If cannot be made equal with right rotation
        if (right_rot_str1[i] != str2[i]) {
            right_flag = false;
        }
    }

    // If both or any one of the rotations
    // of str1 were equal to str2
    if (left_flag || right_flag)
        return true;
    return false;
}

// Driver code
int main()
{

    string str1 = "abcdefg";
    string str2 = "cdefgab";

    // d is the rotating factor
    int d = 2;

    // In case length of str1 < d
    d = d % str1.size();

    if (RotateAndCheck(str1, str2, d))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to reverse an array from left
# index to right index (both inclusive)
def ReverseArray(arr, left, right) :

    while (left < right) :
        temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left += 1;
        right -= 1;

# Function that returns true if str1 can be
# made equal to str2 by rotating either
# d places to the left or to the right
def RotateAndCheck(str1, str2, d) :

    if (len(str1) != len(str2)) :
        return False;

    # Left Rotation string will contain
    # the string rotated Anti-Clockwise
    # Right Rotation string will contain
    # the string rotated Clockwise
    left_rot_str1 = []; right_rot_str1 = [];
    left_flag = True; right_flag = True;
    str1_size = len(str1);

    # Copying the str1 string to left rotation string
    # and right rotation string
    for i in range(str1_size) :
        left_rot_str1.append(str1[i]);
        right_rot_str1.append(str1[i]);

    # Rotating the string d positions to the left
    ReverseArray(left_rot_str1, 0, d - 1);
    ReverseArray(left_rot_str1, d, str1_size - 1);
    ReverseArray(left_rot_str1, 0, str1_size - 1);

    # Rotating the string d positions to the right
    ReverseArray(right_rot_str1, 0, str1_size - d - 1);
    ReverseArray(right_rot_str1,
                 str1_size - d, str1_size - 1);
    ReverseArray(right_rot_str1, 0, str1_size - 1);

    # Compairing the rotated strings
    for i in range(str1_size) :

        # If cannot be made equal with left rotation
        if (left_rot_str1[i] != str2[i]) :
            left_flag = False;

        # If cannot be made equal with right rotation
        if (right_rot_str1[i] != str2[i]) :
            right_flag = False;

    # If both or any one of the rotations
    # of str1 were equal to str2
    if (left_flag or right_flag) :
        return True;
    return False;

# Driver code
if __name__ == "__main__" :

    str1 = list("abcdefg");
    str2 = list("cdefgab");

    # d is the rotating factor
    d = 2;

    # In case length of str1 < d
    d = d % len(str1);

    if (RotateAndCheck(str1, str2, d)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to reverse an array from left
// index to right index (both inclusive)
function ReverseArray(arr, left, right)
{
    var temp;
    while (left < right)
    {
        temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}

// Function that returns true if str1 can be
// made equal to str2 by rotating either
// d places to the left or to the right
function RotateAndCheck(str1, str2, d)
{
    if (str1.length !== str2.length)
        return false;

    // Left Rotation string will contain
    // the string rotated Anti-Clockwise
    // Right Rotation string will contain
    // the string rotated Clockwise
    var left_rot_str1 = [];
    var right_rot_str1 = [];
    var left_flag = true,
    right_flag = true;
    var str1_size = str1.length;

    // Copying the str1 string to left rotation string
    // and right rotation string
    for(var i = 0; i < str1_size; i++)
    {
        left_rot_str1.push(str1[i]);
        right_rot_str1.push(str1[i]);
    }

    // Rotating the string d positions to the left
    ReverseArray(left_rot_str1, 0, d - 1);
    ReverseArray(left_rot_str1, d, str1_size - 1);
    ReverseArray(left_rot_str1, 0, str1_size - 1);

    // Rotating the string d positions to the right
    ReverseArray(right_rot_str1, 0, str1_size - d - 1);
    ReverseArray(right_rot_str1, str1_size - d,
                 str1_size - 1);
    ReverseArray(right_rot_str1, 0, str1_size - 1);

    // Compairing the rotated strings
    for(var i = 0; i < str1_size; i++)
    {
        // If cannot be made equal with left rotation
        if (left_rot_str1[i] !== str2[i])
        {
            left_flag = false;
        }

        // If cannot be made equal with right rotation
        if (right_rot_str1[i] !== str2[i])
        {
            right_flag = false;
        }
    }

    // If both or any one of the rotations
    // of str1 were equal to str2
    if (left_flag || right_flag)
        return true;

    return false;
}

// Driver code
var str1 = "abcdefg";
var str2 = "cdefgab";

// d is the rotating factor
var d = 2;

// In case length of str1 < d
d = d % str1.length;

if (RotateAndCheck(str1, str2, d))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rdtank

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(n)