#Security / Crypto

##Public key encrytion
- Think of messages as modulo N (Larger messages can be broken into smaller peices
- What is a good value for N?

###Properties
- Pick any two primes p and q
- Let N = p * q
- Find any number e so that grd(e,(p-1)(q-1)) = 1
- The following are true
    - x -> x^e mod n is a bijection which is a one to one mapping
    - Let d be e^-1 mod (p-1)(q-1)
    - For all x that in the range of 0 to n-1 * x^e^d = x mod N
    - EXAMPLE : p = 5 , q = 11 -> N =p 1 = 55
        Choose e so that grd (e, (e-1)(11-1)) = grd(e,40) =1
        (grd = greatest common divisor) in this case e = 3 is sufficent
        What is the value of d?
        d = e^-1 mod (p-1)(q-1) = 3^-1 mod 40
        This means that 3 * d = 1 mod 40 (modular inverse)
          
