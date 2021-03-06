# 離散フーリエ変換

- 与えられた数列は${1,2,5,8,4,10,1,…}$
- 与えられた数列は以下の表のECA(Rule90)によって得られている
  - ここでは1から始まり1に戻る周期性を持っている
  - 周期性はセル幅が$2^n (n>0)$の時に得られ、$2^{(n+1)}-2$回の計算で初期値と同じ値になる
    - 例）以下の表では$n=2$なのでセル幅は4、周期は$2^3-2=6$となる

|10進数|セル0|セル1|セル2|セル3|
|  --:|  --:| --:| --:| --:|
|    1|    0|   0|   0|   1|
|    2|    0|   0|   1|   0|
|    5|    0|   1|   0|   1|
|    8|    1|   0|   0|   0|
|    4|    0|   1|   0|   0|
|   10|    1|   0|   1|   0|
|    1|    0|   0|   0|   1|

## 計算

$X$は離散周波数スペクトル密度

$T_0$の単位は秒．観測開始0秒から$T_0$秒までを観測したということ

$x$は$0\sim T_0$秒までに等間隔$$\Delta t$$秒で得られた$N$個の離散的な数値列

$W_n$は$$W_N=e^{-i\frac{2\pi}{N}}$$，つまり$$W_n=\cos\left(\frac{2\pi}{N}\right)-i\sin\left(\frac{2\pi}{N}\right)$$で得られる
$$
\begin{align*}
\begin{pmatrix} 
X_0 \\
X_1 \\
X_2 \\
X_3 \\
X_4 \\
X_5 \\
\end{pmatrix}
&=
\frac{T_0}{6}
\begin{pmatrix} 
W_6^0 & W_6^0 & W_6^0    & W_6^0    & W_6^0    & W_6^0    \\
W_6^0 & W_6^1 & W_6^2    & W_6^3    & W_6^4    & W_6^5    \\
W_6^0 & W_6^2 & W_6^4    & W_6^6    & W_6^8    & W_6^{10} \\
W_6^0 & W_6^3 & W_6^6    & W_6^9    & W_6^{12} & W_6^{15} \\
W_6^0 & W_6^4 & W_6^8    & W_6^{12} & W_6^{16} & W_6^{20} \\
W_6^0 & W_6^5 & W_6^{10} & W_6^{15} & W_6^{20} & W_6^{25} \\
\end{pmatrix}
\begin{pmatrix} 
x_0 \\
x_1 \\
x_2 \\
x_3 \\
x_4 \\
x_5 \\
\end{pmatrix}\\
&=
\frac{1}{6}
\begin{pmatrix} 
W_6^0 & W_6^0 & W_6^0 & W_6^0 & W_6^0 & W_6^0 \\
W_6^0 & W_6^1 & W_6^2 & W_6^3 & W_6^4 & W_6^5 \\
W_6^0 & W_6^2 & W_6^4 & W_6^0 & W_6^2 & W_6^4 \\
W_6^0 & W_6^3 & W_6^0 & W_6^3 & W_6^0 & W_6^3 \\
W_6^0 & W_6^4 & W_6^2 & W_6^0 & W_6^4 & W_6^2 \\
W_6^0 & W_6^5 & W_6^4 & W_6^3 & W_6^2 & W_6^1 \\
\end{pmatrix}
\begin{pmatrix} 
1  \\
2  \\
5  \\
8  \\
4  \\
10 \\
\end{pmatrix}
\end{align*}
$$

$W_6$について求める
$$
\begin{align*}
W_6 &= e^{-i\frac{2\pi}{6}}\\
    &= \frac{1}{2}\left(1-i\sqrt{3}\right)
\end{align*}
$$

$W_6^0 \sim W_6^5$の値は下記の計算によって得られる．
$$
\begin{align*}
W_n^0 &= \left(\frac{1}{2}\left(1-i\sqrt{3}\right)\right)^0 \\
      &= 1 \\
\end{align*}
$$
$$
\begin{align*}
W_n^1 &= \left(\frac{1}{2}\left(1-i\sqrt{3}\right)\right)^1 \\
      &= \frac{1}{2}\left(1-i\sqrt{3}\right) \\
\end{align*}
$$
$$
\begin{align*}
W_n^2 &= \left(\frac{1}{2}\left(1-i\sqrt{3}\right)\right)^2 \\
      &= \frac{1}{4}\left(1-2i\sqrt{3}-3\right) \\
      &= -\frac{1}{2}\left(1+i\sqrt{3}\right) \\
\end{align*}
$$
$$
\begin{align*}
W_n^3 &= \left(\frac{1}{2}\left(1-i\sqrt{3}\right)\right)^3 \\
      &= \frac{1}{8}\left(1-3i\sqrt{3}-9+3i\sqrt{3}\right) \\
      &= -1 \\
