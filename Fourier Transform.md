#FourierAnalysis 
#Mathematics 
#SignalProcessing 


A **Fourier transform** (**FT**) is a [mathematical](https://en.wikipedia.org/wiki/Mathematics "Mathematics") [transform](https://en.wikipedia.org/wiki/Integral_transform "Integral transform") that decomposes [functions](https://en.wikipedia.org/wiki/Function_(mathematics) "Function (mathematics)") into frequency components, which are represented by the output of the transform as a function of frequency. Most commonly functions of [time](https://en.wikipedia.org/wiki/Time "Time") or [space](https://en.wikipedia.org/wiki/Space "Space") are transformed, which will output a function depending on [temporal frequency](https://en.wikipedia.org/wiki/Frequency "Frequency") or [spatial frequency](https://en.wikipedia.org/wiki/Spatial_frequency "Spatial frequency") respectively.

The Fourier transform of a function is a [complex-valued function](https://en.wikipedia.org/wiki/Complex-valued_function "Complex-valued function") representing the [complex sinusoids](https://en.wikipedia.org/wiki/Euler%27s_formula "Euler's formula") that comprise the original function. For each frequency, the magnitude ([absolute value](https://en.wikipedia.org/wiki/Absolute_value#Complex_numbers "Absolute value")) of the [complex value](https://en.wikipedia.org/wiki/Complex_number#Modulus_and_argument "Complex number") represents the [amplitude](https://en.wikipedia.org/wiki/Amplitude "Amplitude") of a constituent complex [sinusoid](https://en.wikipedia.org/wiki/Sine_wave "Sine wave") with that frequency, and the [argument of the complex value](https://en.wikipedia.org/wiki/Argument_(complex_analysis) "Argument (complex analysis)") represents that complex sinusoid's [phase offset](https://en.wikipedia.org/wiki/Phase_offset "Phase offset"). If a frequency is not present, the transform has a value of 0 for that frequency. The Fourier transform is not limited to functions of time, but the [domain](https://en.wikipedia.org/wiki/Domain_of_a_function "Domain of a function") of the original function is commonly referred to as the _[time domain](https://en.wikipedia.org/wiki/Time_domain "Time domain")_. The [Fourier inversion theorem](https://en.wikipedia.org/wiki/Fourier_inversion_theorem "Fourier inversion theorem") provides a _synthesis_ process that recreates the original function from its frequency domain representation.

The Fourier transform is an extension of the [Fourier series](https://en.wikipedia.org/wiki/Fourier_series "Fourier series"), which in its most general form introduces the use of [complex exponential functions](https://en.wikipedia.org/wiki/Euler%27s_formula "Euler's formula").
The fourier transform integral:
$$
\hat{f}(\xi)=\int_{-\infty}^{\infty} f(x) e^{-i 2 \pi \xi x} d x
$$
The fourier inversion integral:
$$
f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{i 2 \pi \xi x} d \xi, \quad \forall x \in \mathbb{R}
$$
