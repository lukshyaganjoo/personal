---
layout: page
title: proofs
---

[so i gave a theory talk](#so-i-gave-a-theory-talk)

# so i gave a theory talk

## notation and some motivation
### notation:
Before I get to some of the really cool motivation for this problem, I wanna make sure that everyone here is familiar with the the kinds of graphs we'll be working with in the domain of this proof. 

![petersen graph](images/Petersen1_tiny.png)
This is the Petersen graph. Veteran graph theoreticians will be familiar with this pentagram inscribed within the spokes of a regular pentagon. The Petersen graph is used as a counter example in tons of graph theory proofs which is one of the reasons it's so well studied, partly what we'll be doing here. The Petersen graph has $10$ nodes and $15$ edges, and is what we call $3$-regular. 

**Note:** A graph is said to be $d$-regular $iff$ every vertex has the same degree $d$. (i.e. it is strongly regular)

![complete graph](images/full.png)

This is the complete graph on $10$ vertices. For the sake of convenience, we will refer to this graph as $K_{10}$. It has $10$ nodes and $45$ edges (i.e., all possible edges among $10$ nodes). If we follow along from the same scheme of defining things, the number of edges in $K_{n}$ (the complete graph with $n$ vertices) is given by $\binom{n}{2}$. 

In this proof, $J_{n}$ refers to the all ones matrix with dimension/size $n * n$

**adjacency matrices:** 

We define the adjacency matrix of a graph $G = (V, E)$ as the following,

$$  
A_{i, j} = \begin{cases}
                1 & \text{there is an edge from} \; j \; \text{to} \; i\\
                0 & \text{there is no edge from} \; j \; \text{to} \; i\\
            \end{cases}
$$

Since we're dealing with an undirected graph in this proof, every edge $ab$ is counted as the same edge as if there were an edge $ba$ in the graph. As a consequence, the adjacency matrices for this family of graphs will be symmetric. 

The way to think about it is that the adjacency matrix of a graph $G$ encodes information about the number of length $1$ paths between any pair of vertices $i$ and $j$, i.e. information about the vertices immediately "adjacent" to each other.

### motivation:
Each node in $K_{10}$ has $9$ edges incident to it while each node in the Petersen graph has $3$ edges incident to it. So it is plausible that $K_{10}$ can be covered perfectly by $3$ Petersen graphs. This means that you can lay down three Petersens on $K_{10}$ so that vertices go to vertices and each edge of $K_{10}$ lies under an edge of exactly one of the three Petersens. This hints at some pretty cutting-edge stuff in the field of graph decomposition and graph coloring and the parallels in higher dimensions is absolutely incredible. With some linear algebra at our disposal, we will show that it is not possible to completely cover $K_{10}$ with three Petersen graphs.

## eigenvalues of the petersen graph

Finding the eigenvalues of any matrix, let alone one that of size $10 * 10$ is a fairly computational task and isn't enlightening in any form whatsoever. So why are we trying to find the eigenvalues of the petersen graph? Well we can take advantage of the fact that the adjacency matrix represents information that carries physical meaning (vertex-edge relations of a graph) and can use the language of linear transformations and some geometric intuition to gain insight into the eigenvalues of this graph.

Let $A$ be the adjacency matrix of the Petersen Graph. If $A$ encodes information about the number of length $1$, $A^2$ represents information about the number of length $2$ paths, and in general, $A^k$ encodes information about the number of $k$-length paths in a given graph. With this information in our belt, we know can make a pretty nifty observation. 

Consider the $i, j^{th}$ entry of the matrix $A^2 + A$ (the sum of the matrices representing information about the number of length $2$ paths and the regular adjacency matrix of the petersen graph). Since, every vertex in the petersen graph has degree $3$, each vertex has $3$ length $2$ paths back itself whereas there are no length $1$ paths from a vertex to itself. With this information under our belt, we can say that 

$$
(A^2 + A)_{i, j} = 
\begin{cases}
3 & \forall i = j \\
1 & \forall i \neq j
\end{cases}
$$

This follows from noticing that any pair of vertices not already joined by an edge are joined by a unique path of length $2$; namely there is a unique vertex which is joined to both. 

We can therefore conclude that the matrix $A$ satisfies the matrix equation $A^2 + A = 2I + J$. 

Note that $J$ has eigenvalue 10 (of multiplicity 1 with eigenvector 1) and eigenvalue 0 of multiplicity 9. Thus $2I + J$ has eigenvalue 12 of multiplicity 1 and eigenvalue 2 of multiplicity 9. Now if $x$ is an eigenvector of A of eigenvalue $\lambda$ then $x$ is an eigenvector of $A^2 + A$ of eigenvalue $\lambda^2 + \lambda$. 

Thus the possible eigenvectors for $A$ are prescribed. We already know that $\mathbf{1}$ is an eigenvector of $A$ of eigenvalue 3 (or at least it is easy to check). The other 9 eigenvalues must satisfy $\lambda^2 + \lambda = 2$ thus either 1 or -2 with total multiplicity being 9. Now the trace of $A$, which is 0, is the sum of the eigenvalues and so we deduce that 1 has multiplicity 5 and -2 has multiplicity 4.

## the actual proof
**Lemma:** $K_{10} = J_{10} - I_{10}$  
The adjacency matrix of $K_{10}$ has all but its diagonal entries being equal to $1$, since
every node in the full graph is connected to every other node except itself. The diagonal entries of $K_{10}$ are filled in with $0$'s since there is no path from any of the nodes to itself. One can also clearly see that the matrix described by the equation $J_{10} - I_{10}$ where $J_{10}$ is the matrix with all its entries being equal to $1$, is a matrix that has all but its diagonal entries being equal to $1$ and its diagonal entries being equal to $0$. 

Therefore the adjacency matrix of $K_{10} = J_{10} - I_{10}$

**Assumption:** $A_P + A_Q + A_R = J_{10} - I_{10}$

We consider three permutation matrices of the Petersen Graph $A_P, A_Q$ and $A_R$ (matrices formed by simultaneous row and column swaps in the original adjacency matrix of the petersen graph). We construct each of these permutation matrices such that $A_Q = CAC^{-1}$ where $C$ is some matrix. By this construction, $A_Q$ and $A$ are similar, and an important consequence is that they have the same eigenvalues. This assumption and construction is true for $A_P$ and $A_R$. 

**Lemma** $\text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$   
We wish to show that $1^{T} = y^{T}(A_P - I_{10})$ for some vector $y \in R^{10}$. Consider $y = 1^{T}$. The matrix product $1^{T}(A_P - I_{10})$ yields the vector whose entries are the sum of the entries of the columns of $A_P - I_{10}$. for an arbitrary column $i$ in its adjacency matrix, by the way the Petersen graph was defined we know that he graph has 3 outgoing edges which means that the sum of the entries of a column in its adjacency matrix is 3. However note that the diagonal entries of the adjacency matrix will be 0 since the Petersen graph does not contain self-loops. After subtracting the $i$th column of $I_{10}$, the sum of the columns of the matrix $A_P - I_{10}$ is 2. Note that the identity matrix has 0 in every entry where $i \neq j$. Since the above holds true for an arbitrary column of the matrix, We can conclude that every column of $A_P - I_{10}$ sums up to a 2. More fundamentally, the product $1^{T}(A_{P} - I_{10})$ generates the all twos
vector or 2$1^{T}$. 

Therefore we can assert that $\text{Span}(1) \subseteq \text{Row} (A_P - I_{10})$.

**side proof**  
Let $A$ and $B$ be two subspaces such that $A \subseteq B$.  
**claim** $B^{\perp} \subseteq A^{\perp}$  
**proof** Let $x$ be an arbitrary vector such that $x \in B^{\perp}$. By definition of the orthogonal complement, we have that $\forall v \in B, x^{T}v = 0$, i.e. they are orthogonal. However we know that any vector contained in $B$ will be a vector contained in $A$, ($A$ is a subset of the vectors contained in $B$). Therefore we can reframe the above statement to be $\forall v \in A, x^{T}v = 0$, that is $x$ is orthogonal to every vector in $A$. By definition, this means that $x \in A^{\perp}$

$\therefore A \subseteq B \rightarrow B^{\perp} \subseteq A^{\perp}$

Using the aforementioned proof and taking orthogonal complements, we have that $\text{Span}(1) \subseteq \text{Row} (A_P - I_{10}) \rightarrow \text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$.

$\therefore \text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$

The above results are also true for $A_Q - I_{10}$ since $Q$ is also a Petersen graph. 

**Lemma** $\text{Null} (A_P - I_{10}) \cap \text{Null} (A_Q - I_{10}) \neq \{0\}$  

**proof**  
For two subspaces $R_1$ and $R_2$ of $\mathbb{R}^{9}$, if $S_1 \cap S_2 = \{0\}$, then $B_{S_1}$ and $B_{S_2}$ are linearly independent.  
We therefore prove by contrapositive. 

We also know that  
$\text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$  
$\text{Null} (A_Q - I_{10}) \subseteq \text{Span} (1)^{\perp}$.  
$B_{ \text{Null} (A_P - I_{10}) } \cup B_{\text{Null} (A_Q - I_{10})}$ has 10 vectors in $R^{9}$ since the bases of each of the null spaces has 5 vectors. Therefore $B_{ \text{Null} (A_P - I_{10}) } \cup B_{\text{Null} (A_Q - I_{10})}$ must be linearly dependent (since they have more vectors than the dimension of the space they exist in).

Therefore $B_{S_1} \cap B_{S_2} \neq \{0\}$ where $S_1$ and $S_2$ refer to the two subspaces above. This implies the existence of a non-zero vector $w$ that exists in their intersection. 

The larger consequence of this is that this vector $w$ is orthogonal to the all ones vector, i.e. ${\bf 1}^{T}w = 0$

## the final stages

$$
\begin{align*}
    &\
    A_P(v) = \lambda v \\
    &\
    A_P(v) = v &&\text{Since 1 is an eigenvalue of $A_P$} \\
    &\
    A_R(w) = J_{10}(w) - I_{10} (w) - A_P(w) - A_Q(w) &&\text{Using the formula above}\\
    &\
    A_R(w) = J_{10}(w) - w - w - w &&\text{Substituting values}
\end{align*}
$$

We now compute $J_{10} (w)$ where $w \in \text{Null} (A_P - I_{10})$  

$$ J_{10}w = \begin{bmatrix}
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1
\end{bmatrix} w = \begin{bmatrix} 1^{T} \\
    1^{T} \\
    1^{T} \\
    1^{T} \\
    1^{T} \\
    1^{T} \\
    1^{T} \\
    1^{T} \\
    1^{T} \\
    1^{T} \end{bmatrix}w = 
    \begin{bmatrix}
    1^{T}w \\
    1^{T}w \\
    1^{T}w \\
    1^{T}w \\
    1^{T}w \\
    1^{T}w \\
    1^{T}w \\
    1^{T}w \\
    1^{T}w \\
    1^{T}w 
\end{bmatrix} = 
\begin{bmatrix}
    0 \\
    0 \\
    0 \\
    0 \\
    0 \\
    0 \\
    0 \\
    0 \\
    0 \\
    0
\end{bmatrix} $$

$\therefore$ $A_R(w) = J_{10}(w) - w - w - w = -3w$.

We have therefore arrived at a contradiction. In the beginning of the proof, we found all the eigenvalues of the Petersen Graph and concluded that -3 was not amongst that list. However as we can see, we have proved that -3 in fact is an eigenvalue for the adjacency matrix of a Petersen graph. Therefore it is not possible to cover the full graph or $K_{10}$ with 3 Petersen graphs. 

<script type="text/javascript" async
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