\end{align*}
$$
$$
\begin{align*}
W_n^4 &= \left(\frac{1}{2}\left(1-i\sqrt{3}\right)\right)^4 \\
      &= \left(\frac{1}{2}\right)^4\left(1-i\sqrt{3}\right)^4 \\
      &= \frac{1}{16}\left(1-2i\sqrt{3}-3\right)^2 \\
      &= \frac{1}{16}\left(-2-2i\sqrt{3}\right)^2 \\
      &= \frac{1}{16}\left(4+8i\sqrt{3}-12\right) \\
      &= \frac{1}{16}\left(-8+8i\sqrt{3}\right) \\
      &= -\frac{1}{2}\left(1-i\sqrt{3}\right) \\
\end{align*}
$$
$$
\begin{align*}
W_n^5 &= \left(\frac{1}{2}\left(1-i\sqrt{3}\right)\right)^5 \\
      &= \frac{1}{32}\left(1-i\sqrt{3}\right)\left(1-i\sqrt{3}\right)^4 \\
      &= \frac{1}{32}\left(1-i\sqrt{3}\right)\left(1-2i\sqrt{3}-3\right)^2 \\
      &= \frac{1}{32}\left(1-i\sqrt{3}\right)\left(-2-2i\sqrt{3}\right)^2 \\
      &= \frac{1}{32}\left(1-i\sqrt{3}\right)\left(4+8i\sqrt{3}-12\right) \\
      &= \frac{1}{32}\left(1-i\sqrt{3}\right)\left(-8+8i\sqrt{3}\right) \\
      &= \frac{1}{32}\left(-8+8i\sqrt{3}+8i\sqrt{3}+24\right) \\
      &= \frac{1}{32}\left(16+16i\sqrt{3}\right) \\
      &= \frac{1}{2}\left(1+i\sqrt{3}\right) \\
\end{align*}
$$
結果をまとめると以下のように得られた．
$$
\begin{align*}
W_n^0 &= 1 \\
W_n^1 &= \frac{1}{2}\left(1-i\sqrt{3}\right) \\
W_n^2 &= -\frac{1}{2}\left(1+i\sqrt{3}\right) \\
W_n^3 &= -1 \\
W_n^4 &= -\frac{1}{2}\left(1-i\sqrt{3}\right) \\
W_n^5 &= \frac{1}{2}\left(1+i\sqrt{3}\right) \\
\end{align*}
$$
値を式に代入して計算を続ける
$$
\begin{align*}
\begin{pmatrix} 
X_0 \\
X_1 \\
X_2 \\
X_3 \\
X_4 \\
X_5 \\
\end{pmatrix}
&=
\frac{1}{6}
\begin{pmatrix} 
1 & 1 & 1 & 1 & 1 & 1 \\
1 & \frac{1}{2}\left(1-i\sqrt{3}\right) & -\frac{1}{2}\left(1+i\sqrt{3}\right) & -1 & -\frac{1}{2}\left(1-i\sqrt{3}\right) & \frac{1}{2}\left(1+i\sqrt{3}\right) \\
1 & -\frac{1}{2}\left(1+i\sqrt{3}\right) & -\frac{1}{2}\left(1-i\sqrt{3}\right) & 1 & -\frac{1}{2}\left(1+i\sqrt{3}\right) & -\frac{1}{2}\left(1-i\sqrt{3}\right) \\
1 & -1 & 1 & -1 & 1 & -1 \\
1 & -\frac{1}{2}\left(1-i\sqrt{3}\right) & -\frac{1}{2}\left(1+i\sqrt{3}\right) & 1 & -\frac{1}{2}\left(1-i\sqrt{3}\right) & -\frac{1}{2}\left(1+i\sqrt{3}\right) \\
1 & \frac{1}{2}\left(1+i\sqrt{3}\right) & -\frac{1}{2}\left(1-i\sqrt{3}\right) & -1 & -\frac{1}{2}\left(1+i\sqrt{3}\right) & \frac{1}{2}\left(1-i\sqrt{3}\right) \\
\end{pmatrix}
\begin{pmatrix} 
1  \\
2  \\
5  \\
8  \\
4  \\
10 \\
\end{pmatrix} \\
&= \frac{1}{6}
\begin{pmatrix} 
1 +2 +5 +8 +4 +10 \\
1 +(1 -i\sqrt{3}) -\frac{5}{2}(1+i\sqrt{3}) -8 -2(1-i\sqrt{3}) +5(1+i\sqrt{3}) \\
1 -(1 +i\sqrt{3}) -\frac{5}{2}(1-i\sqrt{3}) +8 -2(1+i\sqrt{3}) -5(1-i\sqrt{3}) \\
1 -2 +5 -8 +4 -10 \\
1 -(1 -i\sqrt{3}) -\frac{5}{2}(1+i\sqrt{3}) +8 -2(1-i\sqrt{3}) -5(1+i\sqrt{3}) \\
1 +(1 +i\sqrt{3}) -\frac{5}{2}(1-i\sqrt{3}) -8 -2(1+i\sqrt{3}) +5(1-i\sqrt{3}) \\
\end{pmatrix} \\
&= \frac{1}{6}
\begin{pmatrix}
30 \\
\frac{1}{2}(-11 +7i\sqrt{3}) \\
\frac{3}{2}(-1 +3i\sqrt{3}) \\
-10 \\
-\frac{3}{2}(1 +3i\sqrt{3}) \\
-\frac{1}{2}(11 -7i\sqrt{3}) \\
\end{pmatrix} 
= \begin{pmatrix}
5 \\
-\frac{1}{12}(11 -7i\sqrt{3}) \\
-\frac{1}{4}(1 -3i\sqrt{3}) \\
-\frac{5}{3} \\
-\frac{1}{4}(1 +3i\sqrt{3}) \\
-\frac{1}{12}(11 -7i\sqrt{3}) \\
\end{pmatrix}
= \begin{pmatrix}
5 \\
-\frac{11}{12} +\frac{7}{12}i\sqrt{3} \\
-\frac{1}{4} +\frac{3}{4}i\sqrt{3} \\
-\frac{5}{3} \\
-\frac{1}{4} -\frac{3}{4}i\sqrt{3} \\
-\frac{11}{12} +\frac{7}{12}i\sqrt{3} \\
\end{pmatrix}
\end{align*}
$$


