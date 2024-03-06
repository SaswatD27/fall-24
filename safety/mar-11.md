
# Introduction and Motivations
Machine learning is often done with the naive assumption that the data used to train a model is well-behaved. However, a class of attacks known as poisoning attacks have been developed in the last decade or so that involve adding carefully maliciously perturbed points to the training set to make models misbehave. Even the addition of one or a few points can impact the behavior of a model, leading it to exhibit poor performance or misclassify certain points to the adversary's benefit.

Consider the case when a company selling antivirus software relies on the use of ML to train malware classifiers. The data used to train such classifiers is often publicly sourced and given the large amounts of data that training such classifiers may require, it may not be humanly possible to audit each and every data point in the training set. Adversaries can then sneak in carefully perturbed points, given some knowledge about the model's architecture, training data distribution, parameters, etc. (white-box setting) or even just query access to it (black-box setting), and make the trained malware classifier classify some malware as benign software. Issues related to data poisoning have been investigated in the contexts of self-driving cars, medical AI, etc. as well.

For ML and ML security/safety practitioners, it thus becomes key to ensure that their models are *adversarially robust*. To this end, studying possible vulnerabilities (here to data poisoning) and attacks is an important area of security research. ML security research over the last few years has resulted in attacks that utilize human-indistinguishable adversarial points. This document is meant to introduce readers to the rationale behind poisoning attacks, explain their workings, and how they might be prevented.

# Methods

# Key Findings
The [Poisoning Attacks against SVMs](https://arxiv.org/abs/1206.6389) paper contributes these findings:
- An adversary can "construct malicious data" based on predictions of how an SVM's decision function will change in reaction to malicious input
- A "gradient ascent" attack strategy against SVMs can be kernelized, allowing for attacks to be constructed in the input space
    - The attack method can be kernelized because it only depends on "the gradients of the dot products in the input space"
    - This is a big advantage for the attacker when compared to a method which can't be kernelized; an attacker using a non-kernelizable method "has no practical means to access the feature space"
        - The authors note that this emphasizes that "resistance against adversarial data" should be considered in the design of learning algorithms

The [Certified Defenses for Data Poisoning Attacks](https://arxiv.org/abs/1706.03691) paper discusses how certain defenses against data poisoning can be tested against "the entire space of attacks".
- Specifically, the defense must be one that removes "outliers residing outside a feasible set," and minimizes "a margin-based loss on the remaining data"
- The authors' approach can find the upper bound of efficacy of any data poisoning attack on such a classifier
- The authors analyze the case where a model is poisoned and where both the model and its poisoning detector are given poisoned data

# Critical Analysis
The [Poisoning Attacks against SVMs](https://arxiv.org/abs/1206.6389) paper describes a kernelizable method of attacks against SVM models. The authors note that this work "breaks new ground" in the research of data-driven attacks against such models because their attack strategy is kernelizable. Their findings and conclusions are intuitive and easy to follow from the reader's point of view. Their attack strategy description is accompanied by a clear example: an attack on a digit classifier. They clearly show how the attacker is able to use their strategy to modify training input data to produce classification error. These attack modifications are understandable to the user as well: they clearly show how the attacker modifies the data so that the "7 straightens to resemble a 1, the lower segment of the 9 becomes more round thus mimicking an 8," and so on. Overall, the authors of this paper adequately communicate the technical aspects of their attack strategy in a way that even non-technical readers can easily understand, and the conclusions that follow are well-supported by the evidence they gathered in their attack.

    
