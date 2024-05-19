This directory contains several examples used to test the high-effort resub engine (command "resub_core").

abc 02> resub_core -vs 031.pla
Using 2560 divisors with 9 words. Problem has 1 functions and 13266 minterm pairs.
Explored 78 divisor sets. Found 6 solutions. Memory usage 0.83 MB.  Time =     0.00 sec
The best solution:  Set    53 :  Funcs  0  Pairs    0  Start     4698  Weight    6  (0) n0  (11) n11  (15) n15  (21) n21  (39) n39  (47) n47  Cost = 6
  0 : Size =  6  Resub =  5  Bidec =  5  Isop =  5  Bdd =  5  OFF =    19 ( 29.69 %)  ON =    22 ( 34.38 %)  DC =    23 ( 35.94 %)  0x5525502255055000  0xAA8AA288AA2AA020
  1 : Size =  7  Resub =  5  Bidec =  5  Isop =  5  Bdd =  5  OFF =    33 ( 25.78 %)  ON =    40 ( 31.25 %)  DC =    55 ( 42.97 %)
Divisors: Vector has 8 entries: { -1 -1 0 11 15 21 39 47 }
Solution: Vector has 11 entries: { 9 12 14 17 7 18 11 20 4 23 24 }

abc 03> resub_check 031.pla
Verification successful.



