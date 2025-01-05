
**Algorithm 3.16. Levenberg-Marquardt method**

$begin$

$k:=0; v:=2; x:=x_0$

$A:=J(x)^TJ(x); g:=J(x)^Tf(x)$

$found:=(\|g\|_\infty \leq \varepsilon_1);\mu:=\tau*max\{a_{ii}\}$

$while (not found)and(k<k_{max})$

$k:=k+1; Solve(A+\mu I)h_{lm}=-g$

$if \|h_{lm}\| \leq \varepsilon_2(\|x\|+\varepsilon_2)$

$found:=true$

$else$

$x_{new}:=x+h_{lm}$

$\varrho:=(F(x)-F(x_{new}))/(L(0)-L(h_{lm}))$

$if \varrho>0$\{step acceptable\}

$x:=x_{new}$

$A:=J(x)^TJ(x); g:=J(x)^Tf(x)$

$found:=(\|g\|_\infty \leq \varepsilon_1);$

$\mu:=\mu*max\{\frac13,1-(2\varrho-1)^3\};v:=2$

$else$

$\mu:=\mu*v; v:=2*v$

$end$

<img src="https://raw.githubusercontent.com/LesslsMore/blog-img/master/picgo/20250101105233.png" width="90%">

#### 参考文献
- K. Madsen, H. B. Nielsen, O. Tingleff, Methods for Non-Linear Least Squares Problems


