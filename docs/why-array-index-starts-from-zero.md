# 为什么数组索引从零开始？

> 原文:[https://www . geesforgeks . org/why-array-index-starts-from-zero/](https://www.geeksforgeeks.org/why-array-index-starts-from-zero/)

先决条件:[C/c++中的指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)

**原因可能有很多，但这里有两个原因:**

**原因 1 :**
考虑 int arr[100]。答案在于编译器如何解释 arr[i] ( 0 < =i < 100)。
arr[i]解释为*(arr + i)。现在，arr 是数组的地址或数组第 0 个索引元素的地址。因此，数组中下一个元素的地址是 arr + 1(因为数组中的元素存储在连续的存储单元中)，下一个位置的进一步地址是 arr + 2，以此类推。按照上面的参数，arr +我是指距离数组起始元素 I 距离的地址。因此，按照这个定义，对于数组的起始元素，I 将为零，因为起始元素距离数组的起始元素为 0。为了符合 arr[i]的定义，数组的索引从 0 开始。

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include<iostream>
using namespace std;

int main()
{
    int arr[] = {1, 2, 3, 4};

    // Below two statements mean same thing
    cout << *(arr + 1) << " ";
    cout << arr[1] << " ";

    return 0;
}
```

**Output:** 

```
2 2

```