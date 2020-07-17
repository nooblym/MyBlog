# typora数学公式用法

1. 声明数学公式

   + 行内声明

     需要在设置中打开行内公式

     在一对$中间编写数学公式

     如：\$\frac{1}{2}\$显示效果为$\frac{1}{2}$

   + 块声明

     在一对$$中间编写数学公式

     如：\$\$\frac{1}{2}\$\$显示效果独占一行，效果为：​

     $$
     \frac{1}{2}
     $$

2. 上标、下标组合

   上标：底数\^指数，如：$2^x$

   下标：底数\_下标数，如：$2_x$

3. 字体大小控制

   `\displaystyle{}`函数，一个参数，将参数中的内容按原大小显示

   不加此内容，公式会缩至与文字同高。加此内容，公式会以原大小显示

   加格式之后：$\displaystyle {\frac{x+y}{y+z}}$

   加格式之前：$\frac{x+y}{y+z}$

4. 下划线符号

   `\underline{}`给参数显示加下划线

   如：$\underline{x+y}$

5. 标签

   `tag{}`

   如：$\tag{69}$

6. 上大括号

   `overbrace{公式}`

   如：$\overbrace{a+b+c}$

   还可以加上标：$\overbrace{a+b+c}^{2.0}$

7. 下大括号

   `underbrace{公式}`

   如：$a+\underbrace{b+c}_{1.0}+d$

   

8. 上位符号

   `\stacrel{上位符号}{基位符号}`

   如：$\vec{x}\stackrel{\mathrm{def}}{=}{x_1,\dots,x_n}$

