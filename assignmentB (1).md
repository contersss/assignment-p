# Assignment #B: 图论和树算

Updated 1709 GMT+8 Apr 28, 2024

2024 spring, Complied by 孙一弘 工学院

**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统:WIN11

Python编程环境：PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 28170: 算鹰

dfs, http://cs101.openjudge.cn/practice/28170/



思路：

题目意思不太明确，实际上是算有几个连通区域

代码

```python
# 
g = [list(input()) for i in range(10)]
direction = [[1,0],[-1,0],[0,1],[0,-1]]
def dfs(x,y):
    g[x][y] = '_'
    for i in direction:
        nx = x+ i[0]
        ny = y + i[1]
        if 0<= nx <10 and 0<= ny < 10:
            if g[nx][ny] == ".":
                dfs(nx,ny)
res = 0
for i in range(10):
    for j in range(10):
        if g[i][j] == ".":
            res += 1
            dfs(i,j)
print(res)
```



代码运行截图 ==（至少包含有"Accepted"）==



![image-20240505093046878](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240505093046878.png)

### 02754: 八皇后

dfs, http://cs101.openjudge.cn/practice/02754/



思路：

dfs逐个枚举

代码

```python
# 
def valid(x,y,chess):
    for i in range(0,8):
        if chess[x][i] == "Q":
            return False
        if chess[i][y] == "Q":
            return False
    x0,y0 = x,y; x1,y1 = x,y;x2,y2 = x,y; x3,y3 = x,y
    while x0<8 and y0<8:
        if chess[x0][y0] == "Q":
            return False
        x0 += 1;y0 += 1
    while -1<x1<8 and -1<y1<8 :
        if chess[x1][y1] == 'Q':
            return False
        x1 -= 1; y1 -= 1
    while -1<x2<8 and -1<y2<8 :
         if chess[x2][y2] == 'Q':
             return False
         x2 += 1; y2 -= 1
    while -1<x3<8 and -1<y3<8 :
         if chess[x3][y3] == 'Q':
             return False
         x3 -= 1; y3+= 1
    return True


def dfs(row,path):
    if len(path) == 8:
        res.append(path)
        return
    for i in range(0,8):
        if valid(row,i,chess):
            chess[row][i] = "Q"
            dfs(row+1,path + [i+1])
            chess[row][i] = 0
    return
    
    
    
    
    

res = []
n = int(input())
chess = [[0 for _ in range(8)] for __ in range(8)]
dfs(0,[])
res.sort(key = lambda x : int(''.join(map(str,(x)))))
for _ in range(n):
    a = int(input()) - 1
    print(''.join(map(str,res[a])))
```



代码运行截图 ==（至少包含有"Accepted"）==



![image-20240505093134160](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240505093134160.png)

### 03151: Pots

bfs, http://cs101.openjudge.cn/practice/03151/



思路：

bfs

代码

```python
# 
from collections import deque
res = 1000
path = []
a,b,c = map(int,input().split())
stack = deque()
stack.append((0,0,0,[]))
vis = set()
while stack:
    (d,e,f,g) = stack.popleft()
    if d == c or e == c:
        res = f
        path = g
        break
    if (a,e) not in vis:
        stack.append((a,e,f+1,g+["FILL(1)"]))
        vis.add((a,e))
    if (d,b) not in vis:
        stack.append((d,b,f+1,g+["FILL(2)"]))
        vis.add((d,b))
    if (d,0) not in vis:
        stack.append((d,0,f+1,g+["DROP(2)"]))
        vis.add((d,0))
    if (0,e) not in vis:
        stack.append((0,e,f+1,g+["DROP(1)"]))
        vis.add((0,e))

    if d + e > a:
        dd = a
        ee = (d+e) - a
    else:
        dd = d+e
        ee = 0
    if (dd,ee) not in vis:
        stack.append((dd, ee, f + 1, g + ["POUR(2,1)"]))
        vis.add((dd, ee))

    if d + e > b:
        dd = (d+e) - b
        ee = b
    else:
        dd = 0
        ee = d+e
    if (dd, ee) not in vis:
        stack.append((dd, ee, f + 1, g + ["POUR(1,2)"]))
        vis.add((dd, ee))
if res != 1000:
    print(res)
    for i in path:
        print(i)
else:
    print("impossible")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240505093159674](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240505093159674.png)



### 05907: 二叉树的操作

http://cs101.openjudge.cn/practice/05907/



思路：

自己写了一遍但反复rte，最后参考题解又写了一遍

代码

```python
# 
class Node:
    def __init__(self, name):
        self.name = name
        self.child = [None, None]
        self.parent = None
    
    def findLef(self):
        curr = self
        while (lef := nodes[curr.child[0]]):
            curr = lef
        return curr.name

