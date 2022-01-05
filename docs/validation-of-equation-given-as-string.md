# 验证作为字符串给出的方程

> 原文:[https://www . geesforgeks . org/公式验证-给定为字符串/](https://www.geeksforgeeks.org/validation-of-equation-given-as-string/)

给定一个等式形式的字符串，即**A+b+ C–D = E**，其中 A、B、C、D 和 E 是整数，-、+和=是运算符。任务是打印**有效的**如果等式有效，否则打印**无效的**。
**注意:**字符串仅由集合{0，1，2，3，4，5，6，7，8，9，+，-，=}中的字符组成。

**示例:**

> **输入:** str = "1+1+1+1=7"
> **输出:**无效
> 
> **输入:**str = " 12+13-14+1 = 12 "
> T3】输出:有效

**进场:**

*   遍历字符串，将所有操作数存储在一个数组中**操作数[]** 和所有操作符存储在一个数组中**操作符[]** 。
*   现在对**操作数【0】**和**操作数【1】**执行存储在**运算符【0】**中的算术运算，并将其存储在**和**中。
*   然后在 **ans** 和**运算符【2】**上执行秒算术运算，即**运算符【1】**等等。
*   最后，将计算出的**和**与最后一个操作数进行比较，即**操作数【4】**。如果它们相等，则打印**有效**否则打印**无效**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the equation is valid
bool isValid(string str)
{
    int k = 0;
    string operands[5] = "";
    char operators[4];
    long ans = 0, ans1 = 0, ans2 = 0;
    for (int i = 0; i < str.length(); i++) {

        // If it is an integer then add it to another string array
        if (str[i] != '+' && str[i] != '=' && str[i] != '-')
            operands[k] += str[i];
        else {
            operators[k] = str[i];

            // Evaluation of 1st operator
            if (k == 1) {
                if (operators[k - 1] == '+')
                    ans += stol(operands[k - 1]) + stol(operands[k]);

                if (operators[k - 1] == '-')
                    ans += stol(operands[k - 1]) - stol(operands[k]);
            }

            // Evaluation of 2nd operator
            if (k == 2) {
                if (operators[k - 1] == '+')
                    ans1 += ans + stol(operands[k]);

                if (operators[k - 1] == '-')
                    ans1 -= ans - stol(operands[k]);
            }

            // Evaluation of 3rd operator
            if (k == 3) {
                if (operators[k - 1] == '+')
                    ans2 += ans1 + stol(operands[k]);

                if (operators[k - 1] == '-')
                    ans2 -= ans1 - stol(operands[k]);
            }
            k++;
        }
    }

    // If the LHS result is equal to the RHS
    if (ans2 == stol(operands[4]))
        return true;
    else
        return false;
}

// Driver code
int main()
{
    string str = "2+5+3+1=11";
    if (isValid(str))
        cout << "Valid";
    else
        cout << "Invalid";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function that returns true if 
# the equation is valid 
def isValid(string) :

    k = 0; 
    operands = [""] * 5 ; 
    operators = [""] * 4 ; 
    ans = 0 ; ans1 = 0; ans2 = 0; 
    for i in range(len(string)) : 

        # If it is an integer then add 
        # it to another string array 
        if (string[i] != '+' and 
            string[i] != '=' and 
                string[i] != '-') :
            operands[k] += string[i]; 
        else : 
            operators[k] = string[i]; 

            # Evaluation of 1st operator 
            if (k == 1) : 
                if (operators[k - 1] == '+') : 
                    ans += int(operands[k - 1]) + int(operands[k]); 

                if (operators[k - 1] == '-') :
                    ans += int(operands[k - 1]) - int(operands[k]); 

            # Evaluation of 2nd operator 
            if (k == 2) :
                if (operators[k - 1] == '+') :
                    ans1 += ans + int(operands[k]); 

                if (operators[k - 1] == '-') :
                    ans1 -= ans - int(operands[k]); 

            # Evaluation of 3rd operator 
            if (k == 3) : 
                if (operators[k - 1] == '+') :
                    ans2 += ans1 + int(operands[k]); 

                if (operators[k - 1] == '-') :
                    ans2 -= ans1 - int(operands[k]); 
            k += 1

    # If the LHS result is equal to the RHS 
    if (ans2 == int(operands[4])) :
        return True; 
    else :
        return False; 

# Driver code 
if __name__ == "__main__" : 

    string = "2 + 5 + 3 + 1 = 11"; 
    if (isValid(string)) :
        print("Valid"); 
    else :
        print("Invalid"); 

# This code is contributed by Ryuga
```

**Output:**

```
Valid

```