# 最接近 N 的最小数字仅由奇数位组成

给定整数 **N** ，任务是找到最接近 **N** 且仅具有奇数位的数字。 如果存在多个这样的数字，请打印最小值。

**示例：**

> **输入：** N = 725
> **输出：** 719
> **说明：**
> 数字 719 和 731 仅由奇数组成，并且最接近 725.由于最低为 719，因此它是必需的答案。
> 
> **输入：** N = 111
> **输出**：111

**天真的方法**：解决问题的最简单方法是迭代并找到小于和大于 N 的最接近的数字，仅以奇数为数字。 请按照以下步骤解决问题：

1.  如果 **N** 的所有数字都是奇数，则打印 **N** 作为答案。
2.  找出最接近的较小和较大的数字，并返回与 **N** 相差最小的数字。 如果发现两者与 **N** 等距，请打印较小的数字。

***时间复杂度**：O（10 <sup>（len（N）– 1）</sup>）*
***辅助空间：** O（ 1）*

**高效方法**：请按照以下步骤优化上述方法：

1.  如果 **N** 的所有数字都是奇数，则返回 **N** 。
2.  通过以下步骤有效地计算最接近 **N** 的较小数字：
    *   从左到右在 **N** 中找到第一个偶数位的位置，即 **pos** 。
    *   如果第一个偶数数字是 **0** ，则将 **0** 替换为 **9** ，并遍历所有前面的数字，并且对每个数字进行迭代（如果发现是 **1）。** ，将其替换为 **9** 。 否则，将数字减 2 并返回数字。
    *   如果没有发现前面的数字超过 **1** ，则将最高有效数字替换为 **0** 。
    *   如果第一个偶数数字不为零，则将该数字减 1。用 **9** 替换所有后续数字。
3.  通过以下步骤计算最接近 **N** 的较大数：
    *   查找第一个偶数位的位置，即 **pos** 。
    *   将**位置**处的数字加 1。
    *   遍历后续数字，并将其递增**1。**
4.  比较用 **N** 获得的各个最接近的数字的绝对差，并打印出具有最小差的那个。
5.  如果发现两个差异相等，则打印较小的数字。

下面是上述方法的实现：

## 蟒蛇

```

# Python program to implement 
# the above approach 

# Function to return the smaller 
# number closest to N made up of 
# only odd digits 
def closest_smaller(N): 

    N = str(N) 

    l = list(map(int, N)) 
    length = len(l) 

    # Stores the position of 
    # first even digit of N 
    pos = -1

    # Iterate through each digit of N 
    for i in range(length): 

        # Check for even digit. 
        if l[i] % 2 == 0: 
            pos = i 
            break

    # If the first even digit is 0 
    if l[pos] == 0: 

        # Replace 0 with 9 
        l[pos] = 9

        # Iterate over preceding 
        # digits 
        for i in range(pos - 1, -1, -1): 

            # If current digit is 1 
            if l[i] == 1: 

                # Check if it is the  
                # first digit or not 
                if i == 0: 

                    # Append leading 0's 
                    l[i] = 0
                    break

                # Otherwise, replace by 9 
                l[i] = 9

            # Otherwise 
            else: 

                # Decrease its value by 2 
                l[i] -= 2
                break

    # If the first even digit exceeds 0 
    else: 

        # Reduce the digit by 1 
        l[pos] -= 1

    # Replace all succeeding digits by 9 
    for i in range(pos + 1, length): 
        l[i] = 9

    # Remove leading 0s 
    if l[0] == 0: 
        l.pop(0) 

    result = ''.join(map(str, l)) 
    return result 

# Function to return the greater 
# number closest to N made up of 
# only odd digits 
def closest_greater(N): 

    N = str(N) 

    l = list(map(int, N)) 
    length = len(l) 

    # Stores the position of 
    # first even digit of N 
    pos = -1

    # Iterate over each digit 
    # of N 
    for i in range(length): 

        # If even digit is found 
        if l[i] % 2 == 0: 
            pos = i 
            break

    # Increase value of first  
    # even digit by 1 
    l[pos] += 1

    for i in range(pos + 1, length): 
        l[i] = 1

    result = ''.join(map(str, l)) 
    return result 

# Function to check if all  
# digits of N are odd or not 
def check_all_digits_odd(N): 

    N = str(N) 

    l = list(map(int, N)) 
    length = len(l) 

    # Stores the position of 
    # first even digit of N 
    pos = -1

    # Iterating over each digit 
    # of N 
    for i in range(length): 

        # If even digit is found 
        if l[i] % 2 == 0: 
            pos = i 
            break

    # If no even digit is found 
    if pos == -1: 
        return True
    return False

# Function to return the  
# closest number to N 
# having odd digits only 
def closestNumber(N): 

    # If all digits of N are odd 
    if check_all_digits_odd(N): 
        print(N) 
    else: 

        # Find smaller number  
        # closest to N 
        l = int(closest_smaller(N)) 

        # Find greater number  
        # closest to N 
        r = int(closest_greater(N)) 

        # Print the number with least 
        # absolute difference 
        if abs(N - l) <= abs(N - r): 
            print(l) 
        else: 
            print(r) 

# Driver Code. 
if __name__ == '__main__': 

    N = 110
    closestNumber(N) 

```

**Output:**

```
111

```

***时间复杂度：** O（len（N））
**辅助空间：** O（len（N））*

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。