# Lecture 1: Introduction



Admin:
- Notebooks with solutions and homework to do every day
- run nbextensions to convert notebooks with table of contents
- Don't get too hung up on details, big picture matters



### Terminology

- Terminology is very important especially when working with mullti-disciplinary teams

**Model**

- "Model" is a term that will be very important for us. However, it is one that has an almost infinite number of meanings
- Can be a simplification of real world system or process, but is also complex.
- All models are wrong, but that doesn't mean you can get something out of it
- Remember that it is approximations
- Question is not: is th emodel true but 'is the model good enough for the particular application?'

- Workflow: stakeholder asks a question -> conceptual model ny domain specialist -> mathematical equations encapsulating model -> equations are discretised -> output in code
- Verification: does your code have bugs. Can be split in code verification but also solution verification (with user)
- Validations: does your model actually represent the system you are looking at

**Computation Science vs Data Science**

- theory and experimentation have long been described as the two pillars of science (or the scientific method), while over the last 10 or 20 years people have been talking about computation as being the third pillar, and more recently data science being the fourth. 
- However, if you check online you will see there is controversy and much discussion on this.

**Examples**

Discrete vs Continuous

- Some problems, systems we wish to simulate, etc, are fundamentally discrete and so well-suited to fitting onto (i.e. being solved using) computers which are also discrete.

- However, many problems we wish to solve are continuous.
- A key job of a numerical modeller/analyst is to decide how to represent a continuous process by something that fits on a computer, i.e. to come up with a discrete model, and to implement it in code.
- Often, we represent the "continuous" world with a continuous ODE or PDE. The process of turning this into something we can consider and solve with a computer is called discretisation.

Example:


For example, consider population size and its growth.

For a start should population size be considered discrete or continuous in time?

For some biological processes this would be a continuous process (or rather assumed to be continuous even though each individual birth/death is a discrete event!), e.g. human population.
However, for others it is best modelled as being discrete - e.g. for species where generations may not overlap or where there are well-defined, discrete breeding seasons.



Thinking about this as a generic numerical algorithm, it's vitally important that we understand/appreciate the sensitivity of our results to both of these parameters.

Why?

Because:

We might not know the starting population $x_0$ with complete accuracy - does this matter?
We might not know $r$ either, does this matter? Is $r$ completely knowable or will it always contain inevitable uncertainty? Here we are thinking of $r$ as some "physical" parameter that governs our system. Again note the links to COVID-19, in many ways it's $r$ that's more important to consider and get a good estimate of than the initial state $x_0$ of our system.
As we will see later $r$ in this simple example can also be interpreted as a numerical parameter, i.e. as a user/modeller we need to select an appropriate value - how do we do this and what are the consequences of the wrong choice?

- So, for the $r$ parameter value considered here at least, we always end up at the same place - try some more starting values yourself.

- This is essentially telling us that (for this parameter value at least), our system dynamics do not seem to be sensitive to the initial condition(s).

**Sensitivity to Model parameters**

- What was the point of this (it's fun, interesting and allows us to practice some coding and plotting, but also...)
it illustrates a few really important points:

- Even a seemingly very simple discrete algorithm can exhibit very complex behaviour.
- Now this may be what we want as our discrete algorithm may be trying to mimic a real system that is very complex, OR this could be completely spurious behaviour and as a modeller all this behaviour past the value $r=3$ could be completely unexpected, not consistent with the true system, and not what was wanted when the modeller came up with the mathematical model.

**Taylor Series**


- An obvious improvement we can make is to approximate the true function with a linear approximation, instead of simply a constant.
- right weighting of a derivative at x0. 
- of you add enough terms in Taylor series, it becomes 'perfect'.



















