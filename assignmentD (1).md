# Assignment #D: May月考

Updated 1654 GMT+8 May 8, 2024

2024 spring, Complied by孙一弘 工学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：win11

Python编程环境 PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：签到题



代码

```python
# 
a,b= map(int,input().split())

tree = []
for i in range(a+1):
    tree.append(0)
for i1 in range(b):
    x,y = map(int,input().split())
    for i2 in range(x,y+1):
        tree[i2] = 1
    
print(tree.count(0))      
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240512102541588](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240512102541588.png)



### 20449: 是否被5整除

http://cs101.openjudge.cn/practice/20449/



思路：

用int(.,2)二进制转十进制即可

代码

```python
# 
a = input()
for i in range(1,len(a)+1):
    b = int(a[:i],2)
    if b % 5 == 0:
        print("1",end = '')
    else:
        print("0",end = "")
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240512102615239](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240512102615239.png)



### 01258: Agri-Net

http://cs101.openjudge.cn/practice/01258/



思路：dijkstra



代码

```python
# import heapq
while True:
    try:
        n = int(input())
        ver = {i: {} for i in range(n)}
        for i in range(n):
            temp = list(map(int, input().split()))
            for j in range(n):
                if temp[j] != 0:
                    ver[i][j] = temp[j]
        mst = set()
        visited = set([0])
        edges = [(cost, 0, to) for to, cost in ver[0].items()]
        heapq.heapify(edges)
        while edges:
            cost, frm, to = heapq.heappop(edges)
            if to not in visited:
                visited.add(to)
                mst.add((frm, to, cost))
                for to_next, cost2 in ver[to].items():
                    if to_next not in visited:
                        heapq.heappush(edges, (cost2, to, to_next))
        res = sum(cost for frm, to, cost, in mst)
        print(res)
    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240512102730786](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240512102730786.png)



### 27635: 判断无向图是否连通有无回路(同23163)

http://cs101.openjudge.cn/practice/27635/



思路：难在如何判断有无回路



代码

```python
# 
def connection(ver,n):
    visited = [False]*n
    stack = [0]
    visited[0] = True

    while stack:
        node = stack.pop()
        for neighbor in ver[node]:
            if not visited[neighbor]:
                stack.append(neighbor)
                visited[neighbor] = True
    return all(visited)
def cycle(ver,n):
    def dfs(node,visited,parent):
        visited[node] = True
        for neighbor in ver[node]:
            if not visited[neighbor]:
                if dfs(neighbor,visited,node):
                    return True
            elif parent != neighbor:
                return True
        return False
    visited = [False]*n
    for node in range(n):
        if not visited[node]:
            if dfs(node,visited,-1):
                return True
    return False
n,m = map(int,input().split())
ver = [[] for _ in range(n)]
for __ in range(m):
    a,b = map(int,input().split())
    ver[a].append(b)
    ver[b].append(a)

if connection(ver,n):
    print("connected:yes")
else:
    print("connected:no")
if cycle(ver,n):
    print("loop:yes")
else:
    print("loop:no")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240512102824305](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240512102824305.png)





### 27947: 动态中位数

http://cs101.openjudge.cn/practice/27947/



思路：

一开始没有想到使用两个堆来分别记录偏大和偏小的数，题解中使用大顶堆和小顶堆的思路很巧妙

代码

```python
# 
import heapq
n = int(input())
for _ in range(n):
    res = []
    minStack = []
    maxStack = []
    heapq.heapify(minStack)
    heapq.heapify(maxStack)
    for i,num in enumerate(map(int,input().split())):
        if not maxStack or num < -maxStack[0]:
            heapq.heappush(maxStack,-num)
        else:
            heapq.heappush(minStack,num)
        if len(maxStack)- len(minStack) > 1:
            heapq.heappush(minStack,-heapq.heappop(maxStack))
        elif len(minStack) > len(maxStack):
            heapq.heappush(maxStack,-heapq.heappop(minStack))

        if i % 2 == 0:
            res.append(-maxStack[0])
    print(len(res))
    print(*res)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240512103039262](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240512103039262.png)



### 28190: 奶牛排队

http://cs101.openjudge.cn/practice/28190/



思路：

正确思路是找两个边界然后枚举，我自己写的时候只用了一个单调栈，乍一看没什么问题但是题目中相邻数字可能取等的条件导致wa

代码

```python
# 
n = int(input())
heights = [int(input()) for _ in range(n)]

left = [-1]*n
right = [n]*n

stack = []

for i in range(n):
    while stack and heights[stack[-1]] < heights[i]:
        stack.pop()
    if stack:
        left[i] = stack[-1]
    stack.append(i)
stack = []

for i in range(n-1,-1,-1):
    while stack and heights[stack[-1]]> heights[i]:
        stack.pop()
    if stack:
        right[i] = stack[-1]
    stack.append(i)

ans = 0
for i in range(n):
    for j in range(left[i]+1,i):
        if right[j] > i:
            ans = max(ans,i-j+1)
            break
print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240512103241348](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240512103241348.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

依旧是撞上机课导致没时间参加月考，感觉上来讲掌握教材内容可以保证拿到AC4及以上，后两道难题需要在已经学会的数据结构和算法之间综合解决

课下时间在阅读教材，为机考和笔试做准备



