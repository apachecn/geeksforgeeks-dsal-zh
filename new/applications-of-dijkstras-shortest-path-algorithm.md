# Dijkstra 最短路径算法

的应用

> 原文： [https://www.geeksforgeeks.org/applications-of-dijkstras-shortest-path-algorithm/](https://www.geeksforgeeks.org/applications-of-dijkstras-shortest-path-algorithm/)

[Dijkstra 的算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)是解决许多图中非负边权重的单源最短路径问题（即找到图中两个顶点之间的最短距离）的最受欢迎算法之一。 它是由计算机科学家 **Edsger W. Dijkstra** 于 1956 年构思的，并在三年后出版。

Dijkstra 的算法有多个实际用例，其中一些如下：

1.  **Google Maps 中的数字地图服务**：很多时候，我们试图在 G-Maps 中查找从一个城市到另一个城市，或者从您的位置到最近的所需位置的距离。 遇到[最短路径算法](https://www.geeksforgeeks.org/printing-paths-dijkstras-shortest-path-algorithm/)，因为有多种路线/路径连接它们，但必须显示最小距离，因此 Dijkstra 的算法用于查找路径上两个位置之间的最小距离。 将印度视为一个图形，并以一个顶点和一个城市/地方之间的路线为边来表示一个城市/地方，然后使用此算法，计算出任何两个城市/地方之间或从一个城市/地方到另一个城市之间的最短路线 / place 可以计算。
2.  **社交网络应用程序**：在许多应用程序中，您可能已经看到该应用程序建议特定用户可能认识的朋友列表。 您如何看待许多社交媒体公司有效地实现此功能，尤其是当系统拥有十亿用户时。 可以使用通过握手或用户之间的连接测得的用户之间的最短路径来应用标准 Dijkstra 算法。 当社交网络图很小时，它使用标准的 Dijkstra 算法和其他功能来找到最短路径，但是，当该图变得越来越大时，该标准算法需要花费几秒钟的时间进行计数并交替使用高级算法。 使用算法。
3.  **电话网络**：我们知道，在电话网络中，每条线路的带宽均为“ b”。 传输线的带宽是该线可以支持的最高频率。 通常，如果在某条线路中信号的频率较高，则该线路会降低信号。 带宽表示线路可以传输的信息量。 如果我们将一个城市想象成一个图形，则顶点代表交换站，边代表传输线，边的权重代表“ b”。 因此，如您所见，它属于最短距离问题，可以使用 Dijkstra。
4.  **IP 路由查找开放式最短路径优先**：[开放式最短路径优先（OSPF）](https://www.geeksforgeeks.org/open-shortest-path-first-ospf-protocol-states/)是一种链路状态[路由协议](https://www.geeksforgeeks.org/classes-of-routing-protocols/)，用于查找之间的最佳路径 源路由器和目标路由器使用其自己的最短路径优先。 Dijkstra 的算法广泛用于路由器更新其转发表所需的路由协议中。 该算法提供了从源路由器到网络中其他路由器的最短成本路径。
5.  **航班议程**：例如，如果某人需要用于为客户制定航班计划的软件。 该代理有权访问所有机场和航班的数据库。 除了航班号，始发机场和目的地外，航班还有出发和到达的时间。 具体来说，代理希望在给定始发机场和开始时间的情况下确定目的地的最早到达时间。 在那里使用了该算法。
6.  **指定文件服务器**：要在 [LAN（局域网）](https://www.geeksforgeeks.org/local-area-network-lan-technologies/)中指定文件服务器，可以使用 Dijkstra 的算法。 考虑到将文件从一台计算机传输到另一台计算机需要无限的时间。 因此，为了使从文件服务器到网络上每台其他计算机的“跳数”最小，该想法是使用 Dijkstra 的算法来最小化网络之间的最短路径，从而使跳数最少。
7.  **机器人路径**：如今，无人驾驶飞机和机器人已经存在，其中有些是手动的，有些是自动化的。 此算法模块将加载用于将包裹运送到特定位置或用于任务的自动化无人机/机器人，以便在知道源和目的地时，机器人/无人机按照以下说明在有序方向上移动 在最短的时间内保持交付包裹的最短路径。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。