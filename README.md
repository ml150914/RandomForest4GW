# Random Forest for Gravitational Waves

## What's that!?

Gravitational Waves (GW) are ripples in the space-time caused by extremely violent astrophysical or cosmological phenomena. Predicted by Einstein in its famous equations,
the first GW event have been measured by the LIGO observatories the [15th september 2025](https://en.wikipedia.org/wiki/First_observation_of_gravitational_waves), and since then, more than 100 events have been recorded!

Measuring such signal is very complicated, the phisical displacement associated to the passage of a GW is aroung the 1000th-part of a proton's diameter. In addiction,
the data strain is heavily polluted by noise sources, affecting the statistical significance if not taken into account. 

In this work we explore an application of (not-so) modern machine learning algorithm such as Random Forest (RF) to boost the detection significance of a pipeline deployed 
for measuring such signals. 

For the scientific tratement, check the [paper](#arxiv). Here I will introduce briefly the principle and how to deploy the RF for this purpuse. 

## What is a Random Forest? 

The [Random Forests](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf) algorithm is a regression/classification algorithm widely used for tabular data. The main idea is to partionate the features' space into rectangles using the binary tree approach, and then average away noise or biased behaviour by considering  several of such trees in a bootstrapped dataset. 

Its efficiency has been extensively proven in healthcare areas or decision-like problems. Even in [GW its capacities have been proven](https://arxiv.org/pdf/1709.02421)!
In this work, we explored the capability of the algorithm in helping us by distinguish noise artifacts from signal-like triggers provided by the pipeline [MBTA](https://arxiv.org/pdf/2501.04598)
expoiting the O3 data acquisition campaign data. 

## How is the Random Forest applied in this context? 

The Random Forest will help us distinguish noise from signal by assigning to the data a score $p_\mathrm{s}$ that quantifies how 'confident' is the algorithm that a given 
datapoint belong to signal ($p_\mathrm{s} \sim 1$) or noise ($p_\mathrm{s} \sim 0$). 
The data are obtained by the coincidence triggers of MBTA pipeline, and consists in tabular data. Each point will have several features, that characterize the 'noise' or 'signal' population. The Random Forest, once trained, is capable in distinguish between these two. 
Once the algorithm is trained, its efficiency is tested by comparing its score and the usual statistical significance provided by MBTA explotining the [ROC curves](https://en.wikipedia.org/wiki/Receiver_operating_characteristic). 
Finally, we test the strength of this new statistics $p_\mathrm{s}$ by computing the probability of being an astrophysical signal $p_\mathrm{astro}$. 

## Does it work?

The study showed that the Random Forest $p_\mathrm{s}$ statistics is as good as the usual statstical significance used by MBTA, that is quite impressive since obtaining this statistic require a huge effort, while the $p_\mathrm{s}$ is automatically obtained by the algorithm within few seconds!
Also, the $p_\mathrm{astro}$ probability obtained by the Random Forest ranking-statistics is compatible with the one obtained in the usual method, that is something expected since the just mentioned results.

# Ok, how can I play with the codes? 

In the folders '/RF-codes' you will find the Jupyter Notebook that will read the data (that are in '/data' subfolder - check path when you load them), train the random forest and test the algorithm! Everything is commented an explained.
Of course you will need the packages of `scikit-learn` to use the Random Forest algorithm as well as basic python packages such as pandas, numpy or matplotlib!


