# 张宇考研数学

**泰勒展开**

|       $f(x)$        |     $\sum\limits_{n=0}^\infty \frac{f(0)^{(n)}}{n!}x^n$      |
| :-----------------: | :----------------------------------------------------------: |
|      $\sin x$       | $\sum\limits_{n=0}^\infty (-1)^{n}\frac{x^{2n+1}}{(2n+1)!}$  |
|       $\mathrm{sh} x$       |     $\sum\limits_{n=0}^\infty \frac{x^{2n+1}}{(2n+1)!}$      |
|      $\cos x$       |     $\sum\limits_{n=0}^\infty (-1)^n \frac{x^{2n}}{2n!}$     |
|       $\mathrm{ch} x$       |        $\sum\limits_{n=0}^\infty \frac{x^{2n}}{2n!}$         |
|      $\tan x$       |                  $x+\frac{1}{3}x^3+o(x^3)$                   |
|     $\arcsin x$     |                  $x+\frac{1}{6}x^3+o(x^3)$                   |
|     $\arctan x$     |    $\sum\limits_{n=0}^\infty (-1)^n\frac{x^{2n+1}}{2n+1}$    |
|        $e^x$        |          $\sum\limits_{n=0}^\infty \frac{x^n}{n!}$           |
|     $\ln (1+x)$     | $\sum\limits_{n=1}^\infty (-1)^{n+1} \frac{x^n}{n}, -1 < x \le 1$ |
|    $-\ln (1-x)$     |       $\sum\limits_{n=1}^\infty \frac{x^n}{n}, [-1,1)$       |
| $\frac{x}{(1-x)^2}$ |           $\sum\limits_{n=1}^\infty nx^n, (-1,1)$            |
|   $\frac{1}{1+x}$   |      $\sum\limits_{n=0}^\infty (-1)^n x^n, -1 < x < 1$       |
|   $(1+x)^\alpha$​    | $\sum\limits_{n=0}^\infty \frac{\alpha^{\underline{n}}}{n!}x^n, -1 < x < 1$​，端点视$\alpha$​ |

令 $f''_{xx} = A, f''_{yy}=B,f''_{xy}=C$​：

$$
f(x,y) = f(x_0, y_0)+(f'_x,f'_y)\left(\begin{array}{c}\Delta x\\ \Delta y\end{array}\right) + (\Delta x \:\Delta y)\left(\begin{array}{cc}A &B\\ B & C\end{array}\right)\left(\begin{array}{c}\Delta x\\ \Delta y\end{array}\right) + R_2
$$

$\left|\begin{array}{cc}A &B\\ B & C\end{array}\right|$ 正定，极小值；负定，极大值；小于 $0$ 非极值点。

**傅里叶分析**

$g(t)$为周期为$T$的周期函数。

$$
g(t) = \frac{a_0}{2}+\sum\limits_{n=1}^\infty a_n\cos 2\pi fnt + b_n\sin 2\pi fnt \\
a_n = \frac{2}{T}\int_0^T g(t)\cos 2\pi fnt \mathrm{d}t \\
b_n = \frac{2}{T}\int_0^T g(t)\sin 2\pi fnt \mathrm{d}t \\
$$

**恒等变形**

$$
 a^n-b^n = (a-b)\sum\limits_{i=0}^{n-1}a^{n-1-i}b^i \\
\sum\limits_{k=1}^n k^2 = \frac{n(n+1)(2n+1)}{6} \\
\sin\alpha \cos\beta = \frac{1}{2}(\sin(\alpha + \beta) + \sin(\alpha - \beta)) \\
\sin\alpha \sin\beta = \frac{1}{2}(\cos(\alpha - \beta) - \cos(\alpha + \beta)) \\
\cos\alpha \cos\beta = \frac{1}{2}(\cos(\alpha + \beta) + \cos(\alpha - \beta)) \\
$$

**求导**

| $f(x)$                           | $f(x)'$                                                        |
| :---------------:                | :------------------------------------------------------------: |
| $\ln\lvert\sec x + \tan x\rvert$ | $\sec x$                                                       |
| $\ln\lvert\csc x - \cot x\rvert$ | $\cot x$                                                       |

**积分**

