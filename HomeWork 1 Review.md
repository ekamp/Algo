##Homework #1 Review

###Big Oh Notation
- When is T(n) = O(f(n)) ?
- For all sufficently large n T(n) is bounded above by some multiple of f(n)
- Formal definition is : 
  T(n) = O(f(n)) if and only if there exist constants c,n0 > 0 such that T(n) <= cf(n) for all n > n0
- Basically saying that for all n given a constant c, cf(n) will grow larger than T(n). Once grown larger cf(n) will cross T(n) at n0.


![alt text](http://s16.postimg.org/sifiycbap/Screen_Shot_2014_02_16_at_12_59_50_PM.jpg"Big Oh Image")
<br/>
http://postimg.org/image/sifiycbap/


###Big Omega
- T(n) = OMEGA(f(n))
- If and only if there exists constants c and n0 such that T(n) >= cf(n) for all n >= n0
- For all sufficently large n T(n) is bounded <b>below</b> by some multiple of f(n)

http://postimg.org/image/wyzp1vne1

###Theta Notation
- T(n) = O(f(n)) and OMEGA(f(n))
- There exist constants c,c1,n0 such that cf(n) <= T(n) <= c1f(n) for all n >= n0

###Little Oh Notation
- T(n) = o(f(n))
- If T(n) strictly lower bounds f(n) meaning just less than.
- For all constants c > 0 there exists a constant n0 such that T(n) <= cf(n) for all n >= n0



