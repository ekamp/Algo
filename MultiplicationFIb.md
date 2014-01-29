##Fib review

    for(i = 2; i < n; n++)
    {
      fib[n] = fib[n-1] + fib[n-2]
    }
  
  - The addition is the O( of the number of bits in the numbers added) = O(n)
  - The nth Fib number needs .7n bits to be represented
  - Total cost of both lines therefore is O(n^2)
  - f(n) = OMEGA(g(n)) in this case f(n) grows faster than g(n)
  - f(n) = O(g(n)) in this case f(n) runs at the same speed as g(n)
  - Example : 
        f(n) = SQRT(2)^(ln(n))
        g(n) = SQRT(n)
      
        log(SQRT(2))^ln(n) = log(SQRT(n))
        log(n)*ln(2)^(1/2) = ln(n)^(1/2)
        1/2 * ln(n) * log(2) = 1/2ln(n)
        log(n) = log(n)

##Multiplication of n-bit numbers
 Numbers in the order of N (n = log(n))
 
 - Example 13 * 11 = 143 BUT how long does this take?
    - There are n-rows
    - To compute each row either x or 0 is left-shifted
    - In the order of 2n bits
    - You have to sum the rows
    - Do this pairwise O(n) times
    - Each time the cost is O(n)

###Alternative Multiplication
- Two decimal numbers x and y write them next to each other 
- 11 -> 5 -> <del>2</del> -> 1  (Take the half and floor of the number)
- 13 -> 26  -> <del>52</del> ->104 (At the same time your doubling the other number the same number of times)
- Then sum the 13 column ignoring columns in the first row that contain even numbers

####Summarization of this algorithm
    x * y = 2 (x*(y/2)) if y is even
    OR
    x * y = x + 2 ( x * (y/2)) if y is odd
    
#####Run Time
- Will Terminate after <b>log(y)</b> calls since y is halved at each iteration
- The cost of each iteration is : 
    - The expensive operation is addition if y is odd
    - O(n) due to addition
    - Overall again its <b>O(n^2)</b>

##Modular Arithmetic
    if(x = q * n + r with 0 <= r < N
    {  
    //then x and r are congruent modulo N
    //this also means tha N divides x -r
    }
- Therefore what is 253 congrunent mod 60 
    - <b>13</b> closest is 4 which is 240 difference of 13
    - Modular arithmetic limits numbers to a perspecificed range that wrap around when you try to leave this range
            if (x=x') mod N and y = y' mod N
            Then x * y = x' * y' mod N
            x + y = x' + y' mod N
    - For example 2*25 CON xmod 24 -> 2AM
- *Associativity* : x + (y + z) = (x + y) + z mod N
- *Communitivity* : xy = yx mod N
- *Distributivity* : x(y + z) = xy + xz mod N
- 2^345 = (2^5)&^69 = 32^69 = 1 mod 31

###Running Time

####Modular Addition
- x and y are in the range 0...N-1
- The sum can be up to 2N-2
- if the sum exceeds N-1, merely subtract N from the sum to bring it within range
- Therefore it takes O(n)

####Modular multiplication
- THe product can be in the order of (n-1)^2
- The product will be at most 2n bits long since you can take the log(n-1)^2 = 2log(N-1) <= 2n
- x = qN + r
- Divide with N to find how many times N can be in the product (q) subtract q * N from product
- Overall this will take <b>O(n^2)</b>

