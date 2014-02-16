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

##Arithmetic

###Addition
- Addition should take O(n) time assuming that were adding thousand bit numbers
- bits <= 32 bit will take O(1) time

###Multiplication/Division
- Multiplication and Division should take O(n^2) time again using the assumption that the numbers are many bits long


##Modular Arithmetic
- <b>Modular Arithmetic</b> is a system used for dealing with restricted ranges of integers.
- <b>x modulo N</b> is seen as the remainder when x is divided by N.
- <b>Congruent Modulo</b> x and y are congruent modulo if the differ by a multiple N
  - For example 253 is congruent modulo to 13 mod 60 because ---> 253-13 = 240 which is a multiple of 60
  - <b>Substitution Rule</b> if x congruent to x' (mod N) and if y congruent to y' (mod N) then :
    - x+y is congruent to x' + y' (mod N) and x*y is congruent to x' * y' (mod N)
    - <b>Distributive Properties</b>
      - Associativity : x + (y+z) is congruent to (x + y) + z (mod N)
      - Communitivity : xy is congruent to yx (mod N)
      - Distributivity : x(y + z) is congruent to xy + xz (mod N)

###Modular Addition

- To add two numbers x and y we start off with simple addion and then subtract off N to bring it back to the range of 0 to N-1
- Therefore the runtime for this should be linear or O(n) where n is celi(log(n))

###Modular Multiplication
- To multiply two numbers x and y we again just multiply and then divide off N in order to get within the proper range.
- Thus this operation will take O(n^2) time

###Modular Division
- Division has a tricky case of dividing by zero, and with mod division there are even more which increases the runtime of this operation.
- Therefore this operation takes O(n^3) time

##Euclids Rule
- If x and y are positive integers with x >= y then the gcd(x,y) = gcd(x mod y,y)
- gcd(x,y) = gcd(x - y, y)

##Modular Division
- <b>Multiplative Inverse</b> x is the multiplative inverse of a modulo N if ax is congruent to 1 (mod N)
- It will take O(n^3) time to find the multiplative inverse.
- This can be found by running the extended Euclid Algorithm

##Primality Testing
- <b>Fermats little theorem</b> If p is prime, then for every 1 <= a < p, a^(p-1) is congruent to 1 (mod p)
- For example if a=3 and p=7 then wed get 3^(7-1) is congruent to 1 (Mod 7)
- Fermats theorem fails for a rare subset of numbers called carmicheal numbers
- Carmicheal numbers pass Fermats for all a relatively prime to N.
- If we ignore such numbers we can conclude that :
  - if N is prime then a^(N-1) is congruent to 1 (mod N) for all a < N
  - if N is not prime then a^(N-1) is congruent to 1 mod N for at most half the valuesof a < N

##Generating Random Prime numbers
- <b>Lagrange's prime number theorem</b> let pi(x) be the number of primes <= x, then pi(x) is approximately x/ln(x)
- In other words we need to : Pick a random n-bit number N, run primality test on N, If it passes output N else repeat the process.
- This process will take O(n) time

##Cryptography
- <b>One-time pad</b>: secretly choose a binary string r of the same length n-bits as the imported message x that will be sent. Therefore once the message is sent all that needs to be done to decode the message would be to run the encryption algo again. This is acheived via exclusive or, both parties exclusive or the message in order to get the correct result.
- However if a third party intercepts the message all they would have to do is intercept another message to figure out the encryption. x XOR y and x XOR z ---> y XOR z to get the schema and decode the rest of the messages.
- <b>Advanced Encryption Standard</b> Again both parties agree on a random string r however this time the string has a relatively small length such as 128 bits. Then specifies a bijection from 128 bit strings to 128 bit strings.
- For example for a long string or message once sent or encrypted one applys the encryption to each 128 bit segment of the larger string. In order to decode one does the same. At present time general public cannot crack this encryption.
- <b>RSA Encryption</b> : the sender has a public key which encrypts the data. Once sent and recieved the data is decrypted via the recievers private key. 
- RSA scheme is : the encryption function(modulo N) is a bijection on 0 ---> N-1 and the decryption is its inverse.

##Divide and Conquer Algorithms
- Solves a problem by breaking it into subproblems, recursively solving the subproblems and approriately combining their answers.
- T(n) = aT(celi(n/b)) + O(n^d) runtime
- The maximum number of operations the algorithm needs

###Masters Method
- Used to analyse recursive / recurrances (black box for solving recurrences)
- Recurrance formatting
  - Base case : T(n) <= a constant meaning we hit one number
  - For larger n : T(n) <= aT(n/b) + O(n^d)
  - Where a is the number of recursice calls
  - b is the factor by which the input size shrinks from recursion
  - d is the amount of work done outside of the recursive calls
  - These are all independent on the input size n
- Guass's integer multiplication :
  - Algo : Recursively compute ac, ba , (a +b)(c+d)
  - Recurance : 
    - Base case : T(1) <= a constant 
    - For all n > 1 : T(n) <= 3T(n/2) + O(n)
- Master Method has three different runtimes :
  - O(n^d * log(n)) if a = b^d
  - O(n^d) if a < b^d
  - O(n^logb(a)) if a > b^d

####Master Method Examples
- <b>Merge Sort</b> :
  - a = 2 recursive calls
  - b = 2 reduction
  - d = 1 meaning linear work out of recursion
  - case 1 a = b^d ---> 2 = 2^1 
  - runtime therefore is O(nlogn)
- <b>Binary Search</b> 
  - a = 1 recursive call
  - b =2 reduction
  - d = 0 work outside of recursion
  - again this is in case 1
  - therefore we have a runtime O(logn)
- <b>Grade school multiplication non-Gauss</b> 
  - a = 4
  - b = 2
  - d = 1
  - 4 > 2^1
  - Case 3 O(n^logb(a)) which is O(n^(log2(4)) = O(n^2)
- <b>Gauss's Multiplication</b>
  - a = 3
  - b = 2
  - d = 1
  - 3 > 2^1
  - Case 3 O(n^(log2(3))) = O(n^1.6)

