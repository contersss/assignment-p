# Assignment #7: April 月考

Updated 1557 GMT+8 Apr 3, 2024

2024 spring, Complied by  孙一弘 工学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：win11

Python编程环境： PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

### 27706: 逐词倒放

http://cs101.openjudge.cn/practice/27706/



思路：

3min

代码

```python
# 
lis = input().split()
print(' '.join(str(i) for i in lis[::-1]))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240406161414936](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240406161414936.png)



### 27951: 机器翻译

http://cs101.openjudge.cn/practice/27951/



思路：

使用deque进行模拟，5min

代码

```python
# 
from collections import deque
m,n = map(int,input().split())
lis = list(map(int,input().split()))
q = deque()
res = 0
for i in lis:
    if i not in q:
        if len(q) == m:
            q.popleft()
            q.append(i)
            res += 1
        else:
            q.append(i)
            res += 1
    else:
        pass
print(res)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240406161435970](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240406161435970.png)



### 27932: Less or Equal

http://cs101.openjudge.cn/practice/27932/



思路：

注意区分k = 0 的时候

代码

```python
# 
n,k = map(int,input().split())
lis = list(map(int,input().split()))
lis.sort()
if k == 0:
    if lis[0] > 1:
        print(lis[0]-1)
    else:
        print("-1")
elif k == n:
    print(lis[-1])
else:
    if lis[k-1] == lis[k]:
        print("-1")
    else:
        print(lis[k-1])
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240406161527328](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240406161527328.png)



### 27948: FBI树

http://cs101.openjudge.cn/practice/27948/



思路：

根据题意建树然后后序遍历即可。20min

代码

```python
# 
class tree:
    def __init__(self,val):
        self.val = val
        self.l = None
        self.r = None

def build(st,nn):
     if nn == n+1:
         return
     a = len(st) // 2
     if "0" in st and "1" in st:
         node = tree("F")
         node.l = build(st[:a],nn+1)
         node.r = build(st[a:],nn+1)
     elif "0" not in st:
         node = tree("I")
         node.l = build(st[:a],nn+1)
         node.r = build(st[a:],nn+1)
     else:
         node = tree("B")
         node.l = build(st[:a],nn+1)
         node.r = build(st[a:],nn+1)
     return node

def order(root):
    if root is None:
        return []
    return order(root.l) + order(root.r) + [root.val]
n = int(input())
st = input()
root = build(st,0)
print(''.join(str(i) for i in order(root)))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240406161629216](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240406161629216.png)



### 27925: 小组队列

http://cs101.openjudge.cn/practice/27925/



思路：

使用deque来进行队列的进出，20min

代码

```python
# from collections import deque
t = int(input())
dic = {}
for i in range(t):
    lis = list(map(str,input().split()))
    for ii in lis:
        dic[ii] = i
queue = deque()
while 1:
    st = input()
    if st[0] == "S":
        break
    elif st[0] == "E":
        a,b = map(str,st.split())
        c = False
        for i in range(len(queue)):
            if dic[b] == dic[queue[i]] and i+1 == len(queue):
                queue.append(b)
                c = True
                break
            elif dic[b] == dic[queue[i]] and  dic[b] != dic[queue[i+1]]:
                queue.insert(i+1,b)
                c = True
                break
        if not c:
            queue.append(b)
    else:
        print(queue.popleft())

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240406161727401](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240406161727401.png)



### 27928: 遍历树

http://cs101.openjudge.cn/practice/27928/



思路：

主要难度在于建立树以及找到根节点，30min

代码

```python
# 
class Tree:
    def __init__(self, val):
        self.val = val
        self.children = []
        self.parent = None

    def add_child(self, child):
        self.children.append(child)
        child.parent = self

    def traverse(self):
        if self.children == []:
            print(self.val)
        else:
            tmp_nodes = self.children + [self]
            tmp_nodes.sort(key=lambda x: x.val)
            for node in tmp_nodes:
                if node.val != self.val:
                    node.traverse()
                else:
                    print(node.val)

def build_tree(n, nodes):
    for _ in range(n):
        values = list(map(int, input().split()))
        root_val = values[0]
        if root_val not in nodes:
            nodes[root_val] = Tree(root_val)
        t = nodes[root_val]
        for child_val in values[1:]:
            if child_val not in nodes:
                nodes[child_val] = Tree(child_val)
            child = nodes[child_val]
            t.add_child(child)
            child.parent = t

    root = None
    for root_val in nodes:
        if not nodes[root_val].parent:
            root = nodes[root_val]
            break

    return root

if __name__ == "__main__":
    nodes = {}
    n = int(input())
    root = build_tree(n, nodes)
    if root:
        root.traverse()
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240406161926547](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240406161926547.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

由于撞课原因月考只考了40min，AC4，目前月考难度都可以跟得上。感觉这段时间对于树的各种操作越来越得心应手了，主要还是需要准备笔试上的内容。



暂未练习额外机考题目，主要精力在巩固笔试知识
