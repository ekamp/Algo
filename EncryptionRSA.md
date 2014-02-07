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
