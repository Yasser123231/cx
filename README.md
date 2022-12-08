---
Name: Yasir Almulhim
Topic: [4]
Title: Solution methods for general linear systems.
----
# Solution methods for general linear systems.
You are probably familiar with solving systems of linear equations, such as:
$$y=3x+1$$
$$y=5x-4$$
When you solve this system you get a pair of points that tell you where the two lines intersect. <br>
This can be generalized to n number of variables, and it can be written compactly as:
$$Ax=b$$
where x is nx1 matrix containing all the variables, b is nx1 matrix containing constants, and A is nxn matrix containing all the prefactors (constants). <br>
Note: A can be mxn (where m>n). which will be called linear least square problem. However, I won't discuss it in this article.<br>
How to solve this system on a computer? you might be tempted to say just invert the matrix:
$$x=A^{-1}b$$
while this might not be a bad approach for solving by hand, it is not on computers.[^5]
Different approaches are used to solve this problem. They can be classified as follows:
1. Direct methods
* LU factorization.
* Gauss-Jordan method. 
3. Iterative methods


## Conditioning and sensitivity
One of the most, if not the most, important terms in numerical analysis is the Conditioning of a problem. To explain the concept, imagine that you are calculating the population of E-coli (type of bacteria) per hour. it is modeled that the growth is[^2]:
$$No.population=2^t$$ 
where t represents time is hours. Let's say you were to determine the population number after 26 hours, you will get:
$$2^26=67,108,864$$
Say that you made a mistake and calculated it two minutes later, 
$$2^{26.03}-2^{26}=1,568,595$$
a change by 0.03 in input has changed the output by ~1.5 million. <br>
**Definition**:"A problem is said to be insensitive, or well-conditioned, if a given relative change in the input data causes a reasonably commensurate relative change in the solution. A problem is said to be sensitive, or ill-conditioned, if the relative change in the solution can be much larger than that in the input data".[^1].<br>
According to the definition, the previous example is senstive (ill-conditioned). note that the given problem is the subject of sensitivity, not the algorithm.

## Conditioning of Linear Systems 
to determine whether Ax=b is well-conditioned we compute the **condition number**: 
$$condtion(A)\equiv norm(A)\cdot norm(A^{-1}), \text{A has an inverse}$$
if A does not have an inverse, then by definition:
$$condtion(A)=\infty $$
The closer the number to 1 the better conditioned the problem is. 

## Gauss Elimination Method
Gauss Elimination Method or sometimes called LU Factorization is a way of reducing the matrix to an upper or lower triangular matrix. From which we can use backward substitution or forward substitution , respectively.<br>
<a href="url"><img src="https://user-images.githubusercontent.com/119548062/206345759-bbf6d73b-d81a-414e-9492-000a0e309b54.jpeg" height="400" width="250" ></a> <br>
#### How do we do it?
first we will define
$$m_k=a_i/a_k, i=k+1,...,n$$
$$M_k=I-[0,...,0,m_{k+1},...,m_n]e_k, \text{where ek is the kth column of the identity matrix}$$
Then multiply the system by:
$$M_{n-1}...M_{1}Ax=M_{n-1}...M_{1}b$$
The result will be:
$$M_{n-1}...M_{1}Ax=\text{Upper Trinagular Matrix}=U$$
Although the method seems overwhelming at first, if you apply it to a system it would be much clearer (See Heath, Scientific Computing textbook example 2.13)
the only thing left is to perform backward substitution:
$$x_i= {(b_n-\sum_{j=i+1}^{n}(u_{ij}x_j))}/{u_{ii}}$$
where i goes from zero to n-1 [^3]

### Gauss-Jordan method
Rather than performing backward substitution, we can continue our elimination to get a diagonal matrix. Which seems more compelling. But which method should we use?

## How to Chose a Method in Numerical Analysis
As you will often see in the field of Numerical analysis different methods will be available. However, they often will be different in terms of the number of arithmetic operations or cost. The cost of using LU factorization is proportional to ~ $\frac{3}{2}n^3$ (remember n is the size of the matrix A). While if you want to compute the inverse it will cost $\frac{8}{3}n^3$, nearly three times the cost of the LU. The Gauss-Jordan method requires twice the cost of LU. You might be also wondering why we have not discussed Cramer's rule. The reason is, Cramer's rule costs (n+1)![^4], which if you go to high numbers (larger systems) goes to infinity.

| Method        | cost compared to LU |   
| ------------- |:-------------:| 
| Gauss-Jordan      | 2x |  
| inverse      | 3x      |  
| Cramer's | $\infty$      |   

## Iterative method overview
Iterative methods are used to get the solution with much less cost. However, the trade-off is the accuracy of the solution. Iterative methods are usually used in Partial differential equations, where very large linear systems are formed while solving. The Iterative methods start with an initial guess and iterate to get the next iteration until a certain value of a residual is reached. for example. take the Stationary Iterative Methods which have the form:
$$x_{k+1}=Gx_k+c$$

# Refernces
[^1]:Heath, M. T. (2018). Scientific Computing. In Scientific computing: An introductory survey (p. 13). essay, Society for Industrial and Applied Mathematics. 
[^2]:Chasin, awrence, &amp; Mowshowitz, D. (2000). Exponential growth. Retrieved December 7, 2022, from https://ccnmtl.columbia.edu/projects/biology/lecture1/expogrow.html 
[^3]:Frolov, A. (2022, July 18). Backward substitution. AlgoWiki. Retrieved December 7, 2022, from https://algowiki-project.org/en/Backward_substitution 
[^4]:Novozhilov, A. (2021). computational complexity . Retrieved December 8, 2022, from https://www.ndsu.edu/pubweb/~novozhil/Teaching/488%20Data/08.pdf 
[^5]:Gundersen, G. (2020, December 9). Why Shouldn't I Invert That Matrix? Why shouldn't I invert that matrix? Retrieved December 8, 2022, from https://gregorygundersen.com/blog/2020/12/09/matrix-inversion/ 
