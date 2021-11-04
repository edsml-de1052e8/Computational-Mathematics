# Lecture 4: Errors, verification & validation 


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













