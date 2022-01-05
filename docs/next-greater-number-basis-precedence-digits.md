# 基于数字优先的下一个更大的数字

> 原文:[https://www . geeksforgeeks . org/next-better-number-basis-preference-digits/](https://www.geeksforgeeks.org/next-greater-number-basis-precedence-digits/)

给定一个包含 T2 数字的数字。问题是根据给定的数字优先级，在**数**中使用相同的数字组找到下一个更大的数字。例如数字的优先顺序为 **1、6、4、5、2、9、8、0、7、3** ，简单来说就是**1<6<4<5<2<9<8<0<7<3**。如果无法形成下一个更大的数字，则打印原始数字。

示例:

```
Input : num = "231447"
        pre[] = {1, 6, 7, 5, 2, 9, 8, 0, 4, 3}
Output : 237144
According to the precedence of digits 1 is 
being considered as the smallest digit and 3
is being considered as the largest digit.

Input : num = "471"
        pre[] = {1, 6, 7, 5, 2, 9, 8, 0, 4, 3}
Output : 471
```

**进场:**以下是步骤:

1.  创建一个大小为“10”的**优先级[]** 数组。借助优先级数组**pre【】**为**优先级【】**中的每个数字分配一个优先级编号，其中“1”被视为最小优先级，“10”被视为最高优先级。
2.  使用带有手动定义的比较函数的[STL c++ next _ 置换](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)找到下一个更大的置换。

## C++

```
// C++ implementation to find the next greater number
// on the basis of precedence of digits
#include <bits/stdc++.h>

using namespace std;

#define DIGITS 10

// priority[] to store the priority of digits
// on the basis of pre[] array. Here '1' is being
// considered as the smallest priority as '10' as
// the highest priority
int priority[DIGITS];

// comparator function used for finding the
// the next greater permutation
struct compare {
  bool operator()(char x, char y) {
    return priority[x - '0'] < priority[y - '0'];
  }
};

// function to find the next greater number
// on the basis of precedence of digits
void nextGreater(char num[], int n, int pre[]) {
  memset(priority, 0, sizeof(priority));

  // variable to assign priorities to digits
  int assign = 1;

  // assigning priorities to digits on
  // the basis of pre[]
  for (int i = 0; i < DIGITS; i++) {
    priority[pre[i]] = assign;
    assign++;
  }

  // find the next greater permutation of 'num'
  // using the compare() function
  bool a = next_permutation(num, num + n, compare());

  // if the next greater permutation does not exists
  // then store the original number back to 'num'
  // using 'pre_permutation'.
  if (a == false)
    prev_permutation(num, num + n, compare());
}

// Driver program to test above
int main() {
  char num[] = "231447";
  int n = strlen(num);
  int pre[] = {1, 6, 7, 5, 2, 9, 8, 0, 4, 3};
  nextGreater(num, n, pre);
  cout << "Next Greater: " << num;
  return 0;
}
```

**输出:**

```
Next Greater: 237144
```

时间复杂度:O(n)。
辅助空间:O(1)。