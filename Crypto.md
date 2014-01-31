#Security / Crypto 1/31/2014

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
            for d = 27 we have 3 * 27 = 81 = 1 mod 40
            For any message x mod 55, encryption is y = x^3 mod 55
            Decryption is x = y^d mod 55
            For example if x = 13 then y would be 52 mod 55
            13 = 52^27 mod 55
            
###Proof of Properties
 - We have to show that (x^e)^d mod N = x mod N
 - The following are true if e,d have been selected as specified.
 - e*d = 1 mod (p-1)(q-1) -> e*d = k(p-1)(q-1) + 1
 - Then check the difference (x ^ (ed) - x) mod N = (x^(k(p-1)(q-1)+1)) -x mod N and what to show that this is 0

###Fermat's Little Theorem
- If p is prime then for all numbers <= a < p
- a^p = a mod p and a^p-1 = 1 mod p
- For example if p is 7 and a is 2 ---> 2^7 = 128 ---> 128 - 2 = 126 which means it needs to be a multiple of p = 18 * 7
- 2^7 = 2 mod 7

###Application of Fermat's
- Rewrite to : x(x^(p-1))^(k(q-1)) mod p = x(1)^(k(q-1) mod p
- x mod p
- Similarly for q you can do the following
    - x^ed = x mod p
    - x^ed = x mod q
    - This means that x^ed - x is a multiple of p and q
    - Then it must be a multiple of N = p * q
- Lets prove this
- a = 3 p =7
- Consider the sets S = {1,2...p-1} = { 0 * 1 mod p , 0 2 mod p , a(p-1) mod p}
- None of these will be zero and none will be equal
- This works because a * i mod p are all distinct and different from zero
- if a*i = s * j mod p

###Summary of RSA
- Bob : Pick 2 large n-bit random prime numbers p and q
    - Publish your public key (N.e) N =p*q and e relative prime to (p-1)(q-1)
    - Compute private key d = e^-1 mod (p-1)(q-1)
- Alice : Generates encrypted messages y = x^e mod N
- Bob : Decode message x = y^d mod N
- To break the system eve must be able to compute the original message x given y and the pub key (N,e)
- Try to guess x so that y = X^e mod N
- Exponential number of guesses as a function of n (number of bits for p,q)
- Alternatively Eve can try to find values p and q so as to compute d = e^d mod (p-1)(q-1)
- What do we know about p and q
- They are both primes and p*q = N
- But this is the factoring problem and is beleived to be u nfactorable

###RSA Opperations and Running Time
- Modular exponentiation y = e^x mod N / x = y^d mod N
- Selected e so relative prime to (p-1)(q-1)
- Compute d = e ^-1 mod (p-1)(q-1)

###Why is this secure?
- To break the system eve must be able to compute x given y and (N,e)
- Try to guess x so that y = x^e mod N Exponential number of guesses as a function of n number of bits for p,q

###Modular Exponentiation
- x^y mod N
- How big can X^y get?
- for 20 bit numbers 2^19.123123
- We need to perform all intermediate computations mod N
- x mod N x^2 mod N x^3 mod N
- if y is 500 bits long then I have to do the multiplication 2^500
- Idea : square every intermediate result
- x mod n to x^2 mod N x^4 n x^16 mod n...
- How many multiplications will you need now ---> log(y)
- How much time does it take to compute each one of them? --> O(n^2) = O(log(y)^2)

###Examples
- x^25 = x ^ (11001 base 2) = x^(10000) * x^(01000) * x^(00001) = x^16 * x^8 * x^1
- function mod exp(x,y,n) if y = 0 return 1
- z = modexp(x,y/2,n)
- if y is even return z^2 mod N
- else return x * z^2 mod N
