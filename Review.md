# Design and Analysis of Computational Algorithms 344
## Kostas Bekris
## Spring 2014
---
---

### 1/31/14

### Recitation

#### TA's:

- Amr Nagruib Nakry <amrbakry@cs.rutgers.edu>
	- Office hours: Tues 12-1 (Hill 206)
	
- Athansios Krontiris <ak979@cs.rutgers.edu>
	- Office hours: Fri 11-12 (BIM-16) 
	
#### Big O and Big $$$\Omega$$$

\\[ \begin{aligned}
&O: f(n) = O(g(n)) \\\
&\exists n_0 > O\;,\;\; c > 0\;\; s,\,t \\\
&\forall n \geq n_0, O \leq f(n) \leq C g(n) \\\
\end{aligned} \\]

---
\\[ \begin{aligned}
&\Omega: f(n) = \Omega(g(n)) \\\
&\exists n_0 > 0\;,\;\; c > 0\;\;\; s,\,t \\\
&\forall n \geq n_0, O \leq Cg(n) \leq f(n) \\\
\end{aligned} \\]

---
##### Small O:
\\[ \begin{aligned}
&o: f(n) = o(g(n)) \\\
&\exists n_0,\;c > 0\;\;\; s,\,t \\\
&\forall n \geq n_0, o \leq f(n) \leq C g(n) \\\
\end{aligned} \\]

---
### Lecture

#### Cryptography

- Private cryptography are baaaaadddddd
- Public  cryptography is goooooooddddd
- Think of messages as modulo $$$N$$$
	- Larger messages can be broken into smaller pieces
- What is a good value for $$$N$$$?
- **Property:** Pick any 2 primes $$$p$$$ and $$$q$$$. Let $$$N = p*q$$$ - 
\\[ \begin{aligned}
&\forall e \mid \gcd (e(p-1)(q-1)),\;\; \text{where } e \text{ is a relative prime} \\\
\text{The following are true:} \\\
&\text{1)}\;\; x \to x^e \mod N \;\; \text{ is a bijection}\\\
&\text{let } d = e^{-1} \mod (p-1)(q-1) \\\
\text{Then } \\\
&\forall x \in [0, N-1]:(x^e)^d \equiv x \bmod N
\end{aligned} \\]

##### Proof of Property

\\[ \begin{aligned}
\text{We have to show that} \\\
&(x^e)^d \mod N \equiv X \mod N \\\
&\text{The following are true if } e,\; d \text{ have been selected as specified} \\\
&e * d = 1 \mod (p-1)(q-1) \Rightarrow \\\
&e*d = k(p-1)(q-1) + 1 \\\
\text{Then, check the difference:} \\\
&x^{ed} - x \mod N \equiv x^{k(p-1)(q-1)} - x \mod N
\text{I want to show this O} \\\
\end{aligned}\\]

#### *Fermat's Little Theorem*

\\[ \begin{aligned}
\text{If } p \text{ is prime, then } \forall 1 \leq a \leq p \\\
&1 \mod p \equiv a^{p-1}
\end{aligned} \\]

##### Proof
\\[ \begin{aligned}
&\text{Consider the sets} \\\
&S = \\{1, 2, \cdots , p-1\\}= \\\
&\\{a*1 \bmod p, a * 2 \bmod p, \cdots ,a(p-1) \bmod p \\} \\\
&\text{You will always get a rearrangement of the elements.} \\\
&\text{WHY? } d \* i \bmod p \text{ are all distinct and different from Q}
\end{aligned} \\]

#### Summary of RSA

Bob: 

- Pick 2 large(n-bit) random prime numbers $$$p$$$ and $$$q$$$
- Publish $$$(N,e)$$$ where $$$N = p*q$$$ and $$$e$$$ relative
- Compute private key $$$d=e^{-1} \bmod (p-1)(q-1)$$$

Alice:
- Generate encrypted message $$$y=x^e \bmod N$$$

Bob:
- Decode message $$$x=y^d \bmod N$$$

##### Why is this Secure?

- To break the system, Eve must be able to compute $$$X$$$ given $$$y$$$ and $$$(N, e)$$$
- Try to guess $$$x$$$ so that $$$y=x^e \bmod N$$$
	- Exponential # of guesses as a function of $$$$n$$$(# of bits for $$$p, q$$$)
- Alternatively, Eve can try to find values $$$p$$$ and $$$q$$$ so as to compute $$$d=e^{-1} \bmod (p-1)(q-1)$$$
- What do we know about $$$p$$$ and $$$q$$$? 
	- They are primes and $$$p*q=N$$$
- But this is the factoring problem
	- believed to be hard and intractable
- What are the operations of RSA and what is the running time?
	\\[ \begin{aligned}
	&\Rightarrow \text{Modular exponentiation } \\\
	&y=e^x \bmod N\over x=y^d \bmod N \\\
	&\Rightarrow \text{Select } e \text{ so relative prime to } (p-1)(q-1) \\\
	\end{aligned} \\]

#### Modular Exponentiation

