# Assignment #8: 图论：概念、遍历，及 树算

Updated 1919 GMT+8 Apr 8, 2024

2024 spring, Complied by 孙一弘 工学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：win11

Python编程环境： PyCharm 2023.1.4 (Professional Edition)

### 19943: 图的拉普拉斯矩阵

matrices, http://cs101.openjudge.cn/practice/19943/





思路：

定义vertex和graph两个类，然后像搭积木一样调用，本题主要在于练习两个类的书写方法，20min

代码

```python
# class Vertex:
    def __init__(self,key):
        self.id = key
        self.connectedto = {}
    def add(self,nbr,weight = 0):
        self.connectedto[nbr] = weight
    def __str__(self):
        return str(self.id) + ' coonectedto:' + str([x.id for x in self.connectedto])
    def getconnections(self):
        return self.connectedto.keys()
    def getid(self):
        return self.id
    def getweight(self,nbr):
        return self.connectedto[nbr]
class Graph:
    def __init__(self):
        self.list = {}
        self.num = 0
    def add(self,key):
        self.num += 1
        newv = Vertex(key)
        self.list[key] = newv
        return newv
    def get(self,n):
        if n in self.list:
            return self.list[n]
        else:
            return None
    def __contains__(self,n):
        return n in self.list
    def addegde(self,f,t,weight = 0):
        if f not in self.list:
            nv = self.add(f)
        if t not in self.list:
            nv = self.add(t)
        self.list[f].add(self.list[t],weight)
    def getvertices(self):
        return self.list.keys()
    def __iter__(self):
        return iter(self.list.values())

def construct(n,edges):
    graph = Graph()
    for i in range(n):
        graph.add(i)
    for edge in edges:
        a,b = edge
        graph.addegde(a,b)
        graph.addegde(b,a)
    mat = []
    for vertex in graph:
        row = [0] * n
        row[vertex.getid()] = len(vertex.getconnections())
        for neighbor in vertex.getconnections():
            row[neighbor.getid()] -= 1
        mat.append(row)
    return mat
n,m = map(int,input().split())
edges = []
for _ in range(m):
    a,b = map(int,input().split())
    edges.append((a,b))
mat = construct(n,edges)
for row in mat:
    print(" ".join(map(str,row)))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240412144011971](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240412144011971.png)



### 18160: 最大连通域面积

matrix/dfs similar, http://cs101.openjudge.cn/practice/18160



思路：

dfs，之前写过，5min

代码

```python
# maxx = 0
turn = [[0,1],[1,0],[0,-1],[-1,0],[1,1],[-1,-1],[-1,1],[1,-1]]

def dfs(i,j,res,chess):
    global maxx
    if chess[i-1][j] == '.' and chess[i+1][j] == '.' and chess[i][j-1] == '.' and chess[i][j+1] == '.' and chess[i-1][j-1] == '.' and chess[i+1][j+1] == '.' and chess[i-1][j+1] == '.' and chess[i+1][j-1] == '.':
        chess[i][j] = '.'
        return res
    chess[i][j] = '.'
    for ii in turn:
        i,j = i+ ii[0],j+ii[1]
        if chess[i][j] != '.':
            res += dfs(i,j,1,chess)
            i,j = i-ii[0],j-ii[1]
        else:
            i,j = i-ii[0],j-ii[1]
    return res





n = int(input())
for _ in range(n):
    n,m = map(int,input().split())
    chess = []  
    maxx = 0
    chess.append(['.' for _ in range(m+2)])
    for __ in range(n):
        st = input()
        st = '.' + st + '.'
        chess.append([i for i in st])
    chess.append(['.' for _ in range(m+2)])
    for i in range(1,n+1):
        for j in range(1,m+1):
            if chess[i][j] != '.':
                maxx = max(maxx,dfs(i,j,1,chess))
    print(maxx)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240412144021706](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240412144021706.png)



### sy383: 最大权值连通块

https://sunnywhy.com/sfbj/10/3/383



思路：

dfs，15min

代码

