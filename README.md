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

> Release early and often - Vince


1. Updates on packages: 
    - `baker`: 
         1. JAGS is not the only MCMC software that we will be using. Alternatives are [Stan](http://mc-stan.org), [INLA](https://pymc-devs.github.io/pymc3/index.html), [NIMBLE](https://bids.berkeley.edu/research/nimble-numerical-inference-hierarchical-models-using-bayesian-and-likelihood-estimation), [PyMC3 (python-based)](https://pymc-devs.github.io/pymc3/index.html). The methods packages that inHealth platform will host need to have multiple cleanly designed components including data cleaning/formatting, model specification, model fitting (including packages for Bayesian inferences), model checking, visualizations. Such component isolation reduces the burden for maintainence because developers can have changes to a component like JAGS, isolate the impacts, carry out compatibility changes in a systematic way, with regression testing to ensure that one has not broken something by fixing something else. The [`RUnit`](https://cran.r-project.org/web/packages/RUnit/index.html) package for unit testing is helpful for accomplishing the test discipline. We should have unit tests in each of the OSLER-inHealth methods packages.
         1. In the case of `baker`: can minimize the exposure of R code to JAGS so that future updates will not break `baker`.
         1. GitHub is very valuable for mobilizing community energy to do such things -- when you have
users who are compromised by incompatbilities, sometimes one is motivated to carry out the
maintenance work and you get a pull request.  Run your tests and if they pass you can merge
in the patch.
    - `prostate cancer prediction`
        1. Vignette in writing; Julia is working on it with new funding support.

1. Platform components up- and down-stream to methods packages
    - *Upstream* 
        1. Current model of exporting data from EHR, such as EPIC. Developer currently can request data from EPIC and they can run their model locally.
        1. *Good to have*: Tools to harvest EPIC for developers/analysts to do their projects. For example, take all the data related to the search criteria, and determine the treatments used, dates of visit or operation. Because currently data mangement people usually connect the raw database to developers, the methods packages need to articulate the requirements on the input data for each methods package so they can know what needs to be extracted for specific analyses. 
    - *Downstream*: 
        1. Currently need to get data out of EPIC, put them on a separate server, run the code, get the results, and add a link in EPIC to these results. Also, in EPIC, we can document what decisions for patients are made based on the analyses. 
        1. *Obstacles*: EPIC management do not want extraneous information, e.g., image and other things, they want to have a clean body of documents (?).


1. Software capacity for large datasets and/or complex models (scalability)
   - Three challenges to fast Bayesian computing: 
       1. *Large data volume*. Slows down conventional Bayesian posterior computing. Possible solution: approximate Markov chain transition kernel in place of exact ones (approximate MCMC that trades-off bias and computational speed), divide-and-conquer (split data into many small pieces, obtain posteriors for each subset of data or sub-posteriors, and then combine or find the "center" of all sub-posteriors). Examples are: [concensus MCMC](http://www.rob-mcculloch.org/some_papers_and_talks/papers/working/consensus-mc.pdf), [Weierstrass sampler](https://arxiv.org/abs/1312.4605) and finding the [Barycenter of subposteriors](https://arxiv.org/abs/1508.05880).
       1. *Monte Carlo errors that decays at the rate of square root of sample size*. (100 more parallel computers only 10 times more precise)
       1. *High dimensionality of unknown parameters*. Possible solution: hybrid algorithm that run MCMC for a subset of the parameters and use fast estimates for others. For example, first run some fast manifold detection algorithm in high-dimensions, extract the manifold and model data as noisy observation near it; Reference [here](https://projecteuclid.org/download/pdfview_1/euclid.aos/1458245738).

1. Other business:
   1. Plan a session in ENAR or JSM meeting, so that the work built towards the talks can appear in a special issue in JASA or SIM. Also can encourage other researchers in this area to share, combine tools in a mutually beneficial way.
   1. Plan software deliverables for 2017 DC Advisory Board Meeting.

