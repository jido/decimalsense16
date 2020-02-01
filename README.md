# decimalsense16
A 16-bit decimal number format that makes sense

This project takes some of the ideas of [decimalsense numbers](https://github.com/jido/decimalsense) to the half precision decimal number world.

Decimal numbers do not need be that complex.

Numbers
=======

Normal number range:

**1.00e-18** to **9.99e+17**

(hexadecimal _64_ to _7EF3_)

Subnormal number range (non-zero):

**1.0e-20** to **9.9e-19**

(hexadecimal _1_ to _63_)

Zero:

> hexadecimal _0_

One:

> hexadecimal _3FAC_

Two:

> hexadecimal _4010_

Infinity:

> hexadecimal _7F00_

Negative infinity:

> hexadecimal _FF00_

Decimalsense numbers are _monotonic_, the unsigned part is ordered when cast as integer, and _unique_: 
there is only one way to encode a particular nonzero number.

According to IEEE, positive and negative zero are equal which is the only exception to unique number representation.

**Note:** Representation of infinity does not follow the IEEE 754 standard for half precision floating point numbers.

Format
======

~~~
sppppppp pppppppp
~~~

   `s` = sign bit
   
   `p` = 15 significand bits
   
Normal numbers
--------------

~~~
e = (p - 100) / 900
~~~

* Exponent is offset by _18_
* Mantissa is normalised, it goes from _100_ to _999_

Take _18_ away from `e` to read the actual exponent;

Take `e ⨯ 900` away from p to read the mantissa

Subnormal numbers
-----------------

Equivalent to 16-bit integers (ignoring the sign bit) from 0 to 99;

Their exponent is _-18_ and the mantissa is equal to `p`, as it only encodes lower precision numbers between 0.0 and 1.0
