---
layout: default
---

<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />
<title>Regression using Matrix Algebra</title>
	<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?...">
</script>

    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Least-Squares-Regression-Solved-with-Matrix-Algebra">Least Squares Regression Solved with Matrix Algebra<a class="anchor-link" href="#Least-Squares-Regression-Solved-with-Matrix-Algebra">&#182;</a></h1><p>This is an explanation of Least Squares Regression solved using matrix algebra.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Some-sample-data">Some sample data<a class="anchor-link" href="#Some-sample-data">&#182;</a></h3><p>Let's start with a simple set of data for sales and price<br>
y = the number of units sold<br>
x = price per unit<br>
The data shows that when prices are high, the quantity sold is low, and when prices are low the quantity sold is high.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>x <span class="o">&lt;-</span> <span class="kt">c</span><span class="p">(</span><span class="m">6</span><span class="p">,</span><span class="m">7</span><span class="p">,</span><span class="m">9</span><span class="p">,</span><span class="m">10</span><span class="p">,</span><span class="m">11</span><span class="p">,</span><span class="m">12</span><span class="p">,</span><span class="m">14</span><span class="p">,</span><span class="m">18</span><span class="p">,</span><span class="m">26</span><span class="p">)</span> <span class="c1"># of promotions</span>
y <span class="o">&lt;-</span> <span class="kt">c</span><span class="p">(</span><span class="m">170</span><span class="p">,</span><span class="m">221</span><span class="p">,</span><span class="m">264</span><span class="p">,</span><span class="m">308</span><span class="p">,</span><span class="m">444</span><span class="p">,</span><span class="m">540</span><span class="p">,</span><span class="m">388</span><span class="p">,</span><span class="m">677</span><span class="p">,</span><span class="m">711</span><span class="p">)</span> <span class="c1">#revenue</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Least-squares-regression-equation">Least squares regression equation<a class="anchor-link" href="#Least-squares-regression-equation">&#182;</a></h3><p>for points $(x_1,y_1), (x_2,y_2)...(x_n,y_n)$  the least square regression line is:<br>
$f(x)=\beta_0 + \beta_1x$</p>
<p>The errors (also referred to as residuals) are the difference bdtween the actual quantity sold and the regression estimate of the quantity sold. They are<br>
$e_i=y_i-f(x_i)$</p>
<p>The $\beta$ coefficients are those values which minimize the sum of squared errors using the regression function f(x)<br>
$(y_1-f(x_1))^2$ +$(y_2-f(x_2))^2$ + . .$(y_n-f(x_n))^2$</p>
<p>Goal: minimize sum of squared residuals(SSR) where<br>
$SSR=\sum_{i=1}^{n}{e_i}^2$</p>
<p>We can set this up as a system of equations and then solve using matrices<br>
$y_1 = (b + mx_1) + e_1$<br>
$y_2 = (b + mx_2) + e_2$<br>
...<br>
$y_n = (b + mx_n) + e_n$</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<hr>
<h2 id="Single-variable-regression-represented-in-matrix-form">Single variable regression represented in matrix form<a class="anchor-link" href="#Single-variable-regression-represented-in-matrix-form">&#182;</a></h2><p>We can represent our x and y data in matrix form<br>
$Y = \left[\begin{array}{rrr}
y_1\\
y_2\\  
\vdots\\  
y_n
\end{array}\right]$  This is an N x 1 matrix</p>
<p>$X = \left[\begin{array} {rrr}
1 &amp; x_1\\
1 &amp; x_2\\  
\vdots\\    
1 &amp; x_n
\end{array}\right]$  This is a N x 2 matrix. The column of 1s is for the intercept.<br>
Note: if this were multivariate problem with k variables (x's), it would be a N X (1 + k) matrix</p>
<p>$B = \left[\begin{array} {rrr}
b_0\\
b_1
\end{array}\right]$  This is a 2 x 1 matrix<br>
Note: if this were multivariate problem with k variables (x's), it would be a (1+k) X 1 matrix</p>
<p>$E = \left[\begin{array} {rrr}
e_1\\
e_2\\  
\vdots\\  
e_n
\end{array}\right]$  This is a N x 1 matrix</p>
<h3 id="Matrix-form-of-regression-equation">Matrix form of regression equation<a class="anchor-link" href="#Matrix-form-of-regression-equation">&#182;</a></h3><p>$Y = XB + \epsilon$<br>
Regression assumes zero errors (ie some are positive some are negative and should average to zero), so we drop $\epsilon$<br>
Y = XB</p>
<h4 id="Solve-for-B">Solve for B<a class="anchor-link" href="#Solve-for-B">&#182;</a></h4><p>Y = XB<br>
First we put X into a square matrix. We can do that by multiplying by the transpose $X^` $ which gives us a 2x2 matrix<br>
$X^` Y = (X^` X) B$<br>
<br>Next, to isolate B we'll divide both sides by $(X^`{X})$ (this is the same as multiplying both sides by $(X^`{X})^{-1}$<br>
$(X^`{X})^{-1} (X^`{Y}) = (X^`{X})^{-1} (X^` X) B$<br>
<br>Next, noting that a matrix multipled by its inverse is the Identity Matrix I we simplfy the equation to<br>
$(X^`{X})^{-1} (X^`{Y}) = IB$<br>
<br>Finally, noting that any matrix multiplied by the identity matrix is itself. So IB = B. Therefore this simplifies to<br>
$B = (X^`{X})^{-1} (X^T`{Y})$</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<hr>
<h2 id="An-alternative-explanation">An alternative explanation<a class="anchor-link" href="#An-alternative-explanation">&#182;</a></h2><p>$ SSE = \sum_{i=1}^{n}{e_i}^2$ is the forumula we are trying to minimize. We want the sum of these errors (squared) as small as possible.</p>
<p>To convert this formula to matrix notation we can take the vector of errors and multiply it by the transpose.</p>
<p>$SSE = E^`E$<br>
We can confirm that this gives us the sum of squared errors. Let's assume errors are (4, 6, 3). This equation results in a row vector [4 6 3] multiplied by a column vector
$\left[\begin{array} {rrr}
4\\
6\\  
3
\end{array}\right]$ Resulting in 4x4 + 6x6 + 3x3  which is what we want: the sum of the squared errors.</p>
<p>Remember, that $\epsilon$ is equivalent to  $Y -X{\beta}$. Thus<br>
$E^`E  = (Y -X{\beta)}^`(Y -X{\beta}) $<br>
<br> Next, multiply out.<br>
$(Y^` - (X\beta)^`) (Y -X{\beta})$<br>
$Y^`Y - (X\beta)^`Y - Y^`(X{\beta}) + (X\beta)^`X{\beta}$<br>
$Y^`Y - 2YX^`\beta^` + X^`\beta^`(X\beta)$</p>
<p><br>We take the derivative with respect to b and set it to zero.<br>
$-2X^`Y + 2X^`X\beta=0$<br>
$-X^`Y + X^`X\beta=0$<br>
$X^`X\beta =X^`Y$</p>
<h4 id="Solve-for-$\beta$">Solve for $\beta$<a class="anchor-link" href="#Solve-for-$\beta$">&#182;</a></h4><p>isolate $\beta$ by dividing both sides by $(X^`X)$. Note, this is the same as multiplying by $(X^`X)^{-1}$<br>
$(X^`X)^{-1}(X^`X)\beta = (X^`X)^{-1}(X^`Y)$<br>
$\beta = (X^`{X})^{-1} (X^`{Y})$</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Find-$\beta$-coefficients-using-matrix-algebra-from-our-sample-data">Find $\beta$ coefficients using matrix algebra from our sample data<a class="anchor-link" href="#Find-$\beta$-coefficients-using-matrix-algebra-from-our-sample-data">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>$\beta = (X^`{X})^{-1} (X^`{Y})$ is our regression equation</p>
<p>Recall our sample data for sales and prices<br>
y = the number of units sold<br>
x = price per unit</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>x
y
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<ol class="list-inline">
	<li>6</li>
	<li>7</li>
	<li>9</li>
	<li>10</li>
	<li>11</li>
	<li>12</li>
	<li>14</li>
	<li>18</li>
	<li>26</li>
</ol>

</div>

</div>

<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<ol class="list-inline">
	<li>170</li>
	<li>221</li>
	<li>264</li>
	<li>308</li>
	<li>444</li>
	<li>540</li>
	<li>388</li>
	<li>677</li>
	<li>711</li>
</ol>

</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Let's convert the vectors for x and y into matrix Y and matrix X</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>Y <span class="o">&lt;-</span> <span class="kp">as.matrix</span><span class="p">(</span>y<span class="p">);</span>Y
X <span class="o">&lt;-</span> <span class="kt">matrix</span><span class="p">(</span><span class="kt">c</span><span class="p">(</span><span class="kp">rep</span><span class="p">(</span><span class="m">1</span><span class="p">,</span> <span class="kp">length</span><span class="p">(</span>x<span class="p">)),</span> <span class="kt">c</span><span class="p">(</span>x<span class="p">)),</span> nrow <span class="o">=</span> <span class="m">9</span><span class="p">,</span> ncol <span class="o">=</span> <span class="m">2</span><span class="p">);</span>X
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td>170</td></tr>
	<tr><td>221</td></tr>
	<tr><td>264</td></tr>
	<tr><td>308</td></tr>
	<tr><td>444</td></tr>
	<tr><td>540</td></tr>
	<tr><td>388</td></tr>
	<tr><td>677</td></tr>
	<tr><td>711</td></tr>
</tbody>
</table>

</div>

</div>

<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td>1 </td><td> 6</td></tr>
	<tr><td>1 </td><td> 7</td></tr>
	<tr><td>1 </td><td> 9</td></tr>
	<tr><td>1 </td><td>10</td></tr>
	<tr><td>1 </td><td>11</td></tr>
	<tr><td>1 </td><td>12</td></tr>
	<tr><td>1 </td><td>14</td></tr>
	<tr><td>1 </td><td>18</td></tr>
	<tr><td>1 </td><td>26</td></tr>
</tbody>
</table>

</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Step-1:-Calculate-$(X^`{X})^{-1}$">Step 1: Calculate $(X^`{X})^{-1}$<a class="anchor-link" href="#Step-1:-Calculate-$(X^`{X})^{-1}$">&#182;</a></h3><p>From $\beta = (X^`{X})^{-1} (X^`{Y})$ calculate just the $(X^`{X})^{-1}$ part</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="kp">options</span><span class="p">(</span>digits<span class="o">=</span><span class="m">2</span><span class="p">)</span>
<span class="kp">cat</span><span class="p">(</span><span class="s">&quot;The x vector&quot;</span><span class="p">)</span>
X
<span class="kp">cat</span><span class="p">(</span><span class="s">&quot;The x transpose&quot;</span><span class="p">)</span>
XTrans <span class="o">&lt;-</span> <span class="kp">t</span><span class="p">(</span>X<span class="p">);</span> XTrans <span class="c1">#transpose of X </span>
<span class="kp">cat</span><span class="p">(</span><span class="s">&quot;Product of X transpose and X&quot;</span><span class="p">)</span>
XTransX <span class="o">&lt;-</span> XTrans <span class="o">%*%</span> X<span class="p">;</span> XTransX <span class="c1"># product of X transpose and X</span>
<span class="kp">cat</span><span class="p">(</span><span class="s">&quot;(Inverse of product of X Transpose and X&quot;</span><span class="p">)</span>
XTransXInv <span class="o">&lt;-</span> <span class="kp">solve</span><span class="p">(</span>XTransX<span class="p">);</span> XTransXInv <span class="c1">#inverse of X traspose times X</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>The x vector</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td>1 </td><td> 6</td></tr>
	<tr><td>1 </td><td> 7</td></tr>
	<tr><td>1 </td><td> 9</td></tr>
	<tr><td>1 </td><td>10</td></tr>
	<tr><td>1 </td><td>11</td></tr>
	<tr><td>1 </td><td>12</td></tr>
	<tr><td>1 </td><td>14</td></tr>
	<tr><td>1 </td><td>18</td></tr>
	<tr><td>1 </td><td>26</td></tr>
</tbody>
</table>

</div>

</div>

<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>The x transpose</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td>1 </td><td>1 </td><td>1 </td><td> 1</td><td> 1</td><td> 1</td><td> 1</td><td> 1</td><td> 1</td></tr>
	<tr><td>6 </td><td>7 </td><td>9 </td><td>10</td><td>11</td><td>12</td><td>14</td><td>18</td><td>26</td></tr>
</tbody>
</table>

</div>

</div>

<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Product of X transpose and X</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td>  9 </td><td> 113</td></tr>
	<tr><td>113 </td><td>1727</td></tr>
</tbody>
</table>

</div>

</div>

<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>(Inverse of product of X Transpose and X</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td> 0.623 </td><td>-0.0407</td></tr>
	<tr><td>-0.041 </td><td> 0.0032</td></tr>
</tbody>
</table>

</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Step-2:--Calculate-$(X^`{Y})$">Step 2:  Calculate $(X^`{Y})$<a class="anchor-link" href="#Step-2:--Calculate-$(X^`{Y})$">&#182;</a></h3><p>From $\beta = (X^`{X})^{-1} (X^`{Y})$ calculate just the $(X^`{Y})$ part</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>XTransY <span class="o">&lt;-</span> XTrans <span class="o">%*%</span> Y<span class="p">;</span> XTransY
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td> 3723</td></tr>
	<tr><td>55491</td></tr>
</tbody>
</table>

</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Step-3:-Summarize:-find-$\beta$-coefficients-$\beta-=-(X^`{X})^{-1}-(X^`{Y})$">Step 3: Summarize: find $\beta$ coefficients $\beta = (X^`{X})^{-1} (X^`{Y})$<a class="anchor-link" href="#Step-3:-Summarize:-find-$\beta$-coefficients-$\beta-=-(X^`{X})^{-1}-(X^`{Y})$">&#182;</a></h3><p>multiply step 1 x step 2</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="kp">options</span><span class="p">(</span>digits<span class="o">=</span><span class="m">3</span><span class="p">)</span>
B <span class="o">&lt;-</span> XTransXInv <span class="o">%*%</span> XTransY<span class="p">;</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="The-$\beta$-coefficients-are">The $\beta$ coefficients are<a class="anchor-link" href="#The-$\beta$-coefficients-are">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>B
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td>57.4</td></tr>
	<tr><td>28.4</td></tr>
</tbody>
</table>

</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Check-that-$\beta$--coefficients-from-matrix-form-are-the-same-as-from-R-linear-regression-model">Check that $\beta$  coefficients from matrix form are the same as from R linear regression model<a class="anchor-link" href="#Check-that-$\beta$--coefficients-from-matrix-form-are-the-same-as-from-R-linear-regression-model">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span><span class="kp">cat</span><span class="p">(</span><span class="s">&quot;The coefficients using R&#39;s linear regression model are&quot;</span><span class="p">)</span>
lm <span class="o">&lt;-</span> lm<span class="p">(</span>y<span class="o">~</span>x<span class="p">)</span>
<span class="kp">print</span><span class="p">(</span>lm<span class="o">$</span>coefficients<span class="p">,</span>digits<span class="o">=</span><span class="m">3</span><span class="p">)</span>
<span class="kp">cat</span><span class="p">(</span><span class="s">&quot;The coefficients we calculated previously with matrix algebra are the same&quot;</span><span class="p">)</span>
B
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>The coefficients using R&#39;s linear regression model are(Intercept)           x 
       57.4        28.4 
The coefficients we calculated previously with matrix algebra are the same</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>


<div class="output_html rendered_html output_subarea ">
<table>
<tbody>
	<tr><td>57.4</td></tr>
	<tr><td>28.4</td></tr>
</tbody>
</table>

</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Calculate-estimates-for-Y-from-regression-model">Calculate estimates for Y from regression model<a class="anchor-link" href="#Calculate-estimates-for-Y-from-regression-model">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>fx <span class="o">&lt;-</span> B<span class="p">[</span><span class="m">1</span><span class="p">,</span> <span class="m">1</span><span class="p">]</span> <span class="o">+</span> <span class="p">(</span>x <span class="o">*</span> B<span class="p">[</span><span class="m">2</span><span class="p">,</span> <span class="m">1</span><span class="p">])</span>  
<span class="kp">cat</span><span class="p">(</span>fx<span class="p">,</span>digits<span class="o">=</span><span class="m">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>228 256 313 341 370 398 455 568 795 3</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Calculate-errors-and-SSE">Calculate errors and SSE<a class="anchor-link" href="#Calculate-errors-and-SSE">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>Ei <span class="o">&lt;-</span> y <span class="o">-</span> fx
<span class="kp">cat</span><span class="p">(</span><span class="s">&quot;The residuals are &quot;</span><span class="p">)</span>
<span class="kp">cat</span><span class="p">(</span>Ei<span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>The residuals are -57.6 -35 -48.8 -33.1 74.5 142 -66.7 109 -84.2</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>SSE <span class="o">&lt;-</span> <span class="kp">t</span><span class="p">(</span>Ei<span class="p">)</span> <span class="o">%*%</span> Ei 
<span class="kp">cat</span><span class="p">(</span><span class="s">&quot;The SSE (sum of squared errors) is &quot;</span><span class="p">)</span>
<span class="kp">cat</span><span class="p">(</span>SSE<span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>The SSE (sum of squared errors) is 57139</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-r"><pre><span></span>
</pre></div>

</div>
</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>


[back](./)