for o in range(int(input())):
    n, m = map(int, input().split())
    nodes = [Node(i) for i in range(n)] + [None]
    for o in range(n):
        x, *idx = map(int, input().split())
        nodes[x].child = idx
        for i in [0,1]:
            if idx[i] != -1:
                nodes[idx[i]].parent = (nodes[x],i) 
    for o in range(m):
        token, *idx = map(int, input().split())
        if token == 1:
            p = [nodes[i].parent for i in idx]
            for i in [0,1]:
                p[i][0].child[p[i][1]] = idx[1-i]
                nodes[idx[i]].parent = p[1-i]
        else:
            print(nodes[idx[0]].findLef())
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

```
class Node:
    def __init__(self, name):
        self.name = name
        self.child = [None, None]
        self.parent = None
    
    def findLef(self):
        curr = self
        while (lef := nodes[curr.child[0]]):
            curr = lef
        return curr.name

for o in range(int(input())):
    n, m = map(int, input().split())
    nodes = [Node(i) for i in range(n)] + [None]
    for o in range(n):
        x, *idx = map(int, input().split())
        nodes[x].child = idx
        for i in [0,1]:
            if idx[i] != -1:
                nodes[idx[i]].parent = (nodes[x],i) 
    for o in range(m):
        token, *idx = map(int, input().split())
        if token == 1:
            p = [nodes[i].parent for i in idx]
            for i in [0,1]:
                p[i][0].child[p[i][1]] = idx[1-i]
                nodes[idx[i]].parent = p[1-i]
        else:
            print(nodes[idx[0]].findLef())
```





### 18250: 冰阔落 I

Disjoint set, http://cs101.openjudge.cn/practice/18250/



思路：

比较常规的并查集

代码

```python
# 
def find(x):
    if parent[x] != x:
        parent[x] = find(parent[x])
    return parent[x]

def union(x, y):
    root_x = find(x)
    root_y = find(y)
    if root_x != root_y:
        parent[root_y] = root_x

while 1:
    try:
        n,m = map(int,input().split())
        parent = [i for i in range(n+1)]
        for _ in range(m):
            a,b = map(int,input().split())
            if find(a) == find(b):
                print("Yes")
            else:
                print("No")
                union(a,b)
        res = 0
        coca = []
        for i in range(1,n+1):
            if parent[i] == i:
                res += 1
                coca.append(i)
        print(res)
        print(" ".join(map(str,coca)))





    except EOFError:
        break
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240505093401256](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240505093401256.png)



### 05443: 兔子与樱花

http://cs101.openjudge.cn/practice/05443/



思路：

学习了题解中字典嵌套字典的做法，相比使用类更加方便

代码

```python
# 
import heapq
import math
def dijkstra(graph,start,end,P):
    if start == end:
        return []
    dist = {i:(math.inf,[]) for i in graph}
    dist[start] = (0,[start])
    pos = []
    heapq.heappush(pos,(0,start,[]))
    while pos:
        dist1,current,path = heapq.heappop(pos)
        for (next,dist2) in graph[current].items():
            if dist1+dist2< dist[next][0]:
                dist[next] = (dist2+dist1,path+[next])
                heapq.heappush(pos,(dist1+dist2,next,path+[next]))
    return dist[end][1]
P = int(input())
graph = {input():{} for _ in range(P)}
for _ in range(int(input())):
    place1,place2,dist = input().split()
    graph[place1][place2] = graph[place2][place1] = int(dist)

for _ in range(int(input())):
    start,end = input().split()
    path = dijkstra(graph,start,end,P)
    s = start
    current = start
    for i in path:
        s += f'->({graph[current][i]})->{i}'
        current = i
    print(s)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240505093447403](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240505093447403.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周重点仍在于bfs，dfs，djikstra和并查集以及树相关方面，从最后一道题中学到的字典嵌套字典代替GRAPH类的做法，感觉很方便

五一刚回来，暂无额外练习ORZ



