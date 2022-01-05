# c++中使用复数的几何|集合 2

> 原文:[https://www . geesforgeks . org/geometry-using-complex-numbers-c-set-2/](https://www.geeksforgeeks.org/geometry-using-complex-numbers-c-set-2/)

在浏览了[之前的](https://www.geeksforgeeks.org/geometry-using-complex-numbers-stdcomplex-in-c/)帖子后，我们知道了什么是复数，以及如何使用它们来模拟笛卡尔平面中的点。现在，我们将了解如何在 C++中使用来自 STL 的复杂类。
**要使用来自 STL 的复杂类，我们使用#include <复杂>**

**定义点类**
我们可以通过 typedef 复数<双>点来定义我们的点类；在节目开始的时候。点的 X 和 Y 坐标分别是复数的实部和虚部。要访问我们的 X 和 Y 坐标，我们可以使用#定义如下来宏实()和 imag()函数:

```
# include <complex>
typedef complex<double> point;
# define x real()
# define y imag()
```

**缺点:**由于 x 和 y 已经作为宏使用，这些不能作为变量使用。然而，这个缺点并不代表它的许多优点。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to illustrate
// the definition of point class
#include <iostream>
#include <complex>

using namespace std;

typedef complex<double> point;

// X-coordinate is equivalent to the real part
// Y-coordinate is equivalent to the imaginary part
#define x real()
#define y imag()

int main()
{
    point P(2.0, 3.0);
    cout << "The X-coordinate of point P is: " << P.x << endl;
    cout << "The Y-coordinate of point P is: " << P.y << endl;

    return 0;
}
```

输出:

```
The X-coordinate of point P is: 2
The Y-coordinate of point P is: 3
```

**关于平面内 P 个单点 P 的属性实现:**

1.  **P 的 X 坐标:** P.x
2.  **P 的 Y 坐标:** P.y
3.  **P 距原点(0，0)的距离:** abs(P)
4.  **OP 与 X 轴的夹角，其中 O 是原点:** arg(z)
5.  **P 绕原点的旋转:** P *极坐标(r，θ)

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to illustrate
// the implementation of single point attributes
#include <iostream>
#include <complex>

using namespace std;

typedef complex<double> point;
#define x real()
#define y imag()

// The constant PI for providing angles in radians
#define PI 3.1415926535897932384626

// Function used to display X and Y coordinates of a point
void displayPoint(point P)
{
    cout << "(" << P.x << ", " << P.y << ")" << endl;
}

int main()
{
    point P(4.0, 3.0);

    // X-Coordinate and Y-coordinate
    cout << "The X-coordinate of point P is: " << P.x << endl;
    cout << "The Y-coordinate of point P is: " << P.y << endl;

    // Distances of P from origin
    cout << "The distance of point P from orgin is: " << abs(P) <<endl;
    cout << "The squared distance of point P from orgin is: " << norm(P) <<endl;

    // Tangent Angle made by OP with the X-Axis
    cout << "The angle made by OP with the X-Axis is: "
        << arg(P) << " radians" << endl;
    cout << "The angle made by OP with the X-Axis is: "
        << arg(P)*(180/PI) << " degrees" << endl;

    // Rotation of P about origin
    // The angle of rotation = 90 degrees
    point P_rotated = P * polar(1.0, PI/2);
    cout<<"The point P on rotating 90 degrees anti-clockwise becomes: P_rotated";
    displayPoint(P_rotated);

    return 0;
}
```

输出:

```
The X-coordinate of point P is: 4
The Y-coordinate of point P is: 3
The distance of point P from orgin is: 5
The squared distance of point P from orgin is: 25
The angle made by OP with the X-Axis is: 0.643501 radians
The angle made by OP with the X-Axis is: 36.8699 degrees
The point P on rotating 90 degrees anti-clockwise becomes: P_rotated(-3, 4)
```

1.  **向量加法:** P + Q
2.  **向量减法:**P–Q
3.  **欧氏距离:**ABS(P–Q)
4.  **PQ 线斜率:**tan(arg(Q–P))

```
point A = conj(P) * Q
```

1.  **点积:** A.x
2.  **叉积大小:**绝对值(A.y)

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to illustrate
// the implementation of two point attributes
#include <iostream>
#include <complex>

using namespace std;

typedef complex<double> point;
#define x real()
#define y imag()

// Constant PI for providing angles in radians
#define PI 3.1415926535897932384626

// Function used to display X and Y coordinates of a point
void displayPoint(point P)
{
    cout << "(" << P.x << ", " << P.y << ")" << endl;
}

int main()
{
    point P(2.0, 3.0);
    point Q(3.0, 4.0);

    // Addition and Subtraction
    cout << "Addition of P and Q is: P+Q"; displayPoint(P+Q);
    cout << "Subtraction of P and Q is: P-Q"; displayPoint(P-Q);

    // Distances between points P and Q
    cout << "The distance between point P ans Q is: " << abs(P-Q) <<endl;
    cout << "The squared distance between point P ans Q is: " << norm(P-Q) <<endl;

    // Slope of line PQ
    cout << "The angle of elevation for line PQ is: "
        << arg(Q-P)*(180/PI) << " degrees" << endl;
    cout << "The slope of line PQ is: " << tan(arg(Q-P)) <<endl;

    // Construction of point A
    point A = conj(P)*Q;

    // Dot Product and Cross Product
    cout << "The dot product P.Q is: " << A.x << endl;
    cout << "The magnitude of cross product PxQ is: " << abs(A.y) << endl;

    return 0;
}
```

输出:

```
Addition of P and Q is: P+Q(5, 7)
Subtraction of P and Q is: P-Q(-1, -1)
The distance between point P ans Q is: 1.41421
The squared distance between point P ans Q is: 2
The angle of elevation for line PQ is: 45 degrees
The slope of line PQ is: 1
The dot product P.Q is: 18
The magnitude of cross product PxQ is: 1
```

本文由**安雅金达尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。