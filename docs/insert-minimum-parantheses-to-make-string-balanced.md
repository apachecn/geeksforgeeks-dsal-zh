# 插入最小偏角，使弦平衡

> 原文:[https://www . geesforgeks . org/insert-minimum-Paran thesis-to-make-string-balanced/](https://www.geeksforgeeks.org/insert-minimum-parantheses-to-make-string-balanced/)

给定一串数字 S，任务是在字符串 S 中插入最少数量的左右括号，这样得到的字符串是平衡的，每个数字 d 必须在 d 对匹配的括号内。

**示例:**

> **输入:** S = 221
> **输出:** ((22)1)
> **解释:**
> 字符串((2))((2))(1)不是有效解，因为它不是最小长度。
> 
> **输入:**S = 3102
> T3】输出:((3)1)0((2))

**进场:**

1.  首先，我们将为第一个元素插入所需的左括号，并将其值存储在 **p** 中。
2.  然后我们迭代字符串，从 1 到字符串的长度
    *   从前一个元素中减去当前元素(int(S[I-1])–int(S[I]))，并将其值存储在变量 **w** 中。
    *   如果 **w > = 0** ，则插入 w 右括号，并将 p 更新为(p–w)。否则，
    *   在左括号中插入当前值减 p(int(S[I])–p)，并将 p 更新为等于当前值。
    *   在循环的最后，我们通过插入所需的右括号来平衡括号。

下面是上述方法的实现:

```
# Python 3 implementation to balance 
# the string

# Function to insert matching parantheses
def ParanthesesNesting(S):

    # To check first element if 0 or not
    if S[0]=='0':
        out ='0'
        p = 0

    else:
        out ='('*(int(S[0])) + S[0]
        p = int(S[0])

    # Loop from 1 to length of input_string
    for i in range(1, (len(S))):
        w = int(S[i - 1]) - int(S[i])

        # To check w is greater than or 
        # equal to zero or not
        if(w >= 0):
            out = out + ')' * int(w) + S[i]
            p = p - w

        else:
            out = out + '(' * (int(S[i]) - p) + S[i]
            p = int(S[i])

    y = out.count('(') - out.count(')')
    out += ')' * int(y)
    return(out)

# Driver code 
if __name__ == '__main__': 
    string ='221'
    print(ParanthesesNesting(string))
```

**Output:**

```
((22)1)

```