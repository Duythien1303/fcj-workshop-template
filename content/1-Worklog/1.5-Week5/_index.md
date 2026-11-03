---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---


### Objectives for Week 5

- Gain a general understanding of Generative Artificial Intelligence (Generative AI) and its role in modern applications.
- Understand the fundamental concepts of Large Language Models (LLMs), Foundation Models, and methods for applying language models.
- Explore Amazon Bedrock and its capabilities for developing Generative AI applications on Amazon Web Services (AWS).
- Study Prompt Engineering and techniques for improving the quality of AI-generated responses.
- Research Retrieval-Augmented Generation (RAG), Embeddings, Vector Databases, and Knowledge Bases.
- Understand AI Agent architectures and how AI models can be integrated with APIs, tools, and external data sources.

### Tasks to Be Completed This Week

| Day | Tasks | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | - Explore Generative AI and its real-world applications. <br> - Study Large Language Models (LLMs) and Foundation Models. <br> - Understand the differences between Traditional AI, Generative AI, and Agentic AI. <br> - Research AI applications in software development, natural language processing, and automation. | 02/11/2026 | 02/11/2026 | [AWS Generative AI](https://aws.amazon.com/generative-ai/) |
| Tuesday | - Explore Amazon Bedrock and its main capabilities. <br> - Study how Amazon Bedrock provides access to Foundation Models. <br> - Learn about Model Inference, Tokens, Context Windows, and Model Parameters. <br> - Research Prompt Engineering and different prompting techniques. <br> - Explore methods for testing and evaluating AI-generated responses. | 03/11/2026 | 03/11/2026 | [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html) <br> [Prompt Engineering](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-prompt-engineering.html) |
| Wednesday | - Study Retrieval-Augmented Generation (RAG) and its role in Generative AI applications. <br> - Research Embeddings and Vector Databases. <br> - Explore Amazon Bedrock Knowledge Bases. <br> - Study document collection, chunking, information retrieval, and response generation. <br> - Analyze the advantages and limitations of RAG-based systems. | 04/11/2026 | 04/11/2026 | [Amazon Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html) |
| Thursday | - Understand AI Agents and Agentic AI. <br> - Explore AI Agent architectures, including LLMs, Tools, Memory, and APIs. <br> - Study Amazon Bedrock Agents and how their components work together. <br> - Research the integration of AI Agents with AWS Lambda and Backend services. <br> - Explore real-world applications of AI Agents. | 05/11/2026 | 05/11/2026 | [Amazon Bedrock Agents](https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html) |
| Friday | - Review Generative AI, Amazon Bedrock, RAG, and AI Agents studied throughout the week. <br> - Compare Generative AI and Agentic AI in terms of operating principles and practical applications. <br> - Research methods for evaluating the quality of language model responses. <br> - Explore challenges in deploying Generative AI applications, including accuracy, latency, security, and cost. <br> - Complete technical notes on Generative AI technologies available on AWS. | 06/11/2026 | 06/11/2026 | [AWS Generative AI](https://aws.amazon.com/generative-ai/) <br> [AWS Documentation](https://docs.aws.amazon.com/) |

### Expected Achievements for Week 5

#### 1. General Knowledge of Generative AI

- Understand the concept of Generative AI and its role in content generation, information processing, and task automation.
- Differentiate between important AI concepts:

  - **Traditional AI:** AI systems designed to perform tasks such as classification, prediction, and recognition.

  - **Generative AI:** AI technology capable of generating new content, including text, images, software code, and other forms of data.

  - **Agentic AI:** An approach to developing AI systems capable of using tools and coordinating multiple processing steps to accomplish tasks.

- Explore common applications of Generative AI:

  - Chatbots and Virtual Assistants.
  - Document Summarization and Text Analysis.
  - Software Development and Coding Assistance.
  - Information Retrieval and Processing.
  - Workflow Automation.

#### 2. Knowledge of Large Language Models and Foundation Models

- Understand Large Language Models (LLMs) and their capabilities in processing, analyzing, and generating natural language.
- Learn fundamental concepts:

  - **Foundation Model:** A model trained on large amounts of data that can be adapted to different tasks.

  - **Large Language Model (LLM):** A large-scale language model capable of processing and generating text.

  - **Token:** A unit of data used by a model when processing input and generating output.

  - **Context Window:** The maximum amount of context a model can process within a single interaction.

  - **Inference:** The process of using a trained model to generate predictions or responses.

- Understand the role of LLMs in Generative AI applications and AI Agents.

#### 3. Knowledge of Amazon Bedrock

- Understand Amazon Bedrock as a managed AWS service that supports the development and scaling of Generative AI applications.
- Explore how Amazon Bedrock provides access to various Foundation Models through supported interfaces and APIs.
- Study important components and capabilities:

  - **Foundation Models:** AI models designed for tasks such as text generation, data analysis, and content processing.

  - **Model Inference:** The process of sending input data to a model and receiving a generated result.

  - **Knowledge Bases:** Support the integration of AI models with external data sources and knowledge repositories.

  - **Agents:** Support the development of AI systems capable of performing tasks and interacting with external tools.

- Recognize the importance of selecting suitable models based on output quality, response time, task compatibility, and cost.

#### 4. Knowledge of Prompt Engineering

- Understand the role of Prompt Engineering in improving the quality of responses generated by language models.
- Study common prompting techniques:

  - **Zero-shot Prompting:** Asking a model to perform a task without providing examples.

  - **Few-shot Prompting:** Providing several examples to guide the model in performing a task.

  - **Role-based Prompting:** Defining a specific role or context for the model.

  - **Structured Prompting:** Designing prompts with clearly defined tasks, input information, and expected output formats.

- Recognize the importance of testing and evaluating model responses instead of relying on a single generated result.

#### 5. Knowledge of Retrieval-Augmented Generation (RAG)

- Understand Retrieval-Augmented Generation (RAG) as an approach that combines information retrieval from external data sources with the response-generation capabilities of language models.
- Study the fundamental components of a RAG system:

  - **Document Processing:** Preparing and processing source documents.

  - **Chunking:** Dividing documents into smaller sections suitable for retrieval.

  - **Embeddings:** Representing data as numerical vectors.

  - **Vector Database:** A system that stores and searches vectors based on similarity.

  - **Retriever:** A component responsible for finding information relevant to a user's query.

  - **LLM:** A language model that uses retrieved information to generate a response.

- Study the basic RAG workflow:

  1. Collect and prepare source data.
  2. Divide documents into smaller chunks.
  3. Convert document content into embeddings.
  4. Store data for efficient retrieval.
  5. Receive a question from the user.
  6. Retrieve relevant information.
  7. Provide retrieved context to the language model.
  8. Generate a response based on the question and retrieved information.

- Understand the advantages and limitations of RAG, particularly its dependence on data quality and retrieval performance.

#### 6. Knowledge of AI Agents and Agentic AI

- Understand the concept of AI Agents and their ability to perform tasks through the use of external tools.
- Explore the common components of an AI Agent architecture:

  - **LLM:** Supports request interpretation, reasoning, and response generation.

  - **Tools:** External capabilities that an AI system is authorized to use when performing tasks.

  - **Memory:** Mechanisms for maintaining information or context when required by an application.

  - **API Integration:** Enables AI systems to communicate with external services and data sources.

  - **Workflow:** Defines how different components coordinate to accomplish a task.

- Study Amazon Bedrock Agents and related components, including Foundation Models, Instructions, Action Groups, and Knowledge Bases.
- Explore the integration of AI Agents with AWS services and Backend applications.
- Recognize the importance of access control, output evaluation, and activity monitoring when developing AI Agent systems.

#### 7. Comparison Between Generative AI and Agentic AI

| Criteria | Generative AI | Agentic AI |
|---|---|---|
| **Primary Objective** | Generate content or responses based on input | Perform tasks through multiple processing steps |
| **Tool Integration** | Depends on application design | Commonly integrates tools and APIs to execute tasks |
| **Operating Mechanism** | Processes requests and generates outputs | May plan, select tools, and coordinate multiple actions |
| **Common Applications** | Chatbots, content generation, text summarization | Automation assistants, workflow processing, system integration |
| **Challenges** | Accuracy, output quality | Action control, security, reliability, and cost |

Through this comparison, I aim to gain a clearer understanding of the differences between traditional Generative AI applications and Agentic AI systems that coordinate multiple tools to accomplish tasks.

#### 8. Knowledge of Generative AI Evaluation and Deployment

- Explore important factors when evaluating Generative AI applications:

  - **Response Quality:** The relevance and usefulness of generated responses.

  - **Accuracy:** The correctness of information produced by the AI model.

  - **Latency:** The time required to process a request and return a response.

  - **Cost:** Expenses associated with model usage and supporting services.

  - **Security:** The protection of sensitive data and control of access permissions.

  - **Reliability:** The ability to maintain stable and consistent system operation.

- Study **Hallucination**, a phenomenon in which AI models generate inaccurate or unsupported information.
- Recognize the importance of testing, response evaluation, and monitoring during AI application development.
- Understand the importance of selecting suitable models, designing effective prompts, and organizing appropriate data sources to improve system quality.

#### 9. Week 5 Summary

The fifth week of the internship focuses on exploring **Generative AI technologies and their applications on Amazon Web Services**.

The main topics include Large Language Models, Foundation Models, Amazon Bedrock, Prompt Engineering, Retrieval-Augmented Generation, and AI Agents.

Through studying these technologies, the objective is to understand how artificial intelligence models can be integrated with data sources, APIs, and external tools to develop intelligent applications.

Additionally, researching techniques such as Prompt Engineering and RAG helps expand knowledge of methods for improving the quality of language model responses.

Exploring Agentic AI also provides a better understanding of how AI systems can coordinate multiple components to perform complex tasks.

Beyond technical knowledge, the week also covers important factors in evaluating and deploying Generative AI applications, including accuracy, response time, security, reliability, and cost.

These topics provide foundational knowledge of Generative AI and AI services on AWS while expanding an understanding of emerging trends in modern artificial intelligence applications.
