## 2.1 频率混叠现象。
![频谱混叠](频谱混叠.png)
采样信号各频谱分量的互相混叠，称为频谱混叠现象。
理想采样信号在以下两种情况下会发生频率混叠：
1. 当连续信号的频谱带宽<font color=#FF0000>有限时</font>，即 $\omega<w_{max}$ 时，如果此时采样频谱太低（如 $\omega_s<2\omega_{max}$ ），则采样信号的各个周期分量将会相互交叠。
2. 连续信号的频谱是<font color=#FF0000>无限带宽</font>，此时无论怎样提高采样频率，频谱混叠或多或少都会发生。
## 2.2 简述香农采样定理。
如果一个连续信号不包含高于频率 $\omega_{max}$ 的频率分量，那么完全可以用周期 $T<\pi/\omega_{max}$ 的均匀采样值来描述。或者说，如果采样频率 $\omega_s>2\omega_{max}$，那么就可以从采样信号中不失真地恢复原连续信号。
香农采样定理给出了<font color=#FF0000>采样周期的上限</font>。
## 2.3 DA转换器有哪些主要芯片。字长如何选择。
常用8位DA转换芯片DAC0832。
对于DA转换器字长的选择，可以由计算机控制系统中DA转换器后面的执行机构的动态范围来选定。设执行机构的最大输入为 $u_{max}$ ，执行机构的死区电压为 $u_R$，DA转换器字长为 $n$ ，则计算机控制系统的最小输出单位应小于执行机构的死区，即：
$$\frac{u_{max}}{2^n-1}\le u_R$$
所以
$$n\ge \lg(u_{max}/u_R+1)/\lg2$$
## 2.4 DA输出通道的实现方式。
![单极性输出](单极性输出.png)
运算放大器起反相比例求和的作用，可以实现DA单极性输出。此时，$V_{OUT1}$、 $V_{REF}$、 $D_7\sims D_0 (D)$ 的关系为：
$$V_{OUT1}=-V_{REF}D/2^n$$
![双极性输出](双极性输出.png)
$V_{REF}$ 经电阻 $R_1$ 向运算放大器 $A_2$ 提供一个偏流 $I_1$ ，其电流与 $I_2$ 相反，正好使运算放大器 $A_2$ 的输出在运算放大器 $A_1$ 的基础上向上偏移 $0.5V_{REF}$。此时，$V_{OUT2}$ 、 $V_{REF}$ 、 $D_7\sims D_0 (D)$ 的关系为：
$$V_{OUT2}=-(\frac{R_3}{R_1}V_{REF}+\frac{R_3}{R_2}V_{OUT1})=\frac{1}{2}V_{REF}(\frac{D}{2^{n-1}}-1)$$
## 2.5 AD转换器有哪些主要芯片。字长如何选择。
8位8通道AD转换芯片ADC0809、12位逐次逼近式AD转换芯片AD574A。根据输入模拟信号的动态范围可以选择AD转换器的位数。设AD转换器的位数为 $n$ ，模拟输入信号的最大值 $u_{max}$ 为AD转换器的满刻度，则模拟输入信号的最小值 $u_{min}$ 应大于或等于AD转换器的最低有效位。即有：
$$\frac{u_{max}}{2^n-1}\le u_{min}$$
所以
$$n\ge \lg(u_{max}/u_{min}+1)/\lg2$$
## 2.6 AD转换器输入通道的实现方式。
![ADC0809功能框图](ADC0809功能框图.png)
AD输入信号可以有单极性和双极性两种形式。通过对参考电压的不同连接，可以构成不同的模拟量输入电路。AD转换器的输入电压 $V_{in}$ ，位数 $n$ ，参考电压 $V_{REF(+)}$ ， $V_{REF(-)}$ 的关系为：
$$D=\frac{V_{in}-V_{REF(-)}}{V_{REF(+)}-V_{REF(-)}}\times 2^n$$
## 2.7 AD转换时间的含义及其与AD转换速率和位数的关系。
设AD转换器已经处于就绪的状态，从AD转换的启动信号加入时起，到获得数字输出信号为止所需的时间称为AD转换时间，该时间的倒数称为AD转换速率。AD转换速率与AD的位数有关，一般来说，AD的位数越大，则相应的转换速率就越慢。
## 2.8 写出 $f(t)$ 的 $z$ 变换的多种表达方式。
$$Z[f(t)]=Z[f^*(t)]=F(z)=\sum_{k=0}^{\inf}f(kT)z_{-k}$$
## 2.9 证明下列关系
### (1) $Z[a^k]=\frac{1}{1-az_{-1}}$
$$Z[a^k]=F(z)=\sum_{k=0}^{\infty}a^kz^{-k}=\sum_{k=0}^{\infty}(az^{-1})^k=\frac{1-(az^{-1})^{\infty}}{1-az^{-1}}=\frac{1}{1-az^{-1}}$$
### (2) $Z[a^kf(t)]=f(\frac{z}{a})$
$$Z[a^kf(t)]=\sum_{k=0}^{\infty}a^kf(kT)z^{-k}=\sum_{k=0}^{\infty}f(kT)(\frac{z}{a})^{-k}\stackrel{变量代换}{\longrightarrow}F(\frac{z}{a})$$
### (3) $Z[tf(t)]=-Tz\frac{\mathrm d}{\mathrm dt}F(z)$
$$F(z)=Z[f(t)]=\sum_{k=0}^{\infty}f(kT)z^{-k}$$
$$\downarrow 两边求导$$
$$\frac{\mathrm d}{\mathrm dt}F(z)=\sum_{k=0}^{\infty}-kf(kT)z^{-k-1}$$
$$\downarrow 两边同乘-Tz$$
$$-Tz\frac{\mathrm d}{\mathrm dt}F(z)=\sum_{k=0}^{\infty}kTf(kT)z^{-k}=Z[tf(t)]$$
### (4) $Z[t^2]=\frac{T^2z^{-1}(1+z^{-1})}{(1-z^{-1})^3}$
$$T^2z(\frac{\mathrm d}{\mathrm dz}Z[1(t)]+z\frac{\mathrm d^2}{\mathrm dz^2}Z[1(t)])=\sum_{k=0}^{\infty}k^2T^2z^{-k}=Z[t^2]$$
$$\downarrow$$
$$Z[t^2]=\frac{T^2z^{-1}(1+z^{-1})}{(1-z^{-1})^3}$$
### (5) $Z[te^{-at}]=\frac{Te^{-aT}z^{-1}}{(1-e^{-aT}z^{-1})^2}$
$$Z[e^{-at}]=\sum_{k=0}^{\infty}e^{-akT}z^{-k}=\sum_{k=0}^{\infty}(e^{aT}z)^{-k}\stackrel{变量代换}{\longrightarrow}\frac{1}{1-e^{-aT}z^{-1}}$$
由问题（3）可知
$$Z[te^{-at}]=\frac{Te^{-aT}z^{-1}}{(1-e^{-aT}z^{-1})^2}$$
### (6) $Z[a^tf(t)]=F(a^{-T}z)$
$$Z[a^tf(t)]=\sum_{k=0}^{\infty}f(t)(a^{-T}z)^{-k}\stackrel{变量代换}{\longrightarrow}F(a^{-T}z)$$
## 2.10 Z变换的线性定理
$$Z[f_1(t)]=F_1(z), Z[f_2(t)]=F_2(z)$$
$$\downarrow f(t)=af_1(t)\pm bf_2(t)$$
$$F(z)=aF_1(z)\pm bF_2(z)$$
证明：
$$F(z)=\sum_{k=0}^{\infty}[af_1(kT)\pm bf_2(kT)]z^{-k}=aF_1(z)\pm bF_2(z)$$
## 2.11 Z变换的滞后定理
如果$f(t)=0, t\le 0$，则：
$$Z[f(t-nT)]=z^{-n}F(z)$$
$F(z)$ 经过一个 $z^{-n}$ 的纯滞后环节，相当于其时间特性向后移动 $n$ 步。通常在起始点之前，$f(t)=0$ 都可以成立（线性时不变要求）。
证明：
$$Z[f(t-nT)]=\sum_{k=0}^{\infty}f(kT-nT)z^{-k}=z{-n}\sum_{k=0}^{\infty}f(kT-nT)z^{-(k-n)}\stackrel{变量代换k-n=m}{\longrightarrow} z^{-n}\sum_{m=-n}^{\infty}f(mT)z^{-m}$$
$$\downarrow$$
$$Z[f(t-nT)]=z^{-n}\sum_{m=0}^{\infty}f(mT)z^{-m}=z^{-n}F(z)$$
## 2.12 Z变换的超前定理
$$Z[f(t+nT)]=z^{n}F(z)-z^n\sum_{j=0}^{n-1}f(jT)z^{-1}$$
证明：
$$Z[f(t+nT)]=\sum_{k=0}^{\infty}f(kT+nT)z^{-k}=z^n\sum_{k=0}^{\infty}f(kT+nT)z^{-(k+n)}$$
$$\downarrow 变量代换k+n=r$$
$$Z[f(t+nT)]=z^{n}\sum_{r=n}^{\infty}f(rT)z^{-r}=z^n[\sum_{r=0}^{\infty}f(rT)z^{-r}-\sum_{r=0}^{n-1}f(rT)z^{-r}]$$
$$=z^n[F(z)-\sum_{j=0}^{n-1}f(jT)z^{-j}]$$
## 2.13 Z变换初值定理
$$f(0)=\lim_{z\rightarrow\infty}F(z)$$
利用初值定理检查 $z$ 变换的结果非常方便。
证明：
$$F(z)=\sum_{k=0}^{\infty}f(kT)z^{-k}=f(0T)+f(1T)z^{-1}+f(2T)z^{-2}+\cdots$$
$$\downarrow 两边同取 z\rightarrow \infty$$
$$\lim_{z\rightarrow \infty}F(z)=f(0)=\lim_{k\rightarrow 0}f(kT)$$
## 2.14 Z变换终值定理
如果 $f(t)$ 的 $z$ 变换为 $F(z)$ ，而 $1-z^{-1}$ 在 $F(z)$ 在 $z$ 平面以原点为圆心的单位圆上或圆外，没有极点，则
$$\lim_{t\rightarrow \infty}f(t)=\lim_{k\rightarrow \infty}f(kT)=lim_{z\rightarrow 1}F(z)=\lim_{z\rightarrow 1}\frac{(z-1)}{z}F(z)$$
证明：
