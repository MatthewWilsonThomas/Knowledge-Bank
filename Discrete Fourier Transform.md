#SignalProcessing 
#Mathematics 
#FourierAnalysis
#DiscreteMathematics

This is a discrete version of the [[Fourier Transform]]. 
The DFT can transform a sequence of evenly spaced signal to the information about the frequency of all the sine waves that needed to sum to the time domain signal. It is defined as:$$
X_k=\sum_{n=0}^{N-1} x_n \cdot e^{-i 2 \pi k n / N}=\sum_{n=0}^{N-1} x_n[\cos (2 \pi k n / N)-i \cdot \sin (2 \pi k n / N)]
$$
where

-   N = number of samples
-   n = current sample
-   k = current frequency, where $𝑘∈[0,𝑁−1]$
-   $𝑥_𝑛=$ the sine value at sample n
-  $𝑋_k =$ The DFT which include information of both amplitude and phase

### The Inverse DFT
Of course, we can do the inverse transform of the DFT easily:
$$
x_n=\frac{1}{N} \sum_{k=0}^{N-1} X_k \cdot e^{i \cdot 2 \pi k n / N}
$$
Find more about the DFT @ [Wiki](https://en.wikipedia.org/wiki/Discrete_Fourier_transform)
