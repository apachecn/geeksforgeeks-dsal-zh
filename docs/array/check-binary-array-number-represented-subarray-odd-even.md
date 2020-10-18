# 在二进制数组中检查子数组表示的数字是奇数还是偶数

> 原文： [https://www.geeksforgeeks.org/check-binary-array-number-represented-subarray-odd-even/](https://www.geeksforgeeks.org/check-binary-array-number-represented-subarray-odd-even/)

给定一个数组，使其所有项均为 0 或 1。您需要告诉子数组`a[l..r]`表示的数字为奇数或偶数。

**示例**：

```
Input : arr = {1, 1, 0, 1}
        l = 1, r = 3
Output : odd
        number represented by arr[l...r] is 
        101 which 5 in decimal form which is 
        odd

Input :  arr = {1, 1, 1, 1}
         l = 0, r = 3
Output : odd

```



这里要注意的重要一点是，二进制形式的所有奇数均以 1 作为其最右边的位，所有偶数均以 0 作为其最右边的位。

原因很简单，除了最右边的位以外，所有其他位都具有偶数，偶数之和始终为偶数。现在，最右边的位可以具有 1 或 0 的值，因为我们知道偶数+奇数=奇数，因此当最右边的位 为 1 时，数字为奇数；为 0 时，数字为偶数。

因此，要解决此问题，我们只需要检查`a[r]`是 0 还是 1，并因此打印奇数或偶数。

## C++ 

```cpp

// C++ program to find if a subarray 
// is even or odd. 
#include<bits/stdc++.h> 
using namespace std; 

// prints if subarray is even or odd 
void checkEVENodd (int arr[], int n, int l, int r) 
{ 
    // if arr[r] = 1 print odd 
    if (arr[r] == 1) 
        cout << "odd" << endl; 

    // if arr[r] = 0 print even 
    else
        cout << "even" << endl; 
} 

// driver code 
int main() 
{ 
    int arr[] = {1, 1, 0, 1}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    checkEVENodd (arr, n, 1, 3); 
    return 0; 
} 

```