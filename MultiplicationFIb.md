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
      1/2 * ln(n) * log(2) = ...
      

      
  
