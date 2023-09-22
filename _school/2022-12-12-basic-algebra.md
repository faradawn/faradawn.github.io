---
title: "MATH 25400: Basic Algebra"
layout: post
mathjax: true
---

# Chapter 7: Rings

## 7.1 Basic Definition and Examples
- Def (Ring)
    1. addition $(R, +)$ is an abelian group
    2. multiplication is associative
    3. distributive
- Def (Subring)
    1. under addition is a subgroup of $R$
    2. closed under multiplication

- Def (Commutative Ring): multiplication is commutative
- Def (Division Ring): A ring with 1, and every nonzero element $a \in R$ has $ab = ba = 1$.
- Def (Field): A commutative division ring. 

Other definitions:

- Def (Zero Divisor): A nonzero element $a$ with $ab = 0$ or $ba = 0$.
- Def (Unit): An element $u$ with $uv = vu = 1$. Assume $R$ has 1. 
- Def (Integral Domain) A commutative ring with 1 and with no zero divisors. (非零交换幺环)
- Cor (Any Finite Integral Domain is a Field).


## 7.3 Ring Homomorphisms and Quotient Rings
- Def (Ring Homomorphism): For any $r_1, r_2 \in R$
    1. $\varphi(r_1 + r_2) = \varphi(r_1) + \varphi(r_2)$
    2. $\varphi(r_1 r_2) = \varphi(r_1) \varphi(r_2) $
    3. If ring homorphism, $\varphi(1_R) = 1_S$
- Prop
    1. $ker\varphi$ is subring and ideal.
    2. $Im\varphi$ is subring.
- Def (Ideal)
    1. $I$ is a subring of $R$
    2. $rI \subset I$ for all $r \in R$
- Def (Quotient Ring)
    1. addition: $(r + I) + (s + I) = (r+s) + I$
    2. multiplication: $(r + I) \cdot (s + I) = (rs) + I$
- Thm (First Isomorphism Theorem for Rings)
    1. If $\varphi$ is a ring homomorphism, then $R / ker\varphi \cong \varphi(R) $
    2. If $I$ is an ideal of $R$, then $r \mapsto r + I$ is a surjective homomorphism with kernel $I$. 

- Def (Combination of Ideals)
    1. $I + J = \{a_i + b_i \mid a_i \in I, b_i \in J \}$ 
    2. $IJ = \{a_1 b_2 + a_2 b_2 + \cdots + a_n b_n \mid a_i \in I, b_i \in J\}$
    3. $I^n = \{ a_1 a_2 \cdots a_n \mid a_i \in I \} $
- Prop
    1. $I + J$, $IJ$, and $I \cap J $ are ideals
    1. $IJ \subset I \cap J \subset I + J $

## 7.4 Properties of Ideals
- Def (Maximal Ideal): No other ideals contains $I$. 
- Def (Prime Ideal): $ab \in P$ implies either $a \in I$ or $b \in I$. Assume $R$ is commutative.
- Prop
    1. $I$ is a prime ideal if and only if $R/I$ us an integral domain.
    2. $I$ is a maximal ideal if and only if 