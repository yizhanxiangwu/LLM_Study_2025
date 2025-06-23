
## Jacobian

### 1. **什么是Jacobian矩阵？**

- Jacobian矩阵本质是描述**多元变量变换时，每个输出变量对每个输入变量的偏导数**。
- 一般写作
  $$
  J = \begin{bmatrix}
  \frac{\partial x_1}{\partial z_1} & \frac{\partial x_1}{\partial z_2} \\
  \frac{\partial x_2}{\partial z_1} & \frac{\partial x_2}{\partial z_2}
  \end{bmatrix}
  $$

- 它衡量：在$z$空间里微小的变化，映射到$x$空间时怎样被拉伸/扭曲。

---

### 2. **你图中的写法对应物理意义**

- 你公式里的$\Delta x_{ij}/\Delta z_j$，其实就是**在离散情形下**逼近Jacobian矩阵每一项的方式。
- 在$\Delta z_j$足够小的时候，上述比值$\Delta x_{ij}/\Delta z_j$就趋近于偏导$\frac{\partial x_i}{\partial z_j}$。

- 所以**这个2×2的矩阵，就是Jacobian矩阵的“离散近似版”**。

---

### 3. **行列式的意义**

- 杰可比矩阵(Jacobian matrix)的**行列式的绝对值**给出的，就是“体积（或面积）变化的因子”。
- 乘在概率密度变换公式里的，就是让概率守恒。

---

## 一句话总结

> 你公式里那个 $ \begin{bmatrix} \Delta x_{11}/\Delta z_1 & \Delta x_{21}/\Delta z_1 \\ \Delta x_{12}/\Delta z_2 & \Delta x_{22}/\Delta z_2 \end{bmatrix} $ 就是**Jacobian矩阵**在数值/离散情况下的写法（无限细时就是常规偏导形式），它完全等价于连续变量变换公式中的雅可比。

---
