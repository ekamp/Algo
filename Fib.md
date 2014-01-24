#Fibonacci Numbers

##Function Fib(n)
  if(n = 0 || n =1)
    return n
  else
    return fib(n-1) + fib(n-2)
*How much time does it take to solve this problem as a function of n?
*T(n) : number of steps needed to compute Fn
*Problem with this is that there are many computations that are repeated
********************************

##Function fib2
    if(n <= 1)
           return n;
    create an array F[0..n]
    F[0] = 0; f[1] = 1
    for(i = 2; ; n)
    {
        F[i] = F[i-1] + f[i-2];
    }
    return F[n]
    
There will be a linear dependence on input

*So Far all computations were treated as equal cost operations
*Addition can be treated as a single computation step
*But the n-th fibonacci number has 0.694n bits
*Quickly grows bigger than 32 or 64 or register size
*Arithmetic operations on large numbers can be treated as a single step
*We need to think in terms of the representation of numbers
*For example we have a large number n in base b
  You need exactly celi(log base b of (n+1)) digits
  Largest number is N = (b^k)-1
*How much does the size of a number change when we change bases
*The base does not matter

##Cost of addition for 2 numbers
*Example 53 base 2 + 35 base 2 ----> 110101 + 100011 = 1011000 ---> 88
*As a function of the input size I have a linear cost
*What is the cost of fib(n)
    if(n<=1){ T(n) = 1
    if(n >= 2)
    {
      check the value of n
      addition
      T(n-1)
      T(n-2)
    }
  T(n) = 2 + T(n-1) + T(n-2)
  
##Runtime modification
*f(n) = O(g(n))
  if there exists a constant n0 so that
    f(n) <= constant * g(n) for all n >= n0
  f(n) grows no faster than g(n)
  f(n) = n^2
  f2(n) = 2n + 20
  
