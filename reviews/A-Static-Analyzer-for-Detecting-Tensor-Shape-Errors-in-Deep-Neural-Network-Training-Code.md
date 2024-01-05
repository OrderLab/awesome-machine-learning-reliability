# Review for "A Static Analyzer for Detecting Tensor Shape Errors in Deep Neural Network Training Code"

Yuxuan Jiang & Dec 31, 2023

## Motivation & goal

- What problem is this work addressing?

  This paper addresses the problem of detecting tensor shape errors in deep neural network training code.
- Why the problem is important?

  Tensor shape errors are common in deep learning code and they are hard to debug.
  They can cause silent failures and lead to incorrect results.
- What goals does this work aim to achieve?

  This work aims to detect tensor shape errors statically and automatically.

### Related work

- State-of-the-Art Solutions:

  The primary solutions mentioned for detecting shape mismatches in PyTorch applications include Hattori et al.'s semi-static analysis tool, Pythia (for TensorFlow applications), ShapeFlow, and PyExZ3. These tools represent the latest efforts in addressing tensor shape mismatches in deep learning applications.

- Inadequacies of Current Solutions:

  Current solutions are either semi-static or requires effort to modify the script. Semi-static solutions require the user to provide a dataset to run the program so some errors may not be detected. In addition, realistic ML applications are often complex in the sense that they contain many libraries and uses subtle control flow, while existing solutions usually only support a subset of the python syntaxes and available libraries.

### Idea & insight

- What is the key idea of this work?

    This work's key idea is to capture the shape constraints of PyTorch APIs and use constraint solving to detect shape errors (i.e. unsatisfible constraints). Eager simplification and some heuristics were used to reduce the search space.

- What is the insight, if any, behind this idea?

  The insight is that the shape constraints of PyTorch APIs can be captured and solved using constraint solving.

- Why *might* this idea be better than prior work?

  - fully-static analysis: no dataset and modification to the code is needed
  - comprehensive coverage of PyTorch APIs (this is a big deal but I don't think it's on the idea level)

### Solution

- Roughly speaking, how does the solution work?
  The tool works by first converting the PyTorch code into a IR which captures the shape constraints of PyTorch APIs. Then, it symbolically executes the IR, construct constraints. During constraint construction, eager simplification and heuristics are used to reduce the search space and return early results.
  The left-over constraints are solved using Z3 SMT solver.
- What are the key techniques and algorithms used in the solution?
  - symbolic execution
  - constraint solving
  
### Assumption & limitations

- What assumptions do the proposed solution make?
  1. Other than the training or evaluation dataset, every input value required to execute the code is injected by commandline arguments
  2. There is no infinite loop and recursion. We assume that every loop bound except for the datasets will be fixed to a constant.
  3. The unknown loop bound for the datasets is only for the size of each dataset in an epoch, and every iteration is either with a fixed-sized minibatch of the dataset or with a smaller, residual minibatch.
  4. We assume that string-manipulation expressions have no effect on the shape of tensors.

- Are these assumptions reasonable? Are there any assumption that the authors did not describe in the paper?
  The authors didn't really explain why they made these assumptions. I do think that these assumptions are reasonable for most deep learning applications.

  As far as I can tell, these assumptions were made to simplify symbolic execution complexity and reduce the search space.

- What limitations does this solution have?
  1. Heavy reliance on engineers to provide the semantics of the APIs. The paper claims to be superior to other tools as it has a comprehensive coverage of PyTorch APIs. However, in the end, the support for PyTorch APIs is still completely manual. I don't think this paper made any progress in this regard.
  2. The tool cannot handle tensor shapes dependent on other tensors' runtime values. This is a fundamental limitation of the idea as only shape constraints can be captured and solved.
  3. Symbolic execution and constraint solving are expensive. Using this approach, you inevitably end up with some constraints that are too complex to solve. The paper claims that eager simplification and heuristics are used to reduce the search space. However, I don't see significant evidence supporting this claim. I highly doubt the performance of this tool on more complex applications.

### Effectiveness

- What experiments, analyses are conducted to evaluate the solution?
  - PyTea for PyTorch's Official Examples with Shape Errors
  - PyTea for StackOverflow Questions with Shape Errors
- Do these results and analyses back up the paper's claims?
  In terms of effectiveness, PyTea is able to detect most of shape errors without modifying the code, while the other tools cannot even with modification. In terms of efficiency, PyTea is able to analyze most of the examples in a reasonable amount of time (seconds). However, most of the examples are simple (100 to 300 loc) and I don't think they are representative of real-world applications. I highly doubt the performance of this tool on more complex applications, as the cost of symbolic execution and constraint solving is exponential in the worst case.

- Are there any missing aspects in the evaluation?
  1. I do want to see the performance of this tool on more complex applications.
  2. Since the tool needs manual support to understand API semantics, I want to see how much effort is needed to support a new API, as PyTorch is evolving rapidly and other frameworks are gaining popularity.

### Learning & thoughts

I think the idea is good and the problem is super important. Capturing only shape constraints of a tensor efficiently covers the major  I think the authors should have spent more time on improving the performance of the tool and reducing the manual effort needed to support new APIs. This would not be an issue for now but as the ml frameworks evolve, the tool will become less and less useful.

### Unanswered questions

- effort of supporting new APIs
- performance on more complex applications
- How is pytorch code converted to IR? The paper didn't explain this part.

### Conclusion

- How may this work influence the way we build systems in the future?
  I think this work is a good start for us to rethink how we build DL frameworks. PyTorch is a great framework for extreme flexibility and ease of use. However, it is also very easy to make mistakes and introduce external libraries that makes static analysis hard. As the complexity of DL applications increases and production ML systems become more and more important, we need to rethink the design of DL frameworks and how we build them. How can we still provide flexibility and ease of use while making static analysis easier? How can we make sure that the framework is easy to use but hard to misuse? I think these are the questions that we need to answer in the future.
