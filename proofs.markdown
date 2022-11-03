---
layout: page
title: proofs
---

- [so i gave a theory talk](#so-i-gave-a-theory-talk)  
- [cauchy schwarz and beyond](#cauchy-schwarz-and-beyond)

# so i gave a theory talk

## notation and some motivation
### notation:
Before I get to some of the really cool motivation for this problem, I wanna make sure that everyone here is familiar with the the kinds of graphs we'll be working with in the domain of this proof. 

![petersen graph](images/Petersen1_tiny.png)
This is the Petersen graph. Veteran graph theoreticians will be familiar with this pentagram inscribed within the spokes of a regular pentagon. The Petersen graph is used as a counter example in tons of graph theory proofs which is one of the reasons it's so well studied, partly what we'll be doing here. The Petersen graph has $$10$$ nodes and $$15$$ edges, and is what we call $$3$$-regular. 

**Note:** A graph is said to be $$d$$-regular $$iff$$ every vertex has the same degree $$d$$. (i.e. it is strongly regular)

![complete graph](images/full.png)

This is the complete graph on $$10$$ vertices. For the sake of convenience, we will refer to this graph as $$K_{10}$$. It has $$10$$ nodes and $$45$$ edges (i.e., all possible edges among $$10$$ nodes). If we follow along from the same scheme of defining things, the number of edges in $$K_{n}$$ (the complete graph with $$n$$ vertices) is given by $$\binom{n}{2}$$. 

In this proof, $$J_{n}$$ refers to the all ones matrix with dimension/size $$n * n$$.

The row space of a matrix $$A$$ is defined as follows, $$\text{Row}(A) = \{y^T A : y \in \mathbb{R}^{n}\}$$

**lemma** Trace($$A$$) = $$\sum_{x \in E_{x}(A)}^{} \lambda_{x}$$

**lemma** For a symmetric matrix $$A$$, eigenvectors corresponding to *distinct*
eigenvalues are orthogonal 

**proof**  
Let $$x$$ and $$y$$ be eigenvectors of the matrix $$A$$ corresponding to eigenvalues 
$$\lambda_1$$ and $$\lambda_2$$ respectively. Therefore we have that 

$$ \begin{align*}
&\
Ax = \lambda_1 x \\
&\
Ay = \lambda_2 y \\
&\
y^{T} Ax = y^{T} \lambda_1 x &&\text{Multiplying the first equation with $y^T$} \\
&\
y^T A^T x = y^{T} \lambda_1 x &&\text{$A = A^T$} \\
&\
(Ay)^{T} x = \lambda_1 y^{T} x \\
&\
(\lambda_2 y)^T x = \lambda_1 y^{T} x \\ 
&\
\lambda_2 y^{T} x = \lambda_1 y^{T} x \\ 
&\
y^{T} x (\lambda_2 - \lambda_1) = 0
\end{align*} $$

However, we already know that $$\lambda_2 \neq \lambda_1$$. Therefore 
$$\lambda_2 - \lambda_1 \neq 0$$, and it must be the case that $$y^{T}x = 0$$. 

Therefore $$x$$ and $$y$$ are orthogonal.

**adjacency matrices:** 

We define the adjacency matrix of a graph $$G = (V, E)$$ as the following,

$$  
A_{i, j} = \begin{cases}
                1 & \text{there is an edge from} \; j \; \text{to} \; i\\
                0 & \text{there is no edge from} \; j \; \text{to} \; i\\
            \end{cases}
$$

Since we're dealing with an undirected graph in this proof, every edge $$ab$$ is counted as the same edge as if there were an edge $$ba$$ in the graph. As a consequence, the adjacency matrices for this family of graphs will be symmetric. 

The way to think about it is that the adjacency matrix of a graph $$G$$ encodes information about the number of length $$1$$ paths between any pair of vertices $$i$$ and $$j$$, i.e. information about the vertices immediately "adjacent" to each other.

### motivation:
Each node in $$K_{10}$$ has $$9$$ edges incident to it while each node in the Petersen graph has $$3$$ edges incident to it. So it is plausible that $$K_{10}$$ can be covered perfectly by $$3$$ Petersen graphs. This means that you can lay down three Petersens on $$K_{10}$$ so that vertices go to vertices and each edge of $$K_{10}$$ lies under an edge of exactly one of the three Petersens. This hints at some pretty cutting-edge stuff in the field of graph decomposition and graph coloring and the parallels in higher dimensions is absolutely incredible. With some linear algebra at our disposal, we will show that it is not possible to completely cover $$K_{10}$$ with three Petersen graphs.

## eigenvalues of the petersen graph

Finding the eigenvalues of any matrix, let alone one that of size $$10 * 10$$ is a fairly computational task and isn't enlightening in any form whatsoever. So why are we trying to find the eigenvalues of the petersen graph? Well we can take advantage of the fact that the adjacency matrix represents information that carries physical meaning (vertex-edge relations of a graph) and can use the language of linear transformations and some geometric intuition to gain insight into the eigenvalues of this graph.

Let $$A$$ be the adjacency matrix of the Petersen Graph. If $$A$$ encodes information about the number of length $$1$$, $$A^2$$ represents information about the number of length $$2$$ paths, and in general, $$A^k$$ encodes information about the number of $$k$$-length paths in a given graph. With this information in our belt, we know can make a pretty nifty observation. 

Consider the $$i, j^{th}$$ entry of the matrix $$A^2 + A$$ (the sum of the matrices representing information about the number of length $$2$$ paths and the regular adjacency matrix of the petersen graph). Since, every vertex in the petersen graph has degree $$3$$, each vertex has $$3$$ length $$2$$ paths back itself whereas there are no length $$1$$ paths from a vertex to itself. With this information under our belt, we can say that 

$$
(A^2 + A)_{i, j} = 
\begin{cases}
3 & \forall i = j \\
1 & \forall i \neq j
\end{cases}
$$

This follows from noticing that any pair of vertices not already joined by an edge are joined by a unique path of length $$2$$; namely there is a unique vertex which is joined to both. 

We can therefore conclude that the matrix $$A$$ satisfies the matrix equation $$A^2 + A = 2I + J$$. 

Note that $$J$$ has eigenvalue 10 (of multiplicity 1 with eigenvector 1) and eigenvalue 0 of multiplicity 9. Thus $$2I + J$$ has eigenvalue 12 of multiplicity 1 and eigenvalue 2 of multiplicity 9. Now if $$x$$ is an eigenvector of A of eigenvalue $$\lambda$$ then $$x$$ is an eigenvector of $$A^2 + A$$ of eigenvalue $$\lambda^2 + \lambda$$. 

Thus the possible eigenvectors for $$A$$ are prescribed. We already know that $$\mathbf{1}$$ is an eigenvector of $$A$$ of eigenvalue 3 (or at least it is easy to check). The other 9 eigenvalues must satisfy $$\lambda^2 + \lambda = 2$$ thus either 1 or -2 with total multiplicity being 9. Now the trace of $$A$$, which is 0, is the sum of the eigenvalues and so we deduce that 1 has multiplicity 5 and -2 has multiplicity 4.

## the actual proof
**Lemma:** $$K_{10} = J_{10} - I_{10}$$  
The adjacency matrix of $$K_{10}$$ has all but its diagonal entries being equal to $$1$$, since
every node in the full graph is connected to every other node except itself. The diagonal entries of $$K_{10}$$ are filled in with $$0$$'s since there is no path from any of the nodes to itself. One can also clearly see that the matrix described by the equation $$J_{10} - I_{10}$$ where $$J_{10}$$ is the matrix with all its entries being equal to $$1$$, is a matrix that has all but its diagonal entries being equal to $$1$$ and its diagonal entries being equal to $$0$$. 

Therefore the adjacency matrix of $$K_{10} = J_{10} - I_{10}$$

**Assumption:** $$A_P + A_Q + A_R = J_{10} - I_{10}$$

We consider three permutation matrices of the Petersen Graph $$A_P, A_Q$$ and $$A_R$$ (matrices formed by simultaneous row and column swaps in the original adjacency matrix of the petersen graph). We construct each of these permutation matrices such that $$A_Q = CAC^{-1}$$ where $$C$$ is some matrix. By this construction, $$A_Q$$ and $$A$$ are similar, and an important consequence is that they have the same eigenvalues. This assumption and construction is true for $$A_P$$ and $$A_R$$. 

**Lemma** $$\text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$$   
We wish to show that $$1^{T} = y^{T}(A_P - I_{10})$$ for some vector $$y \in R^{10}$$. Consider $$y = 1^{T}$$. The matrix product $$1^{T}(A_P - I_{10})$$ yields the vector whose entries are the sum of the entries of the columns of $$A_P - I_{10}$$. for an arbitrary column $$i$$ in its adjacency matrix, by the way the Petersen graph was defined we know that he graph has 3 outgoing edges which means that the sum of the entries of a column in its adjacency matrix is 3. However note that the diagonal entries of the adjacency matrix will be 0 since the Petersen graph does not contain self-loops. After subtracting the $$i$$th column of $$I_{10}$$, the sum of the columns of the matrix $$A_P - I_{10}$$ is 2. Note that the identity matrix has 0 in every entry where $$i \neq j$$. Since the above holds true for an arbitrary column of the matrix, We can conclude that every column of $$A_P - I_{10}$$ sums up to a 2. More fundamentally, the product $$1^{T}(A_{P} - I_{10})$$ generates the all twos
vector or 2$$1^{T}$$. 

Therefore we can assert that $$\text{Span}(1) \subseteq \text{Row} (A_P - I_{10})$$.

**side proof**  
Let $$A$$ and $$B$$ be two subspaces such that $$A \subseteq B$$.  
**claim** $$B^{\perp} \subseteq A^{\perp}$$  
**proof** Let $$x$$ be an arbitrary vector such that $$x \in B^{\perp}$$. By definition of the orthogonal complement, we have that $$\forall v \in B, x^{T}v = 0$$, i.e. they are orthogonal. However we know that any vector contained in $B$ will be a vector contained in $$A$$, ($$A$$ is a subset of the vectors contained in $$B$$). Therefore we can reframe the above statement to be $$\forall v \in A, x^{T}v = 0$$, that is $$x$$ is orthogonal to every vector in $$A$$. By definition, this means that $$x \in A^{\perp}$$

$$\therefore A \subseteq B \rightarrow B^{\perp} \subseteq A^{\perp}$$

Using the aforementioned proof and taking orthogonal complements, we have that $$\text{Span}(1) \subseteq \text{Row} (A_P - I_{10}) \rightarrow \text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$$.

$$\therefore \text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$$

The above results are also true for $$A_Q - I_{10}$$ since $$Q$$ is also a Petersen graph. 

**Lemma** $$\text{Null} (A_P - I_{10}) \cap \text{Null} (A_Q - I_{10}) \neq \{0\}$$. 

**proof**  
For two subspaces $$R_1$$ and $$R_2$$ of $$\mathbb{R}^{9}$$, if $$S_1 \cap S_2 = \{0\}$$, then $$B_{S_1}$$ and $$B_{S_2}$$ are linearly independent.  
We therefore prove by contrapositive. 

We also know that  
$$\text{Null} (A_P - I_{10}) \subseteq \text{Span} (1)^{\perp}$$  
$$\text{Null} (A_Q - I_{10}) \subseteq \text{Span} (1)^{\perp}$$.  
$$B_{ \text{Null} (A_P - I_{10}) } \cup B_{\text{Null} (A_Q - I_{10})}$$ has 10 vectors in $$R^{9}$$ since the bases of each of the null spaces has 5 vectors. Therefore $$B_{ \text{Null} (A_P - I_{10}) } \cup B_{\text{Null} (A_Q - I_{10})}$$ must be linearly dependent (since they have more vectors than the dimension of the space they exist in).

Therefore $$B_{S_1} \cap B_{S_2} \neq \{0\}$$ where $$S_1$$ and $$S_2$$ refer to the two subspaces above. This implies the existence of a non-zero vector $$w$$ that exists in their intersection. 

The larger consequence of this is that this vector $$w$$ is orthogonal to the all ones vector, i.e. $${\bf 1}^{T}w = 0$$

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

We now compute $$J_{10} (w)$$ where $$w \in \text{Null} (A_P - I_{10})$$  

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

$$\therefore$$ $$A_R(w) = J_{10}(w) - w - w - w = -3w$$.

We have therefore arrived at a contradiction. In the beginning of the proof, we found all the eigenvalues of the Petersen Graph and concluded that -3 was not amongst that list. However as we can see, we have proved that -3 in fact is an eigenvalue for the adjacency matrix of a Petersen graph. Therefore it is not possible to cover the full graph or $$K_{10}$$ with 3 Petersen graphs. 

## key takeaways 
How cool is this!! All we did here was take advantage of some fairly simple 
linear algebra to prove a really fundamental fact about graphs that pop up quite frequently 
in the study of networks. For those interested, there is a conjecture in the "colorful" field of graph 
decomposition by the name of [Ringel's Conjecture](https://www.quantamagazine.org/mathematicians-prove-ringels-graph-theory-conjecture-20200219/)
that actually illustrates how exactly you can cover complete 
graphs of this variety. If there's anything I want you to take away from this proof, it's that 
geometric intution is unparalleled and this technique of analyzing eigenvalues not only can save you 
computation, it gives you critical insight into what the graph actually represents, a deeper understanding 
of what it "does", so to speak. It is so easy to get bogged down in what might just seem 
like computation after computation. But there is a bigger picture, and that bigger picture is usually a bigger 
graph. 

## higher dimensions and moore graphs

**degree-diameter problem:**
In graph theory, the degree diameter problem is the problem of finding the 
largest possible graph $$G$$ (in terms of the size of its vertex set $$V$$) of diameter 
$$d$$ such that the largest degree of the vertices in $$G$$ is at most $$k$$. 
The size of $$G$$ is bounded above by the Moore bound; In general, the largest degree-diameter 
graphs are much smaller than as prescribed by the Moore bound.

**the moore bound and moore graphs**
The moore bound gives us an upper bound on how many nodes a graph can contain with 
diameter $$d$$ and maximum degree $$k$$. An intuitive way to recognize what the moore bound 
actually tells us is how *wide* a graph can get. Let $$M$$ be the moore bound that a
graph of the above specifications can meet, we therefore have that 

$$
M = 1 + k \sum_{i = 0}^{d - 1} (k - 1)^i
$$

Graphs that attain this bound $$M$$ are known as Moore graphs.

**obtaining the moore bound**
![moore graphs](images/notes.jpg)
Consider the breadth first search of a graph $$G$$. From the above picture, we 
can clearly see that level 0 has only one node, this being the root of the tree 
generated by breadth first search. Level 1 has at most $$k$$ nodes since the maximum 
degree of any node in the graph is given by $$k$$. For each node $$i$$ in Level 1, $$i$$ 
can be connected to at most $$k - 1$$ nodes (it's important not to forget the node they are
connected to in Level 0). Since there are $$k$$ nodes in the first level, the maximum number of 
nodes in level 2 is given by $$k(k - 1)$$. 

Generalizing, we have that the number of nodes in a level 
$$j$$ $$\leq k(k - 1)^{j - 1}$$.

Notice that we can count the nodes from level 1 to $$d$$ (we can't have more than 
$$d$$ levels) using a sum given by $$\sum_{i = 1}^{d} k(k - 1)^{i - 1}$$. We also have to account 
for the root node which adds 1 to this total sum formula. After some substitution of variables, we get that
the final expression for the upper bound comes out to be 

$$M = 1 + k \sum_{i = 0}^{d - 1} (k - 1)^{i - 1}$$

**types of moore graphs and its relation to the petersen graph**
The entire reason we're even talking about moore graphs is that the petersen graph 
is a very specific kind of moore graph. Remember that equation we found for the adjacency
matrix of the petersen graph. Well for the moore graphs that are known to exist, they satisfy 
the same "general form" of that equation.

**lemma** The only $$d$$-regular Moore graphs of girth 5 and diameter 2 exist for 
$$d = 2, 3, 7$$ and possibly $$57$$. 

**proof**
Assume $$G$$ is a $$d$$-regular Moore graph of girth 5. A reminder that the girth of a graph is 
defined to be $$2k + 1$$ where $$k$$ is the diameter of the graph. Solving the above equation 
for the girth, we get that the diameter of the graph must be 2, i.e. $$k = 2$$. Substituting in 
this value into the Moore bound, we get that the number of the vertices in the graph is given by 

$$
n = 1 + d + d(d- 1) = d^{2} + 1
$$

As we did for the petersen graph, we consider the square of the adjacency matrix $$A^{2}$$ 
once again. Notice that the adjacenct vertices don't share any neighbours since if they did, 
there would be a triangle in $$G$$. Non-adjacent vertices share exactly one neighbor, because the 
diameter of $$G$$ is 2. Hence, $$A^{2}$$ has $$d$$ on the diagonal, 0 for edges and 1 for non-edges. 
In other words, we have that 

$$
(A^{2} + A)_{i, j} = 
\begin{cases}
d & \forall i = j \\
1 & \forall i \neq j
\end{cases}
$$

We therefore have that $$A$$ satisfies the equation 
$$
A^{2} + A = (d - 1)I + J
$$

**lemma** If $$\lambda$$ is an eigenvalue of $$A$$ different from $$d$$, we 
get from the above equation that $$\lambda^{2} + \lambda - (d - 1) = 0$$

**proof**
I suppose I should have talked about this earlier, but the all ones matrix $$J_d$$
has eigenvalues 0 and $$d$$, where the eigenvalue $$d$$ corresponds to an
eigenspace with the all ones vector or $${\bf 1}$$.

Let $$x$$ be the eigenvector corresponding to eigenvalue 0. Multiplying both sides of 
the equation we have that 

$$\begin{align*}
&\
A^{2}x + Ax = (d - 1)x = 0 \\
&\
\lambda^{2}x + \lambda x = (d - 1)x \\ 
&\
\lambda^2 + \lambda - (d - 1) = 0 
\end{align*}$$

**obtaining the parameters for which moore graphs exist**  
We can use the quadratic formula to ascertain that the roots of the equation $$ax^2 + bx + c = 0$$
are given by $$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$. Plugging in constants from the equation above, we have 
that $$\lambda = \frac{-1 \pm \sqrt{1 + 4(d - 1)}}{2} = - \frac{1}{2} \pm \frac{\sqrt{4d - 3}}{2}$$. 

Assume that $$\frac{-1}{2} + \frac{\sqrt{4d - 3}}{2}$$ has multiplicity $$a$$ and $$\frac{-1}{2} - \frac{\sqrt{4d - 3}}{2}$$ 
has multiplicity $$b$$. Using the fact that the trace of a matrix $$A$$ is the sum of its diagonal entries, we can ascertain that 

$$\begin{align*}
&\
d(1) + (\frac{-1}{2} + \frac{\sqrt{4d - 3}}{2})(a) + (\frac{-1}{2} - \frac{\sqrt{4d - 3}}{2})(b) = 0 \\
&\
d - \frac{a}{2} + \frac{a\sqrt{4d - 3}}{2} - \frac{b}{2} - \frac{b\sqrt{4d - 3}}{2} = 0 \\
&\
d - \frac{a + b}{2} + \frac{1}{2} \; (a - b) \sqrt{4d - 3} = 0
\end{align*}$$

However we know that $$a + b = n - 1$$ and from our previous computation of $$n$$, we get that 
$$a + b = d^{2}$$. Substituting in, we get that 

$$\begin{align*}
&\
d - \frac{d^2}{2} + \frac{1}{2} \; (a - b) \sqrt{4d - 3} = 0 \\
&\
\frac{2d - d^2}{2} + \frac{1}{2} \; (a - b) \sqrt{4d - 3} = 0 \\
&\
(a - b) \sqrt{4d - 3} = d^{2} - 2d 
\end{align*} $$

This statement is only true if $$a = b$$ and $$d = 2$$ (the trivial case of both sides 
being 0) or else $$4d - 3$$ is a square. 

Let $$4d - 3 = s^{2}$$. Therefore, we have that  

$$\begin{align*}
&\
d - \frac{d^2}{2} + \frac{s}{2} \; (a - b) = 0 \\
&\
d - \frac{d^2}{2} + \frac{s}{2} \; (2a - d^{2}) = 0 \\
&\
4d - 3 = s^{2} &&\text{Change of variables we make} \\
&\
d = \frac{1}{4} \; (s^{2} + 3) &&\text{Solving for $d$} \\
&\
\frac{1}{4} \; (s^{2} + 3) - \frac{1}{2} \; (s^2 + 3)^{2} + \frac{s}{2} \; (2a - \frac{1}{16} \; (s^2 + 3)^{2}) = 0\\
&\
s^{5} + s^{4} + 6s^{3} - 2s^2 + (9 - 32a)s - 15 = 0 &&\text{After an ungodly amount of math :(}
\end{align*}
$$

To satisfy the above equation, we have that $$s$$ must divide 15, i.e. $$s \in 
\{1, 3, 5, 15 \}$$. Since $$s^2 = 4d - 3$$, we have that $$d \in \{1, 3, 7, 57 \}$$.  

When $$d = 1$$, we get the complete graph on 2 vertices, i.e. $$K_2$$ which is not a Moore 
graph since it doesn't meet the Moore bound. 

For all the other cases, we have that 
- $$d = 2$$: $$C_5$$
- $$d = 3$$: Petersen Graph
- $$d = 7$$: Hoffman Singleton Graph
- $$d = 57$$: Open problem if this graph exists :0

There's a lemma floating around the internet somewhere where it states that Moore graphs 
don't exist for diameters greater than 2 which is kind of insane if you think about it. It's 
also the reason their existence is so fascinating and why we've listed most of if not all the 
Moore graphs there can be.
# cauchy schwarz and beyond

The object of today's study is the cauchy schwarz inequality specifically the version involving dot
products. For those unaware, the cauchy schwarz is probably one of the most broken 
lemmas in mathematics. So ubiquitious is this theorem, that it is given different names depending 
on the form of the inequality we use and for what purpose specifically we're using it. 

Let's start from the beginning. We will state some different forms of the cauchy schwarz inequality, 
prove the form involving dot products and cover what I think is a really cool problem that uses the inequality. 

For the different forms of the cauchy schwarz inequality, we have
- Probability Theory: $$\lvert \mathbb{E}(XY) \rvert^{2} \leq \mathbb{E}(X^{2}) \mathbb{E}(Y^{2})$$
- $$R^2$$-dot product: $$ \lvert {\bf a}. {\bf b} \rvert^{2} \leq ({\bf a}.{\bf a}) \; ({\bf b}.{\bf b})$$
- $$R^{n} - \; n$$ - dimensional Euclidean Space: $$(\sum_{i = 1}^{n} u_{i} v_{i})^{2} \leq
  (\sum_{i = 1}^{n} u_i)^{2} (\sum_{i = 1}^{n} v_i)^{2}$$ 

**lemma** $$ \lvert {\bf a}. {\bf b} \rvert^{2} \leq ({\bf a}.{\bf a})({\bf b}.{\bf b})$$  
**proof** 

Let $$a$$ and $$b$$ be vectors living in $$R^{n}$$ such that $$a = \langle a_1, a_2, a_3, \dots, a_n \rangle$$ and 
$$b = \langle b_1, b_2, b_3, \dots, b_n \rangle$$. We first simplify both sides of the inequality, and 
proceed from there.  

We have that,

$$
\begin{align*}
&\
\lvert {\bf a}. {\bf b} \rvert^{2} = ({\bf a}. {\bf b}) ({\bf a}. {\bf b}) \\
&\
\lvert {\bf a}. {\bf b} \rvert^{2} = \langle a_1, a_2, a_3, \dots, a_n \rangle \langle b_1, b_2, b_3, \dots, b_n \rangle \\
&\
\lvert {\bf a}. {\bf b} \rvert^{2} = (a_1 b_1 + a_2 b_2 + \dots + a_n b_n) (a_1 b_1 + a_2 b_2 + \dots + a_n b_n) \\
&\
\lvert {\bf a}. {\bf b} \rvert^{2} = (a_1 b_1 + a_2 b_2 + \dots + a_n b_n)^{2} \\
&\
\lvert {\bf a}. {\bf b} \rvert^{2} = (\sum_{i = 1}^{n} a_i b_i)^{2} \\
&\
({\bf a}.{\bf a}) = \langle a_1, a_2, a_3, \dots, a_n \rangle \langle a_1, a_2, a_3, \dots, a_n \rangle \\
&\
({\bf a}.{\bf a}) = a_{1}^{2} + a_{2}^{2} + \dots a_{n}^{2} \\
&\
({\bf a}.{\bf a}) = \sum_{i = 1}^{n} a_{i}^{2} \\
&\
({\bf b}.{\bf b}) = \langle b_1, b_2, b_3, \dots, b_n \rangle \langle b_1, b_2, b_3, \dots, b_n \rangle \\
&\
({\bf b}.{\bf b}) = b_{1}^{2} + b_{2}^{2} + \dots + b_{n}^{2} \\
&\
({\bf b}.{\bf b}) = \sum_{i = 1}^{n} b_{i}^{2}
\end{align*}
$$

For the sake of notational convenience, let us state that 
- $$D = \sum_{i = 1}^{n} a_i b_i$$
- $$A = \sum_{i = 1}^{n} a_{i}^{2}$$
- $$B = \sum_{i = 1}^{n} b_{i}^{2}$$

So we are therefore tasked with proving the following inequality, $$D^{2} \leq AB$$  

Rearranging, we have that 

$$
\begin{align*}
&\
D^{2} \leq AB \\
&\
D^{2} - AB \leq 0 \\
&\
4D^{2} - 4AB \leq 0 &&\text{Multiplying both sides by 4} \\
&\
(2D)^{2} - 4AB \leq 0
\end{align*}
$$

One of the coolest thing about math to me is how you can transform certain kinds of problems 
into problems that might be easier to solve or perhaps represent. This is one of those moments. 
This might look familiar to some people already but given a quadratic equation $$ax^{2} + bx + c = 0$$, 
the discrimanant $$D_{Q}$$ is given by $$b^{2} - 4ac$$. The entire reason I changed the form of the inequality
we had to prove was so that it could better mimic this form of the discriminant for something as widely 
ubiquitous as the quadratic formula. 

**fun lemma :D** $$\frac{\mathbb{E}[Y]^2}{\mathbb{E}[Y^2]} \leq \mathbb{P}(Y \neq 0) \leq \mathbb{E}[Y]$$  
**proof**
We first prove the right-hand side of the inequality, i.e. $\mathbb{P}(Y \neq 0) \leq \mathbb{E}[Y]$. Using the definition of expectation, we have that
$$
\begin{align*}
&\
\mathbb{E}[Y] = \sum_{y \in \Omega_{y}} y \mathbb{P}(Y = y) \\
&\
\mathbb{E}[Y] = \sum_{y \in \Omega_{y}, y \neq 0} y \mathbb{P}(Y = y) &&\text{Separating out the term when $y$ is 0} \\
&\
\mathbb{E}[Y] \geq \sum_{y \in \Omega_{y}, y \neq 0} \mathbb{P}(Y = y) &&\text{Since $y \geq 0$}\\
&\
\mathbb{E}[Y] \geq \mathbb{P}(Y \neq 0)
\end{align*}

We now prove the left-hand side of the inequality, Consider the expression $\mathbb{E}[Y^2] \mathbb{P}(Y \neq 0)$. We have that the following is true
\begin{align*}
&\
\mathbb{E}[Y]^2 \mathbb{P}(Y \neq 0) = \sum_{y \neq 0} \mathbb{P}(Y = y)\; \sum_{y \neq 0} y^{2} \mathbb{P}(Y = y) &&\text{Using the definition of expectation and LOTUS}
\end{align*}
From the above expression, let $a_i = \sqrt{\mathbb{P}(Y = y)}$ and $b_i = y\sqrt{\mathbb{P}(Y = y)}$. We also know from the Cauchy Schwarz inequality above that $\sum_{i = 1}^{n} a_i b_i \leq \sqrt{\sum_{i = 1}^{n} a_{i}^{2}} \sqrt{\sum_{i = 1}^{n} b_{i}^{2}}$. Squaring both sides, we have that another form of this inequality can be written as
$(\sum_{i = 1}^{n} a_i b_i)^{2} \leq \sum_{i = 1}^{n} a_{i}^{2}\sum_{i = 1}^{n} b_{i}^{2}$. We now apply the Cauchy Schwarz inequality to get that
\begin{align*}
&\
\sum_{y \neq 0} \mathbb{P}(Y = y)\; \sum_{y \neq 0} y^{2} \mathbb{P}(Y = y) \geq \sum_{y \neq 0} y \sqrt{\mathbb{P}(Y = y)} \sqrt{\mathbb{P}(Y = y)} \\
&\
\sum_{y \neq 0} \mathbb{P}(Y = y)\; \sum_{y \neq 0} y^{2} \mathbb{P}(Y = y) \geq \sum_{y \neq 0} y \mathbb{P}(Y = y) \\
&\
\sum_{y \neq 0} \mathbb{P}(Y = y)\; \sum_{y \neq 0} y^{2} \mathbb{P}(Y = y) \geq \mathbb{E}[Y] &&\text{Using the definition of expectation} \\
&\
\mathbb{E}[Y]^2 \mathbb{P}(Y \neq 0) \geq \mathbb{E}[Y] \\
&\
\frac{\mathbb{E}[Y]}{\mathbb{E}[Y]^2} \leq  \mathbb{P}(Y \neq 0)
\end{align*}
\qed}
$$
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
