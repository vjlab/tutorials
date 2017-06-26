# Tree Computation
## Maximum Likelihood & Bayesian Paradigms for Tree Computation
Note that these are not two opposing frameworks, nor are they the *only* frameworks for the interpretation of probability.  The (opposing) counterpart to Bayesian statistics is frequentist statistics, which is out of the scope of this tutorial, but quite nicely summed up as follows:

![xkcd1132](https://imgs.xkcd.com/comics/frequentists_vs_bayesians.png)

The bottom line is:
- **Maximum likelihood** methods compute the most likely tree that evolved the observed sequence data. Answers the question: "*Out of all these models, which is the most likely one to have arisen out of the given data?*" Note that ML can only compare between models to pick the most appropriate one - it is unable to assess the correctness of a model.  
- **Bayesian** methods have an extra step of modeling the uncertainty we have about any previous relevant information as a probability distribution by itself. This is called the *prior*. 

*Note: all this is actually much easier in maths, because many things get lost in translation when attempting to convert these concepts into English. Ultimately, it's all just calculus.*

## An Overview of Tree Computing Software
### FastTree
 - Fast, as you may have picked up from the name. Typically terminates within minutes, even with thousands of sequences.
 - Computes only one tree, so the results of FastTree are questionable not so much because of the accuracy of the tree, but because it doesn't give a way to assess the quality of the result (e.g. by likelihood or empirical support).
 - Anecdotally, seems reasonably accurate at computing the initial bifurcations, i.e. identifying major clades. Might get confused by sequences that could go either way. 

### IQTree
 - ML-based. 
 - Not terribly fast. It *could* be faster than RAxML; I've never really tested it. 

### RAxML
 - Very slow, so only used in production when we have to compute publication-quality trees, with a certain number of iterations (>500 or >1000 required for publication, depending on who you ask) - as such, would typically take a week. 
 - Has PTHREADS for multiple-CPU parrallelization, and an SSE-extension to speed things up just that much faster - but still slow.
 - Only use on the HPC.
 - Will only terminate within a reasonable amount of time for <1000 sequences (and that's still pushing it). 
 
### BEAST
 - Bayesian paradigm, so you'll get something like P(Tree|Models, ModelParams). 
 - With a nice point-and-click interface, so probably the most user-friendly. Also has helper programs `BEAUTi` and `Tracer`.
 - Also very slow, but anecdotally faster than RAxML
 - Has GPU support, which on benchmark tests, gives a 4x speedup on M3's K80 GPUs.
