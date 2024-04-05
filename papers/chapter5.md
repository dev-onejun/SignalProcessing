<!--
Since the content becomes bigger, the rendering time of the markdown page increases so that I decided to divide the paper into each chapter. These papers will be combined after the semester is finished.
-->

$$
\text{Acronym & Abbreviation} \\
\begin{array}{|c|c|}
\hline
\text{Finite Impulse Response (FIR)} & \text{Digital Signal Processing (DSP)} \\
\hline
\text{Very Large Scale Integration (VLSI)} & \text{} \\
\hline
\text{} & \text{} \\
\hline
\end{array}
$$

##### Keywords

* Low-pass filter : A filter which passes low frequency component from the given threshold.
* VLSI : A circuit, designed with micro processors and memories.o
* Stem Plot [[1](#mjx-eqn-1), [2](#mjx-eqn-2)]: A plot. drawn as the time x-axis and the value y-axis.

### Chapter 5. FIR Filters

Signal Processing operates with computers on input $x[n]$ to get output $y[n]$. The computers analyze the $x[n]$ with both the time and the frequency domain. For example, Pointwise operation filter like $y[n] = (x[n])^2$ and Running Average filter are available.

Running Average Filter (Moving Average Filter ? [[3](#mjx-eqn-3)]) calculates its output $y[n]$ as the average of three consecutive input $x[n]$ values. Stem plot represents $x[n]$ which is a list of numbers, referring the discrete time signal. The non-zero interval where the $x[n]$ has value is called Support. If $x[n]$ has values only between 0 and 4, its Support is called Finite Support.

3-Point Average System (Running Average Filter ?) adds three consecutive numbers with one present value and two future values and divides it into three. As a result, the system has three features: **1)** The highest frequency of $x[n]$ is smoothed which acts as a low-pass filter. **2)** The peak point is shifted to the left (to the past). **3)** The length of Finite Support of $y[n]$ increases. For instace, if the Finite Support of $x[n]$ was from 0 to 4, the $y[n]$ Finite Support becomes 7. In contrast to using future values, past values are utilized in 3-point Average System if $n$ importantly represents real-time. This system, also called Causal System, is contrasted only in the shifted direction. The peak point is shifted to the right (to the future).

General FIR Filter is included the latter 3-point Average System.
$$
y[n] = \sum_{k=0}^M b_k x[n-k]
$$
For example, if $b_k = \{3, -1, 2, 1\}$ then $y[n] = \sum_{k=0}^3 b_k x[n-k] = 3x[n] - x[n-1] + 2x[n-2] + x[n-3]$. For the case of the latter 3-point Average System, $M$ is 2 and $b_k$ is {$1 \over 3$, $1 \over 3$, $1 \over 3$}. Important that Filter Order $M$ is differ from Filter Length $L = M + 1$. Furthermore, like the 3-point Average System, the length of Support in $y[n]$ is longer than input $x[n]$. Specifically, if input length was $N$, output length becomes $N+M$. (Imagine that 3-point Average (M=2) length is from 5 to 7)


In images, although they do not have the time axis, smoothing with 3-point Average System is able while each pixel in either horizontal or vertical direction is considered as $n$.


### References

* $\text{FIR filter - an overview, https://www.sciencedirect.com/topics/engineering/fir-filter, accessed in Apr. 5th 2024.}$

$\tag*{}\label{1} \text{[1] matplotlib.pyplot.stem, https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.stem.html, accessed in Apr. 5th 2024. [URL]}$
$\tag*{}\label{2} \text{[2] https://zephyrus1111.tistory.com/103, accessed in Apr. 5th 2024. [discouraged]}$
$\tag*{}\label{3} \text{[3] FIR Filters, https://web.njit.edu/~joelsd/Fundamentals/coursework/BME310computingcw7.pdf, New Jersey Institute of Technology, accessed in Apr. 5th 2024. [Class Materials]}$
