# Assignment #9: 图论：遍历，及 树算

Updated 1739 GMT+8 Apr 14, 2024

2024 spring, Complied by 孙一弘 工学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：WIN11

Python编程环境： PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 04081: 树的转换

http://cs101.openjudge.cn/dsapre/04081/



思路：按题意先建立广义的树，再根据左儿子右兄弟建树



代码

```python
# 
from collections import defaultdict

class Node:
    def __init__(self,data):
        self.data = data
        self.children = []
class Tree:
    def __init__(self,data):
        self.data = data
        self.l = None
        self.r = None
s = input()
dic = defaultdict(list)
dic[0].append(Node(0))
summ = 0
pos = 1
for i in s:
    if i == 'd':
        summ += 1
        a = Node(pos)
        dic[summ-1][-1].children.append(a)
        dic[summ].append(a)
        pos += 1
    else:
        summ -= 1
oldmax = max(dic.keys())

def build_tree(a):
    root = Tree(a.data)
    b= a.children[0]
    if b.children:
        root.l = build_tree(b)
    else:
        root.l = Tree(b.data)
    stack =[root,root.l]
    for i in a.children[1:]:
        if i.children:
            stack.append(build_tree(i))
        else:
            stack.append(Tree(i.data))
        stack[-2].r = stack[-1]
    return root
root = build_tree(dic[0][0])

def find(root):
    if root is None:
        return 0
    if root.r is None and root.l is None:
        return 1
    return max(find(root.r),find(root.l))+1
print(f'{oldmax} => {find(root)-1}')
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240422100643487](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240422100643487.png)



### 08581: 扩展二叉树

http://cs101.openjudge.cn/dsapre/08581/



思路：

用栈建树，先加左节点，左节点不为空则加入右，满载则弹出

代码

```python
# 
class Node:
    def __init__(self,data):
        self.data=data
        self.left=None
        self.right=None

def mid(root):
    return ("" if root.left==None else mid(root.left))+(""if root.data=='.'else root.data)+(""if root.right==None else mid(root.right))

def post(root):
    return ("" if root.left==None else post(root.left))+(""if root.right==None else post(root.right))+(""if root.data=='.'else root.data)

s=input()
root=Node(s[0])
stack=[root]
for i in range(1,len(s)):
    a=Node(s[i])
    if stack[-1].left==None :
        stack[-1].left=a
        if a.data!='.':
            stack.append(a)
    else :
        stack[-1].right=a
        stack.pop()
        if s[i]!='.':
            stack.append(a)

print(mid(root))
print(post(root))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240422102647349](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240422102647349.png)



### 22067: 快速堆猪

http://cs101.openjudge.cn/practice/22067/



思路：

懒删除

代码

```python
# import heapq
from collections import defaultdict

queue = []
queue2 = []
heapq.heapify(queue)
out = defaultdict(int)
while 1:
    try:
        a = list(input().split())
        if a[0] == 'pop':
            if queue2:
                out[queue2.pop()] += 1
        elif a[0][0] == 'm':
            if queue2:
                while True:
                    x = heapq.heappop(queue)
                    if not out[x]:
                        heapq.heappush(queue,x)
                        print(x)
                        break
                    out[x] -= 1
        else:
            y = int(a[1])
            queue2.append(y)
            heapq.heappush(queue,y)



    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240422103038117](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240422103038117.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123



思路：

常规dfs

代码

```python
# 
ans = 0
visited = []
move = [[1,2],[2,1],[-1,2],[2,-1],[-1,-2],[-2,-1],[1,-2],[-2,1]]
a,b = 0,0
def dfs(x,y):
    global ans
    if sum([sum(i) for i in visited]) == 0:
        ans += 1
        return
    for i in move:
        ix = x + i[0]
        iy = y + i[1]
        if 0 <= ix < a and 0 <= iy < b:
            if visited[ix][iy]:
                visited[ix][iy] = 0
                dfs(ix,iy)
                visited[ix][iy] = 1


t = int(input())
move = [[1,2],[2,1],[-1,2],[2,-1],[-1,-2],[-2,-1],[1,-2],[-2,1]]
for _ in range(t):
    a,b,c,d = map(int,input().split())
    visited = [[1 for _ in range(b)] for __ in range(a)]
    visited[c][d] = 0
    ans = 0
    dfs(c,d)
    print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240422103057123](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240422103057123.png)



### 28046: 词梯

bfs, http://cs101.openjudge.cn/practice/28046/



思路：

自己写了半天样例能过，最后参照题解修改了一下，主要思想是bfs+路径回溯

代码

```python
# 
from collections import deque

def construct_graph(words):
    graph = {}
    for word in words:
        for i in range(len(word)):
            pattern = word[:i] + '*' + word[i + 1:]
            if pattern not in graph:
                graph[pattern] = []
            graph[pattern].append(word)
    return graph

def bfs(start, end, graph):
    queue = deque([(start, [start])])
    visited = set([start])
    
    while queue:
        word, path = queue.popleft()
        if word == end:
            return path
        for i in range(len(word)):
            pattern = word[:i] + '*' + word[i + 1:]
            if pattern in graph:
                neighbors = graph[pattern]
                for neighbor in neighbors:
                    if neighbor not in visited:
                        visited.add(neighbor)
                        queue.append((neighbor, path + [neighbor]))
    return None

def word_ladder(words, start, end):
    graph = construct_graph(words)
    return bfs(start, end, graph)

n = int(input())
words = [input().strip() for _ in range(n)]
start, end = input().strip().split()

result = word_ladder(words, start, end)

if result:
    print(' '.join(result))
else:
    print("NO")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240422103150412](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240422103150412.png)



### 28050: 骑士周游

dfs, http://cs101.openjudge.cn/practice/28050/



思路：

主要难点在于优化

代码

```python
# 
maze = []
row_nums,col_nums = [-2,-2,-1,-1,1,1,2,2],[-1,1,-2,2,-2,2,-1,1]
ans = 0
done = False
def dfs(num,x,y):
    global ans
    global done
    if done:
        return
    if num == t**2:
        ans += 1
        done = True
        return
    res = order(x,y)
    for i in res:
        nx = int(i[0])
        ny = i[1]
        if 0 <= nx < t and 0 <= ny < t:
            if maze[nx][ny]:
                maze[nx][ny] = False
                dfs(num+1,nx,ny)
                maze[nx][ny] = True

def order(x,y):
    res = []
    for k in range(8):
        if 0 <= x + row_nums[k] < t and 0 <= y + col_nums[k] < t:
            if maze[x + row_nums[k]][y+col_nums[k]]:
                c = 0
                for kk in range(8):
                    if 0 <= x + row_nums[k] + row_nums[kk] < t and 0 <= y + col_nums[k] + col_nums[kk] < t:
                        if maze[x+row_nums[k]+row_nums[kk]][y+col_nums[k]+col_nums[kk]]:
                            c += 1
                res.append((c,x+row_nums[k],y+col_nums[k]))
    res.sort(key = lambda x : x[0])
    return [(y[1],y[2]) for y in res]

t = int(input())
x,y = map(int,input().split())
maze = [[True for _ in range(t)] for _ in range(t)]
maze[x][y] = False
ans = 0
dfs(1,x,y)
if ans > 0 :
    print("success")
else:
    print("fail")
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240422104700608](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240422104700608.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周主要学习了图和复习了一些树的相关操作，对于在各种复杂背景下建树的能力提高的（比如伪满二叉树一类），此外是对上学期学习的bfs和dfs进行了一些温习，其中的边界条件和return条件需要仔细扣。

课下回顾了本学期之前的课件，为笔试做准备