```python
# 
def dfs(node,visited,ad):
    res = val[node]
    if visited[node]:
        return res
    visited[node] = True
    for n in ad[node]:
        if not visited[n]:
            res += dfs(n,visited,ad)
    return res
maxxx = 0
n,m = map(int,input().split())
ad = [[] for _ in range(n)]
val = list(map(int,input().split()))
for _ in range(m):
    a,b = map(int,input().split())
    ad[a].append(b)
    ad[b].append(a)
visited = [False]*n
res = 0
for i in range(n):
    res = max(res,dfs(i,visited,ad))
print(res)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240412144159124](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240412144159124.png)



### 03441: 4 Values whose Sum is 0

data structure/binary search, http://cs101.openjudge.cn/practice/03441



思路：

通过分成两组然后存储字典的方式将时间复杂度降低到o（n^2）,但是使用defaultdict会导致内存过大

代码

```python
# n = int(input())
dic= {}
aa = []
bb= []
cc = []
dd = []
for _ in range(n):
     a,b,c,d = map(int,input().split())
     aa.append(a),bb.append(b),cc.append(c),dd.append(d)
for i in aa:
    for j in bb:
        t = i+j
        if t in dic:
            dic[t] += 1
        else:
            dic[t] = 1
res = 0
for ii in cc:
    for jj in dd:
        if -(ii + jj) in dic:
          res += dic[-(ii+jj)]
print(res)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240412144237282](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240412144237282.png)



### 04089: 电话号码

trie, http://cs101.openjudge.cn/practice/04089/

Trie 数据结构可能需要自学下。



思路：主要是练习了trie这个数据结构，20min



代码

```python
# class trienode:
    def __init__(self):
        self.child = {}

class Trie:
    def __init__(self):
        self.root = trienode()
    def insert(self,nums):
        curnode = self.root
        for x in nums:
            if x not in curnode.child:
                curnode.child[x] = trienode()
            curnode = curnode.child[x]
    def search(self,num):
        curnode = self.root
        for x in num:
            if x not in curnode.child:
                return 0
            curnode = curnode.child[x]
        return 1

t = int(input())
p = []
for _ in range(t):
    n = int(input())
    nums = []
    for _ in range(n):
        nums.append(str(input()))
    nums.sort(reverse = True)
    s = 0
    trie = Trie()
    for num in nums:
        s += trie.search(num)
        trie.insert(num)
    if s>0:
        print("NO")
    else:
        print("YES")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240412144357759](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240412144357759.png)



### 04082: 树的镜面映射

http://cs101.openjudge.cn/practice/04082/



思路：

这题死磕了很久也没有做出来，最后对着题解写了一遍，答案的方法中对队列的运用很巧妙，2h

代码

```python
# 
from collections import deque

class treenode:
    def __init__(self,x):
        self.x = x
        self.children = []

def createNode():
    return treenode("")
def build_tree(list,index):
    node = createNode()
    node.x = list[index][0]
    if list[index][1] == '0':
        index += 1
        child,index = build_tree(list,index)
        node.children.append(child)
        index += 1
        child,index = build_tree(list,index)
        node.children.append(child)
    return node,index
def print_tree(p):
    Q = deque()
    s = deque()

    while p is not None:
        if p.x != '$':
            s.append(p)
        p = p.children[1] if len(p.children) > 1 else None

    while s:
        Q.append(s.pop())

    while Q:
        p = Q.popleft()
        print(p.x, end=' ')
        if p.children:
            p = p.children[0]
            while p is not None:
                if p.x != '$':
                    s.append(p)
                p = p.children[1] if len(p.children) > 1 else None
            while s:
                Q.append(s.pop())


n = int(input())
tempList = input().split()
root, _ = build_tree(tempList, 0)
print_tree(root)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240412144426019](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240412144426019.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周初步接触了图的数据结构以及类的定义方法，感觉跟树的很多地方都有相似的地方所以上手起来很快，bfs和dfs上学期计算概论做的题比较多所以用起来还算是比较顺手，感觉图这部分内容很多地方都需要用到这两种搜素方法。

仍旧处于期中考试期，暂时没有额外精力练习



