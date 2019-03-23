---
layout:     post
title:      NP 问题
subtitle:   NP问题以及NPC问题之间的规约
date:       2019-03-23
author:     ZHD
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - algorithm assignment
---

1. Given two strings $$ x = x_{1}x_{2} . . . xn $$ and$$ y = y_{1}y_{2} . . . y_{m}$$, we wish to find the length of their longest common substring, that is, the largest k for which there are indices i and j with $$x_{i}x_{i+1} . . . x_{i+k−1} = y_{j}y_{j+1} . . . y_{j+k−1}. $$Show how to do this in time O(mn)
使用动态规划算法，定义dp[i][j]为x中的以第i个字符为子串的结尾以及y中以第j个字符为子串结尾的最大公共子串。若x[i]与y[j]相同，那么dp[i][j] = dp[i-1][j-1] + 1,若不相同那么dp[i][j] = 0，则根据该算法求出最大公共子串只需要填充大小为mn的二位表格即可。即算法的时间复杂度为$$ O(mn) $$

2. STING SAT is the following problem: given a set of clauses (each a disjunction of literals) and an integer k, find a satisfying assignment in which at most k variables are true, if such an assignment exists. Prove that STING SAT is NP-complete.
在已知变量分配的条件下可以在多项式时间内验证合取范式的结果是true还是false，所以可知STING SAT是NP问题。其次，将SAT问题的变量个数限制为K个，那么SAT问题至多存在K个变量为true。同时SAT规约到STING SAT问题。因为SAT问题是NPC问题那么STING SAT同样也是NPC问题。

3. Given a directed graph G = (V, E) with weights $$w_e$$ on its edges $$e \in E  $$. The weights can be negative or positive. The ZERO-WEIGHT-CYCLE PROBLEM is to decide if there is a simple cycle in G so that the sum of the edge weights on this cycle is exactly 0. Prove that this problem is NPcomplete.
在已知某一个可能解的情况下，可以在多项式的时间内验证该可能的解是否是正确的解，所以ZERO-WEIGHT-CYCLE问题是NP问题，将子集和问题中所选子集的和设为零，那么子集和问题便规约成了ZERO-WEIGHT-CYCLE问题，一直子集和问题为NPC问题那么ZERO-WEIGHT-CYCLE也为NPC问题。

4. There are N villages, which are numbered from 1 to N, and you should build some roads such that every two villages can connect to each other. We say two villages A and B are connected, if and only if there is a road between A and B, or there exists a village C such that there is a road between A and C, and C and B are connected.
The distance between every two villages is known. Furthermore, there are already some roads between some villages and your job is to build some roads such that all the villages are connect and the distance of all roads newly built is minimum.
将所有已经部分连接的村庄或者独立的村庄都看着一个个独立的集合。然后采用贪心法，找到不同集合之间最短距离，然后将这两个村子连接，即将这两个村子所在的集合合并在一起。之后循环进行直到仅剩一个集合为止，最后所添加的线路的权重和就是所需的最短距离。

5. Let G be a n vertices graph. Show that if every vertex in G has degree at least n/2, then G contains a Hamiltonian path.
图中相连两点度数之和为n那么图中必有哈密尔顿路径。
证：首先任意的不相邻的两个顶点u，v，$$d(u) + d(v) \ge n$$（等式1）.反证满足此条件但是没有哈密尔顿路径。不妨假设G是边极大的非Hamilton图，且满足等式1。若G不是边极大的非Hamilton图，则可以不断地向G增加若干条边,把G 变成边极大的非Hamilton图$$G’$$，$$G’$$依然满足等式1，因为对任意 $$v \in V(G), d_G(v) \leq d_G{'}(v)$$.设u, v是G中不相邻的两点，于是$$G+uv$$是Hamilton图，且其中每条Hamilton回路都要通过边uv. 因此，G中有起点为u，终点为v的Hamilton通路,不存在两个相邻的顶点 $$v_{i-1}$$和$$v_i$$,使得$$v_{i-1}$$与$$v$$相邻且$$v_i$$ 与$$u$$相邻. 若不然, $$(v_1,v_2, … v_{i-1}, v_n, …, v_i
, v_1)$$是$$G$$的Hamilton回路. 设在$$G$$中$$u$$与$$v_{i1}, v_{i2}, …, v_{ik}$$相邻, 则$$v$$与$$v_{i_1-1}, v_{i_2-1}, …v_{i_k-1}$$都不相邻, 因此$$d(u)+d(v) \le k+[(n-1)-k] < n$$. 矛盾.


