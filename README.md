# cx
#Solution methods for general linear systems.
You are probably familiar with solving systems of linear equations, such as:
$$y=3x+1$$
$$y=5x-4$$
When you solve this system you get a pair of points which tell you where the two lines intersect. <br>
This can be generalized to a n number of variables, and it can be written compactly as:
$$Ax=b$$
where x is nx1 matrix containing all the variables, and b is nx1 matrix containing constans, and A is nxn matrix containing all the factors (constants). <br>
How to solve this system, you might be timpted to say just invert the matrix:
$$x=A^{-1}b$$
while this might be a good approach for solving by hand, it is not in computers. 
##
