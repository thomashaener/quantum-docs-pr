---
title: Introduction to the Quantum Numerics Package | Microsoft Docs
description: Introduction to the Quantum Numerics Package
author: thomashaener
ms.author: thhaner
ms.date: 3/29/2019
ms.topic: article
uid: microsoft.quantum.numerics.intro
---

# Introduction

Many quantum algorithms rely on oracles that evaluate mathematical functions on a superposition of inputs.
The main component of Shor's algorithm, for example, evaluates $f(x) = a^x\operatorname{mod} N$ for a fixed $a$, the number to factor $N$, and $x$ a $2n$-qubit integer in a uniform superposition over all $2n$-bit strings.

To run Shor's algorithm on an actual quantum computer, this function has to be written in terms of the native operations of the target machine.
Using the binary representation of $x$ with $x_i$ denoting the $i$-th bit counting from the least-significant bit, $f(x)$ can be written as $f(x) = a^{\sum_{i=0}^{2n-1} x_i 2^i} \operatorname{mod} N$.
In turn, this can be written as a product (mod N) of terms $a^{2^i x_i}=(a^{2^i})^{x_i}$. The function $f(x)$ can thus be implemented using a sequence of $2n$ (modular) multiplications by $a^{2^i}$ conditional on $x_i$ being nonzero. The constants $a^{2^i}$ can be precomputed and reduced modulo N before running the algorithm.

Similarly, this sequence of controlled modular multiplications can be written: Each such multiplication can be performed using a sequence of $n$ controlled modular additions; and each modular addition can be built from a regular addition and a comparator.


Given that so many steps are necessary to arrive at an actual implementation, it would be extremely helpful to have such functionality available from the start. This is why we decided to add support for a wide range of numerics functionality to the QDK.


# Functionality

Besides the integer arithmetic mentioned thus far, the Numerics Library provides

 - (Un)signed integer functionality (multiply, square, division with remainder, inversion, ...) with one or two quantum integer numbers as input
 - Fixed-point functionality (add / subtract, multiply, square, 1/x, polynomial evaluation) with one or two quantum fixed-point numbers as input