$$x^y \bmod N$$
How big can $$$x^y$$$ get? e.g. for 20-bit numbers
$$(2^{19})^{13} = 10\text{ mil. bits long}$$
We need to perform all intermediate computations $$$\bmod\; N$$$ $$x \bmod N \to x^2 \bmod N \to x^3 \bmod N$$
If $$$y$$$ is 500 bits long then I have to do the multiplication $$$2^{500}$$$ times.

Idea: square every intermediate result
$$x \bmod N \to x^2 \bmod N \to x^4 \bmod N \to x^8 \bmod N \to x^{16} \bmod N$$
Now there are $$$n^3$$$ multiplications

$$x^{25_{10}} = x^{11001_2} = x^{10000} * x^{010000} * x^{00001} = x^{16} * x^8 * x^1$$

Sample function:

		function modexp(x,y,N)
		if (y = 0) return 1
		Z = modexp(x, floor(y/2), N)
		if (y is even)
			return z^2 mod N
		else
			return (x * z^2 mod N)

---
### 2/7/14

#### Greatest Common Divisor

\\[ \begin{align}
1035 = 33 * 5 * 23 \\\
759 = 3 * 11 * 23 \\\
\end{align} \\]

##### Euclid's Observation

$$\gcd(x,y) = \gcd(x \bmod y, y)$$
Let's show that: $$$\gcd(x,y) = \gcd(x-y, y)$$$
$$\gcd(x,y) \leq \gcd(x,x-y)$$

$$$g$$$ divides both $$$x$$$ and $$$y$$$

	function Euclid(a,b) {
		if b = 0
			return a;
		return Euclid(b, a mod b);
		}
$$$\text{Euclid} = O(n^2)$$$
\\[ \begin{aligned}
\text{if} a \geq b \text{ then } a \bmod b < \frac{a}{2}
\end{aligned} \\]

##### Lemma

If $$$d$$$ divides both $$$a$$$ and $$$b$$$ and we can write $$$d=ax+by$$$ for $$$x,y$$$ integers 

then $$$d=gcd(x,y)$$$

Since $$$d$$$ divides $$$a$$$ and $$$b$$$,
$$$$a \bmod d = b\bmod d$$

