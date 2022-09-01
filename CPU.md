# CPU Terminology

## 1. Pipeline/Superscalar

[[Pipelined]]
[[Superscalar]]

Execution of an instruction in several steps: microoperations

1. Fetch: Fetch the instruction from memory
2. Decode: What instruction is this?
3. Decode: Place numbers to be added i the correct registers
4. Execute: Add the numbers
5. Execute: Store the result in a register

[[Out-of-order execution]]
[[Speculative execution]]

## 2. HyperThreading/SMT

![[smt-hyperthreading.png]]

Evolution of superscalar architecture.
The concept is often called "Virtual core"
Intel Core i7 2640M is two-core processor with hyperthreading. It has four threads that make OS think that it has four CPUs.

