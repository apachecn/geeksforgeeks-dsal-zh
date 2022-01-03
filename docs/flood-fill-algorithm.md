# 洪水填充算法

> 原文： [https://www.geeksforgeeks.org/flood-fill-algorithm/](https://www.geeksforgeeks.org/flood-fill-algorithm/)

给定 2D 屏幕 **arr [] []** ，其中每个 **arr [i] [j]** 是代表该像素颜色的整数，还给出了像素**的位置 （X，Y）**和颜色`C`，任务是用给定颜色替换给定像素和所有相邻的同色像素的颜色。

**示例**：

> **输入**：arr [] [] = {
> {1，1，1，1，1，1，1，1，}，
> {1，1，1，1，1， 1，0，0}，
> {1，0，0，1，1，1，0，1，1}，
> {1， **2，2，2，2，** 0， 1，0}，
> {1，1，1， **2，2，** 0，1，0}，
> {1，1，1， **2，2，2 ，2，** 0}，
> {1，1，1，1，1， **2，** 1，1}，
> {1，1，1，1，1， **2、2，** 1}}
> X = 4，Y = 4，C = 3
> **输出**：
> 1 1 1 1 1 1 1 1 1
> 1 1 1 1 1 1 0 0 0
> 1 0 0 1 1 0 1 1
> 1 **3 3 3 3** 0 1 0
> 1 1 1 **3 3** 0 1 0
> 1 1 1 **3 3 3 3** 0
> 1 1 1 1 1 1`3`1 1
> 1 1 1 1 1 **3 3** 1
> **说明**：
> 给定 2D 屏幕中的值表示像素的颜色。 X 和 Y 是笔刷的坐标，C 是应该替换屏幕[X] [Y]上所有以前的颜色以及周围所有具有相同颜色的像素的颜色。 因此，所有 2 被 3 代替。

**BFS 方法**：的想法是使用 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)将颜色替换为新颜色。

*   创建一个空的[队列](http://www.geeksforgeeks.org/queue-data-structure/)说 *Q* 。

*   按下输入中指定的像素的起始位置，并为其应用替换颜色。

*   迭代直到`Q`不为空，然后弹出前节点（像素位置）。

*   检查与当前像素相邻的像素，如果有效则推入队列（未用替换色上色，并且颜色与旧颜色相同）。

下面是上述方法的实现：

```

# Python3 implementation of the approach 

# Function that returns true if  
# the given pixel is valid 
def isValid(screen, m, n, x, y, prevC, newC): 
    if x<0 or x>= m\ 
       or y<0 or y>= n or\ 
       screen[x][y]!= prevC\ 
       or screen[x][y]== newC: 
        return False
    return True

# FloodFill function 
def floodFill(screen,   
            m, n, x,   
            y, prevC, newC): 
    queue = [] 

    # Append the position of starting  
    # pixel of the component 
    queue.append([x, y]) 

    # Color the pixel with the new color 
    screen[x][y] = newC 

    # While the queue is not empty i.e. the  
    # whole component having prevC color  
    # is not colored with newC color 
    while queue: 

        # Dequeue the front node 
        currPixel = queue.pop() 

        posX = currPixel[0] 
        posY = currPixel[1] 

        # Check if the adjacent 
        # pixels are valid 
        if isValid(screen, m, n,   
                posX + 1, posY,   
                        prevC, newC): 

            # Color with newC 
            # if valid and enqueue 
            screen[posX + 1][posY] = newC 
            queue.append([posX + 1, posY]) 

        if isValid(screen, m, n,   
                    posX-1, posY,   
                        prevC, newC): 
            screen[posX-1][posY]= newC 
            queue.append([posX-1, posY]) 

        if isValid(screen, m, n,   
                posX, posY + 1,   
                        prevC, newC): 
            screen[posX][posY + 1]= newC 
            queue.append([posX, posY + 1]) 

        if isValid(screen, m, n,   
                    posX, posY-1,   
                        prevC, newC): 
            screen[posX][posY-1]= newC 
            queue.append([posX, posY-1]) 

# Driver code 
screen =[ 
[1, 1, 1, 1, 1, 1, 1, 1],  
[1, 1, 1, 1, 1, 1, 0, 0],  
[1, 0, 0, 1, 1, 0, 1, 1],  
[1, 2, 2, 2, 2, 0, 1, 0],  
[1, 1, 1, 2, 2, 0, 1, 0],  
[1, 1, 1, 2, 2, 2, 2, 0],  
[1, 1, 1, 1, 1, 2, 1, 1],  
[1, 1, 1, 1, 1, 2, 2, 1],  
    ] 

# Row of the display 
m = len(screen) 

# Column of the display 
n = len(screen[0]) 

# Co-ordinate provided by the user 
x = 4
y = 4

# Current colour at that co-ordinate 
prevC = screen[x][y] 

# New colour that has to be filled 
newC = 3

floodFill(screen, m, n, x, y, prevC, newC) 

# Priting the updated screen 
for i in range(m): 
    for j in range(n): 
        print(screen[i][j], end =' ') 
    print() 

```

**Output:**

```
1 1 1 1 1 1 1 1 
1 1 1 1 1 1 0 0 
1 0 0 1 1 0 1 1 
1 3 3 3 3 0 1 0 
1 1 1 3 3 0 1 0 
1 1 1 3 3 3 3 0 
1 1 1 1 1 3 1 1 
1 1 1 1 1 3 3 1

```

**DFS 方法**：类似地，DFS 方法也可以用于实现 Flood Fill 算法。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。