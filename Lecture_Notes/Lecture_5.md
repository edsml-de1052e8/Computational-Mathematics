# LEcture 5: Interpolation 


We will try to be careful to use the term degree consistently as the highest degree power that appears in a polynomial, but order will also be acceptable and may slip in at points and you may come across this elsewhere.
For example

𝑓(𝑥):=1+𝑥−2𝑥4,
 
is a degree four polynomial.

If you don't use this convention, and just use " = " for all of these cases, it's not the end of the world and you won't lose marks! 
I may well slip and not bother being so precise myself in places.


**Interpolation**

- Interpolation generally assumes that these data points are exact (e.g. no measurement errors) and at distinct  𝑥  locations, i.e. there is no ambiguity in a mapping from  𝑥  to  𝑦  (which there would be if we had multiple  𝑦  values for the same  𝑥 ; we will see this scenario in the case of curve-fitting covered below. 
- The same  𝑥  and  𝑦  pairs exactly repeated obviously means repeated data and depending on application all the exact replicas might be removed).


- We could also allow it to be only piecewise continuous (the use of the word piecewise meaning it is continuous in regions, but can be discontinuous in between these regions):
has a gap in between function.

- We have a lot of choice for how we construct the interpolating or curve-fitting function.

- Considerations for how to do this include the required/desired smoothness of the resulting function (i.e. how many smooth derivatives it has - cf. the piecewise polynomial case), replicating known positivity/boundedness or periodicity, the cost of evaluating it, etc.
- Some choices include: polynomials, piecewise polynomials, trigonometric series (i.e. sums of sines and cosines leading to an approximation similar to Fourier series).

NB: when using the plot function, if there is a gap / it is piecewise, there might be a case that the points will be pieced together with fitted lines although it shouldn't be the case
You have to force it NOT to draw that line between those two points.


**Curve-Fitting*

Alternatively, when we have data with noise/errors, or multiple different measurement values ( 𝑦 ) for a single  𝑥 , then we may not want to, or cannot fit a function/curve that goes through all points exactly, and rather have to perform curve-fitting - finding a function that approximates the data in some sense but does not necessarily go through all the points.


- function ```np.polyfit``` fits data as a polynomial
- This uses more data and creates an average fitted line gathered from all data points, previous example only used 2 points and draw a line between them

**POlynomial interpolation**

