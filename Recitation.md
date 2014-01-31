#Recitation Comparing Algorithms
###Big Theta
Theta : f(x) = Theta(g(x))
- if there exists n0 > 0 , c1 > 0, c2 > 0
- 0 <= c1 g(n) <= f(n) <= c2 g(n)
- for all n >= n0

###Big O notation
O : f(n) = O(g(n))
- There exists an n0 > 0 , c >0
- For all n >= n0, 0<= f(n) <= c g(n)

###Big Omega
f(n) = OMEGA(g(n))
- There exists n0 > 0 , c > 0
- For all n >= n0, 0 <= cg(n) <= f(n)

###Proofs
- Small O < Big o <= small-w > Big OMEGA
- f(n) = O(g(n)
- There exists n0 , c > 0
- For all n >= n0 O <= f(n) < cg(n)

###Sample Problems
Rank the following functions
- g1 = OMEGA(g2) , g2 = OMEGA(g3)
- g24 = OMEGA(g25)
- (3/2)^2 , (SQRT(2))^log(n)
- n^3 , log(n^2
