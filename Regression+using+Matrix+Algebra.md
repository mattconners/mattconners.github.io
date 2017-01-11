
# Least Squares Regression Solved with Matrix Algebra

This is an explanation of Least Squares Regression solved using matrix algebra.  


### Some sample data  
Let's start with a simple set of data for sales and price  
y = the number of units sold  
x = price per unit  
The data shows that when prices are high, the quantity sold is low, and when prices are low the quantity sold is high.


```R
y <- c(124,95,71,45,18);y # quantity sold
x <- c(49, 69, 89, 99, 109);x #price per unit
```


<ol class=list-inline>
	<li>124</li>
	<li>95</li>
	<li>71</li>
	<li>45</li>
	<li>18</li>
</ol>




<ol class=list-inline>
	<li>49</li>
	<li>69</li>
	<li>89</li>
	<li>99</li>
	<li>109</li>
</ol>



### Least squares regression equation  


for points $(x_1,y_1), (x_2,y_2)...(x_n,y_n)$  the least square regression line is:  
$f(x)=\beta_0 + \beta_1x + e$   

The errors (also referred to as residuals) are the difference bdtween the actual quantity sold and the regression estimate of the quantity sold. They are    
$e_i=y_i-f(x_i)$ 

The $\beta$ coefficients are those values which minimize the sum of squared errors using the regression function f(x)  
$(y_1-f(x_1))^2$ +$(y_2-f(x_2))^2$ + . .$(y_n-f(x_n))^2$  
 
Goal: minimize sum of squared residuals(SSR) where  
$SSR=\sum_{i=1}^{n}{e_i}^2$    

We can set this up as a system of equations and then solve using matrices  
$y_1 = (b + mx_1) + e_1$  
$y_2 = (b + mx_2) + e_2$  
...  
$y_n = (b + mx_n) + e_n$   




--- 
## Single variable regression represented in matrix form  
We can represent our x and y data in matrix form  
$Y = \left[\begin{array}{rrr}
y_1\\
y_2\\  
y_n
\end{array}\right]$  This is an N x 1 matrix