Suppose we are given a set of  𝑁+1  data points  (𝑥𝑖,𝑦𝑖)  (with distinct  𝑥𝑖 's).

Now suppose we construct a polynomial of degree  𝑁 :
𝑃𝑁(𝑥):=𝑎0+𝑎1𝑥+𝑎2𝑥2+𝑎3𝑥3+…𝑎𝑁𝑥𝑁,
 
where  𝑎0,𝑎1,…,𝑎𝑁  are the coefficients of our polynomial.

- 2 data points: enough to fit a linear function
- 3 data points: fit a quadratic equation
- 6 data points: degree 5 polynomial etc

- Monomials: linear combination of a basis made up of single-term polynomials

- with a degree  𝑁  polynomial we have  𝑁+1  free coefficients, and we have  𝑁+1  pieces of (distinct) information 
- - that the polynomial passes through our data point exactly. This is a well-defined problem with a unique solution and it follows that the polynomial of degree  𝑁  passing through our data is unique.
- be careful what you are plotting with ```polyfit```

- Fitting a single data point
The polynomial that fits the single data point  (𝑥0,𝑦0)  is clearly simply the constant function given by

𝑦=𝑓(𝑥)≡𝑦0,i.e. the degree zero polynomial:𝑦=𝑃0(𝑥)≡𝑎0where𝑎0=𝑦0
 

- Fitting two data points
The polynomial that fits the two data points  {(𝑥0,𝑦0),(𝑥1,𝑦1)}  is clearly the linear function given by

𝑦=𝑓(𝑥)≡𝑎0+𝑎1𝑥,i.e. the degree one polynomial:𝑦=𝑃1(𝑥)≡𝑎0+𝑎1𝑥
 
where through substitution of our data into the functional form we arrive at two simultaneous equations (or a  2×2  matrix system) which can fairly easily be solved by substituting one equation into the other (see earlier lecture)

- Fitting three data points
The polynomial that fits the three data points  {(𝑥0,𝑦0),(𝑥1,𝑦1),(𝑥2,𝑦2)}  is of course a quadratic, but things start to get a bit more complicated now if we actually want to solve for the polynomial coefficients.

Substituting the data into the quadratic leads to a system of three simultaneous equations, or a  3×3  linear system to solve.

This is a lot more tricky to solve by hand than the  2×2  system for the linear coefficients that we could solve through substitution quite easily (see homework for the details).

However, you should be able to show that this system takes the form

111𝑥0𝑥1𝑥2𝑥20𝑥21𝑥22𝑎0𝑎1𝑎2=𝑦0𝑦1𝑦2or equivalently in matrix notation𝑉𝒂=𝒚.
 
If we solve this system by inverting the matrix ( 𝑉 ) we have our quadratic polynomial coefficients:  𝒂=𝑉−1𝒚 .

**Lagrange Polynomial**

- To avoid having to relt on matrices, you can try with a Langrange polynomial
- Lagrange polynomials are a particularly popular choice for constructing an interpolant for a given data set.

Given a set of  (𝑁+1)  points as above, the Lagrange polynomial is defined as the linear combination

𝐿(𝑥):=∑𝑖=0𝑁𝑦𝑖ℓ𝑖(𝑥),
 
where the  ℓ𝑖(𝑥)  are a new choice for our basis functions (different to the monomials, but the same idea in that they form a basis), and the  𝑦𝑖  are the  𝑁+1  weights/coefficients corresponding to this basis.


- Don't need to find new coefficients (y) or new weigths, there are the same as the ys making up the data we are interpolating
- This is the whole point of this approach - we no longer have to compute the weights by inverting a matrix system as we had to above with monomials.

Now, through the construction of this approach, we know the weights directly from the given data.


**Approximating a function**

- Rather than approximating/interpolating arbitrary discrete data given to us somehow 
(e.g. from observations, or from a very expensive computer code which has been run previously), we can of course use the same methods to approximate a given function.

- We may want to do this in order to approximate a complex/expensive function with a simpler, cheaper interpolating function.
- can use theory to bound your interpolation, exact error
- but note that in these ocurences the curve all go through the data
- There are methods where you can control smoothness eg Piecewuse Cubic Hermite Interpolation Polynomial (PCHIP): can be done in Numpy

#### Curve-fitting or Regression

- You know you want a linear model, but the data is noisy. 
- This is straightforward to do for polynomials of different polynomial degree using numpy.polyfit, as demonstrated in the example below where we construct polynomials of degree zero up to five (there being six data points).
- As described in the docs (numpy.polyfit), least squares fitting minimises the sum of the squares of the differences between the data provided and the polynomial approximation
- [Recall that we considered the problem of fitting a linear line which minimised the two-norm of the errors to the data (and compared to other norms) in an earlier lecture when we were considering the impact of outliers in the data].

Let's write a Python function that evaluates the squared error,  𝐸 , and use this function to evaluate the error for each of the polynomials calculated above.

**Extrapolation**


- Interpolation by definition is used to estimate  𝑦  for values of  𝑥  within the bounds of the available data with some confidence.

- Extrapolation on the other hand is the process of estimating (e.g. using the interpolating function)  𝑦  outside the bounds of the available data.


#### Quadrature ###


-Integration is the inverse of differentiation
- Note that there is scope for confusion with this content over the degree polynomial used within a single interval and the number of subintervals that our total interval of interest may be split up into.
- We will attempt to be consistent and use  𝑁  to refer to the "degree" of the polynomial (within an interval or subinterval), and  𝑛  to refer to the total number of "subintervals" (or sometimes "bins") we are using to cover our entire interval.

- Definite vs indefinite: definite is the exact solution derived from interval and area under the curve (the function) vs indefinite gives a function and not specific answer
- NB: don't forget to add constant in the form +C
- This function ( 𝐹 ) is sometimes referred to as the anti-derivative of  𝑓  rather than the indefinite integral.
- Can be computed using SympPy

- Notice that it doesn't matter if we don't know the arbitrary constant mentioned above as it will be cancelled on the RHS in the case of definite integration:

(𝐹(𝑏)+𝐶)−(𝐹(𝑎)+𝐶)=𝐹(𝑏)−𝐹(𝑎).
 
So while we need to be aware of the existence of this constant, for the purpose of quadrature we can just pretend it's zero.

[Aside: Mathematically you might say "we can assume, without loss of generality (w.l.o.g.), that  𝐶=0 ."]

- If the function is complicated or unknown, we can approximate its value or variation (and hence integral) across/within each of these subintervals
- so I = I1+I2 w/ I1 and I2 being subintervals to be integrated
- Better approximation methods as well as smaller subintervals (and hence a larger number of intervals to cover our total interval of interest:  [𝑎,𝑏] ), will lead to lower errors, but will generally cost more to compute of course.
- 














