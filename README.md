# piecewise_fun
Piecewise function library in Python.

## Task:
  - Design and implement a class to store and evaluate a piecewise constant function.
  - Provide an evaluation function, i.e., to give its value (or fail) for any possible real number as input.
  - Provide a function to get its minimum value and argmin.
  - Provide a function to get its maximum value and argmax.
 
## Bonus points:
  - Provide sufficient correctness tests, using PyTest. Pay special attention to handling corner cases or bad input.
  - Provide sufficient timing tests. At which point your functions struggles down 
  - Under which scenario would the 3 class methods slow down ?
  - Provide a Jupyter notebook demonstrating the functionality of your class.
  - Repeat for for a piecewise linear function.
  
--------------------------------------------------------------------------------
## Design Choices:
  - For ease, this is done entirely in a single notebook. Normally this would be split in defferent .py scripts, each one for a class, utils, requirements etc.
  - If a range is wrong as in [2, 1] I chose to throw an exception.
  - If there is overlap, I throw an exception and delegate the issue to the caller.
  - I chose to create a internal private copy of the segments/pieces in order to not distrurb the original version of the calling user, but that can be changed easily for the sake of memory usage.
  - I assume the computation load is going to be in the evaluate function so I prepare the data in the constructor. For the use case of multiple objects created and the evaluate function going to be called only once per object a different implementation is going to be optimal.
  - If the number evaluated does not belong to a given range, I throw an exception.
  - In the future if this library proves useful we can choose to write a base class to derive children for different kinds of equations, or overload the same one.
  - For the linear version a variation point is whether we calculate the equation of the line in the contructor or in the evaluation point. It is understood that the is a small tradeoff of space because the line value have to be stored, but the computation of the line at the evaluation function is gained.
  - Instead of using linspace or range for the input, I chose to take in just the edges in order to be valid for all real numbers. Linspace and range are discrete.

## Optimization:
  - Search function, for now binary search but also a set has been considered due to $O(1)$ complexity but not chosen because it can only be unordered and the lookup gains are mitingated with the current list structure. Also interpolation search could be optimal for a certain distribution of ranges due to $O(loglogn)$ but covering all cases binary search is better due to $O(nlogn)$.
  - Computation load concentrated on constructor because of assumption of repeated use of evaluation function on each object.
  - In future versions, base class for any piecewise function could be built, and then constant, linear etc versions derived.
  - In both classes, in order to optimize the performance we could use numpy arrays instead of lists.
  - If we refactor the code to use numpy arrays, then we could gain extra speedup using numba/jit.
