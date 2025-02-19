# fastlog
A fast, specialized version of log2

For applications which involve the calculation of exponentials, sometimes it is faster to calculate a logarithm instead. The logarithm function provided in the standard c library is accurate and fairly fast, but occasionally it is desirable to sacrifice accuracy for speed. For example, for Monte Carlo Simulations, a large number of comparisons are made, but the comparison in question is simply checking whether a value is greater than or equal to, say, log of a random number.

It is fairly trivial to calculate the floor of log base 2 of an integer by analyzing the number of bits filled in, say, an unsigned integer. On modern hardware this is fairly fast and can be done with built in compiler tools, such as `__builtin_clz` for gcc. However, this alone is not suitable for an estimate. An additional approximation can be achieved by taking the remaining bits and placing them in the mantissa section of the float.

## First approximation
<img width="355" alt="Screenshot 2025-02-17 at 7 11 44 PM" src="https://github.com/user-attachments/assets/c13b2446-0c15-45e2-b48f-0597b8d5a0ae" />

visualization. the red curve represents $\log_2$, and the green line is the approximation obtained with just clz and the bits appended to the float

<img width="532" alt="Screenshot 2025-02-17 at 7 15 20 PM" src="https://github.com/user-attachments/assets/5c88dc66-ca1c-44ca-abc7-de352ce37d05" />

Absolute error of first approximation

## Third Order Approximation
We can achieve higher accuracy by using approximating with a third order polynomial, $\ln_2{x} = c_3x^3+c_2x^2+c_1x^1+c_0$. One boundary condition gives us that $c_0=0$ and $c_3+c_2+c_1=1$. By taking the first derivative we get $\frac{1}{x\ln{(2)}} = 3c_3x^2 + 2c_2x + c_1$, which by taking the values at $x=1$ and $x=2$ allows us to estimate $c_3$ and $c_2$. Some fine-tuning is needed to reduce relative error.



