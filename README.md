# Amharic Text Moderation

This project provides the framework for creating an Amharic text moderation system. The goal of this project is to develop a tool capable of detecting harmful and inappropriate content in Amharic text, particularly for social media platforms. The system leverages natural language processing (NLP) techniques to identify and moderate hate speech, cyberbullying, explicit content, and sensitive topics. While the initial application is focused on social media, this system can be adapted to other platforms, including online forums, news articles, and messaging apps.

The **Amharic Text Moderation** pipeline processes text through multiple stages to assess and classify content based on sentiment, entity recognition, text classification, and topic classification. This project aims to provide an efficient, scalable, and adaptable solution to content moderation in Amharic language settings.

---

## Documentation

- **Overview**: An in-depth introduction to the project, its goals, and architecture.  
  [Read Overview](docs/01_overview.md)

- **Dataset Requirements**: Details on the necessary datasets to build a robust moderation system.  
  [Read Dataset Requirements](docs/02_dataset_requirements.md)

- **Found Datasets**: A list of available datasets suitable for training models for Amharic text moderation.  
  [Read Found Datasets](docs/03_found_datasets.md)

- **Dataset Challenges**: Discusses the challenges in working with Amharic text data and potential solutions.  
  [Read Dataset Challenges](docs/04_dataset_challenges.md)

- **Model Selection**: Criteria and suggestions for selecting appropriate models for sentiment analysis, entity recognition, and more.  
  [Read Model Selection](docs/05_model_selection.md)

- **Pipeline Architecture**: A detailed explanation of the system architecture and its components.  
  [Read Pipeline Architecture](docs/06_pipeline_architecture.md)

- **Decision Engine**: Describes the logic used to determine moderation decisions.  
  [Read Decision Engine](docs/07_decision_engine.md)
---

## Architecture Diagram

Here is the high-level architecture of the Amharic text moderation pipeline:

![Text Moderation Pipeline](/Diagram/RLNTZkCq5BxtKnn5MZGL7J7CWeH66hJzQLc9Tgdw0qW8hLpdD35rx60xiriXxWiy0XBYYXi4T-pxz4quTYRPj9gRoSJvllFpVUUuBvpdrbU5ObvwXJ0eScwbW3M-zJ0tALhkfT6ma2KggP6nal1Io99h3yd6eKs0EzYSdo-uHNekZAC_r.png)  
High-level architecture of the Amharic text moderation pipeline. View the diagram in SVG format [here](https://www.plantuml.com/plantuml/svg/RLNTZkCq5BxtKnn5MZGL7J7CWeH66hJzQLc9Tgdw0qW8hLpdD35rx60xiriXxWiy0XBYYXi4T-pxz4quTYRPj9gRoSJvllFpVUUuBvpdrbU5ObvwXJ0eScwbW3M-zJ0tALhkfT6ma2KggP6nal1Io99h3yd6eKs0EzYSdo-uHNekZAC_rWXqpjJ0nM9n3fsZvodt75RUM9uXN8tfRSiTzY9XlZh7ZqnHeBuCExg8EiISFqWAg62WkJeuwI9kE3Z7ZL585ngSw8pQYvZnv1pJaM4WmiFLXLs4cYAcMoxsC3EcZ8ZfZB7xUtX23Aapk5fO5AOeAuzf3-xlsGQkFm_wtC788lVuqQPCwH69ZCxRpnDDPXrWIVHCorZOrQDnryF9Sjq7L_BHeNT6MfkIV1qfJjbtKl2QzkrilZHRj9xVKHv5mOJhmyJdMWhAqQSaIcO4xSCNg97qRAAICNVHCuJ6mevrZCrNRUht5eiS2ywqyGXMPha7imi6_yG0afBQV2tJv0uIlXKVtpvF-k4OGxCI7Pr_bvn-_Ujq_EVqoxlJR-zEn_-IFjH7_vwEVzGlVvwElv-EVoVVHx8FJTVKjgU0QrfzX5LHwFGrzo7xxStj9zStdrrJ1UndXZg5K72qycBuoCRMk14rkggsXVGDYerQdQReHTuCGYC7VM-9eSl0QQVrtD5UYttQ_RevMAdAadrVuk6DiQdhik92Nxh_CepNgaGKUH--skrGE-p34BNCT4CU3c9vQTjxy1Xsna9OVcWMhIqywlJ4-WMXXeCcuYX7iQyZl9JE6tku_1Z7FWWyjVXZXLeqYF6445o9IeNgbzBjQQwChGqQ7pGlf82BlGx9nvE6FSWoYrbWHw8x4m8-lNa67tOSUHxV9uzZ2BStpthTMEaFbVEmpYbERbJgOCWTfc1qOtTSFDUbbAKY_og5mUNAc-kXCc9FQ-S43qtrOPNprBoXK6G3uyh3UnW30AY3pKchUDPu4x_DeqgREtXblDmTQf6lsdjpYOLvm3Gws6axwJ5K3jiQBjB42OYKgk2QWZn8V1CPdLelE3FPMGRuclpOIaMZ6rQAiRhCwOnm9kl-r3JMHJ_FBjNWudJMqDOsd4-vSl6A97SUqC47y8giZVztiDyWxeFcw2sNEaoLsSMSgeEY0-rpWitmhHHKINt_EiPUKCLLeVu7)

---