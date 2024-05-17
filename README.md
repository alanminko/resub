
## Resubstitution Engines and Benchmarks

This repository contains guidelines for running various resubstitution engines in [ABC](https://github.com/berkeley-abc/abc).

The engines are exercised on the level of individual Boolean transforms. The focus is not high performance on specific benchmarks but rather
conceptual understanding and implementation flexiblity needed for building efficient optimization frameworks based on Boolean resubstitution.

---

### Engine Taxonomy

ABC Command | Short Description | Publication
------------|-------------------|--------------
resub_unate | Fast resub based on detecting unate divisors | [paper](https://people.eecs.berkeley.edu/~alanmi/publications/2021/tcad21_sim.pdf)
resub_core | Generic high-effort resub engine based on support selection | [paper](https://people.eecs.berkeley.edu/~alanmi/publications/2018/dac18_eco.pdf)
twoexact | SAT-based exact synthesis with side-divisors | [paper](https://people.eecs.berkeley.edu/~alanmi/publications/2018/dac18_topo.pdf)

The first engine is the fastest one among those presented here. It works well when the resulting resub function contains only a few nodes.
It is good for developing rewriting-style optimizations when relatively small (possibly six-input) cuts are computed, 
followed by collecting a set of divisors supported by each cut. The divisor functions can be represented using truth tables 
(in the case of six-input cuts, each truth table is one 64-bit machine word).
The fast unate resub can be applied to reexpress a target node in terms of other divisors supported by the cut.
An efficient GPU-based implementation of this engine may be developed.

The second engine uses more effort to perform two steps. Given a target node and a set of divisors, 
the first step is to compute a small support (or a good-quality support if the divisors have non-unit weights)
sufficient for expressing the target node. The second step is to find the new function of the node in terms of the support variables.
This engine works for incompletely-specified functions. It can be iterated to find solutions for multi-output functions.
The engine was used to derive patch functions in the ECO application, winning the first place in [2017 ICCAD CAD competition](https://www.iccad-contest.org/2017/) (Problem A).

The third engine is a high-effort SAT-based exact synthesis engine applicable to multi-output Boolean functions and relations with side-divisor, 
that is, reusable divisor functions other than primary inputs. (The original formulation of SAT-based exact synthesis did not consider side-divisors).
This engine computes the smallest possible implementation of the resub functions in terms of the number of nodes
in an and-inverter graph (AIG) or an xor-and-inverter graph (XAIG).

The three engines presented here have a shared input/output representation format.

---

### Input Format

The input format is a modified version of [Espresso PLA format](https://people.eecs.berkeley.edu/~alanmi/research/espresso/espresso_5.html) (.type fr).

The modifications include
* **Representation of Boolean relations**
  * For this some input combinations are duplicated with different output combinations.
* **Input patterns are represented as minterms**
  * This restriction works well when [simulation signatures](https://people.eecs.berkeley.edu/~alanmi/publications/2024/tech24_resub.pdf) are used. It may be removed in the future.

Examples of completely-specified functions, incompletely-specified functions, and Boolean relations represented by the proposed format 
can be found in Figure 1 of the following [technical report](https://people.eecs.berkeley.edu/~alanmi/publications/2024/tech24_resub.pdf).

---

### Output Format

The output format represents the resulting AIGs or XAIGs as arrays of node fanins.

An example of the AIG produced by a resubstitution engine is given in Section V of the [technical report](https://people.eecs.berkeley.edu/~alanmi/publications/2024/tech24_resub.pdf).

---

### Verification

The results produced by the resub engines can be verified using command "resub_check".

---

### Benchmarks

Three representative sets of resub benchmarks are currently available:
* **Resub instances generated by command "resub"**
  * These instances are useful to test the fast resub engine (command "resub_unate")
* **Resub instances generated by command "runeco"**
  * These instances are useful to test the high-effort resub engine (command "resub_core")
* **Boolean relations generated by command "&genrel"**
  * These instances are useful to test SAT-based exact synthesis (command "twoexact")

---

### Acknowledgment

This work is done in collaboration with Yukio Miyasaka (UC Berkeley), Alessandro Tempia Calvino (EPFL), and Andrea Costamagna (EFPL).

It is supported in part by the SRC Contract 3173.001 ``Standardizing Boolean transforms to improve quality and runtime of CAD tools''
and the NSA grant ``Novel methods for synthesis and verification in cryptanalytic applications''.

---



