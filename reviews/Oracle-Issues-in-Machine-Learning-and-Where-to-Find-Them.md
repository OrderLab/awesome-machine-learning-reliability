# Oracle Issues in Machine Learning and Where to Find them

Motivation & Goal:

- What problem is this work addressing?

    This work systematically explores the “oracle” problem in machine learning and proposed two semantics to semi-automatically find some high-level issues. The work also illustrate the need for software engineering strategies that especially target and assess the oracle.

- Why the problem is important?

    The problem is important because ML applications are important and therefore their reliability and correctness is important.

- What goals does this work aim to achieve?
  - To illustrate the importance of addressing the oracle problem in ML
  - Propose two heuristics for surfacing various potential oracle issues:
    - Information Entropy
    - Semantic Analysis

“As we will show, these issues occur with regard to label taxonomy and information representation. As we will argue, for certain ML use cases, these could be explicitly harmful to a practical system’s integrity.” ([Liem and Panichella, 2020, p. 484](zotero://select/library/items/FTTVC75J)) ([pdf](zotero://open-pdf/library/items/48TJVEMC?page=2))

## Related Work

Differential Testing:

- CRADLE (**related work**): use differential testing to find bugs in deep learning libraries through cross-backend validation? what is this.

- Use multiple well-designed models to examine the integrity of the dataset (if these models disagree with the dataset in consistent ways, there might be a problem in the dataset.

## Solution

1. Deepen the understanding of the judgments of different models:

    with ***Shannon entropy.***

    Smaller values indicate the probabilities will be concentrated over fewer object classes. (**model predictions can be assumed *to be confident* and *predictable.***

    By computing and analyzing H(y) for predictions made by different models, we have a heuristic that can help us uncovering possible oracle issues -- **in particular in relation to ambiguity and observability of object classes.**

“However, when moving towards broader visual understanding and reassessments of the trustability of existing oracles, certain classification ‘mistakes’ may be more logical and explainable in comparison to the ground truth than others.” ([Liem and Panichella, 2020, p. 485](zotero://select/library/items/FTTVC75J)) ([pdf](zotero://open-pdf/library/items/48TJVEMC?page=3&annotation=HB9LN79U))

## Conclusions

If for a given **image**, all models fail to recognize the ground truth class in the top-5,

- while showing **high** entropy in their predictions: **no clear object class is present in the image**

- while showing **low** entropy and consistency: **another object class is more salient than the labeled ground truth**

If for a given **class,** models consistently have problems recognizing the ground truth in the top-5, the image class may not visually standout.

If two classes are consistently confused by the models, they may have been synonyms, homonyms, or meronyms.

## Insights

1. Image classes are often not independent. However, their mathematical representation implies they are.
2. Maximum likelihood criteria will nudge models towards treating the classes as independent.
3. Traditional final success assessment ignores prediction confidence (instead, they only cares about the presence of global truth in top-5, etc.)