6. Show that INDEPENDENT SET PROBLEM is NP-hard even graphs of maximum degree 3.
图$$G(V,E)$$的补图为$$G'(V,E')$$其中$$E'$$包含图G不在$$E$$中点的无序对。集合S为团当且仅当S为图$$G'$$的独立集。因此可以将图的团问题规约为补图的独立集问题，因为图的团问题是NP-hard问题那么图的独立集问题同样也是NP-hard问题。

7. For your new startup company, Uber for Algorithms, you are trying to assign projects to employees. You have a set $$P$$ of $$n$$ projects and a set $$E$$ of $$m$$ employees. Each employee $$e$$ can only work on one project, and each project $$p \in P $$has a subset$$ E_p \subseteq E $$of employees that must be assigned to $$ p$$ to complete $$p$$. The decision problem we want to solve is whether we can assign the employees to projects such that we can complete (at least) $$k$$ projects.

* Give a straightforward algorithm that checks whether any subset of $$k$$ projects can be completed to solve the decisional problem. Analyze its time complexity in terms of $$m$$, $$n$$, and $$k$$.
首先声明大小为m的数组M并初始化为0，然后遍历K个项目，查看每一个项目的员工，每查看一个员工就将M中该员工对应下标的值加一，同时判断该员工是否已经被安排多个项目，即该值大于1，若大于1则不可以完成K个项目，若遍历结束没有值大于1，那么说明可以完成K项目，则其时间复杂度为$$O(mk)$$

* Show that the problem is NP-hard via a reduction from 3D matching.
令3Dmatching的3个集合为$$X,Y,Z$$，集合$$X$$的值为$$\{x_1,x_2,...,x_n\}$$,集合$$Y$$的值为$$\{y_1,y_2,...,y_n\}$$,集合$$Z$$的值为$$\{z_1,z_2,...,z_n\}$$，然后判断是否存在至少K个matching,规约过程：令集合$$X$$中每一个值代表一个项目。$$E_{p1} \subset E_p$$,$$E_{p2} = E_p - E_{p1}$$,集合$$Y$$中的值代表集合$$E_{p1}$$,集合$$Z$$中的值代表集合$$E_{p2}$$,此时3Dmatching问题便规约成了此题的问题，若存在一个分配满足完成至少K项目的要求，那么便存在至少K个matching，若没有一个分配满足要求，那么在集合$$X,Y,Z$$之间也不存在至少K个matching。


8. Let $$d \in N$$ The d-COLORABILITY problem is to decide whether a given graph $$G = (V, E)$$ can be colored by d colors. i.e., whether there exists a function$$ f : V → {1, . . . , d} $$ such that for every $$u, v \in V $$with $$ \{u, v\} \in E $$ we have $$f(u) \not= f(v)$$. Formulate d-COLORABILITY as a search problem.Give a reduction from 4-COLORABILITY to 7-COLORABILITY.
在图G外增加3个点，然后3个点的每一个都和其他的点全连接，此时构成新的图L，因为另外增加的3个点都是相邻的所以必然使用3个不同的颜色，所以若图L能够用7个颜色着色，那么图G就能够用4个颜色着色，若图L不能用7个颜色着色，那么图G也不能用4个颜色着色，此时4着色问题就归约到了7着色问题。










