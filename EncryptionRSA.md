#RSA/Encryption
- Pick 2 large n bit primes p and q 
- N = p * q
- e = gcd(e(p-1)(q-1) = 1
- d = d = e^-1 mod(p-1)(q-1)
- Bob : x = y ^d mod N
- Alice y = x^e mod N


##Greatest Common Divisor
  1035 = 33523
  759 = 31125
  If u can facto efficently this would be a solution
  
##Euclids observation
  - gcd(x,y) = gcd(x mod y, y)
  - Example = gcd(25,11) = gcd(11,3)
  - Lets show that gcd(x,y) = gcd(x-y,y)
  - g divides y and divides xy
  - so it has to divide x
  - so it is a common divisor for x and y
  - gcd(x,y) = gcd(x,x-y)
  - gcd(y,x-y) <= gcd(x,y)

##Function Euclid
      if(b == 0)
      {
        return a;
      }
      return Euclid(b, a mod b);
- if the numbers have n bits after 2 rounds we will be dealing with n-1 numbers. Recursive calls 2n cost of (a mod b) 
- O(n^2) total overall cost
<b><u>Lema</b></u>
- If d divides both a and b and we can write d = ax + by for x,y integers then d = gcd(x,y)
- Since d divides a and b d <= gcd(a,b)
- But the gcd must also divide ax + by
- a = ka * gcd(a,b)
- b = kb * gcd(a,b)
- d = a * x * b * y
- Therefore the gcd(a,b) <= d
- d = gcd(a,b)

##Function Extended Euclid(a,b)
    if(b == 0)
    {
      return x = 1. y = 0 , d = a;
    }
    else
    {
    Extended_euclid(b, a mod b)
    return (y' , x' a/b * y' , d)
    }
###Proof of Correctness
- d is correct because it agrees with Euclid's rule
- for x,y we will use induction : base case : d = a = a *1 + b 0    x = 1 , y = 0 correct
- Inductive Assumption
    - d = b * x' + (a mod b) * y'
    - d = gcd(a,b) = gcd(b, amod b) = bx' + (a - a/b * b)y' = ay' + b(x' - (a/b)*y')
    - if a,b relative primes : a*x + b*y = 1

##Multiplitive Inverse modulo N
- x is the a inverse of a if a*x = 1 mod N (In RSA d*e = 1 mod(p-1)(q-1)
- such an inverse does not always exist
- When gcd(a,N) = 1 then Extended Euclid algorithm gives expresion : 
  - a * x + N*y = 1 , a*x = 1 mod N
  - X will be the inverse of a modulo N
- Find the inverse of 11 modulo 25
    gcd(11,25) = gcd(25,11)(4,-9,1)
    gcd(11,3)(-1,4,1) = 
      gcd(3,2)(1,-1,1) = 
        gcd(2,1)(x = 0 ,y=1 , d=1)  = 
          gcd(1,0) (x = 1 , y = 0, d =1)
            gcd(a,b) = gcd(b, a mod b)
              -9 * 11 = 1 modulo 25 --> 16 * 11 = 1 mod 2

##Modular Division Theorem
- For all a in [1 to n] a will have a multiplitive inverse modulo N if and onlly if it is relative prime to N
- You can compute this in O(n^3) time with the extended Euclid Algorithm

##Primality Test
- Remember Fermod's Little Theorem
- if p is prime then 1 <= a < p ; a^p-1 = 1 mod p
- Pick a --> [is a^(p-1) = 1 modn] Yes(cannot disprove that p is not prime) No(p is not prime)
- We hope that if we call this test multiple times for a non-prime p that it will fail quickly

##Function Primality (N)
- Pick positive integer a from 1 to n - 1 at random
- if a^(n-1) = 1 mod N {return SUCCESS} else {return FAILURE}

##Carmicheal numbers 
 -Not prime but Fermat's test succeeds always
- Ignore these numbers for now (They are rare)
- Then for a prime number the test will always succeed but for a non-prime will fail with a certain probability

####Lema
- if a^N-1  = 1 mod N for some a relative prime to N, then it must be the case that the primality test will fail for at least half the choices of a.
- Proof : fpr all b < N so that the primality test succeeds then there must be a number (a*b) so that
  (a*b)^N-1 = a^N-1 b^n-1 != 1 mod N
- All these elements (a*b) for fixed a's and b's are distinct. So at least half of the numbers < n will fail
- pr(algo returning success for n prime) = 1
- pr(algo retruning success for n non-prime) <= 1/2
