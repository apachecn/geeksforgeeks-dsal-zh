# 使用方向跟踪法

以螺旋形式打印给定矩阵

> 原文:[https://www . geeksforgeeks . org/print-a-给定螺旋形状矩阵-使用方向跟踪-方法/](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form-using-direction-tracking-method/)

给定一个二维矩阵 **mat[][]** ，任务是以螺旋形式打印它。
**例:**

> **输入:** mat[][] = {
> {1，2，3，4}，
> {5，6，7，8}，
> {9，10，11，12}，
> {13，14，15，16 } }
> T7】输出:1 2 3 4 8 12 16 15 14 13 9 5 6 7 11 10
> **输入:**mat[]= {

**逼近:**这个问题用方向法很容易解决。因为我们从东方方向开始，所以每当下一个索引无效(超出矩阵)或访问较早时，总是向右拐。接下来的方向将是**东- >南- >西- >北->……**从**mat【0】【0】**开始，直到矩阵的所有元素都被遍历完。
以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define R 5
#define C 5

enum direction { east,
                 west,
                 north,
                 south };

// Function to set the new direction on turning
// right from the current direction
void turnright(enum direction& c_direction)
{
    switch (c_direction) {
    case east:
        c_direction = south;
        break;
    case west:
        c_direction = north;
        break;
    case north:
        c_direction = east;
        break;
    case south:
        c_direction = west;
        break;
    }
}

// Function to return the next possible cell
// indexes with current direction
pair<int, int> next(int i, int j,
                    const enum direction& c_direction)
{
    switch (c_direction) {
    case east:
        j++;
        break;
    case west:
        j--;
        break;
    case north:
        i--;
        break;
    case south:
        i++;
        break;
    }
    return pair<int, int>(i, j);
}

// Function that returns true
// if arr[i][j] is a valid index
bool isvalid(const int& i, const int& j)
{
    if (i < R && i >= 0 && j >= 0 && j < C)
        return true;
    return false;
}

// Function that returns true if arr[i][j]
// has already been visited
bool alreadyVisited(int& i, int& j, int& mini, int& minj,
                    int& maxi, int& maxj)
{

    // If inside the current bounds then
    // it has not been visited earlier
    if (i >= mini && i <= maxi && j >= minj && j <= maxj)
        return false;
    return true;
}

// Function to update the constraints of the matrix
void ConstraintWalls(int& mini, int& minj, int& maxi,
                     int& maxj, direction c_direction)
{

    // Update the constraints according
    // to the direction
    switch (c_direction) {
    case east:
        mini++;
        break;
    case west:
        maxi--;
        break;
    case north:
        minj++;
        break;
    case south:
        maxj--;
        break;
    }
}

// Function to print the given matrix in the spiral form
void printspiral(int arr[R][C])
{

    // To store the count of all the indexes
    int count = 0;

    // Starting direction is East
    enum direction current_direction = east;

    // Boundary constraints in the matrix
    int mini = 0, minj = 0, maxi = R - 1, maxj = C - 1;
    int i = 0, j = 0;

    // While there are elements remaining
    while (count < (R * C)) {

        // Print the current element
        // and increment the count
        cout << arr[i][j] << " ";
        count++;

        // Next possible cell if direction remains the same
        pair<int, int> p = next(i, j, current_direction);

        // If current cell is already visited or is invalid
        if (!isvalid(p.first, p.second)
            || alreadyVisited(p.first, p.second, mini, minj, maxi, maxj)) {

            // If not visited earlier then only change the constraint
            if (!alreadyVisited(i, j, mini, minj, maxi, maxj))
                ConstraintWalls(mini, minj, maxi, maxj, current_direction);

            // Change the direction
            turnright(current_direction);

            // Next indexes with new direction
            p = next(i, j, current_direction);
        }

        // Next row and next column
        i = p.first;
        j = p.second;
    }
}

// Driver code
int main()
{
    int arr[R][C];

    // Fill the matrix
    int counter = 1;
    for (int i = 0; i < R; i++)
        for (int j = 0; j < C; j++)
            arr[i][j] = counter++;

    // Print the spiral form
    printspiral(arr);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

R=5
C=5

direction = ['east', 'west', 'north', 'south']

# Function to set the new direction on turning
# right from the current direction
def turnright(c_direction):
    if c_direction=='east':
        return 'south'
    elif c_direction=='west':
        return 'north'
    elif c_direction=='north':
        return 'east'
    else:
        return 'west'

# Function to return the next possible cell
# indexes with current direction
def next(i,  j, c_direction):

    if c_direction=='east':
        j+=1
    elif c_direction=='west':
        j-=1;
    elif c_direction=='north':
        i-=1
    else:
        i+=1

    return (i, j)

# Function that returns true
# if arr[i][j] is a valid index
def isvalid(i, j):

    if (i < R and i >= 0 and j >= 0 and j < C):
        return True
    return False

# Function that returns true if arr[i][j]
# has already been visited
def alreadyVisited(i, j, mini, minj, maxi, maxj):

    # If inside the current bounds then
    # it has not been visited earlier
    if (i >= mini and i <= maxi and j >= minj and j <= maxj):
        return False
    return True

# Function to update the constraints of the matrix
def ConstraintWalls(mini,  minj, maxi, maxj, c_direction):

    # Update the constraints according
    # to the direction
    if c_direction=='east':
        mini+=1
    elif c_direction=='west':
        maxi-=1
    elif c_direction=='north':
        minj+=1
    else:
        maxj-=1
    return mini,  minj, maxi, maxj

# Function to print the given matrix in the spiral form
def printspiral( arr):

    # To store the count of all the indexes
    count = 0

    # Starting direction is 'east'
    current_direction = 'east'

    # Boundary constraints in the matrix
    mini = 0; minj = 0; maxi = R - 1; maxj = C - 1
    i = 0; j = 0

    # While there are elements remaining
    while (count < (R * C)):

        # Print the current element
        # and increment the count
        print(arr[i][j],end=" ")
        count+=1

        # Next possible cell if direction remains the same
        p = next(i, j, current_direction)

        # If current cell is already visited or is invalid
        if (not isvalid(p[0], p[1])
            or alreadyVisited(p[0], p[1], mini, minj, maxi, maxj)):

            # If not visited earlier then only change the constraint
            if (not alreadyVisited(i, j, mini, minj, maxi, maxj)):
                mini, minj, maxi, maxj=ConstraintWalls(mini, minj, maxi, maxj, current_direction)

            # Change the direction
            current_direction=turnright(current_direction)

            # Next indexes with new direction
            p = next(i, j, current_direction)

        # Next row and next column
        i = p[0]
        j = p[1]

# Driver code
if __name__ == '__main__':
    arr=[[0 for j in range(C)]for i in range(R)]

    # Fill the matrix
    counter = 1
    for i in range(R):
        for j in range(C):
            arr[i][j] = counter
            counter+=1

    # Print the spiral form
    printspiral(arr)
    print()
# This code is contributed by Amartya Ghosh
```

**Output:** 

```
1 2 3 4 5 10 15 20 25 24 23 22 21 16 11 6 7 8 9 14 19 18 17 12 13
```

**时间复杂度:**O(R * C)
T3】空间复杂度: O(1)