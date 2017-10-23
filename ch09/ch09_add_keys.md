
[TOC]



# 补充题解 - 《经典》- 第 9 章动态规划初步

## 习题 9-7 Locker, Tianjin 2012, UVa1631

记初始数字序列为S[0,N)，目标序列为T[0,N)

每次转动可以选择选择相邻的1到3个。那么从左到右决策每一位时同时考虑相关的3位，具体来说设D(i,d0,d1,d2)为$[i,N)$区间的每一位还未考虑，(i, i+1, i+2)三位上的数字分别是$d_0,d_1,d_2$，还需要的最少转动次数。

则状态转移方法如下:

1. $i = N-1$时，$D = min((d_0 - T_{N-1} + 10) \mod 10, (T_{N-1} - d_0 + 10) \mod 10)$，其实就是看看把$d_0$转动到$T_{N-1}$的上下两个方向哪种转动次数更小。
2. $d_0 = T_i $时，$D = D(i+1, d_1, d_2, S_{i+3})$。
3. 考虑往T上转k = $(T_i -d_0 + 10) \mod 10$次，则i+1, i+2位往上转的次数$k_1, k_2$就是满足$k\geq k_1 \geq k_2 \geq 0$的所有情况，针对每种情况 $D(i, d_0, d_1, d_2) = min(D(i, d_0, d_1, d_2), k + D(i+1, up(d_1, k_1), up(d_2, k_2)))$。其中up(a,b)表示数字a朝上转b得到的数字：$(a+b) \mod 10$。
4. T往下转k的情况同理。

则所求结果就是：$D(0, S_0, S_1, S_2 )$。