[insert shit here]

	function extended Euclid(a,b)
		if b = 0
			return x = 1, y = 0, d = a;
			(x',y',d') = extended Euclid(b a mod b);
			return(y', x' - ceil(a/b) * y', d);
			
#### Multiplicative Inverse modulo N

$$$x$$$ is a m.i.m.N. of $$$a$$$ if $$ax \equiv 1\bmod N$$

(In RSA $$$de\equiv 1\bmod (p-1)(q-1)$$$)

Such an inverse does not always exist	

When $$$\gcd(a,n) = 1$$$ then Extended Euclid algorithm gives an expression

Ex: Find the inverse of 11 modulo 25

\\[\begin{aligned}
\gcd(11,25) &= \gcd(25,11) \\\
&=\gcd(25,11) \\\
&=\gcd(11,3) \\\
&=\gcd(3,2) \\\
&=\gcd(2,1) \\\
&=\gcd(1,0) \\\
\end{aligned} \\]

#### Modular Division Theorem

\\[\begin{aligned}
&\forall a\in [1,\dotsc, N] \\\
&a \text{ will havea  multiplicative inverse modulo }N \\\
&\text{ if it is a relative prime to } N \\\
\end{aligned} \\]

#### Primality Test (Test of Prime-ness)

Remember Fermat's Little Theorem
If $$$p$$$ is prime, then $$$1 \leq a < p$$$ $$A^{p-1} \equiv 1\bmod p$$

Pick an value $$$a$$$. If it doesn't not satisfies the *Primality Test*, $$$p$$$ is not prime.
- We hope that if we call this test multiple times for a non-prime $$$p$$$ that it will fail quickly.

function Primality(N):

pick positive integer $$$a \in [1, N-1]$$$ at random

if $$$(a^{N-1}\equiv 1\bmod N)$$$ return SUCCESS

else return FAILURE

- **Carmichael numbers:** Not prime but Fermat's test succeeds.
	- Ignore these numbers for now (they are rare)
- Thus for a prime number test will always succeed
- For a non-prime it will fail with a certain probability

---
### 2/14/14

### Recitation

- How do you prove $$$a\equiv a\pmod n$$$
	- Show that $$$n\;|\;a-a\to n\;|\;0$$$
- In general, $$$a\equiv b\pmod n \iff n\;|\;a-b$$$

#### Substitution Rule:
\\[\begin{aligned}
&x\equiv y\bmod n,\; x'\equiv y'\bmod n \\\
\implies &x + x'\equiv y + y'\bmod n \\\
\implies &x * x'\equiv y * y'\bmod n \\\
\end{aligned} \\]

- Let $$$n$$$ be a nonnegative integer. Prove $$$n\equiv n\bmod 10$$$
\\[\begin{aligned}
	ed&\equiv 1\pmod{(p-1)(q-1)} \\\
	(m^e)^d&\equiv m\bmod{pq} \\\
	ed &= k(p-1)(q-1) + 1 \\\
	m^{ed} &= m^{1+k(p-1)(q-1)}\equiv m\bmod pq \\\
	p-q &=10\,,\;1+k(p-1)(q-1) = 5 \\\
	\text{for }\; p&=5,\;q=2
\end{aligned}\\]
 
 - for $$$k\in \mathbb{Z}, k$$$ is a self-inverse iff
 	\\[\begin{aligned}
 	k*k\equiv1&\bmod \;p\; (p\text{ is prime}) \\\
 	p\;|\;k^2-1&\iff p\;|\;(k-1)(p-1) \\\
 	p\;|\; k-1 &\text{ or } p\;|\;k+1 \\\
 	k-1=np &\text{ or }k+1=np \\\
 	k=np\pm1&\implies k\equiv\pm1\bmod p \\\
 	\end{aligned} \\]

---
### Lecture

#### Divide & Conquer

- Break your problem into smaller instances
- Recursively solver smaller subproblems
- Combine these answers
- Before for multiplication: $$x*y=2x\*\Big\lfloor{y\over2}\Big\rfloor$$ if $$$y$$$ is even, $$x+2x\*\Big\lfloor{y\over2}\Big\rfloor$$ if $$$y$$$ is odd.
- Another idea for multiplication:
	$$x: 10101\,|\,00100\quad x=2^{n/2}*x_L+x_R$$
	$$y: \quad y_L\quad\quad y_R \quad\quad y=2^{n/2}\*y_L + y_R$$
- In the above representation, we have
	- additions (linear cost)
	- multiplication with powers of 2 (linear cost) (left shifts)
	- four multiplications between $$$n/2$$$-bit numbers
- We can define a recursive relations:$$T(n)=4T\left({n\over2} + O(n)\right)$$
- Gauss' observation: Rework the above expression so as to make use of only 3 $$$n\over2$$$ size multiplications. $$x_Ly_R + X_Ry_L = (x_L + x_R)(y_L + y_r) - x_Ly_L - x_Ry_R$$
$$x\*y=2^nx_Ly_L+2^{n\over2}(x_Ly_R+x_Ry_L) = x_Ry_R$$
$$x\*y=2^nx_Ly_L+2^{n\over2}(x_Ly_R+x_Ry_L) = x_Ry_R$$
$$T(n)=3T\left({n\over2} + O(n)\right)$$
- Make a tree of height $$$\lg n$$$
- At the $$$(\lg n)^{2n}$$4=
- We are solving mult. w a d&c approach
- By decreasing # of recursive calls we managed to get a running time

#### Master Theorem

- If you have a recursive case the function of the form $$$T(n) = a*T\left\lceil{n\over b}\right\rceil$$$ + O(n^d) then: $$$T(n) = O(n^d), O(n^d\log n), O(n^{\log_b a})$$$ for $$$d >, =, < \log_b a$$$
- Assume that $$$n$$$ is a power of $$$b$$$ for convenience
- The size of the problem decreases by $$$b$$$ at every level
- We need $$$\log_b n$$$ levels to stop the recursion.
- At level $$$k$$$ we have $$$a^k$$$ subproblems of size $$${n\over b} k$$$
- Work at level k: $$a^k * O\left({n\over b^k}^d\right) = O\left(n^d\right)*\Big({a\over b^d}^k\Big)$$
- **3 cases:**
	1. If $$${a\over b^d} < 1$$$: series is decreasing. Dominating term is the first one
		- Running time: $$$O(n^d)$$$
	2. If $$${a\over b^d} > 1(\implies d < \log_b a)$$$: series is increasing. Dominating term is the last one
		- Running time: $$$O(n^{log_b a})$$$
	3. If $$${a\over b^d} = 1 \implies d=\log_b a$$$ then all terms are equivalent to $$$O(n^d)=O(n^{log_b a})$$$
		- Overall cost: $$$O(n^d\log_b n)$$$
- The overall cost is also going to be some eq that Bekris fucking covered up
	- t(-.- t)
	
##### Example: Binary Search

\\[\begin{aligned}
T(n) = 1 * T({n\over 2}) + O(1) \\\
a = 1, b = 2, d = 0
\end{aligned}\\]

#### Sorting Problem

- A sequence of elements $$$(a_1,\dotsc,a_n)$$$ output a permutation $$$(a_1',\dotsc,a_n')$$$ so that $$$\forall i\,\exists j$$$ such that $$$a_j' = a_i$$$ and $$$a_1'\leq a_2'\leq \dotso\leq a_n'$$$
- We will review 2 families of sorting algorithms:
	- Comparison sorts:
		- Merge sort
		- Heap sort
		- Quick sort
		- Insertion sort
	- Non-comparison sorts:
		- Counting sort
		- Radix sort

- **Merge Sort**
	- Split the list into two halves. Recursively sort each half and then merge them.
	- Cost of merging two sorted $$$n\over2$$$ lists is $$$O(n)$$$	\\[\begin{aligned}
	T(n) = 2 * T({n\over 2}) + O(1) \\\
	a = 2, b = 2, d = 1
	\end{aligned}\\]
