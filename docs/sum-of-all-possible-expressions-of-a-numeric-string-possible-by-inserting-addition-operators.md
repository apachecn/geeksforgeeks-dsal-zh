# 通过插入加法运算符

对一个数字串的所有可能表达式求和

> 原文:[https://www . geeksforgeeks . org/通过插入加法运算符对数字字符串进行所有可能的表达式求和/](https://www.geeksforgeeks.org/sum-of-all-possible-expressions-of-a-numeric-string-possible-by-inserting-addition-operators/)

给定一个长度为 **N** 的数字[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是通过多次在字符串字符之间插入**'+**运算符来找到所有可能表达式的总和。

**示例:**

> **输入:** str = "125"
> **输出:** 176
> **解释:**
> 在第一个索引后插入“+”将 str 修改为“1+25”且值= 26
> 在第二个索引后插入“+”将 str 修改为“12+5”且值= 17
> 在第一个和第二个索引后插入“+”将 str 修改为“1+2+5”且值= 8
> 因此，所有可能表达式的总和为 125
> 
> **输入:**str = " 9999999999 "
> T3】输出: 12656242944

**方法:**想法是以所有可能的方式在字符串的所有可能的索引处插入 **'+'** 运算符，并计算总和。最后，打印得到的总和。按照以下步骤解决问题:

*   初始化一个变量，比如说 **sumOfExp** 来存储所有可能表达式的总和，方法是在字符串的所有可能索引处插入**“+”**运算符。
*   [迭代生成字符串所有可能的索引子集](https://www.geeksforgeeks.org/power-set/)。对于索引的每个子集，在该子集的元素处插入“+”运算符，并将 **sumOfExp** 增加当前表达式的总和。
*   最后打印 **sumOfExp** 的值。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find sum of all expressions by
# inserting '+' operator at all possible indices
def findSumOfExpressions(S, N):

    # Stores sum of all expressions by inserting
    # '+' operator at all possible indices
    sumOfExp = 0

    # Generate all possible subset
    # of indices iteratively
    for i in range(2 ** (N - 1)):

        # Stores sum of 
        # current expressions
        ans_sub = 0

        # Stores numbers of
        # current expressions
        subst = S[0]

        # Traverse the string at insert + at
        # current subset of indices
        for j in range(N - 1):

            # If current index exists
            # in the current subset
            if (i >> j) & 1:

                # Update ans_sub
                ans_sub += int(subst)

                # Update subst
                subst = S[j + 1]
            else:

                # Update subst
                subst += S[j + 1]

            # + can't be inserted after
            # the last index    
            if j == N - 2:
                ans_sub += int(subst)

        # Update ans
        sumOfExp += ans_sub

    # Base case     
    if N == 1:
        print(int(S))
    else:

        # Print answer
        print(sumOfExp)

# Driver Code
if __name__ == '__main__':

    # Given string
    S = "9999999999"

    # Length of the string
    N = len(S)

    # Function call
    findSumOfExpressions(S, N)
```

**Output:**

```
12656242944

```

***时间复杂度:**O(2<sup>N</sup>* N)*
***辅助空间:** O(1)*