9. 占位符

   quad空格

   `\quad`

   如：$x\quad y$

   两个quad空格

   `\qquad`

   如：$x\qquad y$

   大空格

   `\`

   $x \ y$

   中空格

   `\:`

   $x \: y$

   小空格

   `\,`

   $x \, y$

   贴近

   `\!`

   $x \! y$

10. 括号

    小括号

    `\big{(}左括号，\big{)}右括号，使用：\big(式子\big)`

    如：$\big(a+b\big)$

    中括号

    `\left[式子\right]`

    如：$\left[ abc \right]$

    大括号(花括号)

    `\{算式\}`

    如：$\{x + y\}$

    自适应括号

    `\left(算式 \right)`

    $\left(xyz\right)$

11. 四则运算

    加

    $x+y=z$

    减

    $x-y=z$

    加减运算

    `\pm`

    $x \pm y = z$

    乘

    ​	叉乘

    ​	`\times`

    ​	$x \times y = z$

    ​	点乘

    ​	`\cdot`

    ​	$x \cdot y = z$

    除

    ​	除号

    ​	`\div`

    ​	$x \div y = z$

    ​	斜杠除

    ​	$x / y = z$

    分式

    `\frac{分子}{分母}或{分子}\over{分母}`

    $\frac{x+y}{y+z}$ 

    ${x+y}\over{y+z}$

12. 绝对值

    $y = |x|$

13. 平均数

    `\overline{算式}`

    $\overline{xyz}$

14. 开方

    开平方

    `\sqrt{开项式}`

    $\sqrt x$

    开多次方

    `\sqrt[开方数]{被开方数}`

    $\sqrt[3]{x+y}$

15. 对数

    `\log{真数}`

    $\log{x}$

    可以使用下标添加底

    $\log_a{x}$

16. 极限

    `\lim`

    `\displaystyle \lim`

    `\to`趋向符号、箭头

    `\infty`无穷符号

    $\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$

     $\displaystyle \lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$

17. 求和

    `\sum`

    $\sum^{x \to -\infty}_{y \to 0}{\frac{x}{y}}$ 

    $\displaystyle \sum^{x \to -\infty}_{y \to 0}{\frac{x}{y}}$

18. 积分

    `\int`

    $\int^{\infty}_{0}{xdx}$

     $\displaystyle \int^{\infty}_{0}{xdx}$

19. 微分

    `\partial`微分符号

    $\frac{\partial x}{\partial y}$ 

    $\displaystyle \frac{\partial x}{\partial y}$

20. 逻辑运算

    大于：$x+y>z$

    大于等于：`\geq`如：$x+y \geq z$

    小于：$x+y<z$

    小于等于：`\leq`如：$x+y \leq z$

    等于：$x+y=z$

    不等于：`\neq`如：$x \neq y$

    不大于等于：`$x \neq y$`或`\not\geq`如：$x \ngeq y$ ，$x \not\geq y$

    不小于等于：`\nleq`或`\not\leq`如：$x \nleq y$ ，$x \not\leq y$

    约等于：`\approx`如：$\frac{1}{3} \approx 0.3$ ，$\displaystyle \frac{1}{3} \approx 0.3$

    恒等于：`\equiv`如：$x + y \equiv z$

21. 集合运算

    属于：`\in`如：$x \in A$

    不属于：`\notin`或`\not\in`如：$x \notin A, y \not \in B$

    子集：`\subset`如：$A \subset B$

    非子集：`\not\subset`如：$A \not\subset B$

    真子集：`\subseteq`如：$A \subseteq B$

    非真子集：`\subsetneq`如：$A \subsetneq B$

    交集：`\cap`如：$A \cap B$

    并集：`\cup`如：$A \cup B$

    差集：`\setminus`如：$A \setminus B$

    同或运算：`\bigodot`如：$A \bigodot B$

    同与运算：`\bigotimes`如：$A \bigotimes B$

    常用数集：

    `\mathbb{大写数集字母}`

    + 实数集$\mathbb{R}$
    + 自然数集$\mathbb{N}$
    + 正整数集$\mathbb{N^* N_+}$
    + 整数集$\mathbb{Z}$
    + 有理数集$\mathbb{Q}$

    空集：

    `\empty`或`\emptyset`

    $\emptyset$

22. 数学符号

    去穷`\infty`如：$\infty$

    向量符号`\vec{字母}`如：$\vec{AC} = \vec{AB} + \vec{BC}$

    导数

    ​	一阶导数：`\dot{a}`如：$\dot{a}$

    ​	二阶导数：`\ddot{a}`如：$\ddot{a}$

    ​	三阶导数：`\dddot{a}`如：$\dddot{a}$

    ​	以此类推：``如：

    箭头

    ​	上箭头`\uparrow`如：$\uparrow$

    ​	双线上箭头`\Uparrow`如：$\Uparrow$

    ​	下箭头`\downarrow`如：$\downarrow$

    ​	双线下箭头`\Downarrow`如：$\Downarrow$

    ​	左箭头`\leftarrow`如：$\leftarrow$

    ​	双线左箭头`\Leftarrow`如：$\Leftarrow$

    ​	右箭头`\rightarrow`如：$\rightarrow$

    ​	双线右箭头`\Rightarrow`如：$\Rightarrow$

    ​	左右双实线箭头`\Leftrightarrow`如：$\Leftrightarrow$

23. 希腊字母

    | 大写字母 |    效果    |    实现    | 小写字母 |    效果    |    实现    |
    | :------: | :--------: | :--------: | :------: | :--------: | :--------: |
    |    A     |  $\Alpha$  |  `\Alpha`  |    α     |  $\alpha$  |  `\alpha`  |
    |    B     |  $\Beta$   |  `\Beta`   |    β     |  $\beta$   |  `\beta`   |
    |    Γ     |  $\Gamma$  |  `\Gamma`  |    γ     |  $\gamma$  |  `\gamma`  |
    |    Δ     |  $\Delta$  |  `\Delta`  |    δ     |  $\delta$  |  `\delta`  |
    |    Ε     | $\Epsilon$ | `\Epsilon` |    ε     | $\epsilon$ | `\epsilon` |
    |    Ζ     |  $\Zeta$   |  `\Zeta`   |    ζ     |  $\zeta$   |  `\zeta`   |
    |    Η     |   $\Eta$   |   `\Eta`   |    η     |   $\eta$   |   `\eta`   |
    |    Θ     |  $\Theta$  |  `\Theta`  |    θ     |  $\theta$  |  `\theta`  |
    |    Ι     |  $\Iota$   |  `\Iota`   |    ι     |  $\iota$   |  `\iota`   |
    |    Κ     |  $\Kappa$  |  `\Kappa`  |    κ     |  $\kappa$  |  `\kappa`  |
    |    Λ     | $\Lambda$  | `\Lambda`  |    λ     | $\lambda$  | `\lambda`  |
    |    Μ     |   $\Mu$    |   `\Mu`    |    μ     |   $\mu$    |   `\mu`    |
    |    Ν     |   $\Nu$    |   `\Nu`    |    ν     |   $\nu$    |   `\nu`    |
    |    Ξ     |   $\Xi$    |   `\Xi`    |    ξ     |   $\xi$    |   `\xi`    |
    |    Ο     | $\Omicron$ | `\Omicron` |    ο     | $\omicron$ | `\omicron` |
    |    Π     |   $\Pi $   |   `\Pi`    |    π     |   $\pi$    |   `\pi`    |
    |    Ρ     |   $\Rho$   |   `\Rho`   |    ρ     |   $\rho$   |   `\rho`   |
    |    Σ     |  $\Sigma$  |  `\Sigma`  |    σ     |  $\sigma$  |  `\sigma`  |
    |    Τ     |   $\Tau$   |   `\Tau`   |    τ     |   $\tau$   |   `\tau`   |
    |    Υ     | $\Upsilon$ | `\Upsilon` |    υ     | $\upsilon$ | `\upsilon` |
    |    Φ     |   $\Phi$   |   `\Phi`   |    φ     |   $\phi$   |   `\phi`   |
    |    Χ     |   $\Chi$   |   `\Chi`   |    χ     |   $\chi$   |   `\chi`   |
    |    Ψ     |   $\Psi$   |   `\Psi`   |    ψ     |   $\psi$   |   `\psi`   |
    |    Ω     |  $\Omega$  |  `\Omega`  |    ω     |  $\omega$  |  `\omega`  |

