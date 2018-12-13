---
layout: post
title: 'Notes: Probability Theory'
date: '2017-08-30 13:21:25'
excerpt_separator: <!--more-->
categories: technical
---

*As part one of a series on probability theory, here are some notes on
the Kolmogorov axioms*<!--more-->*, which boil probability theory down to
four simple rules.
I learned most of this from Rozanov's
[short and readable text](https://www.amazon.com/Probability-Theory-Concise-Course-Mathematics/dp/0486635449).
To provide context I start with the mathematical theory of set functions, called
"measure theory", before turning to the axioms and their consequences.*

For starters, let
\\(
    2^\Omega
\\)
be the power set whose universal set is
\\(
    \Omega
\\).


**Definition 1.**
A collection of sets
\\(
    \mathcal{F}
\subseteq
    2^\Omega
\\)
qualifies as a
*sigma algebra*
if it contains the null set as well as all possible complements and countable
unions of its members.


#### Claim 1. \\(\mathcal{F}\\) contains all countable intersections of its members.

Proof:
This follows from de Morgan's laws.


**Definition 2.**
A non-negative real-valued function on a sigma algebra,
\\(
    \mu
:
    \mathcal{F}
\rightarrow
    \mathbb{R}^+
\\),
qualifies as a
*measure*
when it is additive over countable disjoint unions ("sigma additive") and
vanishes on the null set.

Pairing a set with one of its sigma algebras constitutes a
*measurable space*.
From there, picking a specific measure completes a
*measure space*.
Our definition of measure is actually slightly too restrictive in the sense that
measures can be infinite-valued as well as real-valued.
Finite-valued measures are special in that they can be normalized to make
probability spaces.


**Definition 3.**
A
*probability space*
is a measure space whose universal set has measure 1.


In the terminology of probability theory the universal set is called the
*sample space*.
The sample space contains all possible *outcomes*
\\(
    \omega
\in
    \Omega
\\)
of an experiment.
Subsets of the sample space are called
*events*
and the collection of events
\\(
    A
\in
    \mathcal{F}
\\)
in question forms the sigma algebra of our probability space.
Pairwise disjoint series of events are termed
*mutually exclusive*.

The measure on a probability space is denoted by
\\(
    \mathrm{P}
\\).
This associates a
*probability*
\\(
    \mathrm{P}(A)
\\)
with each event
\\(
    A \in \mathcal{F}
\\),
representing the likelihood of observing
\\(
    \omega
\in
    A
\\)
as an outcome of our experiment.
For example, a typical event in a continuous-outcome experiment would be an
interval on the number line.
Its probability is likelihood that our next measurement falls within this
interval.

The following example illustrates these concepts by enumerating all possible
probability spaces for a discrete binary experiment, termed a
*Bernoulli trial*.


**Example.**
Consider a single-coin-toss experiment where the sample space is
\\(
    \Omega
=
    \\{\mathrm{H}, \mathrm{T}\\}
\\),
heads or tails.
The simplest sigma algebra on this set is the trivial one,
\\(
    \mathcal{F}\_\mathrm{t}
=
    \\{\varnothing, \Omega\\}
\\),
and the only other one possible is
\\(
    \mathcal{F}\_\mathrm{n}
=
    \\{\varnothing, \\{\mathrm{H}\\}, \\{\mathrm{T}\\}, \Omega\\}
\\).
In either case, we have
\\(
    \mathrm{P}(\varnothing)
=
    0
\\)
and
\\(
    \mathrm{P}(\Omega)
=
    1
\\)
by definition.
By sigma additivity, the remaining probabilities in
\\(
    \mathcal{F}\_\mathrm{n}
\\)
are characterized by the following relationship
\\[
    \mathrm{P}(\\{\mathrm{H}\\})
+
    \mathrm{P}(\\{\mathrm{T}\\})
=
    1
\\]
since the union of these events is
\\(
    \Omega
\\).
Therefore, we can define a continuous series of probability spaces by setting
\\(
    \mathrm{P}(\\{\mathrm{H}\\})
:=
    \varphi
\\)
and
\\(
    \mathrm{P}(\\{\mathrm{T}\\})
:=
    1
-
    \varphi
\\)
for any
\\(
    \varphi
\\)
on the unit interval.
In a fair coin-toss experiment we have the additional constraint that
\\(
    \\{\mathrm{H}\\}
\\)
and
\\(
    \\{\mathrm{T}\\}
\\)
must have equal probabilities, requiring
\\(
    \varphi
=
    \frac{1}{2}
\\).


Combining definitions 2 and 3,[^footnote1]
the probability measure is characterized by three properties.
1. *non-negativity*:
\\(
    \mathrm{P}(A)
\geq
    0
\\)

2. *unitarity*:
\\(
    \mathrm{P}(\Omega)
=
    1
\\)

3. *sigma additivity*:
\\(
    \mathrm{P}(\bigcup_i A_i)
=
    \sum_i
    \mathrm{P}(A_i)
\\)
for mutually exclusive
\\(
    A_i
\\)'s.

These are the *Kolmogorov axioms*, which form the basis for modern probability
theory.
The series of proofs at the end of this post should give you a sense of how they
can be used to derive results in probability theory.


**Definition 4.**
The probability of an intersection
\\(
    \mathrm{P}(A\cap B)
\\)
is called the
*joint probability* of \\(A\\) and \\(B\\).


**Definition 5.**
The
*conditional probability*
of
\\(
    A
\\)
given
\\(
    B
\\)
is defined as follows.
\\[
    \mathrm{P}(A\,|\,B)
\equiv
    \mathrm{P}(A \cap B) /
    \mathrm{P}(B)
\\]


Intuitively, a joint probability represents the likelihood that an outcome
satisfies two events simultaneously, prior to any additional information,
whereas a conditional probability is the likelihood that an outcome falls under
one event after being informed that it satisfies another.
In the second case, the additional information restricts the space of possible
outcomes to those contained in the conditional event.
To see why our formula works, suppose we have been told that
\\(
    \omega \in B
\\)
and wish to know the likelihood that
\\(
    \omega
\\)
is in
\\(
    A
\\)
too.
Given the information, we can restrict ourselves to the case when
\\(
    A
\\)
is a subset of
\\(
    B
\\),
which simplifies our formula to
\\(
    \mathrm{P}(A\,|\,B)
\equiv
    \mathrm{P}(A) / \mathrm{P}(B)
\\).
We see that this is our original measure, renormalized with respect to
\\(
    B
\\).
The next two results formalize this notion of "restricting" the probability
space.


#### Claim 2. \\( \mathcal{F}|\_B \equiv \\{ A \cap B \,|\, A \in \mathcal{F} \\} \\) forms a sigma algebra on \\( B \\).

Proof:
It inherits the null set via
\\(
    \varnothing \cap B
=
    \varnothing
\\).
Closure under complementation follows from
\\(
    \bar{A} \cap B
=
    \bar{A}|\_B
\\).[^footnote2]
The distributive property of intersections ensures closure under countable
unions.



#### Claim 3. \\(P(\,\cdot\,|\,B)\\) is a probability measure on \\(\mathcal{F}|\_B\\).

Proof:
On its domain this function is proportional to
\\(
    \mathrm{P}
\\),
so non-negativity and sigma additivity are inherited.
The proportionality constant ensures that
\\(
    \mathrm{P}(B\,|\,B)
=
    1
\\),
so unitarity is also satisfied.


**Definition 6.**
Events
\\(
    A
\\)
and
\\(
    B
\\)
are
*independent*
if the probability of one is unaffected by information about the other,
i.e.
\\(
    \mathrm{P}(A\,|\,B)
=
    \mathrm{P}(A)
\\).
A series of events is considered *mutually indepent* if each one is independent
from all possible intersections of its companions.

### Complements.

#### Claim 4. \\( \mathrm{P}(\bar{A}) = 1 - \mathrm{P}(A) \\)

Proof:
This follows from substituting
\\(
    \Omega
=
    \bar{A}
\cup
    A
\\)
into the unitarity axiom and using sigma additivity.


### Unions.


#### Claim 5. \\( \mathrm{P}(A\cup B) = \mathrm{P}(A) + \mathrm{P}(B) - \mathrm{P}(A\cap B) \\)

Proof:
This follows from using sigma additivity on the probabilities of
\\(
    (A \cup B)
=
    A
\cup
    (B \setminus A)
\\)
and
\\(
    B
=
    (B \setminus A)
\cup
    (A \cap B)
\\).



#### Claim 6. \\( \mathrm{P}(A_1 \cup \cdots \cup A_n) = {\displaystyle \sum\_{k=1}^n \sum\_{i_1<\cdots<i_k} (-)^k\, \mathrm{P}(A_{i_1} \cap \cdots \cap A_{i_k}) } \\)

Proof:
For
\\(
    n = 2
\\)
this is claim 5.
For the general case claim 5 gives
\\[
    \mathrm{P}(A_1 \cup \cdots \cup A_{n-1})
+
    \mathrm{P}(A_n)
-
    \mathrm{P}((A_1 \cup \cdots \cup A_{n-1}) \cap A_n)\,\,.
\\]
Proceeding by induction, assume the proposition holds for
\\(
    n-1
\\)
and expand the first term.
After distributing the intersection, expand the third term as well.
Substituting these into our expression completes the proof.


### Intersections.

#### Claim 7.  *Product rule*. \\( \mathrm{P}(A \cap B) = \mathrm{P}(A\,|\,B) \mathrm{P}(B) \\)

Proof:
This follows from the definition of conditional probability.



#### Corollary 1.  *Chain rule*. \\({\displaystyle \mathrm{P}(A_1 \cap \cdots \cap A_n) = \prod\_{i=1}^n \mathrm{P}(A_i\,|\bigcap\_{j<i} A_j) }\\)

Proof:
This follows from repeated use of the product rule.



#### Corollary 2. \\( {\displaystyle \mathrm{P}(A_1 \cap \cdots \cap A_n) = \prod\_{i=1}^n \mathrm{P}(A_i)} \\) if mutually independent.


### Bayes' rule!

Here let
\\(
    \\{B_i\\}_{i=1}^n
\\)
be mutually exclusive events that cover the sample space.


#### Theorem 1.  *Law of total probability*. \\( {\displaystyle \mathrm{P}(A) = \sum\_{i=1}^n \mathrm{P}(A\,|\,B_i) \mathrm{P}(B_i) } \\)

Proof:
Expand
\\(
    \mathrm{P}(A)
\\)
as follows and then use the product rule.
\\[
{\displaystyle
    \mathrm{P}(A \cap (B_1 \cup \cdots \cup B_n))
=
    \sum_{i=1}^n
    \mathrm{P}(A \cap B_i)
}
\\]



#### Theorem 2.  *Bayes' rule I*. \\( \mathrm{P}(B\,|\,A) = \dfrac{     \mathrm{P}(A\,|\,B)     \mathrm{P}(B) }{     \mathrm{P}(A) } \\)

Proof:
This follows from the definition of conditional probability and the symmetry of
intersections.



#### Corollary 3 *Bayes' rule II*. \\( {\displaystyle \mathrm{P}(B_i\,|\,A) = \frac{\mathrm{P}(A\,|\,B_i) \mathrm{P}(B_i)}{\sum_j \mathrm{P}(A\,|\,B_j) \mathrm{P}(B_j) } } \\)




##### Footnotes:

[^footnote1]:  \\( P(\varnothing) = 0 \\) follows from sigma additivity over \\( \Omega = \Omega \cup \varnothing \\)
[^footnote2]:  \\(\bar{A}\\) denotes \\( \Omega \setminus A\\) and \\( \bar{A}\|\_B \\) denotes \\( B \setminus A \\)
