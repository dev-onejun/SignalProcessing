# SPAYN: Signal Processing is All You Need (A Review)

$$
\displaylines{
\mathbf{\text{Wonjun Park}} \\
\mathrm{\text{Computer Science and Engineering}} \\
\mathrm{\text{Konkuk University}} \\
\mathrm{\text{Seoul, South Korea}} \\
\mathrm{\text{kuwjjgjk at konkuk.ac.kr}}
}
$$

### *Abstract*

Translating analog information into digital is inevitable to address data in computers. Signal Processing is a way that conducts these translations. This paper reviews key concepts of this method, involving Fourier Transform, FIR, and Convolution Operation. These operations which can be applied to any digital signals such as audio, images, and videos derives CNN, the popular architecture of the neural network in AI tasks. In other words, the paper also tackles a few parts of deep learning. I expect that this work summarizes the whole concepts of Signal Processing in one paper.

$$
\displaylines{
\mathbf{\text{Acronym / Abbreviation}} \\
\begin{array}{|c|c|}
\hline
\text{Convolutional Neural Network (CNN)} & \text{Finite Impulse Response (FIR)} \\
\hline
\text{Artificial Intelligence (AI)} & \text{Electrical Engineering (EE)} \\
\hline
\text{} & \text{} \\
\hline
\end{array}
}
$$

##### *keywords*
* **Complex Numbers**: the number presented as $z = a + bj$ where $a, b$ are real numbers and $j$ is an imaginary number.
* **Trigonometric Functions**: The functions like $\sin, \cos$ and $\tan$. $\cos$ is an even function and $\sin$ is an odd function.
    * $\cos\theta = \sin{({\pi \over 2} - \theta)}$
    * $\sin\theta = \cos{({\pi \over 2} - \theta)}$
    * $\cos(\theta_1 + \theta_2) = \cos\theta_1\cos\theta_2 - \sin\theta_1\sin\theta_2$
    * $\sin(\theta_1 + \theta_2) = \sin\theta_1\cos\theta_2 + \cos\theta_1\sin\theta_2$
* **Conjugate Relationship**: If the terms of the imaginary part in two formulas are opposite as plus and minus, the two formulas are in the Conjugate Relationship [[5]](#mjx-eqn-5). The terms in the relationship is often presented as $Z$ and $Z^*$
    * e.g. $e^{j\varphi}$ and $e^{-j\varphi}$ are in the Conjugate Relatioship, because $e^{j\varphi} = \cos\varphi + j\sin\varphi$ and $e^{-j\varphi} = \cos\varphi - j\sin\varphi$. ( $\leftarrow \sin(-x) = -\sin(x)$ ). They are represented as $Z$ and $Z^*$.
    * $Z + Z^* = 2 Re\{Z\} \quad\to\quad Re\{Z\} = {1 \over 2} (Z + Z^*)$

## I. Introduction

Signal Processing is from EE and Computer Engineering, adjacent in Math, Physics, Computer Science and Applications. This means that knowledgments of such areas are required to grasp what Signal Processing is.

**FIR is a basic operation ?**

Joseph Fourier was a French mathematician who developed Fourier Series [[1]](#mjx-eqn-1). Based on his series, Fourier Transform was devised upon by other scholars. Fourier Transform significantly affects to the real world in recent 40 years, applying to **1)** audio processing for sound and music which is a 1-dimensional signal, **2)** image processing which addresses a 2-dimensional signal, **3)** video processing, a 3-dimensional signal, which is a sequence of images with time-axis, **4)** Telecommunications, **5)** Machine Learning, and **6)** Deep Learning.

...

Sinusoids are trigonometric functions which shows its value periodically.

Numbers like $z = x + yi$ are referred to **Complex Numbers** where $x, y$ are real numbers and $i$ is an imaginary number. The square of $i$ is -1, which is $i^2 = -1$. In EE, the imaginary number is written as $j$. Two coordinates are used when it comes to expressing Complex Number. **1)** Cartesian Coordinate System is the coordiante system where $x$-axis is real number and $y$-axis is imaginary number. **2)** Polar Coordinate used the unit vector to express Complex Number.

The **Euler's formula** [[6]](#mjx-eqn-6) establishes the fundamental relationship between the trigonometric functions and the complex exponential function. If $\theta$ is defined as $\omega t$ in the Euler's formula, $\omega$ is interpreted as angle per second. For instance, $\omega = 20\pi$ means a vector rotating $20\pi$ in a second. <!-- IT'S AN AMAZING FORMULA ...-->>

