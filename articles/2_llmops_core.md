# LLMOps Core

***Deploy and operate GenAI applications***

Generative AI has introduced a new way to build and operate AI applications that is different from predictive AI. To build a generative AI application, you must choose from a diverse range of architectures and sizes, curate data, engineer optimal prompts, tune models for specific tasks, and ground model outputs in real-world data.

This document describes how you can adapt DevOps and MLOps processes to develop, deploy, and operate generative AI applications on existing foundation models.

You can find more details about DevOps, MLOps and the difference between then, reading this [document](1_mlops_core.md).

### What are foundation models?

Foundation models are the core component in a generative AI application. These models are large programs that use datasets to learn and make decisions without human intervention, are trained on many types of data including text, images, audio, and video. Foundation models include large language models (LLMs) such as Llama 3.1 and multimodal models such as Gemini.

Foundation models are trained on massive and diverse datasets. This training lets you use foundation models to develop applications for many different use cases. Foundation models have emergent properties, which let them provide resposes to specific inputs without explicit training.

Because of these emergent properties, foundation models are challenging to create and operate and require you to adapt your DevOps and MLOps processes.


#### Lifecycle of a generative AI application

The lifecycle of a generative AI application has several phases:
1. **Discovery:** Developers choose the best foundation model for their use case by considering strengths, weaknesses, and costs.
2. **Development and experimentation:** Developers create and refine prompts to get the desired output, using techniques like few-shot learning and model chaining to guide the model.
3. **Deployment:** Developers manage different artifacts like prompts templates and fine-tuned models, ensuring they meet infrastructure requirements for the deployment process.
4. **Continuous monitoring:** Administrators improve performance and ensure fairness, transparency, and accountability in the model's outputs.
5. **Continuous improvement:** Developers adjust models through new techniques or by combining models to improve performance, reduce costs, or lower latency.

Data engineering is important throughout the process to ensure accurate and up-to-date outputs by using reliable data.

### Find the foundation model for your use case

When choosing a foundation model for your use case, it's important to consider several factors:
1. **Quality:** Test prompts to check the output quality
2. **Latency and throughput:** Ensure the model meets the speed and performance requirements of your use case, such as low latency for chatbots.
3. **Development and maintenance time:** Managed models may require less effort than self-deployed models.
4. **Usage cost:** Consider the costs of infrastructure and usage.
5. **Compliance:** Check if the model meets regulatory and licensing requirements.

Choosing the right model is challenging because each one has different architectures, datasets, and licenses, and each use case has unique needs.

### Develop and experiment


### References
- [Deploy and operate generative AI applications by Google](https://cloud.google.com/architecture/deploy-operate-generative-ai-applications)
