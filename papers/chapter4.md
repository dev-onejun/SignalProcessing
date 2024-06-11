$$
\text{Acronym & Abbreviation} \\
\begin{array}{|c|c|}
\hline
\text{A-to-D (Analog to Digital)} & \text{D-to-A (Digital to Analog)} \\
\hline
\text{} & \text{} \\
\hline
\end{array}
$$

##### Keywords
* **Aliasing**: An effect that processed signals are not distinctive for they have exactly same values for x[n].

### Chapter 4. Sampling and Aliasing

Systems in Signal Processing change $x(t)$ into $y(t)$ to improve the quality of the $x(t)$, to focus on interested parts in $x(t)$, and to extract information from $x(t)$. For example, Low-frequency Filters are utilized to concentrate on the bass from music. Image deblurring is also an another example of Signal Processing, refining images more clear.

Before using computers to process signals, electronic circuits such as resistors, capacitors, op-amps and transistors directly translated analog signals $x(t)$ into target analog signals $y(t)$. In these days, rather than making use of the electronic circuits, A-to-D and D-to-A converters have sampled, enabling computers to address signals by storing the signals in their memories.

The definition of Sampling process is $\{ x(t) \to x[n] \text{ | } n \in Z\text{, } t = n T_s \}$. Sampling Frequency (Rate) or Samples per Second $f_s$ and Sampling Period $T_s$ have the same relationship as an analog $f_s = {1 \over T_s}$. Take example of the relationship with specific numbers. If $T_s$ is given as 125 micro seconds, $T_s = 125 \text{ micro sec} = 125 \times 10^{-6} \text{sec} \to f_s = {1 \over T_s} = 8000 \text{ samples/sec}$. During Sampling, between the ideal formula $x[n] = x(n T_s)$, Quantization, from Real Number $Z$ to a n-bits representation, should be performed. However, Quantization is not considered in this paper, tackling only the ideal formula.

The quality of reconstrcuted signal $y(t)$ is susceptible from a sampling rate $f_s$. Specifically, the maximum frequency of $x(t)$ determines the adequate sampling frequency $f_s$.

### References
