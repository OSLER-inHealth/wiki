# wiki
wiki for OSLER-inHealth

A scanned document of Yates' formalization of [modeling strategy is available](https://drive.google.com/open?id=0B5HGTlNkLUZOWXVUbVg0Mi1KeXZxQ0NrT3BHZ2RoRDUtQTBR).

A google document with an overall strategic software vision is [Zhenke's overview](https://drive.google.com/open?id=163_B8owojulBmZzGhqYJreWNsjkTbbCM6LTGLU-xbR4).  Write to Vince if you have access issues.

Pneumonia data in a public version -- we should have a node in this repo that has a .rda or some
readily parsable text for this data structure

Good rationale for the chosen structure in terms of the statistical components of the model, also include 
Yates' layout

Formula prototype -- probably a list of formulas at this time, whose symbols refer to the data structure
or the relationships in the formalism

What JAGS models are written by hand, and what exists to compose such models from more informal specifications
of models?

What needs to be done to get our data into JAGS for the baker model/pneumonia case

Compare to the situation with prostate model.


# Meeting Minutes

## December 1st, 2016

1. Updates on packages: 
    - `baker`: 
         1. JAGS is not the only MCMC software that we will be using. Alternatives are [Stan](http://mc-stan.org), [INLA](https://pymc-devs.github.io/pymc3/index.html), [NIMBLE](https://bids.berkeley.edu/research/nimble-numerical-inference-hierarchical-models-using-bayesian-and-likelihood-estimation), [PyMC3 (python-based)](https://pymc-devs.github.io/pymc3/index.html). The methods packages that inHealth platform will host need to have multiple cleanly designed components including data cleaning/formatting, model specification, model fitting (including packages for Bayesian inferences), model checking, visualizations. Such component isolation reduces the burden for maintainence because developers can have changes to a component like JAGS, isolate the impacts, carry out compatibility changes in a systematic way, with regression testing to ensure that one has not broken something by fixing something else. The [`RUnit`](https://cran.r-project.org/web/packages/RUnit/index.html) package for unit testing is helpful for accomplishing the test discipline. We should have unit tests in each of the OSLER-inHealth methods packages.
         1. GitHub is very valuable for mobilizing community energy to do such things -- when you have
users who are compromised by incompatbilities, sometimes one is motivated to carry out the
maintenance work and you get a pull request.  Run your tests and if they pass you can merge
in the patch.
    - `prostate cancer prediction`
