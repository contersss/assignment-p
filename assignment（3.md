# Assignment #3: March月考

Updated 1537 GMT+8 March 6, 2024

2024 spring, Complied by  孙一弘 工学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：win11

Python编程环境： PyCharm 2023.1.4 (Professional Edition)





## 1. 题目

**02945: 拦截导弹**

http://cs101.openjudge.cn/practice/02945/

10min

思路：

dp，最长下降子序列

##### 代码

```python
# k = int(input())
lis = list(map(int,input().split()))
dp = [1 for i in range(k)]
for i in range(1,k):
    for j in range(i-1,-1,-1):
        if lis[j] >= lis[i]:
            dp[i] = max(dp[j]+1,dp[i])
print(max(dp))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240310182802461](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240310182802461.png)



**04147:汉诺塔问题(Tower of Hanoi)**

http://cs101.openjudge.cn/practice/04147

15min

思路：

经典递归问题出

##### 代码

```python
# def Han_No_Ta(n, i, j, k):
    if (n == 1):
        print(n,":",i, "->", k,sep = '')
        return
    else:
        Han_No_Ta(n - 1, i, k, j,)
        print(n, ":", i, "->", k, sep='')
        Han_No_Ta(n - 1, j, i, k,)

a,i,j,k = input().split()
a = int(a)
m =  1
Han_No_Ta(a, i, j, k)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240310182827864](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240310182827864.png)



**03253: 约瑟夫问题No.2**

http://cs101.openjudge.cn/practice/03253

20min

思路：调试了半天，各种判断语句的顺序比较重要，可能换一种思路做会更方便



##### 代码

```python
# while 1:
    n,p,m = map(int,input().split())
    if n == 0 and p == 0 and m == 0:
        break
    lis = [i for i in range(n+10)]

    k = 0
    ii = 0

    while 1:
        if k == n:
            break
        if p >= n +1:
            p = 1
        if lis[p] <= 9999:
            ii += 1
        if ii == m:
            if k != n-1:
                print(p, ",", sep='', end='')
            else:
                print(p, sep='', end='')
            lis[p] = 10000
            k += 1
            ii = 0
        p +=1
        if p >= n +1:
            p = 1
    print()


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240310182935823](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240310182935823.png)



**21554:排队做实验 (greedy)v0.2**

http://cs101.openjudge.cn/practice/21554

3min

思路：做过



##### 代码

```python
# n = int(input())
stu = list(map(int,input().split()))
for i in range(n):
    stu[i] = [stu[i],i+1]
stu.sort(key = lambda x :x[0])
summ = stu[0][0]
res = 0
for i in stu:
    print(i[1],end = ' ')
for i in range(1,n):
    res += summ
    summ += stu[i][0]
res = res/n
print()
print(f'{res:.2f}')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240310182949851](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240310182949851.png)



**19963:买学区房**

http://cs101.openjudge.cn/practice/19963

3min

思路：也做过



##### 代码

```python
# a = int(input())
res = 0
pairs = [i[1:-1] for i in input().split()]
dis = [sum(map(int,i.split(','))) for i in pairs]
price = list(map(int,input().split()))
xjb = []
for i in range(a):
    xjb.append(dis[i]/price[i])
aa = sorted(price)
bb = sorted(xjb)
if a % 2 != 0:
    mp = aa[a//2]
    xp = bb[a//2]
else:
    mp = (aa[a//2]+aa[a//2-1])/2
    xp = (bb[a//2]+bb[a//2-1])/2
for i in range(a):
    if xjb[i] > xp and price[i] <mp:
        res += 1
print(res)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240310183018721](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240310183018721.png)



**27300: 模型整理**

http://cs101.openjudge.cn/practice/27300



思路：主要在于写一个转换字符串和数值的函数

10min

##### 代码

```python
# def compare(x):
    if "M" in x:
        return float(x.replace("M",""))*1000000
    elif "B" in x:
        return float(x.replace("B",""))*1000000000
    else:
        return float(x)

n = int(input())
dic = {}
for i in range(n):
    a,b = input().split("-")
    if a not in dic.keys():
        dic[a] = [b]
    else:
        dic[a] = dic[a] + [b]
h = list(dic.keys())
h.sort()
for key in h:
    dic[key].sort(key = lambda x:compare(x))
    res = ", ".join(dic[key])
    print(f"{key}: {res}")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240310184614327](C:\Users\13661\AppData\Roaming\Typora\typora-user-images\image-20240310184614327.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

因为撞课所以做月考的时间不长，最后一道题思路很明确但是没时间了，前面的dp因为好久不练习刚开始没看出来。

在课下去b站提前学了二叉树和AVL树的原理及其相关操作，初步接触了树这一数据结构，



