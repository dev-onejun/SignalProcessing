<!--
Since the content becomes bigger, the rendering time of the markdown page increases so that I decided to divide the paper into each chapter. These papers will be combined after the semester is finished.
-->

$$
\text{Acronym & Abbreviation} \\
\begin{array}{|c|c|}
\hline
\text{Finite Impulse Response (FIR)} & \text{Digital Signal Processing (DSP)} \\
\hline
\text{Very Large Scale Integration (VLSI)} & \text{Linear Time-Invariant (LTI)} \\
\hline
\text{} & \text{} \\
\hline
\text{} & \text{} \\
\hline
\end{array}
$$

##### Keywords

* Low-pass filter : A filter which passes low frequency component from the given threshold.
* VLSI : A circuit, designed with micro processors and memories.
* Stem Plot [[1](#mjx-eqn-1), [2](#mjx-eqn-2)]: A plot. drawn as the time x-axis and the value y-axis.
* window: The length of some input $x[n]$ to compute the output $y[n]$.

### Chapter 5. FIR Filters

Signal Processing operates with computers on input $x[n]$ to get output $y[n]$. The computers analyze the $x[n]$ with both the time and the frequency domain. For example, Pointwise operation filter like $y[n] = (x[n])^2$ and Running Average filter are available.

Running Average Filter (Moving Average Filter ? [[3](#mjx-eqn-3)]) calculates its output $y[n]$ as the average of three consecutive input $x[n]$ values. Stem plot represents $x[n]$ which is a list of numbers, referring the discrete time signal. The non-zero interval where the $x[n]$ has value is called Support. If $x[n]$ has values only between 0 and 4, its Support is called Finite Support.

3-Point Average System (Running Average Filter ?) adds three consecutive numbers and divides it into three. Firstly, the system which used one present value and two future values has three features: **1)** The highest frequency of $x[n]$ is smoothed which acts as a low-pass filter. **2)** The peak point is shifted to the left (to the past). **3)** The length of Finite Support of $y[n]$ increases. For instance, if the Finite Support of $x[n]$ was from 0 to 4, the $y[n]$ Finite Support becomes 7. Secondly, in contrast to using future values, past values and a present value are utilized in 3-point Average System if $n$ importantly represents real-time. This system, also called Causal System, is contrasted with the system with future values only in the shifted direction. The peak point is shifted to the right (to the future).

General FIR Filter formula is shown as the following.
$$
y[n] = \sum_{k=0}^M b_k x[n-k]
$$
For example, if $b_k = \{3, -1, 2, 1\}$ then $y[n] = \sum_{k=0}^3 b_k x[n-k] = 3x[n] - x[n-1] + 2x[n-2] + x[n-3]$. For the case of the latter 3-point Average System, $M$ is 2 and $b_k$ is {$1 \over 3$, $1 \over 3$, $1 \over 3$}. Important that Filter Order $M$ is differ from Filter Length $L = M + 1$. Furthermore, like the 3-point Average System, the length of Support in $y[n]$ is longer than input $x[n]$. Specifically, if input length was $N$, output length becomes $N+M$. (Imagine that 3-point Average (M=2) length is from 5 to 7)

Unit-Impulse function $\delta[n]$ is the special input signal which has only one non-zero value when $n = 0$. The function represents any discrete signals with shifting and scaling its function like $\delta[n-3]$ and $4\delta[n]$. In other words,
$$
x[n] = \sum_{k=-\infty}^{\infty} x[k] \delta[n-k]
$$
Furthermore, when the input $x[n]$ is the unit impulse signal $\delta[n]$, the output $y[n]$ is called Impulse Response $h[n]$. Interestingly, $h[n]$ has exactly same values with $b_k$, the filter coefficients so that the general FIR filter formula is rewritten as
$$
y[n] = \sum_{k=0}^M h[k] x[n-k]
$$
which is called a finite convolution sum.

Usually, a star (*) represents the convolution operator for $-\infty < n < \infty$ by writing $y[n] = h[n] * x[n]$, reading the formula as "the output sequence y[n] is obtained by convolving the impulse response h[n] with the input sequence x[n]".

<!-- So, all the sampling signals can be addressed as a unit impulse signal so that their outputs are all called Impulse Response ??? -->

Comparing two kinds of point average systems shows its effect clearly. When the input $x[n]$ has its period 8, while 7-point Average System removes the cosine function as making the difference between max and min smaller, 3-point Average System still presents its period obviously, smoothing both the start and the end slightly. In other words, the more the number of the point is close to the period, the more the periodic of the signal is disappear.

LTI systems have three features: **1)** Time-Invariance, **2)** Linearity, and **3)** Causality. **Time-Invarianc** means tha the output sequence $w[n]$ is definitive regardless of the time shifting whether the its position is before the system or after the system. **Linearity** refers to both two properties, scaling and superposition. Similar with Time-Invariance, regardless of the position of scaling and superposition, $w[n]$ is definitive.Specifically, Scaling is presented as $\{\alpha > 0, \alpha \in R \ |\ \alpha x[n] \to \alpha y[n]\}$ and Superposition is represented as $\text{When } x_1[n] \to y_1[n] \text{ and } x_2[n] \to y_2[n] \text{ are given, } x_1[n] + x_2[n] \to y_1[n] + y_2[n] \text{ is satisfied}$. Causality is achieved by using present and past values except future values.

In conclusion, LTI systems meet the following compound proposition; "The system is linear" $\equiv$ "If $x_1[n] \to y_1[n]$ and $x_2[n] \to y_2[n]$, then $\alpha x_1[n] + \beta x_2[n] \to \alpha y_1[n] + \beta y_2[n]$". The compound proposition is utilized to probe if the system is linear or not. For instance, $y[n] = x[n]^2$ is not linear. To probe this, let's assume that the system is linear. The scaling superposition of $x_1[n] \to x_1[n]^2$ and $x_2[n] \to x_2[n]^2$ should be same with $(\alpha x_1[n] + \beta x_2[n]) \to (\alpha x_1[n] + \beta x_2[n])^2$. However, the scaling superposition, applying scaling superpoisition after the system, is $\alpha (x_1n[n])^2 + \beta (x_2[n])^2$ so that the assumption was contradictory. Hence, the system is not linear.

---
In images, although they do not have the time axis, smoothing with 3-point Average System is able while each pixel in either horizontal or vertical direction is considered as $n$.


### References

* $\text{FIR filter - an overview, https://www.sciencedirect.com/topics/engineering/fir-filter, accessed in Apr. 5th 2024.}$

$\tag*{}\label{1} \text{[1] matplotlib.pyplot.stem, https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.stem.html, accessed in Apr. 5th 2024. [URL]}$
$\tag*{}\label{2} \text{[2] https://zephyrus1111.tistory.com/103, accessed in Apr. 5th 2024. [discouraged]}$
$\tag*{}\label{3} \text{[3] FIR Filters, https://web.njit.edu/~joelsd/Fundamentals/coursework/BME310computingcw7.pdf, New Jersey Institute of Technology, accessed in Apr. 5th 2024. [Class Materials]}$
