# 使用二分搜索法的 Python 数字猜谜游戏

> 原文:[https://www . geesforgeks . org/number-猜测-python 中的游戏-使用-binary-search/](https://www.geeksforgeeks.org/number-guessing-game-in-python-using-binary-search/)

在猜数字游戏中，用户选择一个定义范围内的数字，然后程序猜测该数字。如果猜测的数字是错误的，那么用户告诉程序实际数字是否大于猜测的数字。同样，程序再次猜测数字，直到实际数字没有被猜到。
**方法:**想法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，在每一步中减少搜索空间的一半。以下是方法说明:

*   初始化猜测数字的开始和结束范围。
*   猜测数字作为搜索空间的中间。那就是
    ![Number = \frac{startRange + endRange}{2} ](img/9dc24aa44ba77ccac98553564e16868b.png "Rendered by QuickLaTeX.com")

*   如果猜测的数字是正确的，那么终止程序。
*   否则，询问用户猜测数是否小于猜测数。如果是，则相应减少搜索空间。

以下是上述方法的实现:

## 计算机编程语言

```
# Python implementation for the
# number guessing using
# Binary Search

# Global Arguments for playing game
args = ["N", "N", "Y"]
index = -1

# Temporary function for taking
# input from the local arguments list
def input():
    global index, args;
    index += 1
    return args[index]

# Function to guess the number in
# a defined range of the number
def guessNumber(startRange, endRange):
    if startRange > endRange:
        return True

    # Middle of the range
    mid = (startRange + endRange)//2

    # Asking user about the
    # actual number
    print("Is the number is ",
        mid, "?", end = " ")
    user = input()
    print(user)

    # Condition to check if the
    # guessed number is actual number
    if user == "Y" or user == "y":
        print("Voila ! Successfully Guessed Number.")
        return False

    # Condition to check if the
    # guessed number is not correct
    elif user == "N" or user == "n":
        print("Actual number is greater than",\
                        mid, "?", end = " ")
        user = input()
        print(user)
        if user == "Y" or user == "y":
            return guessNumber(mid+1, endRange)
        elif user == "N" or user == "n":
            return guessNumber(startRange, mid-1)
        else:
            print("Invalid Input. Print 'Y'/'N'")
            return guessNumber(startRange, endRange)

    # Condition to check if the user
    # input was invalid
    else:
        print("Invalid Input. Print 'Y'/'N' ")
        return guessNumber(startRange, endRange)

# Driver Code
if __name__ == "__main__":
    print("Number Guessing game in python")
    startRange = 1
    endRange = 10
    print("Guess a number in range (1 to 10)")

    out = guessNumber(startRange, endRange)

    if out:
        print("Bad Choices")
```

**Inputs:** 

```
N
N
Y
```

**Outputs:** 

```
Number Guessing game in python
Guess a number in range (1 to 10)
Is the number is  5 ? N
Actual number is greater than 5 ? N
Is the number is  2 ? Y
Voila ! Successfully Guessed Number.
```