# fastlog
A faster low accuracy version of log2

For applications which involve the calculation of exponentials, sometimes it is faster to calculate a logarithm instead. The logarithm function provided in the standard c library is accurate and fairly fast, but occasionally it is desirable to sacrifice accuracy for speed. For example, for Monte Carlo Simulations, a large number of comparisons are made, but the comparison in question is simply checking whether a value is greater than or equal to, say, log of a random number.

It is fairly trivial to calculate the floor of log base 2 of an integer by analyzing the number of bits filled in, say, an unsigned integer. On modern hardware this is fairly fast and can be done with built in compiler tools, such as `__builtin_clz` for gcc. However, this alone is not suitable for an estimate. An additional approximation can be achieved by taking the remaining bits and placing them in the mantissa section of the float.

## First approximation

## Second Order Approximation

## Newton's method

We can use Newton's method to iterate from a close guess to a better one, using the derivative of the graph.

