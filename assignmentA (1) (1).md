# Assignment #A: 图论：算法，树算及栈

Updated 2018 GMT+8 Apr 21, 2024

2024 spring, Complied by 孙一弘 工学院

**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**



操作系统：win11

Python编程环境：PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 20743: 整人的提词本

http://cs101.openjudge.cn/practice/20743/



思路：栈的运用，需要一个temp来暂时储存需要反序的字符串



代码

```python
# s = input()
stack = []
recent = ''
flag = False
for i in s:
    if i == ")":
        temp = []
        while stack and stack[-1] != "(":
            temp.append(stack.pop())
        if stack:
            stack.pop()
        stack.extend(temp)
    else:
        stack.append(i)
print("".join(stack))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240428211657751](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240428211657751.png)



### 02255: 重建二叉树

http://cs101.openjudge.cn/practice/02255/



思路：

之前做过类似的

代码

```python
# 
class Tree:
    def __init__(self,x):
        self.val = x
        self.l = None
        self.r = None



def build(pre,inn):
    if not pre and not inn:
        return None
    root = Tree(pre[0])
    r = pre[0]
    index = inn.index(r)
    root.l = build(pre[1:1+index],inn[:index])
    root.r = build(pre[1+index:],inn[index+1:])
    return root

def pos(root):
    if not root:
        return []
    return pos(root.l) + pos(root.r) + [root.val]

while 1:
    try:
        a, b = map(str, input().split())
        root = build(a,b)
        print(''.join(map(str,pos(root))))
    except EOFError:
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240428211733590](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240428211733590.png)



### 01426: Find The Multiple

http://cs101.openjudge.cn/practice/01426/

要求用bfs实现



思路：

bfs枚举01

代码

```python
# 
from collections import deque
def check(st):
    st = str(st)
    for i in st:
        if i == "1" or i == "0":
            pass
        else:
            return False
    return True

while 1:
    n = int(input())
    if n == 0:
        break
    stack = deque()
    stack.append(1)
    stack.append(0)
    while stack:
        a = stack.popleft()
        if a%n == 0 and a!= 0:
            print(a)
            break
        stack.append(a*10+1)
        stack.append(a*10)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240428211806598](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240428211806598.png)



### 04115: 鸣人和佐助

bfs, http://cs101.openjudge.cn/practice/04115/



思路：主要难点在于走过的路可以重复走，在查克拉花费小于之前的情况下



代码

```python
# from collections import deque


class Node:
    def __init__(self, x, y, tools, steps):
        self.x = x
        self.y = y
        self.tools = tools
        self.steps = steps


M, N, T = map(int, input().split())
maze = [list(input()) for _ in range(M)]
visit = [[[0]*(T+1) for _ in range(N)] for _ in range(M)]
directions = [[-1, 0], [1, 0], [0, -1], [0, 1]]
start = end = None
flag = 0
for i in range(M):
    for j in range(N):
        if maze[i][j] == '@':
            start = Node(i, j, T, 0)
            visit[i][j][T] = 1
        if maze[i][j] == '+':
            end = (i, j)
            maze[i][j] = '*'
            
queue = deque([start])
while queue:
    node = queue.popleft()
    if (node.x, node.y) == end:
        print(node.steps)
        flag = 1
        break
    for direction in directions:
        nx, ny = node.x+direction[0], node.y+direction[1]
        if 0 <= nx < M and 0 <= ny < N:
            if maze[nx][ny] == '*':
                if not visit[nx][ny][node.tools]:
                    queue.append(Node(nx, ny, node.tools, node.steps+1))
                    visit[nx][ny][node.tools] = 1
            elif maze[nx][ny] == '#':
                if node.tools > 0 and not visit[nx][ny][node.tools-1]:
                    queue.append(Node(nx, ny, node.tools-1, node.steps+1))
                    visit[nx][ny][node.tools-1] = 1
                    
if not flag:
    print("-1")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240428211949788](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240428211949788.png)



### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/



思路：

dijkstra，之前做过

代码

```python
# 
import heapq

turn = [[1, 0], [0, 1], [-1, 0], [0, -1]]

n, mm, p = map(int, input().split())

m = []
m.append(['#' for _ in range(mm + 2)])
for _ in range(n):
    x = input().split()
    m.append(['#'] + [i if i != '#' else '#' for i in x] + ['#'])
m.append(['#' for _ in range(mm + 2)])
ress = []
for _ in range(p):
    a, b, c, d = map(int, input().split())
    vis = {}
    vis[(a + 1, b + 1)] = 0
    queue = []
    if m[a + 1][b + 1] == "#" or m[c+1][d+1] == "#":
        ress.append(10000)
        continue
    heapq.heappush(queue, (0, a + 1, b + 1, int(m[a + 1][b + 1]) if m[a + 1][b + 1] != '#' else 0))
    goal = (c + 1, d + 1)
    found = False
    res = 10000

    while queue:
        segs, x, y, pre = heapq.heappop(queue)
        if (x, y) == goal:
            res = segs
            found = True
            break

        for i in range(4):
            newX, newY = x + turn[i][0], y + turn[i][1]
            if m[newX][newY] != '#':
                new_segs = segs + abs(pre - int(m[newX][newY]))
                if (newX, newY) not in vis or new_segs < vis[(newX, newY)]:
                    vis[(newX, newY)] = new_segs
                    heapq.heappush(queue, (new_segs, newX, newY, int(m[newX][newY])))

    ress.append(res if found else 10000)
for r in ress:
    if r != 10000:
         print(r)
    else:
        print("NO")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240428212030830](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240428212030830.png)



### 05442: 兔子与星空

Prim, http://cs101.openjudge.cn/practice/05442/



思路：参考了题解，学会了最小生成树这一算法



代码

```python
# import heapq

def prim(graph, start):
    mst = []
    used = set([start])
    edges = [
        (cost, start, to)
        for to, cost in graph[start].items()
    ]
    heapq.heapify(edges)

    while edges:
        cost, frm, to = heapq.heappop(edges)
        if to not in used:
            used.add(to)
            mst.append((frm, to, cost))
            for to_next, cost2 in graph[to].items():
                if to_next not in used:
                    heapq.heappush(edges, (cost2, to, to_next))

    return mst

def solve():
    n = int(input())
    graph = {chr(i+65): {} for i in range(n)}
    for i in range(n-1):
        data = input().split()
        star = data[0]
        m = int(data[1])
        for j in range(m):
            to_star = data[2+j*2]
            cost = int(data[3+j*2])
            graph[star][to_star] = cost
            graph[to_star][star] = cost
    mst = prim(graph, 'A')
    print(sum(x[2] for x in mst))

solve()

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240428212439877](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240428212439877.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周主要还是进一步学习了搜索的相关算法，并巩固了之前树的知识，学到了最小生成树这一算法

在课外回顾了下上学期计算概论时做过的bfs和dfs题目



