Types of uncertainty
The first question I’d like to address is what is uncertainty? There are actually different types of uncertainty and we need to understand which types are required for different applications. I’m going to discuss the two most important types – epistemic and aleatoric uncertainty.

Epistemic uncertainty
Epistemic uncertainty captures our ignorance about which model generated our collected data. This uncertainty can be explained away given enough data, and is often referred to as model uncertainty. Epistemic uncertainty is really important to model for:

Safety-critical applications, because epistemic uncertainty is required to understand examples which are different from training data,
Small datasets where the training data is sparse.
Aleatoric uncertainty
Aleatoric uncertainty captures our uncertainty with respect to information which our data cannot explain. For example, aleatoric uncertainty in images can be attributed to occlusions (because cameras can’t see through objects) or lack of visual features or over-exposed regions of an image, etc. It can be explained away with the ability to observe all explanatory variables with increasing precision. Aleatoric uncertainty is very important to model for:

Large data situations, where epistemic uncertainty is mostly explained away,
Real-time applications, because we can form aleatoric models as a deterministic function of the input data, without expensive Monte Carlo sampling.

label: bayesianism

source: Deep Learning Is Not Good Enough, We Need Bayesian Deep Learning for Safe AI (https://alexgkendall.com/computer_vision/bayesian_deep_learning_for_safe_ai/)
