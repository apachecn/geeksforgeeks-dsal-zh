# 计算机图形学中的点裁剪算法

> 原文:[https://www . geesforgeks . org/点裁剪-算法-计算机-图形/](https://www.geeksforgeeks.org/point-clipping-algorithm-computer-graphics/)

**裁剪:**在计算机图形学中，我们的屏幕就像一个二维坐标系。没有必要在我们的观察窗格(即我们的计算机屏幕)上查看每个点。我们可以查看位于特定范围(0，0)和(Xmax，Ymax)内的点。因此，剪辑是一个过程，它识别图片中在我们的查看窗格内部或外部的那些部分。
在点裁剪的情况下，我们只在窗口上显示/打印我们的查看窗格范围内的点，范围外的其他点将被丢弃。
**例**

```
Input :

Output :
```

**点裁剪算法:**

1.  获取两个观察窗格的最小和最大坐标。
2.  获取一个点的坐标。
3.  检查给定输入是否位于查看窗格的最小和最大坐标之间。
4.  如果是，显示位于该区域内的点，否则将其丢弃。

## C++

```
// C++ program for point clipping Algorithm
#include <bits/stdc++.h>
using namespace std;

// Function for point clipping
void pointClip(int XY[][2], int n, int Xmin, int Ymin,
                                int Xmax, int Ymax)
{
    /*************** Code for graphics view
    // initialize graphics mode
    detectgraph(&gm,&gr);
    initgraph(&gm,&gr,"d:\\tc\\BGI");
    for (int i=0; i<n; i++)
    {
    if ( (XY[i][0] >= Xmin) && (XY[i][0] <= Xmax))
    {
            if ( (XY[i][1] >= Ymin) && (XY[i][1] <= Ymax))
        putpixel(XY[i][0],XY[i][1],3);
    }
    }
    **********************/
    /**** Arithmetic view ****/
    cout << "Point inside the viewing pane:" << endl;
    for (int i = 0; i < n; i++)
    {
        if ((XY[i][0] >= Xmin) && (XY[i][0] <= Xmax))
        {
            if ((XY[i][1] >= Ymin) && (XY[i][1] <= Ymax))
                cout <<"[" << XY[i][0] <<","<<XY[i][1]<<"] ";
        }
    }

    // print point coordinate outside viewing pane
    cout<<"\n"<< endl;
    cout << "Point outside the viewing pane:"<<endl;
    for (int i = 0; i < n; i++)
    {
        if ((XY[i][0] < Xmin) || (XY[i][0] > Xmax))
            cout << "[" << XY[i][0] << "," << XY[i][1] << "] ";
        if ((XY[i][1] < Ymin) || (XY[i][1] > Ymax))
            cout << "[" << XY[i][0] << "," << XY[i][1] << "] ";
    }
}

// Driver code
int main()
{
    int XY[6][2] = {{10, 10}, {-10, 10}, {400, 100},
                    {100, 400}, {400, 400}, {100, 40}};

    // getmaxx() & getmaxy() will return Xmax, Ymax
    // value if graphics.h is included
    int Xmin = 0;
    int Xmax = 350;
    int Ymin = 0;
    int Ymax = 350;
    pointClip(XY, 6, Xmin, Ymin, Xmax, Ymax);
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program for point clipping Algorithm
#include<stdio.h>
//#include<graphics.h>

// Function for point clipping
void pointClip(int XY[][2], int n, int Xmin, int Ymin,
                                   int Xmax, int Ymax)
{
    /*************** Code for graphics view
    // initialize graphics mode
    detectgraph(&gm,&gr);
    initgraph(&gm,&gr,"d:\\tc\\BGI");
    for (int i=0; i<n; i++)
    {
    if ( (XY[i][0] >= Xmin) && (XY[i][0] <= Xmax))
    {
            if ( (XY[i][1] >= Ymin) && (XY[i][1] <= Ymax))
        putpixel(XY[i][0],XY[i][1],3);
    }
    }
    **********************/
    /**** Arithmetic view ****/
    printf ("Point inside the viewing pane:\n");
    for (int i=0; i<n; i++)
    {
        if ((XY[i][0] >= Xmin) && (XY[i][0] <= Xmax))
        {
            if ((XY[i][1] >= Ymin) && (XY[i][1] <= Ymax))
                printf ("[%d, %d] ", XY[i][0], XY[i][1]);
        }
    }

    // print point coordinate outside viewing pane
    printf ("\nPoint outside the viewing pane:\n");
    for (int i=0; i<n; i++)
    {
        if ((XY[i][0] < Xmin) || (XY[i][0] > Xmax))
            printf ("[%d, %d] ", XY[i][0], XY[i][1]);
        if ((XY[i][1] < Ymin) || (XY[i][1] > Ymax))
            printf ("[%d, %d] ", XY[i][0], XY[i][1]);
    }
}

// Driver code
int main()
{
    int XY[6][2] = {{10,10}, {-10,10}, {400,100},
                    {100,400}, {400,400}, {100,40}};

    // getmaxx() & getmaxy() will return Xmax, Ymax
    // value if graphics.h is included
    int Xmin = 0;
    int Xmax = 350;
    int Ymin = 0;
    int Ymax = 350;
    pointClip(XY, 6,  Xmin, Ymin, Xmax, Ymax);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for point clipping Algorithm
class GFG
{

// Function for point clipping
static void pointClip(int XY[][], int n,
                        int Xmin, int Ymin,
                        int Xmax, int Ymax)
{
    /*************** Code for graphics view
    // initialize graphics mode
    detectgraph(&gm,&gr);
    initgraph(&gm,&gr,"d:\\tc\\BGI");
    for (int i=0; i<n; i++)
    {
    if ( (XY[i][0] >= Xmin) && (XY[i][0] <= Xmax))
    {
            if ( (XY[i][1] >= Ymin) && (XY[i][1] <= Ymax))
        putpixel(XY[i][0],XY[i][1],3);
    }
    }
    **********************/
    /**** Arithmetic view ****/
    System.out.printf ("Point inside the viewing pane:\n");
    for (int i = 0; i < n; i++)
    {
        if ((XY[i][0] >= Xmin) && (XY[i][0] <= Xmax))
        {
            if ((XY[i][1] >= Ymin) && (XY[i][1] <= Ymax))
                System.out.printf ("[%d, %d] ", XY[i][0], XY[i][1]);
        }
    }

    // print point coordinate outside viewing pane
    System.out.printf ("\nPoint outside the viewing pane:\n");
    for (int i=0; i<n; i++)
    {
        if ((XY[i][0] < Xmin) || (XY[i][0] > Xmax))
            System.out.printf ("[%d, %d] ", XY[i][0], XY[i][1]);
        if ((XY[i][1] < Ymin) || (XY[i][1] > Ymax))
            System.out.printf ("[%d, %d] ", XY[i][0], XY[i][1]);
    }
}

// Driver code
public static void main(String[] args)
{
        int XY[][] = {{10,10}, {-10,10}, {400,100},
                    {100,400}, {400,400}, {100,40}};

    // getmaxx() & getmaxy() will return Xmax, Ymax
    // value if graphics.h is included
    int Xmin = 0;
    int Xmax = 350;
    int Ymin = 0;
    int Ymax = 350;
    pointClip(XY, 6, Xmin, Ymin, Xmax, Ymax);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program for poclipping Algorithm

# Function for poclipping
def pointClip(XY, n, Xmin, Ymin, Xmax, Ymax):

    """************** Code for graphics view
    # initialize graphics mode
    detectgraph(&gm, &gr)
    initgraph(&gm, &gr, "d:\\tc\\BGI")
    for (i=0 i<n i++)

    if ((XY[i][0] >= Xmin) and
        (XY[i][0] <= Xmax))

        if ((XY[i][1] >= Ymin) and
            (XY[i][1] <= Ymax))
        putpixel(XY[i][0], XY[i][1], 3)

    *********************"""
    """*** Arithmetic view ***"""
    print("Point inside the viewing pane:")
    for i in range(n):
        if ((XY[i][0] >= Xmin) and
            (XY[i][0] <= Xmax)):
            if ((XY[i][1] >= Ymin) and
                (XY[i][1] <= Ymax)):
                print("[", XY[i][0], ", ", XY[i][1],
                      "]", sep = "", end = " ")

    # prpocoordinate outside viewing pane
    print("\n\nPoint outside the viewing pane:")
    for i in range(n):    
        if ((XY[i][0] < Xmin) or (XY[i][0] > Xmax)) :
            print("[", XY[i][0], ", ", XY[i][1],
                  "]", sep = "", end = " ")
        if ((XY[i][1] < Ymin) or (XY[i][1] > Ymax)) :
            print("[", XY[i][0], ", ", XY[i][1],
                  "]", sep = "", end = " ")

# Driver Code
if __name__ == '__main__':
    XY = [[10, 10], [-10, 10], [400, 100],
          [100, 400], [400, 400], [100, 40]]

    # getmaxx() & getmaxy() will return Xmax,
    # Ymax value if graphics.h is included
    Xmin = 0
    Xmax = 350
    Ymin = 0
    Ymax = 350
    pointClip(XY, 6, Xmin, Ymin, Xmax, Ymax)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program for point clipping Algorithm
using System;

class GFG
{

// Function for point clipping
static void pointClip(int [,]XY, int n,
                        int Xmin, int Ymin,
                        int Xmax, int Ymax)
{
    /*************** Code for graphics view
    // initialize graphics mode
    detectgraph(&gm,&gr);
    initgraph(&gm,&gr,"d:\\tc\\BGI");
    for (int i=0; i<n; i++)
    {
    if ( (XY[i,0] >= Xmin) && (XY[i,0] <= Xmax))
    {
            if ( (XY[i,1] >= Ymin) && (XY[i,1] <= Ymax))
        putpixel(XY[i,0],XY[i,1],3);
    }
    }
    **********************/
    /**** Arithmetic view ****/
    Console.Write("Point inside the viewing pane:\n");
    for (int i = 0; i < n; i++)
    {
        if ((XY[i, 0] >= Xmin) && (XY[i, 0] <= Xmax))
        {
            if ((XY[i, 1] >= Ymin) && (XY[i, 1] <= Ymax))
                Console.Write("[{0}, {1}] ", XY[i, 0], XY[i, 1]);
        }
    }

    // print point coordinate outside viewing pane
    Console.Write("\nPoint outside the viewing pane:\n");
    for (int i = 0; i < n; i++)
    {
        if ((XY[i, 0] < Xmin) || (XY[i, 0] > Xmax))
            Console.Write("[{0}, {1}] ", XY[i, 0], XY[i, 1]);
        if ((XY[i, 1] < Ymin) || (XY[i, 1] > Ymax))
            Console.Write("[{0}, {1}] ", XY[i, 0], XY[i, 1]);
    }
}

// Driver code
public static void Main(String[] args)
{
        int [,]XY = {{10, 10}, {-10, 10}, {400, 100},
                    {100, 400}, {400, 400}, {100, 40}};

    // getmaxx() & getmaxy() will return Xmax, Ymax
    // value if graphics.h is included
    int Xmin = 0;
    int Xmax = 350;
    int Ymin = 0;
    int Ymax = 350;
    pointClip(XY, 6, Xmin, Ymin, Xmax, Ymax);
}
}

// This code contributed by Rajput-Ji
```

**输出:**

```
Point inside the viewing pane:
[10, 10] [100, 40] 

Point outside the viewing pane:
[-10, 10] [400, 100] [100, 400] [400, 400] [400, 400] 
```

**时间复杂度:** O(N)
**辅助空间:** O(1)
**相关帖子:**
[线裁剪|集 1(Cohen–Sutherland 算法)](https://www.geeksforgeeks.org/line-clipping-set-1-cohen-sutherland-algorithm/)
[多边形裁剪| Sutherland–Hodgman 算法](https://www.geeksforgeeks.org/polygon-clipping-sutherland-hodgman-algorithm-please-change-bmp-images-jpeg-png/)
本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。