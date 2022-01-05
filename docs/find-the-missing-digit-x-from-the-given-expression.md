# 从给定的表达式中找出缺失的数字 x

> 原文:[https://www . geeksforgeeks . org/从给定表达式中找到缺少的数字 x/](https://www.geeksforgeeks.org/find-the-missing-digit-x-from-the-given-expression/)

给定一个字母数字字符串，由单个字母表 **X** 组成，表示形式的一种表达:

> **A 运算符 B = C**
> 其中 A、B 和 C 表示整数，运算符可以是+、-、*或/

任务是计算整数 A、B 和 C 中任何一个出现的缺失数字 **X** ，使得给定的表达式有效。

**示例:**

> **输入:** S = "3x + 12 = 46"
> **输出:** 4
> **说明:**
> 46 减 12 得 34。
> 所以，在比较 3x 和 34 的时候。x = 4 的值
> 
> **输入:**S =“4–2 = x”
> **输出:** 2
> **解释:**
> 解出方程后，x 的值= 2。

**方法:**按照以下步骤解决问题:

*   [拆分字符串](https://www.geeksforgeeks.org/split-string-java-examples/)提取两个操作数，运算符和结果。
*   检查结果中是否存在 X。如果是这样，那么通过用运算符对第一个操作数和第二个操作数进行运算来计算结果的值。
*   否则，如果结果中不存在 X。然后检查第一个操作数中是否存在 X。如果是，那么对第二个操作数应用运算，并用运算符进行结果运算。
*   否则，如果第一个操作数中也没有 X。然后检查第二个操作数中是否存在 X。如果是这样，那么对第一个操作数应用运算，并用运算符进行结果运算。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program to find missing
# digit x in expression

def MissingDigit(exp):

    # Split the expression to
    # extract operands, operator
    # and resultant
    exp = list(exp.split())

    first_operand = exp[0]
    operator = exp[1]
    second_operand = exp[2]
    resultant = exp[-1]

    # If x is present in resultant
    if 'x' in resultant:
        x = resultant
        first_operand = int(first_operand)
        second_operand = int(second_operand)

        if operator == '+':
            res = first_operand + second_operand
        elif operator == '-':
            res = first_operand - second_operand
        elif operator == '*':
            res = first_operand * second_operand
        else:
            res = first_operand // second_operand

     # If x in present in operands
    else:

        resultant = int(resultant)

        # If x in the first operand
        if 'x' in first_operand:

            x = first_operand
            second_operand = int(second_operand)

            if operator == '+':
                res = resultant - second_operand
            elif operator == '-':
                res = resultant + second_operand
            elif operator == '*':
                res = resultant // second_operand
            else:
                res = resultant * second_operand

        # If x is in the second operand
        else:

            x = second_operand
            first_operand = int(first_operand)

            if operator == '+':
                res = resultant-first_operand
            elif operator == '-':
                res = first_operand - resultant
            elif operator == '*':
                res = resultant // first_operand
            else:
                res = first_operand // resultant

    res = str(res)
    k = 0
    for i in x:
        if i == 'x':
            result = res[k]
            break
        else:
            k = k + 1

    return result

# Driver Code
if __name__ == '__main__':
    # input expression
    exp = "3x + 12 = 46"

    print(MissingDigit(exp))
```

**Output:**

```
4

```

**时间复杂度:** O(L)，其中是方程的长度。
**辅助空间:** O(1)