|       $f(x)$       |                   $\int f(x) \mathrm{d}x$                    |
| :----------------: | :----------------------------------------------------------: |
| $\sqrt{a^2 + x^2}$ | $\frac{x}{2}\sqrt{a^2+x^2}+\frac{a^2}{2}\ln (\frac{\sqrt{a^2 + x^2}}{a}+\frac{x}{a})+C$ |
|  $\sqrt{a^2-x^2}$  | $\frac{x}{2}\sqrt{a^2-x^2}+\frac{a^2}{2}\arcsin(\frac{x}{a})+C$ |
|    $\sin^2(x)$     |             $\frac{x}{2}-\frac{\sin (2x)}{4}+C$              |

**图像**

|          极坐标方程          |                                                 |
| :--------------------------: | :---------------------------------------------: |
|            心形线            |           $r=a(1-\cos \theta)(a > 0)$           |
|            玫瑰线            |             $r=a\sin 3\theta(a>0)$              |
|         阿基米德螺线         |      $r = a\theta (a > 0, \theta \ge 0)$]       |
|         伯努利双扭线         | $r^2 = a^2 \cos 2\theta, r^2 = a^2 \sin \theta$ |
|         **参数方程**         |                                                 |
|            平摆线            |     $x = r(t - \sin t); y = r(1 - \cos t)$      |
| 星型线（大圆$r$为小圆$4$倍） |         $x = r\cos^3 t; y = r\sin^3 t$          |
|         **空间平面**         |                                                 |
|            马鞍面            |                     $z=xy$                      |
|            抛物面            |                   $z=x^2+y^2$                   |
|            圆锥面            |               $z=\sqrt{x^2+y^2}$                |

**微分方程**

|                        原式                         |         代换         |                       化简                       |
| :-------------------------------------------------: | :------------------: | :----------------------------------------------: |
|                 $y'+p(x)y=y^nq(x)$                  |     $z=y^{1-n}$      |           $\frac{1}{1-n}z'+p(x)z=q(x)$           |
|                    $y''=f(y,y')$                    |        $y'=p$        |    $p\frac{\mathrm{d}p}{\mathrm{d}y}=f(y,p)$     |
|            $y''+py'+q=f(x)e^{\alpha x}$             | $y=R(x)e^{\alpha x}$ | $R''+R'(2\alpha + p)+(\alpha^2+p\alpha+q)R=f(x)$ |
| $x^ny^{(n)}+p_1x^{n-1}y^{(n-1)}+\cdots +p_nxy=f(x)$ |       $x=e^t$        |           $x^iy^{(i)}=D(D-1)(D-i+1)y$​            |

**空间几何**

方程组曲线的切向量：

$$
\begin{cases}
F(x,y,z)=0\\
G(x,y,z)=0
\end{cases}\Rightarrow
\tau = \left|\begin{array}{ccc}
\boldsymbol{i} &\boldsymbol{j} &\boldsymbol{k}\\
F'_x &F'_y &F'_z\\
G'_x &G'_y &G'_z
\end{array}\right|
$$

点 $P_0(x_0,y_0,z_0)$ 到平面 $Ax+By+Cz+D=0$ 的距离为：

$$
\frac{\left| Ax_0 + By_0 + Cz_0 + D\right|}{\sqrt{A^2+B^2+C^2}}
$$

向量场 $\boldsymbol{A}(x,y,z)=P(x,y,z)\boldsymbol{i}+Q(x,y,z)\boldsymbol{j}+R(x,y,z)\boldsymbol{k}$ ：

$$
\mathrm{div} \boldsymbol{A}=\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}\\
\mathrm{rot} \boldsymbol{A}= \left| \begin{array}{ccc}
\boldsymbol{i} &\boldsymbol{j} &\boldsymbol{k}\\
\frac{\partial}{\partial x}&\frac{\partial}{\partial y}&\frac{\partial}{\partial z}\\
P &Q &R
\end{array} \right|
$$

向量三重积：

$$
\boldsymbol{A}\times (\boldsymbol{B}\times \boldsymbol{C})=(\boldsymbol{A}\cdot \boldsymbol{C})\boldsymbol{B}-(\boldsymbol{A}\cdot \boldsymbol{B})\boldsymbol{C}
$$

**分布**

| 分布         | 期望        | 方差          |
| :------------: | :-----------: | :-------------: |
| $B(n,p)$     | $np$        | $np(1-p)$     |
| $P(\lambda)$ | $\lambda$   | $\lambda$     |
| $G(p)$     | $1/p$​       | $(1-p)/p^2$   |
| $U(a,b)$     | $(a+b)/2$   | $(b-a)^2/12$  |
| $E(\lambda)$ | $1/\lambda$ | $1/\lambda^2$ |
| $\chi^2(n)$  | $n$         | $2n$          |
