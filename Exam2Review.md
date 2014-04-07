#Exam 2 Review

##Greedy Algorithms
###Main Principle
Greedy algorithms build up to a solution peice by peice always choosing the solution that will yeild the most obvious and immediate benefit

###Coin Changing Problem US Currentcy
- The coin changing problem is the following : Someone wants to give change to a customer in coins whats the best way?
  - The highest coin is chosen that does not exceed the amount of change currently left to give.
  - This loop continues until there is no more change to give
  - For example if change is 35 cents then it starts by selecting a quarter which is 25 cents then a dime and so on

###Huffman Coding
<i>Huffman Coding is used to compress data in order to save space</i>
- In order to save space Huffman coding uses a prefix-free binary tree in order to encode
- In order to optimize the tree and save as much space as possible we want to make sure each leaf corresponds to a symbol
- In this method the number of bits required for a symbol is exactly the depth of the tree
- Alternatively we can calculate the cost by seeing that the frequency of any node is the sum of the frequencies of decendant leaves.
- <b>The cost of a tree is the sum of the frequencies of all leaves and nodes except the root.</b>
- <i>We also know that the lowest frequencies must be at the botton of the tree</i>
- To construct the tree first find the two nodes with the lowest frequency i and j and assign them to a node with the frequency i +j
- Continue this process until all frequencies are represented as leaves in the tree.
- Building the tree will take O(nlog(n)) time if a heap is used

###Horn Formulas
- A set of expressions with literals Implications and Negative Clauses
- Implications :
    - Left hand side is an AND of any number of positive literals
    - Right hand side is a single positive literal  (z^w) -> u
- Negative Clauses
  - Consists of an OR of any number of negative literals   (!u OR !v OR !y)
- Given the set of clauses the goal is to determine whether there is a consisten explaination that satisfies them
- <b>Strategy</b>
    - Start with all variables as false
    - Then we start to make some true one by one only to satify the implications (RHS)
    - Then turn to the negative clauses and make sure their satified
- If a certain set of variables is set tot true, then they must be true in any satisfying assignment.

###Set Cover
<b>Basically how many elements out of a set are needed to satisfy some condition</b>
- An example is suppose you have a set of schools Si and you want to see how many schools from the set will cover the country, essencially outputting a set of Sx Schools
- More generally we can see that B contains n elements and that the optimal cover consists of k sets, then the greedy will use (kln(n)) sets.
- <b>Strategy</b>
    - Use greedy to grab the largest sets first without going over the contraint
    - School example (grab school that covers the largest without going over and second largest w/o going over and so on)
- Let nt be the number of elements still not covered after t iterations, k sets are needed for optimal therefore nt/k extra will me needed.
- nt+1 <= nt - nt/k = nt(1 - 1/k)
- The approximation value of this greedy vs optimal is ln(n)

##Elements of Dynamic Programming

###Longest Increasing Subsequences
- Input : sequence of numbers a1...an
- Subsequence is a set of numbers and an increasing subsequence is one that increases from left to right
- For example 5,2,8,6,3,6,9,7 longest subsequence is 2,3,6,9 when put in graph form this is called a dag
- Once turned into a graph we want to find the largest subsequence by setting L(j) = 1 + max{L(i) : i,j within e} for each subproblem
- <b>Running Time</b>
    - Building the graph <i>O(n)</i>
    - Running n subproblems to find the result O(n^2)

###Matrix Chain Multiplication
<i>Given a sequence or chain of A1...An of n matricies to be multiplied we wish to compute the product A1,A2...An</i>
- This multiplication is associative so all parenthesizations yield the same product
- <b>Fully Parenthesized</b> : if it is a single matrix or the product of two martricies surrounded by parens
- For example {A1,A2,A3,A4} can be fully parenthesized in the following way
    - (A1(A2(A3A4)))
    - (A1((A2A3)A4))
    - ((A1A2)(A3A4))
    - ((A1(A2A3))A4)
    - (((A1A2)A3)A4)
- We can multiply two matricies A and B only if they are compatible meaning that one matricy must have the same number of columns as the other matricy has rows.
- Due to this some groupings of chains are more efficient being that multiplying 100 rows 5 times is faster than multiplying 10 rows 5 times.
- <b>Matrix-chain multiplication problem</b> : given a chain of matricies {A1,A2,A3...An} fully parenthesize the product in a way that minimizes the number of scalar multiplications.
<b>Strategy</b>
- Take the sequence of matricies and seperate out into two subsequences
- Find the minimum cost of multiplying out the subsequences
- Add the costs together and the cost of multiplying the resultant frequencies
- Do this where each sequence can be split and take the minimum
- To make sure that it is O(n<sup>3</sup>) we have to use memorization to remember common pairs so we do not redundantly compute values

<b>Pseodocode</b>

~~~c
for(int i = 0 ; i < 1; i++)
{
}
~~~

<b>Runtime O(n<sup>3</sup>)</b>

####Multiplication Given Dimensions
- 