# Lecture 4: Errors, verification & validation 
*04/11/21*


**What is a model**

- At a high level we can think of a model as a mapping or a function that takes in input data and generates output data.

- A key aspect of asking the question is my model right, is asking the question how will my model be used and by whom?
- Acknowledge that models are far from perfect. Running multiple models  then becomes quite handy 

**Verification & Validation**

- Validation: not the thing you do first, this is higher level, need code to answer that questions first. Whether the equations (i.e. the "mathematical model") we implement in our computational model appropriately represent the real system we are seeking to model/simulate.
- Verification: in a sense 'have I written the algorithm the right way?'. are we solving these equations correctly?

- Sanity check: check something that is really obvious and check if it is true. Can also be called a trend check eg. when you increse your data iteratively
- If you discount the potential for getting the right answer for the wrong reasons (which you shouldn't!), then generally "validation" ⟹ "verification".
- In almost all situations you have to assume that "verification" ⇏ "validation". 
- There are arguably some exceptions to this but it would be best practice to ignore these.

**Code Verification**

- Really about finding bugs. In practice as compilers change previously hidden bugs may suddenly cause problems. Changes in external libraries, e.g. API changes, may also generate bugs in your code.
- Checking that the errors from the code, when solving a problem with an exact solution, converge at the expected rate is the most powerful approach to perform code verification
- This is because when performed carefully a convergence analysis will often show up even the smallest, subtlest bug which may not be obviously clear at all from a single run of the code.
- At some point it becomes hard to drive errors down all the way to zero. 

- Can use benchmark solutions, depends on different 'community' and scientific subject. 
- Should be a solution that you are trying to achieved
- Other benefits include increasing performance with timing benchmarks
- Note that single points are generally dangerous, not representative. 
- There is important value in simplifying your problem eg. when you put 0 as your input to you get 0?
- The benefit here is that if we fail some aspect of code verification we can systematically de/in-crease complexity in both models side by side (e.g. turning off/on terms in the equations one by one) and the point at which we see differences helps us track down our bug.
- If you've written a new model, can compare it with external model (that is well-established, has been validated etc if that exists) 

Summary of Code Verification:
- Sanity tests (qualitative): eg. IRL does it make sense?
- Trend/conservation tests
- Benchmark test
- Comparison tests
- Against exact solutions eg. analytic solutions or Method of Manufactured Solutions


**Solution verification*

- Some of these will lead to a disastrous (unstable / obviously wrong) solution. This is a comparatively good result as something is obviously wrong and generally will be easy to figure out, also the simulation will ideally die quickly meaning minimal time is wasted.
- Sensitivity testing:  more pragmatic approach whereby we alter all the user choices in the model and check that whatever conclusions or use we want to make from the numerical results, are insensitive to these choices.

NB: don't do one simulation, testing round & do sensitivity testing 


**Validation**

- Validation: process of determining the degree to which a model with its associated data is an accurate representation of the real world as determined by experimental data, the metrics of which are chosen from the perspective of the intended uses of the model.

- In general we wouldn't necessarily expect a great agreement with data without some "model calibration"
- Calibration can be via trial and error (and hence user experience is very important), or it can be automated.  
- Don't use an unphysical parameter to calibrate model 

**Errors**

**Magnitudes**

- The absolute error is defined as the magnitude of the difference
- The relative error is defined as ;insert equation; from which if we want we can obtain a percentage error if we multiple by 100:


**Norms**

- A norm on some space (could be finite dimensional, e.g. the space of all vectors, matrices; or it could be infinite dimensional, e.g. the space of all continuous functions) is a function which assigns to every entry in that space a size.
- It is often denoted by the operator  ‖⋅‖  (where  ⋅  is a placeholder symbol indicating that we stick in the thing we are measuring the size of) 

- What norm you are using matters: for vectors of different length and outliers
- Better to plot fitted line over values more or less aligned and omit the errors on that line (make it stop before)

- Max norm not really affected when using value at the final time 

**Code Verification: Comparing algorithms**

- We have three scenarios:

1. We can find an analytic solution where we don't need to simplify the type of problem we want to solve.
2. We need to simplify our problem in order to find an analytic solution.
3. We can construct a solution to the full problem (plus some extra terms, i.e. arguably more complex rather than simplified!).

- when testing try testing with at least two different simplifications 

- Now with PDEs we don't have much chance of finding an exact solution to a general problem we write done, but with ODEs we have a chance.

Python has a symbolic math package called SymPy.

**Plotting errors using a log-log plot**

- Why did we plot the convergence of the method (i.e. the error as a function of interval size (or number of subintervals)) using logarithmic scales on both the  𝑥  and the  𝑦  axis?

- This is a very common thing to do when we think we have some polynomial relationship.

- In our case of ODE solvers, based on the Taylor series derivation where we we truncated the full expression by throwing away the second order terms, we can expect the error to be dominated for small  Δ𝑡  values by the quadratic terms

- The line is not necessarily straight to the right of the image (i.e. for larger  Δ𝑡  values) as other (higher-order) parts of the full error expansion are contributing to the total error in a non-trivial manner. 


**The Method of Manufactured Solutions (MMS)**

Let's suppose for whatever reason we couldn't find a convenient exact solution - there just isn't one we can write down in analytic form, we don't know how to use symbolic tools, it's too difficult or we don't have time, ...

This is where the Method of Manufactured Solutions provides a very powerful and convenient approach.


- first write the manufactured solution then find the function and the ODE that it is the exact solution to. 
- write exact solution -> differentiate it -> go back to the solution by finding the f



**MMS for PDEs**

- Since we choose  𝑦mms  we can compute the appropriate derivatives etc contained in  𝐿  analytically and have an exact expression for the RHS residual - in typical O/PDE language we effectively have an additional source term.

- We simply update our code with this additional source term and conduct a convergence analysis using  𝑦mms  as the exact solution.


**Other errors**

- rounding off
- Truncation errors
- overflow















