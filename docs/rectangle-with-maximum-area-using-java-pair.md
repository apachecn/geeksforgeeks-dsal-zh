# 使用 Java 对的最大面积矩形

> 原文:[https://www . geeksforgeeks . org/最大使用面积矩形-java-pair/](https://www.geeksforgeeks.org/rectangle-with-maximum-area-using-java-pair/)

给定一个包含矩形长度和宽度的数组对。任务是找到矩形的最大面积。

示例:

```
Input: (1, 2), (3, 5), (1, 1), (4, 2)
Output: 15

Input: (3, 5), (5, 5), (9, 10)
Output: 90

```

**接近**:

1.  使用用户定义的*配对类*存储矩形的宽度和高度。
2.  制作这个类的数组。
3.  现在，遍历数组，每次找到该区域。此外，记录最大面积。
4.  返回矩形的最大面积。

```
// Java code to find maximum Area
import java.io.*;
import java.util.*;

// Pair class
class Rectangle {

    // length and
    int length;
    int breadth;

    // Rectangle Constructor
    public Rectangle(int x, int y)
    {
        this.length = x;
        this.breadth = y;
    }
}

// Class Area to calculate Area of rectangles
class Area {

    // Function to calculate area
    static int calculate_Area(Rectangle arr[])
    {

        int max_Area = Integer.MIN_VALUE;

        // loop to iterate through all rectangles
        // and keep track of max area
        for (int i = 0; i < arr.length; i++) {
            int temp_area = arr[i].length * arr[i].breadth;
            if (temp_area > max_Area) {
                max_Area = temp_area;
            }
        }
        return max_Area;
    }
}

// Driver class with main function
class GFG {

    // Driver code
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        // Creating an array of Pair
        Rectangle arr[] = new Rectangle[3];

        int x = 10, y = 20;
        arr[0] = new Rectangle(x, y);

        x = 5;
        y = 25;
        arr[1] = new Rectangle(x, y);

        x = 15;
        y = 10;
        arr[1] = new Rectangle(x, y);

        x = 12;
        y = 12;
        arr[2] = new Rectangle(x, y);

        Area obj = new Area();
        System.out.println(obj.calculate_Area(arr));
    }
}
```

**Output:**

```
200

```