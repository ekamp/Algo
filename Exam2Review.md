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
    - Running n subproblems to find the result O(n<sup>2</sup>)

###Longest Common Subsequence
- Used to find the longest subsequence common to all subsequences in a set of sequences many times only two.
- This is used many times to compare two files within a file system also can be used to compare two strains of DNA
- Need to see if one sequence is a subsequence of another
- Given two sequences X and Y we say that Z is a subsequence of X and Y if Z is contained within both X and Y
- In the longest common subsequence given X and Y we wish to find the max length subsequence present in both x and y
<b>Procedure</b>
  - <b>Brute Force</b>
    - Enumerate all subsequences of X and check if it is a subsequence of Y
    - Since we have m subsequences this approach will take 2<sup>m</sup> time
  - <b>Recursion</b>
      - Assuming that c[i,j] is the length of the LCS
        - c[i,j] = 
          - 0 if i = 0 or j = 0
          - c[i-1,j-1] if i,j > 0 and x<sub>i</sub> = y<sub>j</sub>
          - max(c[i,j-1],c[i-1,j]) if i,j > 0 and x<sub>i</sub> != y<sub>j</sub>
</br>
<b>Finding the previous pointer for a digit</b>
- Find c[i,j] for x<sub>i-1</sub> and y<sub>j</sub>
- Find c[i,j] for x<sub>i</sub> and y<sub>j-1</sub>
- Determine the difference
</br>
- The runtime to find the longest common subsequence is O(X.length * Y.length)</br>
<b>Psedocode Find the Length of the LCS</b>
~~~c
  int m = X.length;
  int n = Y.length;
  let b[] and c[] be the new tables

  for(i = 1 to m)
  {
    c[i,0] = 0
  }
  for(j = 0 to n)
  {
    c[0,j] = 0
  }
  for(i = 1  to m)
  {
    for(j = 1 to n)
    {
      if(x<sub>i</sub> == y<sub>j</sub>
      {
        c[i,j] = c[i-1,j-1] + 1
        b[i,j] = c[i-1,j-1] + 1
      }
      else if(c[i-1,j] >= c[i,j-1]
      {
        c[i,j] = c[i-1,j]
        b[i,j] = c[i-1,j]
      }
      else
      {
        b[i,j] = c[i,j-1]
      }
    }
  }
  return c and b
~~~
<i>Running time for this is O(mn) since each entry takes O(1)</i>


###Finding the LCS of two strings or of two subsequences
- Finding the LCS of two strings hinders on two properties
    - First property (If the two strings end in the same character)
        - For example BANANA and ATANA
        - Remove and store the same last element until no common element between the strings is found, we find (ANA)
        - Now we look at the remaining seqences (BAN , AT)
        - Using inspection we see that the common sequences here is just A
        - Now append the removed elements to the element(s) found by inspection and we get out answer (AANA)
        - More formally we say that : 
            - x<sub>n</sub> = y<sub>m</sub> = LCS(x<sub>n</sub> , y<sub>m</sub>) = LCS(x<sub>n-1</sub> , y<sub>m-1</sub>)x<sub>n</sub>
    - Second Property (If the two strings do not end in the same character
        - We need to then find the LCS(x<sub>n-1</sub>,y<sub>m</sub>) and LCS(x<sub>n</sub>,y<sub>m-1</sub>)
        - For example we have X : ABCDEFG and Y : BCDGK, the LCD(X,Y) either ends in G or does not
            - Case ends in G
                - Therefore it cannot end in K so we remove k from the sequence Y getting BCDG, and now we can say that LCS(x<sub>n</sub>,y<sub>m</sub>) = LCS(x<sub>n</sub>,y<sub>m-1</sub>)
            - Case does not end in G
                - Then we remove G from X and get ABCDEF and therefore say that LCS(x<sub>n</sub>,y<sub>m</sub>) = LCS(x<sub>n-1</sub>,y<sub>m</sub>)
            - Therefore based on either case we are either looking for LCS(x<sub>n</sub>,y<sub>m-1</sub>) or LCS(x<sub>n-1</sub>,y<sub>m</sub>) which are both subsequences of X and Y therefore the longer one will become out LCS
</br>
<b>Strategy</b>
- Given two sequences X and Y
- If X and Y are equal return x<sub>n</sub>,y<sub>m-1</sub> or x<sub>n-1</sub>,y<sub>m</sub>
- Otherwise compare LCS(x<sub>n</sub>,y<sub>m-1</sub>) and LCS(x<sub>n</sub>,y<sub>m-1</sub>) continuing to compare until similarities are found and return the largest similarity

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
</br>
<b>Pseodocode</b>

~~~c
for(i = 1 to n)
{
  C(i,i) = 0
}
for(s = 1 to n-1)
{
  for(i = 1 to n-s)
  {
    j = i+s
    C(i,j) = min{C(i,k) + C(k+1,j) + m<sub>i-1</sub> * m<sub>k</sub> * m<sub>j</sub> : i <= k < j}
  }
  return C(1,n)
}

~~~

<b>Runtime O(n<sup>3</sup>)</b>

####Multiplication Given Dimensions
- Given the dimensions of matricies compute the number of operations necessary to multiply all of them together
- For example consider the matricies A<sub>1</sub>[10,100] , A<sub>2</sub>[100,5] , A<sub>3</sub>[5,50]
- In order to compute the number of operations needed to get the product of all the matricies we need to compute the different sets of multiplication as follows.
    - ((A<sub>1</sub>A<sub>2</sub>)A<sub>3</sub>) we compute 10 * 100 * 5 = 5,000 multiplications (A1 A2) the 10 * 5 * 50 2,500 for (A12 A3) = 7,500
        - Basically A1 * A2 will result in [A1.x,A2.y] then we do A1.x * A2.y * A3.y -> Prod 2 -> Answer = Prod1 + Prod2 
    - (A<sub>1</sub>(A<sub>2</sub>A<sub>3</sub>)) we compute 100 * 5 * 50 = 25,000 multiplications(A2,A3) and 100 * 50 * 100 = 50,000 -> 50,000 + 25,000 = 75,000 multiplications
    - Therefore from this result we see that we should choose the first grouping which takes 7,500 multiplications

###Knapsack Problem
- During a robbery  burglar finds much more loot than he intended on carrying and has to decide what to take
- His bag can hold w pounds, and there are n items of value v<sub>i</sub> and weight w<sub>i</sub>
- This can be solved in <b>O(nw)</b> time


<b>With Repetition</b>

- If we say that K(w) will give us the optimal solution we can assume the following
    - If item i is in the optimal solution set then we can remove i and say that the remainder items are K(w-w<sub>i</sub>) + v<sub>i</sub>
    - Since we do not know which i will result in the max solution we remove different items until a max is found
    - We continue this until all the weights have been explored and optimized
~~~c
  K(0) = 0 ;
  for(w = 1 to W)
  {
    K(w) = max{K(w-wi - vi) : wi <= w}
  }
return K(W)
~~~

<b>Without Repetition</b>
- Unlike before with repeptition we now have to consider if the item has been used before so we make sure 0 <= j <= n where j is the number of items.
- And now we say that K(w,j)  = max value using capacity w and number of items j
- Now its like before we need to see if the item needs to be in the optimal set so we say the following : 
    - K(w,j) = max { K(w - w<sub>j</sub> , j-1) + v<sub>j</sub> , K(w,j-1)}
- Now the algo involves filling out a 2d table and looks liike the following 
- Running time for this algo remains the same at O(nw)

~~~c
  //Initialize all K(0,j) = 0 and all k(w,0) = 0
  for(j = 1 to n)
  {
    for(w = 1 to n)
    {
      if(wj > w)
      {
        k(w,j) = k(w,j-1)
      }
      else
      {
        K(w,j) = max{ K(w,j-1), K(w-wj,j-1) + vj}
      }
    }
  }
  return K(W,n)
~~~
</br>
<b>Example Problem</b>
//none T_T

####Determining the number of subproblems
- If the input to a problem is x<sub>1</sub>...x<sub>n</sub> and the subproblems identified by a dynamic programming solution have the form x<sub>1</sub>...x<sub>i</sub>, i<= n how many subproblems exist? Similarly for inputs x<sub>1</sub>...x<sub>n</sub> and y<sub>1</sub>...y<sub>n</sub> where subproblems are x<sub>1</sub>,x<sub>i</sub>(1<=n) and y<sub>1</sub>...y<sub>j</sub>(j<=m). Similarly for input x<sub>1</sub>...x<sub>n</sub> and subproblems x<sub>i</sub>...x<sub>j</sub>
- Based on previous problems there should be i * n  subproblems taking O(ixn) time to run

###Adjancency Matrix Representation for Graphs
- Represented by an n x n array where the a<sub>ij</sub>th entry is a 1 if theres an edge from v<sub>i</sub> to v<sub>j</sub> and a 0 if there is no edge between v<sub>i</sub> and v<sub>j</sub>

####Advantages
- Presence of an edge can be found in constant time with only one memory access

####Disadvantages
- Takes O(n<sup>2</sub>) space to store the graph
- Many graphs are sparse in practice meaning they have relatively few edges

###Adjancency List Representation for Graphs
- The size of this representation is the size of the edges. Contains a linked list per vertex. The linked list for the vertex holds all verticies it has an outgoing edge to. This way an edge only appears once if directed or twice if undirected.

####Advantages
- Size of the graph representation is now O(|e|) where e is the number of edges
- Better for sparse graphs and in general takes less space

####Disadvantages
- Takes longer to iterate through to see if an edge is contained O(e) worst case

