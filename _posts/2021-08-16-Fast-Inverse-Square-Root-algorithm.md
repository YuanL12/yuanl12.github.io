---
title: 'Fast Inverse Square Root Algorithm'
date: 2021-08-15
permalink: /posts/2021/08/Fast-Inverse-Square-Root-Algorithm/
tags:
  - Algorithm
  - C++
---

# Fast Inverse Square Root algorithm
This is a famous algorithm from Quake III. It utilizes
- IEEE 754
- Newton method
- Approximation of function $log(1+x)\approx x + \mu$, where $\mu = 0.0430 $ is a **mysterious** term.

## Code
```C++
float Q_rsqrt( float number )
{
	long i;
	float x2, y;
	const float threehalfs = 1.5F;

	x2 = number * 0.5F;
	y  = number;
	i  = * ( long * ) &y;                       // evil floating point bit level hacking
	i  = 0x5f3759df - ( i >> 1 );               // what the fuck? 
	y  = * ( float * ) &i;
	y  = y * ( threehalfs - ( x2 * y * y ) );   // 1st iteration
//	y  = y * ( threehalfs - ( x2 * y * y ) );   // 2nd iteration, this can be removed

	return y;
}
```


##  IEEE 754
There are two types of number that are used in this algorithm. Let's review them:
- `long` 32 bits integer number
- `float` 32 decimal number (single)

Next, we define IEEE 754, which is a float number representation composed of three components:
- sign(1-bit):  0 postive, 1 negative
- Exponent(8-bits): represent exponent numbers (start from -127)
- Mantissa(23-bits): represent mantissa number after decimal dot

### example
``` 
85.125
85 = 1010101
0.125 = 001
85.125 = 1010101.001
       = 1.010101001 x 2^6 
       = (1+M/2^23) x 2^(E - 127)
sign = 0 

1. Single precision:
biased exponent 127+6 = 133 = E
133 = 10000101
Normalised mantisa = 010101001
we will add 0's to complete the 23 bits

The IEEE 754 Single precision is:
= 0 10000101 01010100100000000000000
This can be written in hexadecimal form 42AA4000
```

## IEEE 754 with bit representation
We first define the bits reprsentation of a positive IEEE 754 number $a$ with E and M to be $a_i = 2^{23}\times E + M$, which is equivalent to shift E by 23 dits and then add the bits of M into it. 
> **Note**: The bits reprsentation of a positive IEEE 754 number is also very easy to find. If `y` is a float type number (IEEE 754) like `float y;`, then by `long i = * (long *) &y`, `i` is the bits reprsentation of `y`. 



Now, given a positive IEEE 754 number with E and M, which is equal to 

$$
a = (1 + \frac{M}{2^{23}} ) \cdot 2^{E - 127}
$$

, taking logarithm with base 2 gives 

$$
\log_2(1 + \frac{M}{2^{23}} ) +  E - 127
$$

, and then apply tricks $log(1+x)  \approx x + \mu$, where $\mu = \frac{1}{2} - \frac{1+ \ln(\ln 2)}{2 \ln 2}\approx0.0430$.
 is the term computed from the approximation of smallest maximum norm error.

> **How to compute $\mu$** : 
> The mathematical problem is $\min_{m, \mu} \max_{x\in[0,1]} |h(x)|$, where $h(x) = \log_2(1+x) - (mx+\mu)$. The three possible maximum point is $x = 0,1,\theta$, where $\frac{\partial h}{\partial x} (\theta) = 0$. Then $m$ and $\mu$ is computed by solving $h(0) = h(1) = - h(\theta)$.   


Finally,

$$
\begin{aligned}
\log_2(a)
&=\log_2(1 + \frac{M}{2^{23}} ) +  E - 127\\
&\approx \frac{M}{2^{23}} + \mu + E - 127\\
&\approx \frac{M + 2^{23} \cdot E}{2^{23}} + \mu - 127\\
& = \frac{a_i}{2^{23}} + \mu - 127,\\
&\text{where $a_i$ is the bit representation of } a.
\end{aligned}


$$

shows that the bit representation of a number is closely related to its logarithm up to some scaling and shifting.

## Back to algorithm
`float y`
- IEEE 754
- no bit manipulation
- used to store number 

`long i`
- ordinary 32-bit number
- has bit manipulation

`i = (long) y`
- The normal way of converting float to long, eg, 3 <--3.33 
- but will lose so much information.

`i = * (long *) &y`
- Using pointer to convert the type of the address to long without modifying the contents pointed to.
- now `i` is y's bits representation, which is about equal to log(y) up to some scaling and shifting.

`i = 0x5f3759df - ( i >> 1);`

In order to compute $\frac{1}{\sqrt{y}}: = z$, it is easier to compute $\log(z)$, and 

$$
\begin{aligned}
\log(z) & = \frac{1}{2^{23}} (M_z + 2^{23} \cdot E_z ) + \mu - 127 \\
& = \log(\frac{1}{\sqrt{y}})\\ 
& = (-\frac{1}{2})\log(y)\\
& =- \frac{1}{2} (\frac{1}{2^{23}} (M_y + 2^{23} \cdot E_y ) + \mu - 127) 
\end{aligned}
$$

Since we only need to compute the bit representation of $z: M_z + 2^{23} \cdot E_z$, from above, it is equal to 

$$
\begin{aligned}
M_z + 2^{23} \cdot E_z
= & \frac{3}{2} 2^{23} (127 - \mu) - \frac{1}{2} (M_y + 2^{23} \cdot E_y )\\
= & \text{ 0x5f3759df}  - ( i >> 1)  
\end{aligned}
$$

, where $i$ is the bit representation of $y$, and 0x5f3759df = $\frac{3}{2} 2^{23} (127 - \mu)$ and $\mu = \frac{1}{2} - \frac{1+ \ln(\ln 2)}{2 \ln 2}$.

`y = * ( float * ) &i;`
- convert back to a float number

`y = y * (threehalfs - ( x2 * y * y ) );`

Newton Method:
Used to find root of $f(x) = 0$, updated by
$x_{new} = x - \frac{f(x)}{f'(x)}$.

Here $f(y) = \frac{1}{y^2} - x =0$, given $x$ we hope to find $y$. Thus,

$$
\begin{aligned}
y_{new} & = y + \frac{y}{2} (1 - x y ^2) \\ &= y(\frac{3}{2} - \frac{x}{2} y ^2)
\end{aligned}
$$

