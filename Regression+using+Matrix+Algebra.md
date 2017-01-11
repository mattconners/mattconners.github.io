
# Least Squares Regression Solved with Matrix Algebra

This is an explanation of Least Squares Regression solved using matrix algebra.  
Purpose: understand the concept of least squares and how to find minimum sum of squared errors using matrix algebra.

Start by creating two vectors for x and y  
Scenario: x are prices, y are sales


```R
x <- c(49, 69, 89, 99, 109)
y <- c(124,95,71,45,18)
```

Create X and Y Matrices


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



Least Squares Linear Equation  

for points $(x_1,y_1), (x_2,y_2)...(x_n,y_n)$  the least square regression line is:  
$f(x)=\beta_0 + \beta_1x + \epsilon$     

which minimizes the sum of squared errors using the regression function f(x)  
$(y_1-f(x_1))^2$ +$(y_2-f(x_2))^2$ + . .$(y_n-f(x_n))^2$  
Errors (residuals)are  
$\epsilon_i=y_i-f(x_i)$  

Goal: minimize sum of squared errors

$SSR=\sum_{i=1}^{n}{e_i}^2$    

Set up as a system of equations and then solve using matrices  
$y_1 = (b + mx_1) + \epsilon_1$  
$y_2 = (b + mx_2) + \epsilon_2$  
...  
$y_n = (b + mx_n) + \epsilon_n$   

$Y = \left[\begin{array}{rrr}
y_1\\
y_2\\  
y_n
\end{array}\right]$  

$X = \left[\begin{array} {rrr}
1 & x_1\\
1 & x_2\\  
1 & x_n
\end{array}\right]$  

$B = \left[\begin{array} {rrr}
b\\
m
\end{array}\right]$  

$E = \left[\begin{array} {rrr}
e_1\\
e_2\\  
e_n
\end{array}\right]$  

Form of final equation  
$Y = XB + E$  
$XB = Y - E$  
$B = (Y - E) / X$

Solve for B  
$B = (X^T{X})^{-1} (X^T{Y})$  
$SSE = E^TE$

### Step 1: Calculate $(X^T{X})^{-1}$


```R
options(digits=2)
print("The x vector")
X
print("x transpose")
XTrans <- t(X); XTrans #transpose of X 
print("product of X transpose and X")
XTransX <- XTrans %*% X; XTransX # product of X transpose and X
print("(XInverse of product of X Transpose and X")
XTransXInv <- solve(XTransX); XTransXInv #inverse of X traspose times X

```

    [1] "The x vector"



<table>
<tbody>
	<tr><td>1  </td><td> 49</td></tr>
	<tr><td>1  </td><td> 69</td></tr>
	<tr><td>1  </td><td> 89</td></tr>
	<tr><td>1  </td><td> 99</td></tr>
	<tr><td>1  </td><td>109</td></tr>
</tbody>
</table>



    [1] "x transpose"



<table>
<tbody>
	<tr><td> 1 </td><td> 1 </td><td> 1 </td><td> 1 </td><td>  1</td></tr>
	<tr><td>49 </td><td>69 </td><td>89 </td><td>99 </td><td>109</td></tr>
</tbody>
</table>



    [1] "product of X transpose and X"



<table>
<tbody>
	<tr><td>  5  </td><td>  415</td></tr>
	<tr><td>415  </td><td>36765</td></tr>
</tbody>
</table>



    [1] "(XInverse of product of X Transpose and X"



<table>
<tbody>
	<tr><td> 3.169  </td><td>-0.03578</td></tr>
	<tr><td>-0.036  </td><td> 0.00043</td></tr>
</tbody>
</table>



Step 2:  Calculate $(X^T{Y})$


```R
XTransY <- XTrans %*% Y; XTransY
```


<table>
<tbody>
	<tr><td>  353</td></tr>
	<tr><td>25367</td></tr>
</tbody>
</table>



Step 3: Summarize: find Matrix $B = (X^T{X})^{-1} (X^T{Y})$  
multiply step 1 x step 2


```R
options(digits=2)
B <- XTransXInv %*% XTransY; B
```


<table>
<tbody>
	<tr><td>211.3</td></tr>
	<tr><td> -1.7</td></tr>
</tbody>
</table>



Calcluate Sum of Square Errors


```R
options(digits=2)
fx <- 211 + (x * -1.7); fx
options(digits=2)
fx1 <- B[1, 1] + (x * B[2, 1]);fx1

```


<ol class=list-inline>
	<li>127.7</li>
	<li>93.7</li>
	<li>59.7</li>
	<li>42.7</li>
	<li>25.7</li>
</ol>




<ol class=list-inline>
	<li>128.224137931034</li>
	<li>94.3275862068964</li>
	<li>60.4310344827585</li>
	<li>43.4827586206896</li>
	<li>26.5344827586206</li>
</ol>



Calculate Errors and SSE


```R
Ei <- y - fx; Ei
SSE <- t(Ei) %*% Ei; SSE
```


<ol class=list-inline>
	<li>-3.7</li>
	<li>1.3</li>
	<li>11.3</li>
	<li>2.29999999999998</li>
	<li>-7.70000000000002</li>
</ol>




<table>
<tbody>
	<tr><td>208</td></tr>
</tbody>
</table>




```R

```
