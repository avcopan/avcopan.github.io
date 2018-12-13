---
layout: post
title: 'Notes: The Moore-Penrose Pseudoinverse'
date: '2017-07-07 19:47:05'
excerpt_separator: <!--more-->
categories: technical
---


*Notes on the Moore-Penrose pseudoinverse, building on my
[previous post about SVD]({{site.url}}/blog/2017/07/06/svd.html).*
<!--more-->
*The most common application of this concept is
[ordinary least squares regression](https://en.wikipedia.org/wiki/Ordinary_least_squares),
which attempts to model a data series with a linear equation.
The challenge is that real-world data rarely if ever fits a perfect line, so an
exact solution is impossible.
As we show in Claim 3, the Moore-Penrose pseudoinverse gets us as close as
possible to an exact solution by minimizing the squares of our prediction errors.*

**Definition 1.**
Two complex matrices
\\(
    \mathbf{M}
\\)
and
\\(
    \mathbf{M}^+
\\)
are *Moore-Penrose pseudoinverses* of each other if they are mutual weak inverses[^footnote1]
with Hermitian left and right products.[^footnote2]
These four conditions are the *Moore-Penrose criteria*.


Showing how to construct a pseudoinverse, let's show why this definition really does construct something kind of like an inverse.
Let's denote the left and right products by
\\(
    \mathbf{P}
\equiv
    \mathbf{M}\mathbf{M}^+
\\)
and
\\(
    \mathbf{Q}
\equiv
    \mathbf{M}^+\mathbf{M}
\\).
We will show that these matrices are [orthogonal projections](https://en.wikipedia.org/wiki/Projection_(linear_algebra)#Orthogonal_projections)
onto the column and row spaces of the transformation.


#### Claim 1. \\(\mathbf{P}\\) is an orthogonal projection onto the column space of \\(\mathbf{M}\\).

Proof:
The Moore-Penrose Hermiticity criteria require that
\\(
    \mathbf{P}
=
    \mathbf{P}^\dagger
\\)
and weak inversion implies
\\(
    \mathbf{P}^2
=
    \mathbf{P}
\\),
confirming that this is an orthogonal projection.
Furthermore, since this projection is a right product of
\\(
    \mathbf{M}
\\),
its column space is a subspace of this matrix.
Conversely, note that every
\\(
    \mathbf{v}
\\)
in
\\(
    \mathbf{M}
\\)'s
column space has the form
\\(
    \mathbf{M}
    \mathbf{w}
\\)
and therefore
\\[
    \mathbf{P}
    \mathbf{v}
=
    \mathbf{M}
    \mathbf{M}^+
    \mathbf{M}
    \mathbf{w}
=
    \mathbf{M}
    \mathbf{w}
=
    \mathbf{v}
\\]
by weak inversion, which makes their column spaces equal.


#### **Claim 2.** \\(\mathbf{Q}\\) is an orthogonal projection onto the row space of \\(\mathbf{M}\\).

This proof is similar to the one for claim 1.


How do these properties make our pseudoinverse inverse-like?
Suppose the transformation is square and its column space covers the
whole codomain.  Then this matrix is invertible and we have
\\(
    \mathbf{P}
=
    \mathbf{1}
\\),
which says that the pseudoinverse is the true inverse.

More generally, we can show that
\\(
    \mathbf{x}
\approx
    \mathbf{x}\_\circ
\equiv
    \mathbf{M}^+
    \mathbf{b}
\\)
is always the nearest possible solution to the linear equation
\\(
    \mathbf{M}
    \mathbf{x}
=
    \mathbf{b}
\\).
If only one solution exists, this is it.
If multiple solutions exist, this is one of them.
If no solutions exist, this is as close as you can get.



#### **Claim 3.**  \\(\mathbf{x}\_\circ=\underset{\mathbf{x}}{\arg\min}\,\|\mathbf{M}\mathbf{x}-\mathbf{b}\|^2\\)

Proof:
Claim 1 implies that
\\(
    \mathbf{M}
    \mathbf{x}\_\circ
=
    \mathbf{P}
    \mathbf{b}
\\)
is the component of
\\(
    \mathbf{b}
\\)
in the column space, which puts
\\(
    \mathbf{M}
    \mathbf{x}\_\circ
-
    \mathbf{b}
\\)
[in the left null space](https://en.wikipedia.org/wiki/Row_and_column_spaces#Relation_to_the_left_null_space).
Now consider an arbitrary trial vector of the form
\\(
    \mathbf{x}
=
    \mathbf{x}\_\circ
+
    \mathbf{d}
\\)
and note the following orthogonality relationship.
\\[
    \langle
        \mathbf{M}
        \mathbf{d}
    ,
        \mathbf{M}
        \mathbf{x}\_\circ
    -
        \mathbf{b}
    \rangle
=
    \mathbf{d}^\dagger
    \mathbf{M}^\dagger
    (
        \mathbf{M}
        \mathbf{x}\_\circ
    -
        \mathbf{b}
    )
=
    0
\\]
By the Pythagorean theorem, we have that
\\[
    \|
        \mathbf{M}
        \mathbf{x}
    -
        \mathbf{b}
    \|^2
=
    \|
        \mathbf{M}
        \mathbf{x}\_\circ
    -
        \mathbf{b}
    +
        \mathbf{M}
        \mathbf{d}
    \|^2
=
    \|
        \mathbf{M}
        \mathbf{x}\_\circ
    -
        \mathbf{b}
    \|^2
+
    \|
        \mathbf{M}
        \mathbf{d}
    \|^2
\\]
which shows that
\\(
    \mathbf{x}
\\)
has a greater error than
\\(
    \mathbf{x}\_\circ
\\).

To conclude our brief survey, we will prove that every complex matrix has a
Moore-Penrose pseudoinverse.
As a bonus, our existence proof will provide us with a simple formula for
computing the pseudoinverse of a matrix from its [SVD]({{site.url}}/blog/2017/07/06/svd.html).

Let
\\(
    \boldsymbol\Sigma
\\)
be a tall matrix of the form
\\(
    \begin{pmatrix}
        \mathbf{S}\\\
        \mathbf{0}
    \end{pmatrix}
\\)
where
\\(
    \mathbf{S}
\\)
is square and diagonal.


#### **Lemma 1.** \\(\boldsymbol\Sigma^+=(\mathbf{S}^+\ \mathbf{0})\\), where \\(\mathbf{S}^+\\) inverts the nonzero diagonals of \\(\mathbf{S}\\).

Proof:
That
\\(
    \mathbf{S}^+
\\)
satisfies the Moore-Penrose criteria follows immediately from considering its
diagonal elements.
Straightforward block matrix algebra then shows that, for example,
\\[
    \boldsymbol\Sigma^+
    \boldsymbol\Sigma
    \boldsymbol\Sigma^+
=
    \begin{pmatrix}
        \mathbf{S}^+
        \mathbf{S}
        \mathbf{S}^+
    &
        \mathbf{0}
    \end{pmatrix}
=
    \begin{pmatrix}
        \mathbf{S}^+
    &
        \mathbf{0}
    \end{pmatrix}
=
    \boldsymbol\Sigma^+
\\]
and the remaining criteria are confirmed similarly.



#### **Claim 4.** Every complex matrix has a Moore-Penrose pseudoinverse.

Proof:
We define the pseudoinverse of
\\(
    \mathbf{M}
\\)
from its singular value decomposition[^footnote4] as
\\(
    \mathbf{M}^+
\equiv
    \mathbf{V}
    \boldsymbol\Sigma^+
    \mathbf{U}^\dagger
\\).
Lemma 1 shows that
\\(
    \boldsymbol\Sigma^+
\\)
exists and straightforward algebra confirms that the Moore-Penrose criteria are satisfied.


[^footnote1]: \\(\mathbf{M}^+\\) is a weak inverse of \\(\mathbf{M}\\) if \\(\mathbf{M}\mathbf{M}^+\mathbf{M}=\mathbf{M}\\).

[^footnote2]: By which I mean \\( \mathbf{M}\mathbf{M}^+ \\) and \\( \mathbf{M}^+\mathbf{M} \\).

[^footnote4]: \\( \mathbf{M} = \mathbf{U} \boldsymbol\Sigma \mathbf{V}^\dagger \\) 
