# cx
# Solution methods for general linear systems.
You are probably familiar with solving systems of linear equations, such as:
$$y=3x+1$$
$$y=5x-4$$
When you solve this system you get a pair of points which tell you where the two lines intersect. <br>
This can be generalized to a n number of variables, and it can be written compactly as:
$$Ax=b$$
where x is nx1 matrix containing all the variables, and b is nx1 matrix containing constans, and A is nxn or mxn (where m>n) matrix containing all the factors (constants). <br>
How to solve this system, you might be timpted to say just invert the matrix:
$$x=A^{-1}b$$
while this might be a good approach for solving by hand, it is not in computers. To explain why we need to introduce the condtining and senstivity of the problem.
Different approaches are used to solve this problem. They can be classified ass follows:
1. Square linear system
2. Rectaunglar linear system
* Unordered sub-list. 

##Conditioning and senstivity
One of the most, if not the most, important terms in numerical analysis is Condtioning of a problem. To explain the concept imagine that you are claculating population of E-coli (type of bacteria) per hour. it is modeled that the growth is[^2]:
$$No.population=2^t$$ 
where t represents time is hours. Let's say you were to deteramine the population number after 26 hours, you will get:
$$2^26=67108864$$
Say that you made a mistake and calculated two minute later, 
$$2^{26.03}-2^{26}=1,568,595$$
a change by 0.03 in input has changed the output by ~1.5 milion. <br>
**Defintion**:"A problem is said to be insensitive, or well-conditioned, if a given relative change in the input data causes a reasonably commensurate relative change in the solution. A problem is said to be sensitive, or ill-conditioned, if the relative change in the solution can be much larger than that in the input data".[^1].

## Conditioning of Linear Systems 
to deteramine weather Ax=b is well-condtioned we compute the **condition number**: 
$$condtion(A)\equiv norm(A)\cdot norm(A^{-1}), \text{A has an inverse}$$
if A does not have an inverse, then by definition:
$$condtion(A)=\infty $$
The closer the number to 1 the better conditioned the problem is. 

## Gauss Elimination Method
Gauss Elimination Method or sometimes called LU Factorization is a way of reducing the matrix to un upper or lower triangular matrix. From which we can use backward susbtitation or forward subsitation ,respectively.<br>
<a href="url"><img src="https://user-images.githubusercontent.com/119548062/206345759-bbf6d73b-d81a-414e-9492-000a0e309b54.jpeg" height="400" width="250" ></a> <br>
#### How we do it?
first we will define
$$m_k=a_i/a_k, i=k+1,...,n$$
$$M_k=I-[0,...,0,m_{k+1},...,m_n]e_k, \text{where ek is the kth coulmn of the identity matrix}$$
$$M_{n-1}...M_{1}Ax=M_{n-1}...M{1}b$$
$$M_{n-1}...M_{1}Ax=\text{Upper Trinagular Matrix}=U$$
Altough the method seems overwhelming as first, but if you apply it at system it would be much more clearer (See Heath, Scientific Computing textbook example 2.13)
the only thing left is to preform backward substitation:
$$x_i= {(b_n-\sum_{j=i+1}^{n}(u_{ij}x_j))}/{u_{ii}}$$
where i goes from zero to n-1 [^3]



# Refernces
[^1]:Heath, M. T. (2018). Scientific Computing. In Scientific computing: An introductory survey (p. 13). essay, Society for Industrial and Applied Mathematics. 
[^2]:Chasin, awrence, &amp; Mowshowitz, D. (2000). Exponential growth. Retrieved December 7, 2022, from https://ccnmtl.columbia.edu/projects/biology/lecture1/expogrow.html 
