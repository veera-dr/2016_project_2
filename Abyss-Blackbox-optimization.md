ABySS Blackbox Optimization
================
Nivretta Thatra
October 15, 2016

Abstract
========

-   When tackling optimization of parameters, the process is manual and tedious: submitting jobs to a scheduler, rerunning failed jobs, inspecting outputs, tweaking parameters, and repeating. In genome sequence assembly, for example, there are a variety of parameters related to expected coverage of the reads and heuristics to remove read errors and collapse heterozygous variation.

-   BlackBox parameter optimization tools do exist, but their usibility and speed need to be compared & evaluated.
-   Approaches of optimimation tools:
    -   *Exploitation Approach*: Start halfway and try a point to the left and to the right, find next best, iterate
    -   *Exploration Approach*: Try a bunch of random ranges
    -   *Grid Search Approach*
-   Here we evaluate 3 optimization tools - Opal, SpearMint, and ParOpt - on a dataset of a human bacterial artificial chromosome (BAC), using the assembler [ABySS](https://github.com/bcgsc/abyss#readme).

-   We find that

Goals/Methods
=============

Evaluate 3 parameter optimization tools for usability and speed
---------------------------------------------------------------

-   Divvy up 3 tools for testing
-   Download ABySS
-   Access dataset from ORCA computing machine

-   Backend
    -   What types of input parameters (discrete with large/small ranges, continuous, binary)
    -   Make it portable to other commandline tools so optimizer can be told how to launch the tool
-   Results output
    -   Generate target metrics vs parameters plot
    -   Generate Pareto frontier of the target metric and a second metric of interest (contiguity and correctness) likely in R using ggplot
    -   Generate a report of the results of the optimization
-   Write a short report of our experience
-   Post on GitHub pages
-   Possibly submit to a preprint server (bioRxiv, PeerJ, Figshare)
-   Possibly submit for peer review, such as F1000Research Hackathons

Dataset(s) and Optimizers
-------------------------

-   Dataset
-   a human bacterial artificial chromosome (BAC), using assembler [ABySS](https://github.com/bcgsc/abyss#readme)

-   Metrics
-   The key metrics are *contiguity* (a.) and *correctness* (b. through d.).
    1.  contiguity (NG50, N50) and aligned contiguity (NGA50, NA50)
    2.  number of breakpoints when aligned to the reference as a proxy for misassemblies
    3.  number of mismatched nucleotides when aligned to the reference, Q = -10\*log(mismatches / total\_aligned)
    4.  completeness, number of reference bases covered by aligned contigs divided by number of reference bases
-   We'll be optimizing the NG50 metric (or NGA50 with a reference genome) and reporting (but probably not optimizing) the correctness metrics.
-   The primary parameter we'll be optimizing is k (a fundamental parameter of nearly all de Bruijn graph assemblers), and there's a bunch other parameters that we can play with (typically thresholds related to expected coverage).

-   Optimizers being evaluated
    -   [OPAL](http://pythonoptimizers.github.io/opal/) by @dpo — [Optimization of algorithms with OPAL](http://link.springer.com/article/10.1007/s12532-014-0067-x)
    -   'nondifferentiable optimization tools'
    -   'runs on most platforms supporting the Python language and possessing a C++ compiler'
    -   'an optimization method supported by a strong convergence theory, yielding solutions that are local minimizers in a meaningful sense'

    -   [SpearMint](https://github.com/hips/spearmint) by @mgelbart — [Predictive Entropy Search for Multi-objective Bayesian Optimization](https://arxiv.org/abs/1511.05467)
    -   Bayesian method for identifying the Pareto set of multi-objective optimization problems, when the functions are expensive to evaluate
    -   a sum of objective specific acquisition functions, which enables the algorithm to be used in decoupled scenarios in which the objectives can be evaluated separately and perhaps with different costs

    -   [ParOpt](https://github.com/sseemayer/ParOpt) by @sseemayer
    -   [scipy.optimize](http://docs.scipy.org/doc/scipy/reference/optimize.html)
    -   [Nelder-Mead](https://en.wikipedia.org/wiki/Nelder%E2%80%93Mead_method)

    -   Possibly R packages, [a long list](https://cran.r-project.org/web/views/Optimization.html)
    -   Possibly Python packages, [like scikit-optimize](https://scikit-optimize.github.io/)

Results
-------