$X = \left[\begin{array} {rrr}
1 & x_1\\
1 & x_2\\  
1 & x_n
\end{array}\right]$  This is a N x 2 matrix. The column of 1s is for the intercept.    
Note: if this were multivariate problem with k variables (x's), it would be a N X (1 + k) matrix

$B = \left[\begin{array} {rrr}
b_0\\
b_1
\end{array}\right]$  This is a 2 x 1 matrix  
Note: if this were multivariate problem with k variables (x's), it would be a (1+k) X 1 matrix


$E = \left[\begin{array} {rrr}
e_1\\
e_2\\  
e_n
\end{array}\right]$  This is a N x 1 matrix  


### Matrix form of regression equation    
$Y = XB + \epsilon$    
Regression assumes zero errors (ie some are positive some are negative and should average to zero), so we drop $\epsilon$  
Y = XB  

#### Solve for B    
Y = XB  
First we put X into a square matrix. We can do that by multiplying by the transpose $X^` $ which gives us a 2x2 matrix     
$X^` Y = (X^` X) B$    
<br>Next, to isolate B we'll divide both sides by $(X^`{X})$ (this is the same as multiplying both sides by $(X^`{X})^{-1}$    
$(X^`{X})^{-1} (X^`{Y}) = (X^`{X})^{-1} (X^` X) B$  
<br>Next, noting that a matrix multipled by its inverse is the Identity Matrix I we simplfy the equation to    
$(X^`{X})^{-1} (X^`{Y}) = IB$    
<br>Finally, noting that any matrix multiplied by the identity matrix is itself. So IB = B. Therefore this simplifies to  
$B = (X^`{X})^{-1} (X^T`{Y})$ 
 

--- 
## An alternative explanation  
$ SSE = \sum_{i=1}^{n}{e_i}^2$ is the forumula we are trying to minimize. We want the sum of these errors (squared) as small as possible.

To convert this formula to matrix notation we can take the vector of errors and multiply it by the transpose.

$SSE = E^`E$  
We can confirm that this gives us the sum of squared errors. Let's assume errors are (4, 6, 3). This equation results in a row vector [4 6 3] multiplied by a column vector
$\left[\begin{array} {rrr}
4\\
6\\  
3
\end{array}\right]$ Resulting in 4x4 + 6x6 + 3x3  which is what we want: the sum of the squared errors.

Remember, that $\epsilon$ is equivalent to  $Y -X{\beta}$. Thus  
$E^`E  = (Y -X{\beta)}^`(Y -X{\beta}) $   
<br> Next, multiply out.  
$(Y^` - (X\beta)^`) (Y -X{\beta})$  
$Y^`Y - (X\beta)^`Y - Y^`(X{\beta}) + (X\beta)^`X{\beta}$  
$Y^`Y - 2YX^`\beta^` + X^`\beta^`(X\beta)$ 

<br>We take the derivative with respect to b and set it to zero.  
$-2X^`Y + 2X^`X\beta=0$    
$-X^`Y + X^`X\beta=0$  
$X^`X\beta =X^`Y$  
#### Solve for $\beta$  
isolate $\beta$ by dividing both sides by $(X^`X)$. Note, this is the same as multiplying by $(X^`X)^{-1}$  
$(X^`X)^{-1}(X^`X)\beta = (X^`X)^{-1}(X^`Y)$  
$\beta = (X^`{X})^{-1} (X^`{Y})$ 

## Find $\beta$ coefficients using matrix algebra from our sample data


$\beta = (X^`{X})^{-1} (X^`{Y})$ is our regression equation 

Recall our sample data for sales and prices  
y = the number of units sold  
x = price per unit  


```R
x
y
```


<ol class=list-inline>
	<li>49</li>
	<li>69</li>
	<li>89</li>
	<li>99</li>
	<li>109</li>
</ol>




<ol class=list-inline>
	<li>124</li>
	<li>95</li>
	<li>71</li>
	<li>45</li>
	<li>18</li>
</ol>



Let's convert the vectors for x and y into matrix Y and matrix X


```R
Y <- as.matrix(y);Y
X <- matrix(c(rep(1, length(x)), c(x)), nrow = 5, ncol = 2);X
```


<table>
<tbody>
	<tr><td>124</td></tr>
	<tr><td> 95</td></tr>
	<tr><td> 71</td></tr>
	<tr><td> 45</td></tr>
	<tr><td> 18</td></tr>
</tbody>
</table>




<table>
<tbody>
	<tr><td>1  </td><td> 49</td></tr>
	<tr><td>1  </td><td> 69</td></tr>
	<tr><td>1  </td><td> 89</td></tr>
	<tr><td>1  </td><td> 99</td></tr>
	<tr><td>1  </td><td>109</td></tr>
</tbody>
</table>



### Step 1: Calculate $(X^`{X})^{-1}$  
From $\beta = (X^`{X})^{-1} (X^`{Y})$ calculate just the $(X^`{X})^{-1}$ part  


```R
options(digits=2)
cat("The x vector")
X
cat("The x transpose")
XTrans <- t(X); XTrans #transpose of X 
cat("Product of X transpose and X")
XTransX <- XTrans %*% X; XTransX # product of X transpose and X
cat("(Inverse of product of X Transpose and X")
XTransXInv <- solve(XTransX); XTransXInv #inverse of X traspose times X

```

    The x vector


<table>
<tbody>
	<tr><td>1  </td><td> 49</td></tr>
	<tr><td>1  </td><td> 69</td></tr>
	<tr><td>1  </td><td> 89</td></tr>
	<tr><td>1  </td><td> 99</td></tr>
	<tr><td>1  </td><td>109</td></tr>
</tbody>
</table>



    The x transpose


<table>
<tbody>
	<tr><td> 1 </td><td> 1 </td><td> 1 </td><td> 1 </td><td>  1</td></tr>
	<tr><td>49 </td><td>69 </td><td>89 </td><td>99 </td><td>109</td></tr>
</tbody>
</table>



    Product of X transpose and X


<table>
<tbody>
	<tr><td>  5  </td><td>  415</td></tr>
	<tr><td>415  </td><td>36765</td></tr>
</tbody>
</table>



    (Inverse of product of X Transpose and X


<table>
<tbody>
	<tr><td> 3.169  </td><td>-0.03578</td></tr>
	<tr><td>-0.036  </td><td> 0.00043</td></tr>
</tbody>
</table>



### Step 2:  Calculate $(X^`{Y})$  
From $\beta = (X^`{X})^{-1} (X^`{Y})$ calculate just the $(X^`{Y})$ part   


```R
XTransY <- XTrans %*% Y; XTransY
```


<table>
<tbody>
	<tr><td>  353</td></tr>
	<tr><td>25367</td></tr>
</tbody>
</table>



### Step 3: Summarize: find $\beta$ coefficients $\beta = (X^`{X})^{-1} (X^`{Y})$  
multiply step 1 x step 2


```R
options(digits=3)
B <- XTransXInv %*% XTransY;
```

### The $\beta$ coefficients are


```R
B
```


<table>
<tbody>
	<tr><td>211.27</td></tr>
	<tr><td> -1.69</td></tr>
</tbody>
</table>



### Check that $\beta$  coefficients from matrix form are the same as from R linear regression model


```R
cat("The coefficients using R's linear regression model are")
lm <- lm(y~x)
print(lm$coefficients,digits=3)
cat("The coefficients we calculated previosly with matrix algebra are the same")
B
```

    The coefficients using R's linear regression model are(Intercept)           x 
         211.27       -1.69 
    The coefficients we calculated previosly with matrix algebra are the same


<table>
<tbody>
	<tr><td>211.27</td></tr>
	<tr><td> -1.69</td></tr>
</tbody>
</table>



### Calculate estimates for Y from regression model  


```R
fx <- B[1, 1] + (x * B[2, 1])  
cat(fx,digits=3)
```

    128 94.3 60.4 43.5 26.5 3

### Calculate errors and SSE


```R
Ei <- y - fx
cat("The residuals are ")
cat(Ei)

```

    The residuals are -4.22 0.672 10.6 1.52 -8.53


```R
SSE <- t(Ei) %*% Ei 
cat("The SSE (sum of squared errors) is ")
cat(SSE)
```

    The SSE (sum of squared errors) is 205
