# Challenges of Large Language Models Applications
By Matheus Gonzalez

---
You don't test GenAI, you evaluate it. Generative AI is nondeterministic, meaning its responses are not standardized and cannot be tested in a quantitative way.

To identify possible problems that happen with LLMs, we need to go deep about Regression and Non-Regression Tests and how to apply it using LLMOps.

### Regression and Non-Regression Tests in LLMOps

**Regression Tests**

Ensure that new version of your LLM system does not break existing functionalities. Example, if your chatbot answered questions about credit card correctly in v1, it must still do so in v2 after retraining or prompt tuning.

What to test: 
- **Accuracy -** Check if the model still produces correct answers on known-good inputs. Expert examples can helps in this step, it can serve as benchmarks, providing a high-quality reference point for assessing model performance. Combining expert examples with algorithms like **BLEU**, **ROUGE**, and **BERTScore** we could produce a scale solution that can handle a large volume of information.

- **Hallucination Rate -** Ensure that the updated model doesn't invent facts. In this case we calculate the percentage of model responses that include made-up or unverifiable information (true/false). I found two automated ways to calculate it, using a LLM as a Judge (e.g, "Does this answer contain hallucinations? Only answer Yes or No."), and using RAGAS if you're using a RAG system.

- **Latency Regression -** Check if model response time increases after updates. In this step we can conduct a Stress Test / Load Test to guarantee that the LLM system will response at the expected time 

- **Prompt-template Compatibility -** Check if old prompt structures still work after prompt refactoring or system prompt changes. We can create unit tests that test different phrasing or structures of the prompt.

- **Vector store schema change -** Changes to vector schema or backend can silently break your RAG system, causing degraded results or completely empty retrievals which leads to hallucinations from the LLM. One way to ensure the schema is using Pydantic to schema validation.

**Non-Regression Tests**

Ensures that everything still works as expected after any kind of changes (even if you didn't retrain the model)

These tests are like "health checks" to make sure your system didn't accidentally break because of:

- **LLM version change -** If you changed GPT-3.5 to GPT-4 or switched from OpenAI to Mistral, for example, it's important run the same test prompts through the old and new models and evaluate the response using BLEU, ROUGE e BERTScore.

- **Model Drift -** The model's output gradually changes over time usually because the model API, retriever, or fine-tuning data has shifted. In other words, same prompt = different answer today vs last week. It happens a lot with closed models as OpenAI for example. To detect, you can stores outputs from known "golden prompts" over time, re-run them weekly and compare with previous answers (diffing) using BERTScore or LLM as a judge.

- **Data drift (Input drift) -** The data you're sending to the model is changing over time and your prompts is not handling it well anymore. To detect it before cause any problem, you could create a pipeline to cluster or analyze embeddings (e.g, TSNE or PCA) using real inputs, clustering and storage it periodicaly to compare the distance between clusters through the time. Also, create alerts for data drift rate it's a good strategy.


### Conclusion

LLMs present unique operational challenges due to their nondeterministic behavior and dynamic interaction with external tools and data. Traditional software testing isn't enough, instead, we must evaluate these systems through structured regression and non-regression tests.

By embracing LLMOps principles, we gain tools to measure:
- Whether model performance remains consistent across versions
- Whether prompt or schema changes break outputs
- And whether silent shifts in data or model behavior compromise system quality.

Testing LLMs isn't about getting the same output every time. It's about ensuring the system stay useful, truthful, and stable even when its components update.

**How to implement**

- Snapshot critical prompts and expected outputs
- Use **pytest** or **LangChain Expression Language (LCEL)** to validate answers
- Compare outputs across versions with similarity metrics (BLEU, ROUGE, cosine similarity)
- Visualize drift with dashboards (e.g, LangSmith, Weights & Biases)


### Glossary

- **BLEU (Precision):** Compares n-grams in the model's output to the reference (correct) answer. This metric rewards exact matches, for example the reference "I love chocolate cake" and the model output "I like chocolate cake" will produce a low BLEU score because "love" is different of "like", even if meaning is close. ([bleu - huggingface](https://huggingface-co.translate.goog/spaces/evaluate-metric/bleu?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc))

- **ROUGE (Recall/Overlap):** Focus on recall, measures overlap in words/phrases between model output and reference. Example, calculating ROUGE using the following reference="I love chocolate cake" and model output="I like chocolate cake" will produce a high score because many words overlap, even if phrasing is different.

- **BERTScore (Meaning/Similarity):** Uses BERT embeddings to check semantic similarity, looking at the meaning rather than exact words. Example, reference="I love chocolate cake" and model output="I like chocolate cake", in this example BLEU/ROUGE might penalize the score, but BERTScore will produce a high score because semantically it's the same. ([bert_score - huggingface](https://huggingface.co/spaces/evaluate-metric/bertscore))

- **RAGAS:** A library that provides tools to supercharge the evaluation of LLM applications. ([docs.ragas.io](https://docs.ragas.io/en/stable/))


### References

- [Challenges and Applications of Large Language Models](https://arxiv.org/pdf/2307.10169)
- [(Why) Is My Prompt Getting Worse? Rethinking Regression Testing for Evolving LLM APIs](https://arxiv.org/html/2311.11123v2)
- [Evaluation Strategies for LLMOps: Ensuring Accurate Cognitive Applications](https://medium.com/@fearney/evaluation-strategies-for-llmops-ensuring-accurate-cognitive-applications-b3806dbb74ab)
- [Tests for Topic Drift in MLOps and LLMOps](https://alice-sh-wong.medium.com/tests-for-topic-drift-in-mlops-and-llmops-6dac0eefc3d4)