周波数$k \Delta f$[$Hz$]（ここでは-2,-1,0,1,2,3）で解を書き直すと以下のようになる．
$$
\begin{pmatrix} 
X_0 \\
X_1 \\
X_2 \\
X_3 \\
X_4 \\
X_5 \\
\end{pmatrix}
=
\begin{pmatrix} 
X_0 \\
X_1 \\
X_2 \\
X_3 \\
X_{-2} \\
X_{-1} \\
\end{pmatrix}
=
\begin{pmatrix}
5 \\
-\frac{11}{12} +\frac{7}{12}i\sqrt{3} \\
-\frac{1}{4} +\frac{3}{4}i\sqrt{3} \\
-\frac{5}{3} \\
-\frac{1}{4} -\frac{3}{4}i\sqrt{3} \\
-\frac{11}{12} +\frac{7}{12}i\sqrt{3} \\
\end{pmatrix}
$$
得られたりさん周波数スペクトル密度から元の連続的な波$x(t)$を三角関数で近似した関数を求めるには以下の式を用いる．$Re$は実部，$Im$は虚部を表している．
$$
\begin{align*}
x(t) &\approx \frac{a_0}{2}+\sum_{k=1}^{N/2}\left(a_k\cos\left(t\frac{2k\pi}{T_0}\right)+b_k\sin\left(t\frac{2k\pi}{T_0}\right)\right) \\
a_k &= ReX_{T_0} (k\Delta f) + ReX_{T_0}(-k\Delta f) \\
b_k &= -ImX_{T_0} (k\Delta f) + ImX_{T_0}(-k\Delta f) \\
\end{align*}
$$
これを元に近似した関数を求める．
$$
\begin{align*}
a_0 &= 5 \\
a_1 &= -\frac{11}{12} -\frac{11}{12} = -\frac{11}{6} \\
a_2 &= -\frac{1}{4} -\frac{1}{4} = -\frac{1}{2} \\
a_3 &= -\frac{5}{3} \\
b_1 &= -\frac{7}{12}i\sqrt{3} + \frac{7}{12}i\sqrt{3} = 0 \\
b_2 &= -\frac{3}{4}i\sqrt{3} -\frac{3}{4}i\sqrt{3} = -\frac{3}{2}i\sqrt{3}\\
b_3 &= 0
\end{align*}
$$

$$
\begin{align*}
x(t) \approx& \frac{a_0}{2} +\sum_{k=1}^{3}\left(a_k\cos\left(2\pi t(k\Delta f)\right) +b_k\sin\left(2\pi t(k\Delta f)\right)\right) \\
=& \frac{a_0}{2} +a_1 \cos{2\pi t} +a_2 \cos{4\pi t} +a_3\cos{6\pi t} \\
&+ b_1 \cos{2\pi t} +b_2 \cos{4\pi t} +b_3\cos{6\pi t} \\
=& \frac{5}{2} -\frac{11}{6}\cos{2\pi t} -\frac{1}{2}\cos{4\pi t} -\frac{5}{3}\cos{6\pi t} \\
&+ 0 \cdot \cos{2\pi t} -\frac{3}{2}i\sqrt{3} \cos{4\pi t} +0 \cdot \cos{6\pi t} \\
=& \frac{5}{2} -\frac{11}{6}\cos{2\pi t} -\frac{1}{2}\cos{4\pi t} -\frac{5}{3}\cos{6\pi t} -\frac{3}{2}i\sqrt{3} \cos{4\pi t}\\
\end{align*}
$$

