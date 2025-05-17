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


### Data Science Steps for ML

In any ML project, after you define the business use case and establish the success criteria, the process of delivering an ML model to production involves many steps, for example: data extraction, analysis, preparation, model training, model evaluation, validation, serving, and model monitoring.

The level of automation of these steps ***defines the maturity of the ML process, which reflects the velocity of training new models given new data or training new models given new implementations***.


### MLOps level 0: Manual process

In this level, the process for building and deploying ML models is entirely manual. This is considered the basic level of maturity, or level 0.

![Manual ML steps to serve the model as a prediction service](img/mlops-cd-and-automation-pipelines-in-ml-2-manual-ml-level-0.svg)

**Characteristics**

MLOps level 0 is a manual, script-driven process where each step, including data analysis, preparation, model training, and validation, is performed interactively by data scientists. There is a clear separation between data scientists, who create models, and engineers, who deploy them as prediction services, leading to potential training-serving skew. Model iterations are infrequent, with new versions deployed only a few times a year. Continuous integration (CI) and continuous deployment (CD) are not implemented, as model changes are rare.

The process focuses solely on deploying the model for prediction, without active performance monitoring or tracking of model behavior, which may result in undetected performance degradation. Deployment often includes A/B testing or online experiments before full deployment.

**Challenges**

Level 0 is common in businesses just starting with ML, relies on a manual, data-scientist-drive process. While sufficient for infrequent model updates, it faces challenges in real-world deployments, where models often fail due to environmental or data changes. To maintain accuracy, active monitoring of model performance, frequent retraining with up-to-date date, and continuous experimentation with new implementations are essential. Implementing CI/CD and continuous training (CT) practices can streamline this process, enabling quicker updates and improvements to the model pipeline.


### References

- [MLOps: Continuous delivery and automation pipelines in machine learning](https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning)
