This directory contains examples of using SAT-based exact synthesis for solving multi-output functions and Boolean relations using command "twoexact".

As an example, consider testcase "mul22.pla" representing a 2x2 unsigned multiplier. The provably smallest circuit composed of 8 two-input and-nodes can be computed as follows:


abc 01> twoexact -N 7 -a mul22.pla
This resub problem is not a relation.
Inputs = 4. Divisors = 0. Outputs = 4. Nodes = 7.  InP = 0. OutP = 0.
Variables:  Function = 22.  Structure = 132.  Internal = 336.  Total = 490.
Timeout = 0. OnlyAnd = 1. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 490 variables and 4051 clauses was dumped into file "_temp_.cnf".
The problem has no solution. SAT solver time =     0.30 sec
Total runtime =     0.30 sec

abc 01> twoexact -N 8 -a mul22.pla
This resub problem is not a relation.
Inputs = 4. Divisors = 0. Outputs = 4. Nodes = 8.  InP = 0. OutP = 0.
Variables:  Function = 25.  Structure = 156.  Internal = 384.  Total = 565.
Timeout = 0. OnlyAnd = 1. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 565 variables and 5044 clauses was dumped into file "_temp_.cnf".
The problem has a solution. SAT solver time =     0.25 sec
This 4-var function (5 divisors) has 8 gates (0 xor) and 4 levels:
13  =  10
14  =  9
15  =  12
16  =  8
12  =  d & 11
11  =  b & ~8
10  =  a & c
 9  =  ~7 & ~8
 8  =  5 & 6
 7  =  ~5 & ~6
 6  =  b & c
 5  =  a & d
Verification successful.  Total runtime =     0.25 sec
Written MiniAIG into the AIGER file "mul22_twoexact.aig.aig".


If we allow xor-nodes, we can implement it using 7 two-input nodes:

abc 01> twoexact -N 6 mul22.pla
This resub problem is not a relation.
Inputs = 4. Divisors = 0. Outputs = 4. Nodes = 6.  InP = 0. OutP = 0.
Variables:  Function = 19.  Structure = 110.  Internal = 288.  Total = 417.
Timeout = 0. OnlyAnd = 0. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 417 variables and 3176 clauses was dumped into file "_temp_.cnf".
The problem has no solution. SAT solver time =     0.19 sec
Total runtime =     0.20 sec

abc 01> twoexact -N 7 mul22.pla
This resub problem is not a relation.
Inputs = 4. Divisors = 0. Outputs = 4. Nodes = 7.  InP = 0. OutP = 0.
Variables:  Function = 22.  Structure = 132.  Internal = 336.  Total = 490.
Timeout = 0. OnlyAnd = 0. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 490 variables and 4044 clauses was dumped into file "_temp_.cnf".
The problem has a solution. SAT solver time =     0.03 sec
This 4-var function (5 divisors) has 7 gates (1 xor) and 2 levels:
12  =  8
13  =  7
14  =  11
15  =  10
11  =  ~8 & 9
10  =  8 & 9
 9  =  b & d
 8  =  a & c
 7  =  5 ^ 6
 6  =  a & d
 5  =  b & c
Verification successful.  Total runtime =     0.03 sec
Written MiniAIG into the AIGER file "mul22_twoexact.aig".


As an example of applying exact synthesis to Boolean relations, consider the full adder, which can be implemented using 7 two-input and-nodes.

abc 03> twoexact -I 3 -N 6 -a fa.pla
This resub problem is not a relation.
Inputs = 3. Divisors = 0. Outputs = 2. Nodes = 6.  InP = 0. OutP = 0.
Variables:  Function = 19.  Structure = 74.  Internal = 144.  Total = 237.
Timeout = 0. OnlyAnd = 1. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 237 variables and 1403 clauses was dumped into file "_temp_.cnf".
The problem has no solution. SAT solver time =     0.07 sec
Total runtime =     0.07 sec

abc 03> twoexact -I 3 -N 7 -a fa.pla
This resub problem is not a relation.
Inputs = 3. Divisors = 0. Outputs = 2. Nodes = 7.  InP = 0. OutP = 0.
Variables:  Function = 22.  Structure = 92.  Internal = 168.  Total = 282.
Timeout = 0. OnlyAnd = 1. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 282 variables and 1854 clauses was dumped into file "_temp_.cnf".
The problem has a solution. SAT solver time =     0.14 sec
This 3-var function (4 divisors) has 7 gates (0 xor) and 4 levels:
11  =  10
12  =  ~8
10  =  ~7 & ~9
 9  =  ~b & ~6
 8  =  ~5 & ~7
 7  =  b & 6
 6  =  ~4 & ~5
 5  =  a & c
 4  =  ~a & ~c
Verification successful.  Total runtime =     0.14 sec
Written MiniAIG into the AIGER file "fa_twoexact.aig".


However, if we modify the full adder and allow it to produce values 1 or 2 in each case when the original full adder produces value 1, it can be realized with only four two-input nodes.

abc 03> twoexact -I 3 -N 3 -a fa1.pla
Inputs = 3. Divisors = 0. Outputs = 2. Nodes = 3.  InP = 0. OutP = 0.
Variables:  Function = 10.  Structure = 32.  Internal = 72.  Total = 114.
Timeout = 0. OnlyAnd = 1. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 114 variables and 514 clauses was dumped into file "_temp_.cnf".
The problem has no solution. SAT solver time =     0.00 sec
Total runtime =     0.00 sec

abc 03> twoexact -I 3 -N 4 -a fa1.pla
Inputs = 3. Divisors = 0. Outputs = 2. Nodes = 4.  InP = 0. OutP = 0.
Variables:  Function = 13.  Structure = 44.  Internal = 96.  Total = 153.
Timeout = 0. OnlyAnd = 1. Fancy = 0. OrderNodes = 0. UniqueFans = 0. Verbose = 1.
CNF with 153 variables and 764 clauses was dumped into file "_temp_.cnf".
The problem has a solution. SAT solver time =     0.00 sec
This 3-var function (4 divisors) has 4 gates (0 xor) and 2 levels:
 8  =  5
 9  =  ~7
 7  =  ~b & 6
 6  =  ~a & ~c
 5  =  c & 4
 4  =  a & b
Verification successful.  Total runtime =     0.00 sec
Written MiniAIG into the AIGER file "fa1_twoexact.aig".