$$
\begin{array}{cc}
& e^{j\theta} = \cos\theta+j\sin\theta \\
& re^{j\theta} = r\cos\theta+jr\sin\theta \\
\\
(\theta \to \omega t) & e^{j\omega t} = \cos\omega t+j\sin\omega t \\
& re^{j\omega t} = r\cos\omega t+jr\sin\omega t
\end{array}
$$

The real part of the Euler's formula $\cos{\omega t}$ can be converted into the signal sinusoids.

$$
\begin{array}{cc}
& A\cos{(\omega t)} = Re\{Ae^{j\omega t}\} \\
(\omega t \to \omega t + q) & Re\{Ae^{j(\omega t + \varphi)}\} = A\cos{(\omega t + \varphi)} \\
& x(t) = A\cos{(\omega t+\varphi)} = Re\{Ae^{j(\omega t + \varphi)}\} = Re\{\underline{A}e^{j\omega t}\underline{e^{j\varphi}}\}
\end{array}
$$

where $Ae^{j\varphi}$ is called **Complex Amplitude $X$** or **Phasors**. This relationship implicates that a signal sinusoid is driven if the real part of the Euler's formula is given. In other words, the function is derived when $(A, \varphi)$ is solved from the Euler's formula. For example,

> $$
> \begin{array}{ccc}
> x(t) & = Re\{ -3je^{j\omega t}\} & \to X = Ae^{j\varphi} = -3j \\
> & & \to A = 3 (A > 0), e^{j\varphi}=-j \\
> & & \to \varphi=-{\pi \over 2}\ \text{(The Euler's Formula)} \\
> & = 3\cos{(\omega t -{\pi \over 2})} &
> \end{array}
> $$

Furthermore, when $x(t) = \sqrt{3}\cos(77\pi t + 0.5\pi)$ is given, $X$ is derived from the sinusoid.

> $$
> \omega = 77\pi,\quad \varphi = 0.5\pi,\quad A = \sqrt{3} \\
> x(t) = Re\{\sqrt{3} e^{j(77\pi + 0.5\pi)} \} \to X = \sqrt{3}e^{j 0.5\pi}
> $$

Both left-hand side and right-hand side in the Euler's formula always equal even if they are transformed by each forumla.

$$
\begin{array}{ccc}
\underline{e^{j(\theta_1+\theta_2)}} & = \underline{e^{j\theta_1}e^{j\theta_2}} & = (\cos\theta_1 + j\sin\theta_1)(\cos\theta_2 + j\sin\theta_2) \\
& & = (\cos\theta_1\cos\theta_2 - \sin\theta_1\sin\theta_2) + j (\sin\theta_1\cos\theta2 + \cos\theta_1\sin\theta_2) \\
& & = \underline{\cos(\theta_1+\theta_2) + j\sin(\theta_1+\theta_2)}
\end{array}
$$

The difference between the real part and the imaginary part in the Euler's formula is $\pi \over 2$. Specifically, $\sin(\omega t + \varphi) = \cos(\omega t + \varphi - {\pi \over 2})$ is met.

When sinusoids which have a same frequency are given, they are able to be compounded into one single sinusoid based on the Phasor Addition Rule [[3]](#mjx-eqn-3).

$$
\begin{array}{c}
\text{COMPLEX ADDITION RULE} \\
\hline
\sum_{k=1}^N X_k = \sum_{k=1}^N A_k e^{j\varphi_k} = Ae^{j\varphi} \qquad\gets \text{the sum of complex numbers is just a complex number} \\
\end{array} \\
\ \\
\text{A Sum of Sinusoids} \\
\begin{array}{cc}
\hline
\sum_{k=1}^N A_k \cos(\omega_0 t + \varphi_k) & = \sum_{k=1}^N Re\{A_k e^{j(\omega_0 t + \varphi_k)}\} \\
& = Re\{(\sum_{k=1}^N A_k e^{j\varphi_k}) e^{j\omega_0 t}\} \\
& = Re\{(Ae^{j\varphi})e^{j\omega_0 t}\} \\
& = A\cos(\omega_0 t + \varphi)
\end{array}
$$

Take $x_1(t)=\cos(77\pi t)$ and $x_2(t)=\sqrt{3}\cos(77\pi t + 0.5\pi)$ for example. From $A_1=1, \varphi_1=0$ and $A_2=\sqrt{3}, \varphi_2={\pi \over 2}$

> $$ \require{AMScd}
> \begin{array}{cc}
> A_1 e^{j\varphi_1} + A_2 e^{j\varphi_2} & = 1e^{j0} + \sqrt{3}e^{j0.5\pi} \\
> \text{(from the Euler's formula)} & = 1 + \sqrt{3}j \\
> \text{(present on the polar coordinate)} & \begin{CD} @AA{\sqrt{3} \\}A \\ @>1>> \end{CD}
> \end{array}
> $$

The sum of the two vectors makes a new vector which is the result of the complex addition. The size of the result vector becomes $A$ and the angle of the vector from $x$-axis is $\varphi$. As a result, the compounded sinusoid $x_3(t) = 2\cos(77\pi + {\pi \over 3})$. *(One more practice is in the class material in Chapter 2 page 50)*

However, the reality is more complex than the sum of the same frequency. To present a sum of different frequencies of sinusoids like a harmony in music and a vowel in human speech, an expansion of the above sum method is required.

The **Inverse Euler Formula** [[4]](#mjx-eqn-4), a transition that the real function is transited into the complex function, is so useful that the formula is frequently utilized during a specturm interpretation. In other words, the time domain function is converted into the frequency domain function and vice versa.

|$\begin{array}{ccc} \cdot \text{ Euler formula :} & e^{j \omega t} = \cos(\omega t) + j \sin(\omega t) & \cdots \quad (1) \\ \cdot \; \omega t \to - \omega t\text{ :} & e^{- j \omega t} = \cos(- \omega t) + j \sin(- \omega t) \\ & = \cos(\omega t) - j \sin(\omega t) & \cdots \quad (2) \\ \end{array}$|$$\text{INVERSE EULER FORMULA}$$ $\begin{array}{cc} \cdot \; (1) + (2) & = e^{j \omega t} + e^{- j \omega t} = 2 \cos(\omega t) \\ & \to \underline{\cos(\omega t) = {1 \over 2} (e^{j \omega t} + e^{- j \omega t})} \\ \cdot \; (1) - (2) & = e^{j \omega t} + e^{- j \omega t} = 2 \sin(\omega t) \\ & \to \underline{\sin(\omega t) = {1 \over 2j} (e^{j \omega t} - e^{- j \omega t})} \end{array}$|
|--|--|

By the Inversed Euler's Formula, the signal in the time domain $x(t)$ can be defined as $A \cos{(\omega t)} = A {1 \over 2} (e^{j\omega t} + e^{-j\omega t})$. In addition, $x(t)$ defined as $\sin$ function can be converted into the sum of two complex exponentials which is a normal formula of $x(t)$ and $\cos$ function;

> $$
> \begin{array}{ccc}
> A \sin{(7t)} & = {A \over 2j}e^{j7t} - {A \over 2j}e^{-j7t} & \text{(Inversed Euler's Formula)} \\
> & = {1 \over 2} A e^{-j0.5\pi} e^{j7t} + {1 \over 2} A e^{j0.5\pi} e^{-j7t} & ({1 \over j} = {j \over j^2} = -j = e^{-{\pi \over 2}})
> \end{array}
> $$

A Spectrum is presented as the frequency $f$ axis and the Complex Amplitude axis. In other words, the Spectrum has a frequency information so that when the spectrum of the signal is given, the time domain function $x(t)$ is derived.
<!-- WHY THE FREQUENCIES IN SPECTRUM SHOWS CONJUGATE RELATIONSHIPS? -->
<!--
Direct Current (DC) in EE jargon is another name for zero-freq component. DC component always has \varphi = 0 or \pi.
-->
> $$
> \begin{array}{ccc}
> x(t) & = 10 + 7 e^{-j {\pi \over 3}} e^{j2\pi(100)t} + 7 e^{j {\pi \over 3}} e^{-j2\pi(100)t} + 4 e^{j {\pi \over 2}} e^{j2\pi(250)t} + 4 e^{-j {\pi \over 2}} e ^{-j2\pi(250)t} & \\
> & = 10 + 14 \cos(2\pi(100)t - {\pi \over 3}) + 8 \cos(2\pi(250)t + {\pi \over 2}) & \text{(Inversed Euler's Formula)}
> \end{array}
> $$

In conclusion, the multiple frequencies of the signal time domain function $x(t)$ is showed as

$$
x(t) = A_0 + \sum_{k=1}^N A_k \cos(2 \pi f_k t + \varphi_k)
$$

A sheet-music notation is an example of a time-frequency diagram. The horizontal axis is the time domain. Since the more a note becomes higher, the more the frequency of the note becomes higher, the vertical axis is the frequency domain. The note A has 440 $Hz$ frequency.

## II. Literature Reviews

#### A. Signals in Sinusoids and The Euler's Formula

Sinusoids refers to both sine and cosine functions which are same when the consine function is shifted $\pi \over 2$ to the $x$-axis or the sine function is shifted  $- {\pi \over 2}$ to the $x$-axis. The definition of a signal as a mathematical function which has time-axis uses sinusoids with the following formula;
$$\text{Signal in Time Domain}\quad x(t) = A \cos{(2\pi(f)t + \varphi)}$$

Period $T$ should be defined to use Frequency $f$. $T$ is an interval time, required to complete one cycle in sinusoids. The unit of $T$ is a second. $f$ is the number of repeated cycles in a second which is expressed as $f = {1 \over T}$. The unit of $f$ refers to $Hz = {1 \over sec}$ derived from $1 \over T$. $2\pi(f)$ refers to Radian Frequency, $\omega\ (radian/sec)$. While *frequency* normally refers to Cycle Frequency $f$, Radian Frequency $\omega$ is considered as *frequency* in Signal Processing. Phase $\varphi$ is related with a time shift or delay. Although Amplitude $A$, the strength of the signal, is continuously getting smaller due to the air impedeance in the large scale, $A$ is addressed as constant value. Imagine the situation that people speak for example. The sound is disappeared after a few time take. These relationships are summarized in the following table.

$$\begin{array}{c|c}
\mathbf{FORMULA} & \mathbf{FROM} \\
\hline
\omega=(2\pi)f \\
\hline
T={1 \over f}={2\pi \over \omega} &\gets f={\omega \over 2\pi}
\end{array}$$

Signal sinusoids can be plotted if $(A, \omega, \varphi)$ are given, and vice versa. $A\cos{(\omega t+\varphi)}$ can be represented as $A\cos{(\omega(t-t_m))}$ where the $t_m$ makes the sinusoid the peak.

$\varphi$ is ambiguous since sinusoids are periodic with the period $2\pi$, resulting in $A\cos({\omega t + \varphi + 2\pi, 4\pi, 6\pi, \dots}) = A\cos{(\omega t + \varphi)}$.


An analog signal which indicates continuous signals is presented as sinusoids. To digitize $x(t)$ into $x[n]$ when $x(t)$ is an analog and $x[n]$ is a digital, sampling is required. Take 11,025 samples per second for example. The unit, samples per second, means $Hz$ same as sampling rate and sampling frequency. The length of the sample referring to Sampling Period $T$, is ${1 \over 11025} (sec/sample) = 90.7 \times 10^{-6} sec = 90.7 microsec$.

Normally, the audible rate of human is 20,000 $Hz$ so that the best sampling rate is 44,100 $Hz$, normally offered by CD <!--WHY?-->.

In order to calculate the volume of $x[n]$ with 16-bit samples (Quantize - to express Amplitude) and Stereo (2 channels) audio, the volume represents as $$2 \times {16 \over 8} \times 60 \times 44100 = 10,584,000\text{ Bytes} = 10.584\text{ MB}$$ where $2$ indicates stereo channels, $16 \over 8$ means Amplitude converted bits into bytes, $60$ is specified as seconds, and $44100$ is Sampling Rate, $Hz$.

---



#### B. Radian and Degree

## III. Works

#### A. CNN Summarization

#### B. Publication Presentation

## IV. Implementation

## References

$\tag*{}\label{1} \text{[1] https://en.wikipedia.org/wiki/Joseph_Fourier, accessed in Mar. 8 2024 [discouraged]}$
$\tag*{}\label{2} \text{[2] https://resources.pcb.cadence.com/blog/2023-adc-sampling-rate,  accessed in Mar. 8 2024 [discouraged]}$
$\tag*{}\label{3} \text{[3] http://www.spec.gmu.edu/~pparis/classes/notes_201/notes_2019_09_10.pdf, accessed in Mar. 18 2024 [Class Materials]}$
$\tag*{}\label{4} \text{[4] http://musicweb.ucsd.edu/~trsmyth/compExpAndSpecRep/Inverse_Euler_Formulas.html, accessed in Mar. 19 2024 [Class Materials, but discouraged]}$
$\tag*{}\label{5} \text{[5] https://mathbang.net/338#gsc.tab=0, accessed in Mar. 27 2024 [discouraged]}$
$\tag*{}\abel{6} \text{[6] https://en.wikipedia.org/wiki/Euler's_formula, accessed in Mar. 27 2024 [discouraged]}$

