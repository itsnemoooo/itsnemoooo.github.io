---
title: "What I learned in Filters"
date: YYYY-MM-DD
categories: [Blogs]
---
### What You’ll Learn

Let's explore the design and analysis of analog and digital filters, covering essential techniques and concepts in filter approximation and frequency transformation. I took Filters at SMU under Dr. Peikari, and then I followed back up to TA the following year. It is perfect for those interested in signal processing, telecommunications, and control systems, offering practical and theoretical insights into creating various types of filters for real-world applications. It also set me up well for my Samsung interviews.

The course focuses on two primary areas: analog filter approximation and digital filter design. It begins with the basics of analog filter design using classic approximations, then shifts to digital filters, introducing techniques for converting analog designs into digital formats. By the end, you’ll have the skills to design low-pass, high-pass, band-pass, and band-reject filters with both analog and digital methods.

### Key Topics

#### 1. Analog Filter Approximation Methods

In analog filter design, EE 5371 covers three key approximation methods, each with unique characteristics:

- **Butterworth Filters**: Known for a smooth, maximally flat frequency response, ideal when a ripple-free passband is required.
  
    ```python
    # Python example (using scipy.signal) for designing a Butterworth filter
    from scipy.signal import butter, freqs
    import matplotlib.pyplot as plt

    # Design a 3rd order Butterworth low-pass filter with cutoff at 1 rad/s
    b, a = butter(3, 1, analog=True)
    w, h = freqs(b, a)
    plt.plot(w, 20 * np.log10(abs(h)))
    plt.xscale('log')
    plt.title('Butterworth Filter Frequency Response')
    plt.xlabel('Frequency [radians / second]')
    plt.ylabel('Amplitude [dB]')
    plt.show()
    ```

- **Chebyshev Filters**: These filters allow for a faster transition between passband and stopband by introducing controlled ripples in the response.

- **Bessel Filters**: Bessel filters are used when maintaining a linear phase response is critical, such as in audio applications.

#### 2. Frequency Transformations

Frequency transformations allow you to adapt a low-pass filter prototype to different configurations like high-pass, band-pass, and band-reject filters.

```python
from scipy.signal import bilinear, freqz

# Example of frequency transformation using bilinear transformation
fs = 1000  # Sampling frequency
low_cutoff = 100  # Cutoff frequency of the filter

# Design a low-pass digital filter
b, a = bilinear([1], [1, low_cutoff], fs=fs)
w, h = freqz(b, a, fs=fs)

plt.plot(w, 20 * np.log10(abs(h)))
plt.title('Low-Pass Filter Frequency Response')
plt.xlabel('Frequency [Hz]')
plt.ylabel('Amplitude [dB]')
plt.grid()
plt.show()
```
### 3. Digital Filter Design

The course covers two main types of digital filters:

- **IIR Digital Filters**: Infinite Impulse Response (IIR) filters are efficient and typically based on analog filter prototypes. Techniques include **impulse-invariant transformation** and **bilinear transformation**.

- **FIR Digital Filters**: Finite Impulse Response (FIR) filters use **frequency sampling** and **windowing techniques** to design filters with linear phase response, ideal for applications requiring minimal phase distortion.

```python
from scipy.signal import firwin, freqz
import matplotlib.pyplot as plt
import numpy as np

# FIR filter design using window method
numtaps = 29  # Number of filter coefficients (length of the filter)
cutoff = 0.3  # Normalized cutoff frequency (0 to 1, where 1 is Nyquist)

fir_coeff = firwin(numtaps, cutoff)
w, h = freqz(fir_coeff)

plt.plot(w / np.pi, 20 * np.log10(abs(h)))
plt.title('FIR Filter Frequency Response')
plt.xlabel('Normalized Frequency')
plt.ylabel('Amplitude [dB]')
plt.grid()
plt.show()
``` 
### Why this is valuable
Filter design is a vital skill across various fields including communications, control systems, audio processing, and image processing. By understanding both analog and digital filtering techniques, you’ll be equipped to create solutions for real-world challenges in these domains.
