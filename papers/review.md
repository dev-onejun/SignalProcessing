# SPAYN: Signal Processing is All You Need (A Review)

### *Abstract*

Translating analog information into digital is inevitable to address data in computers. Signal Processing is a way that conducts these translations. This paper reviews key concepts of this method, involving Fourier Transform, FIR, and Convolution Operation. These operations which can be applied to any digital signals such as audio, images, and videos derives CNN, the popular architecture of the neural network in AI tasks. In other words, the paper also tackles a few parts of deep learning. I expect that this work summarizes the whole concepts of Signal Processing in one paper.

#### Acronym/Abbreviation
* Convolutional Neural Network (CNN)
* Finite Impulse Response (FIR)
* Artificial Intelligence (AI)
* Electrical Engineering (EE)

##### *keywords*
* **Complex Numbers**: the number presented as $z = a + bj$ where $a, b$ are real numbers and $j$ is an imaginary number.
* **Trigonometric Functions**: The functions like $\sin, \cos$ and $\tan$.
    * $\sin\theta = \cos{({\pi \over 2} - \theta)}$
    * $\cos\theta = \sin{({\pi \over 2} - \theta)}$

## I. Introduction

Signal Processing is from Electrical Engineering and Computer Engineering, adjacent in Math, Physics, Computer Science and Applications. This means that knowledgments of such areas are required to grasp what Signal Processing is.

**FIR is a basic operation ?**

Joseph Fourier was a French mathematician who developed Fourier Series [1]. Based on his series, Fourier Transform was devised upon by other scholars. Fourier Transform significantly affects to the real world in recent 40 years, applying to **1)** audio processing for sound and music which is a 1-dimensional signal, **2)** image processing which addresses a 2-dimensional signal, **3)** video processing, a 3-dimensional signal, which is a sequence of images with time-axis, **4)** Telecommunications, **5)** Machine Learning, and **6)** Deep Learning.

...

Sinusoids are trigonometric functions which shows its value preriodically.

Numbers like $z = x + yi$ are referred to Complex Numbers where $x, y$ are real numbers and $i$ is an imaginary number. The square of $i$ is -1, which is $i^2 = -1$. In EE, the imaginary number is written as $j$. Two coordinates are used when it comes to expressing Complex Number. 1) Cartesian Coordinate System is the coordiante system where $x$-axis is real number and $y$-axis is imaginary number. 2) Polar Coordinate used the unit vector to express Complex Number.

The Euler's formula establishes the fundamental relationship between the trigonometric functions and the complex exponential function.

$$
e^{j\theta} = \cos\theta+j\sin\theta \\
re^{j\theta} = r\cos\theta+jr\sin\theta
$$

If $\theta$ is defined as $\omega t$, $\omega$ is interpreted as angle per second. For instance, $\omega = 20\pi$ means a vector rotating $20\pi$ in a second.
$$ e^{j\omega t} = \cos\omega t+j\sin\omega t $$

The real part of the Euler's formula can be converted into the signal sinusoids.

$$
\text{FROM}\quad Re\{Ae^{j\omega t}\} = A\cos{(\omega t)} \to Re\{Ae^{j(\omega t + \varphi)}\} = A\cos{(\omega t + \varphi)} \\
x(t) = A\cos{(\omega t+\varphi)} = Re\{Ae^{j(\omega t + \varphi)}\} = Re\{Ae^{j\omega t}e^{j\varphi}\}
$$

where $Ae^{j\omega}$ is called Complete Amplitude $X$. This relationship implicates the method to get a signal sinusoid function if the real part of the Euler's formula is given. In other words, the function is derived when $A$ and $\varphi$ is solved from the Euler's formula. For example,

$$
x(t) = Re\{ -3je^{j\omega t}\} \\
\to A = 3 (A > 0), e^{j\varphi}=-j \quad \to \varphi=-{\pi \over 2}\ \text{(The Euler's Formula)} \\
\to 3\cos{(\omega t -{\pi \over 2})}
$$

## II. Literature Reviews

#### A. Sinusoids and Signals

Sinusoids refers to both sine and cosine functions which are same when the consine function is shifted $\pi \over 2$ to the $x$-axis or the sine function is shifted  $- {\pi \over 2}$ to the $x$-axis. The definition of a signal as a mathematical function which has time-axis uses sinusoids with the following formula;
$$A \cos{(2\pi(f)t + \varphi)}$$

Period $T$ should be defined to use Frequency $f$. $T$ is an interval time, required to complete one cycle in sinusoids. The unit of $T$ is a second. $f$ is the number of repeated cycles in a second which is expressed as $f = {1 \over T}$. The unit of $f$ refers to $Hz = {1 \over sec}$ derived from $1 \over T$. $2\pi(f)$ refers to Radian Frequency, $\omega\ (radian/sec)$. Phase $\varphi$ is related with a time shift or delay. Although Amplitude $A$, the strength of the signal, is continuously getting smaller due to the air impedeance in the large scale, $A$ is addressed as constant value. Imagine the situation that people speak for example. The sound is disappeared after a few time take. These relationships are summarized in the following table.

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

In order to calculate the volume of $x[n]$ with 16-bit samples (Quantize - to express Amplitude) and Stereo (2 channels) audio, the volume represents as $$2 \times {16 \over 8} \times 60 \times 44100 = 10,584,000 Bytes = 10.584 MB$$ where $2$ indicates stereo channels, $16 \over 8$ means Amplitude converted bits into bytes, $60$ is specified as seconds, and $44100$ is Sampling Rate, $Hz$.

## III. Works

#### A. CNN Summarization

#### B. Publication Presentation

## IV. Implementations

## References

https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference

* [1] https://en.wikipedia.org/wiki/Joseph_Fourier . acessed in Mar 8, 2024. [discouraged]
* [2] https://resources.pcb.cadence.com/blog/2023-adc-sampling-rate . accessed in Mar 8, 2024. [discouraged]

