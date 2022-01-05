# 镜头焦距程序

> 原文:[https://www.geeksforgeeks.org/program-focal-length-lens/](https://www.geeksforgeeks.org/program-focal-length-lens/)

写一个程序来确定镜头的焦距。
焦距是镜片中心到主焦点的距离。为了确定镜头的焦距，我们应该知道镜头和图像之间的距离(I)以及镜头和物体之间的距离(O)。这里，我们将使用镜头方程，也称为焦距方程。
镜头方程为:

```
 =  + 
```

这里，
F 为焦距
I 为镜头与影像的距离
O 为镜头与物体的距离
例:

```
Input : O = 50, I = 2
Output : F = 1.92308

Input : O = 25, I = 5
Output : F = 4.16667
```

## C++

```
// C++ program to determine
// the focal length of a lens
#include <iostream>
using namespace std;

// Function to determine the focal length of a lens
float focal_length(float image_distance, float object_distance)
{
    return 1 / ((1 / image_distance) + (1 / object_distance));
}

// Driver function
int main()
{
    // variable to store the distance
    // between the lens and the image
    float image_distance = 2;

    // variable to store the distance
    // between the lens and the object
    float object_distance = 50;

    cout << "Focal length of a lens is "
         << focal_length(image_distance, object_distance)
         << " units .";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine
// the focal length of a lens

import java.io.*;

class GFG {

    // Function to determine the focal
    // length of a lens
    static float focal_length(float image_distance,
                              float object_distance)
    {
        return 1 / ((1 / image_distance) +
                           (1 / object_distance));
    }

    public static void main(String[] args)
    {

        // variable to store the distance
        // between the lens and the image
        float image_distance = 2;

        // variable to store the distance
        // between the lens and the object
        float object_distance = 50;

        System.out.println("Focal length of a lens is "
        + focal_length(image_distance, object_distance)
                                         + " units.");
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python3 program to determine
# the focal length of a lens

# Function to determine the focal length of a lens
def focal_length(image_distance, object_distance)
    : return 1 / ((1 / image_distance) + (1 / object_distance))

# Driver Code
# Variable to store the distance
# between the lens and the image
image_distance = 2

# Variable to store the distance
# between the lens and the object
object_distance = 50

result = focal_length(image_distance, object_distance)
print("Focal length of a lens is ", result, " units.")
```

## C#

```
// C# program to determine
// the focal length of a lens
using System;

class GFG {

    // Function to determine the focal
    // length of a lens
    static float focal_length(float image_distance,
                            float object_distance)
    {
        return 1 / ((1 / image_distance) +
                    (1 / object_distance));
    }

    // Driver code
    public static void Main()
    {

        // variable to store the distance
        // between the lens and the image
        float image_distance = 2;

        // variable to store the distance
        // between the lens and the object
        float object_distance = 50;

        Console.WriteLine("Focal length of a lens is "
        + focal_length(image_distance, object_distance)
                                        + " units.");
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to determine
// the focal length of a lens
// Function to determine the
// focal length of a lens
function focal_length($image_distance,
                      $object_distance)
{
    return 1 / ((1 / $image_distance) +
               (1 / $object_distance));
}

    // Driver Code

    // variable to store the distance
    // between the lens and the image
    $image_distance = 2;

    // variable to store the distance
    // between the lens and the object
    $object_distance = 50;

    echo "Focal length of a lens is "
        , focal_length($image_distance,
                      $object_distance)
        , " units .";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// javascript program to determine
// the focal length of a lens

// Function to determine the focal
    // length of a lens
    function focal_length(image_distance,
                              object_distance)
    {
        return 1 / ((1 / image_distance) +
                           (1 / object_distance));
    }

// Driver Function

         // variable to store the distance
        // between the lens and the image
        let image_distance = 2;

        // variable to store the distance
        // between the lens and the object
        let object_distance = 50;

        document.write("Focal length of a lens is "
        + focal_length(image_distance, object_distance)
                                         + " units.");

</script>
```

**输出:**

```
Focal length of a lens is 1.92308 units . 
```