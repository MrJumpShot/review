# Floyd算法

Floyd算法可以解决多源最短路径的问题，但是缺点在于三层循环时间复杂度较大，

```
    // 核心代码就是三层循环
    void floyd() {
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    a[i][j] = Math.min(a[i][j], a[i][k] + a[k][j]);
                }
            }
        }
    }
```

看代码的特点，很显然特别像是一种动态规划。我们从动态规划的角度考虑，解动态规划题目的重点就是合理的定义状态，划分阶段，我们定义 `f[k][i][j]`为经过前`k`的节点，从i到j所能得到的最短路径，`f[k][i][j]`可以从`f[k-1][i][j]`转移过来，即不经过第`k`个节点，也可以从`f[k-1][i][k]+f[k-1][k][j]`转移过来，即经过第`k`个节点。观察一下这个状态的定义，满足不满足最优子结构和无后效性原则。