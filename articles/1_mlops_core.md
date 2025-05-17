# MLOps Core

This document discusses techniques for implementing and automating continuous integration, continuous delivery, and continuous training for machine learning systems.

In other words, we want to apply DevOps principles to ML systems (MLOps). Practicing MLOps means that you advocate for automation and monitoring at all steps of ML system construction, including integration, testing, releasing, deployment and infrastructure management.

Only a small fraction of a real-world ML system is composed of the ML code.

![Elements of ML](img/mlops-cd-and-automation-pipelines-in-ml-elements-of-ml.png)

To develop and operate complex systems like these, you can apply DevOps principles to ML systems. This document covers concepts to consider when setting up an MLOps environment for your data science practices, such as CI, CD, and CT in ML.


### DevOps versus MLOps
***What is the difference between traditional CI/CD and CI/CD for ML?***

DevOps is a popular practice in developing and operating large-scale software systems. This practice provides benefits such as shortening and development cycles, increasing deployment velocity, and dependable releases. To achieve these benefits, you introduce two concepts in the software system development:

- Continuous integration (CI)
- Continuous delivery (CD)

As ML system is a software system, so similar practices apply to help guarantee that you can reliably build and operate ML systems at scale.

ML and other software systems are similar in continuous integration of source control, unit testing, integration testing, and continuous delivery of the software module or the package. However, in ML, there are a few notable differences:
- CI is no longer only about testing and validating code and components, but also testing and validating data, data schemas, and models.
- CD is no longer about a single software package or a service, but a system (an ML training pipeline) that should automatically deploy another service (model prediction service).
- CT is a new property, unique to ML systems, that's concerned with automatically retraining and serving the models.