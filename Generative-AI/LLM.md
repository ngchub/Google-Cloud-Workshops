# What is Large Language Models?
**Large**, **general-purpose** language models can be **pre-trained** and then **fine-tuned** for spesific purposes.

## Problems could be solved with Large Language Models
  - Text Classification
  - Question answering
  - Document summarization
  - Text generation
    
## What **large** stands for?
  - Large training dataset
  - Large number of parameters

## What **general purpose** stand for?
  - Commonality of human languages
  - Resourse restriction

## What **pre-trained** and **fine-tuned** stand for?
  - **Pre-trained** meaning to pre-train a large language model for a general purpose with a ***large dataset***
  - **Fine-tuned** means fine-tuned it for a spesific aims with a much smaller dataset.

## Benefits of using large language models
  - A single model can be used for different tasks <br/>
    This large language models are trained with petabytes of data and generate billions of parameters are smart enough to solve different tasks, including **language translation**, **sentence completion**, **text classification**, **question answering**, and more.
  - The fine-tuned process requires minimal field data <br/>
    Large language models require minimal field training data when you tailor them to solve your spesific problem. This models obtain decent performance ***even with little domain training data***. They can be used for few shot or even zero-shot scenarios. In ML, **few shot** means to train amodel with minimal data, and **zero shot** omplies that a model can recognize things that have not explicitly been taight in the training before. 
  - The performance is continuously growing with more data and parameters.

## Pathways Language Model (PaLM)
  - Released in April 2022 by Google.<br/>
  - 540 billion-parameter model that achieves a state of art performance across multiple language tasks.
  - Leverages the new Pathway system which has enabled Google to efficiently train a single model across multiple TPU V4 pods.
  - Orchestrates distributed computation for accelerators. 

## Transformer model
![Screenshot from 2023-06-21 14-19-16](https://github.com/nildenist/Generative-AI/assets/28653377/e4b48b9c-e44f-473a-968b-ea09a44e6447)

The encoder encodes the input sequence and passes it to the decoder, which learns how to decode the represantations for a relevant task. 

## Generative Language Models | LaMDA, PaLM, GPT, etc.

![Screenshot from 2023-06-21 14-25-05](https://github.com/nildenist/Generative-AI/assets/28653377/cf768bab-d8cc-4a1c-8751-8ce81aefbb77)

## Compare

| LLM Development <br/> (using pre-trained APIS)  | Traditional ML Development |
| -------- | ------- |
| NO ML expertise needed  | YES ML expertise needed    |
| NO training examples | YES training examples     |
| NO need to train a model    | YES need to train a model    |
| Thinks about prompt design  | YES compute time+hardware  |
|  | Thinks about minimizing a loss function  |

## Use Case

### Question Answering(QA)

![Screenshot from 2023-06-21 14-28-19](https://github.com/nildenist/Generative-AI/assets/28653377/9225fa5c-ea82-4cf7-8f71-5b3662e43d37)

  - QA is a subfield of Natural Language Processing that deals with the task of automatically answering questions posed in natural language.
  - QA models are able to retrieve the answer to a question from a given text. This is useful for searching for an answer in a document. Depending on the model used, the answer can be directly extracted from text or generated from scratch.

The key here is that you need domain knowledge to develop therse question-answering models. 

### Question Answering Required Domain Knowledge
![Screenshot from 2023-06-21 14-29-10](https://github.com/nildenist/Generative-AI/assets/28653377/cab3eec1-4f47-4907-9fc0-41a5c38ce7ba)

### Generative QA 

![Screenshot from 2023-06-21 14-32-34](https://github.com/nildenist/Generative-AI/assets/28653377/ebc4fc1f-85c1-4e9a-af9e-5a757b22f082)

Using Generative QA, the model generates free text directly based on context. There is no need for <ins> domain knowledge. </ins>

### Bard 

Bard is a large language model chat bot developed by Google AI.

![Screenshot from 2023-06-21 15-10-46](https://github.com/nildenist/Generative-AI/assets/28653377/1c3bdb0a-2970-4be2-bb47-9ea32d60fac1)

![Screenshot from 2023-06-21 15-10-57](https://github.com/nildenist/Generative-AI/assets/28653377/95fdaaa4-3a74-4b13-9d5e-2ceb016ad0f8)

![Screenshot from 2023-06-21 15-11-09](https://github.com/nildenist/Generative-AI/assets/28653377/6d351907-d320-4268-9ba9-3595d8b39d09)

In all answers, Bard answers the question, but it added an additional context.
In each of questions, a desired response was obtained. This is due to prompt design.

### Prompt Design

Prompt design is the process of creating prompts that elicit the desired response from a language model. 

Prompt Design adn Prompt Engineering are two closely-related concepts in natural language processing. <br/>
Both involve the process of creating a prompt that is clear, concise, and informative. However, there are some ket differences between the two. 

![Screenshot from 2023-06-21 15-11-24](https://github.com/nildenist/Generative-AI/assets/28653377/13373bc5-8ae4-44b2-ac1e-3c3a05ce9f61)

  - In <ins>prompt design</ins> if hte system is being asked to translate a text from English to French, the prompt should be written in English and should specify that the translation should be a French.
  - It is more generalized concept.
  - It is essential.

  - In <ins>prompt engineering</ins> this is the process of creating a prompt that is designed to improve performance. This may involve domain-spesific knowledge, providing examples of the desired output, or using keywords that are known to be effective for the spesific system.
  - It is more specialized concept.
  - It is only necessary for systems that require a high degree of accuracy or performance.


## Kinds of LLM

![Screenshot from 2023-06-21 16-29-36](https://github.com/nildenist/Generative-AI/assets/28653377/f99d0de5-9d80-4035-914b-845fec2b6e35)

### Generic (or Raw) Language Models 
![Screenshot from 2023-06-21 16-29-45](https://github.com/nildenist/Generative-AI/assets/28653377/b10678d8-6a17-4893-8113-6f97a73783b3)

The next word is a token based on the language in the training data. <br/>
In this example, "the cat sat on," the next word should be "the". As can be seen in the pictore above, "the" is the most likely next word. <br/>

Think of this type as an autocomplete in search.  <br/>


### Instruction Tuned Language Models 

![Screenshot from 2023-06-21 16-30-01](https://github.com/nildenist/Generative-AI/assets/28653377/53569163-ecdb-4699-a6dc-608fc9fea194)

The model is trained to predict a response to the instructions given in the input. 

![Screenshot from 2023-06-21 16-30-29](https://github.com/nildenist/Generative-AI/assets/28653377/e046a9ea-e1b5-47ae-9f6b-de114969e350)

For example, generate a poem in the style of X, give me a list of keywords based on semantic similariy for X.

![Screenshot from 2023-06-21 16-30-37](https://github.com/nildenist/Generative-AI/assets/28653377/5ed9c12e-cc7b-4198-af39-b1546fe98172)

In this example,, classify the text into neutral, negative, or positive. 

### Dialog Tuned Language Models 

![Screenshot from 2023-06-21 16-31-30](https://github.com/nildenist/Generative-AI/assets/28653377/0527fd53-f80e-4824-b191-1b9dc47ebba6)

The model is trained to have a dialogue by the next response. 

![Screenshot from 2023-06-21 16-31-42](https://github.com/nildenist/Generative-AI/assets/28653377/a1c4ee63-2433-47a3-8b07-700c05a4d7f9)

  - Dialog-tuned models are a special case of ***instruction tuned*** models where requests are typically framed as questions to a chat bot.
  - It is expected to be in the context of a longer back and forth conversation, and typically works better with natural question-like phrasings.


## Chain of Thought Reasoning 

![Screenshot from 2023-06-21 16-31-57](https://github.com/nildenist/Generative-AI/assets/28653377/a370cc20-b529-4d61-a453-a645f4c0bd26)

![Screenshot from 2023-06-21 16-32-30](https://github.com/nildenist/Generative-AI/assets/28653377/7d9669c2-fb47-4178-a1a4-f7aa0760014c)

Test-spesific tunning can make LLMs more reliable. <br/>
**VertexAI** provides task-spesific foundation models. 

## Use Case Examples

![Screenshot from 2023-06-21 16-32-38](https://github.com/nildenist/Generative-AI/assets/28653377/3956c50a-1d08-4069-871b-50c70e9dece0)

  - You need to gather sentiments, or <ins>how your customers are feeling about your product or service</ins>.
      - You can use the ***classification task*** sentiment analysis task model.
  - Same to **vision tasks**. If you need to perform occupancy analytics, there is task-spesific model for your use case.


### Tuning

![Screenshot from 2023-06-21 16-32-57](https://github.com/nildenist/Generative-AI/assets/28653377/76921cdf-f001-40a3-9084-d8326e5962d4)

Tuning a model enables you to customize the model reponse based on examples of the task that you want the model to perform. It is essentially the process of adapting a model to a new domain, or set of custom use cases by training the model on new data. <brr/>

For example, we may collect training data and une the model specifically for the legal or mdeical domain.

### Fine Tuning

![Screenshot from 2023-06-21 16-33-07](https://github.com/nildenist/Generative-AI/assets/28653377/2334a941-8bd1-48bf-b611-7f724bdaa09b)

You can also further tune the model by fine tuning  where you bring your own dataset and retrain the model by tuning every weight in the LLM. This requires a big training job and hosting your own fine-tuned model. 

## Medical Domain Use Cases

![Screenshot from 2023-06-21 16-33-16](https://github.com/nildenist/Generative-AI/assets/28653377/03899979-987a-4b67-94dd-a465db025e27)

**Fine tuning** is expensive nd not realistic in many cases. 

![Screenshot from 2023-06-21 16-33-25](https://github.com/nildenist/Generative-AI/assets/28653377/e1f2d23d-a3ac-411e-a445-97f0f224806a)

### More efficient methods of tunung

![Screenshot from 2023-06-21 16-33-32](https://github.com/nildenist/Generative-AI/assets/28653377/f7e22826-77c8-442c-ab74-cd3b5cff112d)


## GenAI Studio

![Screenshot from 2023-06-21 16-33-43](https://github.com/nildenist/Generative-AI/assets/28653377/1d7d47a9-6861-4cfc-af31-4e7d4c2a233b)

  - GeAI Studio lets you quickly explore and customize generative AI models that you can leverage in your applications on Google Cloud.
  - GenAI Studio helps developers create and deploy Generative AI models by providing a variety tools and resources that make it easy to get started. For example,
      - there is library of pre-trained models,
      - a tool for fine tuning models,
      - a tool for deploying models to production,
      - and a community forum for developers to share ideas and collaborate.

## GenAI App Builder

![Screenshot from 2023-06-21 16-34-04](https://github.com/nildenist/Generative-AI/assets/28653377/696be576-b93f-4127-b5e7-bd7d44f109c3)

It has a drag-and-drop interface that makes it easy to design and build apps, a visual editor that makes it easy to create and edit app content, a built-in search engine that allows users to search for information within the app and a conversational AI engine that allows user to interact with the app using natural language. You can create your own
  - chat bots,
  - digital assistants,
  - custom search engines,
  - knowledge bases,
  - training applications,
  - and more.


## PaLM API

![Screenshot from 2023-06-21 16-34-29](https://github.com/nildenist/Generative-AI/assets/28653377/780e2f23-8de5-4575-aa4c-a054b5e4a3de)

Lets you test and experiment with Google's large language models and GenAI tools. <br/>
To make prototyping quick and more accessible, developers can integrate PaLM API with **MakerSuite** and use it to accesss the API using a graphical user interface. **MakerSuite** includes a number of different tools such as 
  - model-training tool,
      -Helps developers train ML models on their data using different algorthms.
  - model-deployment tool,
      - Helps developers deploy ML models to production with  a number of different deployment options. 
  - model-monitoring tool.
      - Helps developers monitor the performance of their ML models in production using a dashboard and a number of different metrics. 

# Introduction to Large Language Models: Quiz

<h3> Question 1. What are some of the applications of LLMs? </h3>

- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete probabilities, classes, and predictions.<br/>
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating creative content.<br/>
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete predictions. <br/>
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete classes. <br/>
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete probabilities. <br/>
</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
   
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete probabilities, classes, and predictions.<br/>
- [x] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating creative content.<br/>
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete predictions. <br/>
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete classes. <br/>
- [ ] LLMs can be used for many tasks, including: <br/>
      1.Writing<br/>
      2.Translating<br/>
      3.Coding<br/>
      4.Answering questions<br/>
      5.Summarizing text<br/>
      6.Generating non-creative discrete probabilities. <br/>

 </b>
</div>
</details>


<h3> Question 2. What are some of the benefits of using large language models (LLMs)? </h3>

- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate non-probabilities and human-quality text.<br/>
      2.They can be used for many tasks, such as text summarization and code generation.<br/>
      3.They can be trained on massive datasets of text, image, and code.<br/>
      4.They are constantly improving.<br/>
- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate discrete classes and human-quality text.<br/>
      2.They can be used for many tasks, such as text summarization and code generation.<br/>
      3.They can be trained on massive datasets of text and code.<br/>
      4.They are constantly improving.<br/>
- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate human-quality text.<br/>
      2.They can be used for a variety of tasks.<br/>
      3.They can be trained on massive datasets of text and code.<br/>
      4.They are constantly improved.<br/>
- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate human-quality text. <br/>
      2.They can be used for many tasks, such as text summarization and code generation. <br/>
      3.They can be trained on massive datasets of text, images, and code. <br/>
      4.They are constantly improving. <br/>
- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate probabilities and human-quality text.<br/>
      2.They can be used for many tasks, such as text summarization and code generation.<br/>
      3.They can be trained on massive datasets of text and code.<br/>
      4.They are constantly being improved.<br/>
</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
   

- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate non-probabilities and human-quality text.<br/>
      2.They can be used for many tasks, such as text summarization and code generation.<br/>
      3.They can be trained on massive datasets of text, image, and code.<br/>
      4.They are constantly improving.<br/>
- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate discrete classes and human-quality text.<br/>
      2.They can be used for many tasks, such as text summarization and code generation.<br/>
      3.They can be trained on massive datasets of text and code.<br/>
      4.They are constantly improving.<br/>
- [x] LLMs have a number of benefits, including: <br/>
      1.They can generate human-quality text.<br/>
      2.They can be used for a variety of tasks.<br/>
      3.They can be trained on massive datasets of text and code.<br/>
      4.They are constantly improved.<br/>
- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate human-quality text. <br/>
      2.They can be used for many tasks, such as text summarization and code generation. <br/>
      3.They can be trained on massive datasets of text, images, and code. <br/>
      4.They are constantly improving. <br/>
- [ ] LLMs have a number of benefits, including: <br/>
      1.They can generate probabilities and human-quality text.<br/>
      2.They can be used for many tasks, such as text summarization and code generation.<br/>
      3.They can be trained on massive datasets of text and code.<br/>
      4.They are constantly being improved.<br/>

 </b>
</div>
</details>


<h3> Question 3. What are large language models (LLMs)?: </h3>

- [ ] Generative AI is a type of artificial intelligence (AI) that only can create new content, such as text, images, audio, and video by learning from new data and then using that knowledge to predict a discrete, supervised learning output.
- [ ] An LLM is a type of artificial intelligence (AI) that can generate human-quality text. LLMs are trained on massive datasets of text and code, and they can be used for many tasks, such as writing, translating, and coding.
- [ ] Generative AI is a type of artificial intelligence (AI) that can create new content, such as discrete numbers, classes, and probabilities. It does this by learning from existing data and then using that knowledge to generate new and unique outputs.
- [ ] Generative AI is a type of artificial intelligence (AI) that only can create new content, such as text, images, audio, and video by learning from new data and then using that knowledge to predict a classification output.

</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
  
- [ ] Generative AI is a type of artificial intelligence (AI) that only can create new content, such as text, images, audio, and video by learning from new data and then using that knowledge to predict a discrete, supervised learning output.
- [x] An LLM is a type of artificial intelligence (AI) that can generate human-quality text. LLMs are trained on massive datasets of text and code, and they can be used for many tasks, such as writing, translating, and coding.
- [ ] Generative AI is a type of artificial intelligence (AI) that can create new content, such as discrete numbers, classes, and probabilities. It does this by learning from existing data and then using that knowledge to generate new and unique outputs.
- [ ] Generative AI is a type of artificial intelligence (AI) that only can create new content, such as text, images, audio, and video by learning from new data and then using that knowledge to predict a classification output.

 </b>
</div>
</details>

<h3> Question 4. What are some of the challenges of using LLMs? Select three options. </h3>

- [ ] They can be biased.
- [ ] After being developed, they only change when they are fed new data.
- [ ] They can be used to generate harmful content.
- [ ] They can be expensive to train.

</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
  
- [x] They can be biased.
- [ ] After being developed, they only change when they are fed new data.
- [x] They can be used to generate harmful content.
- [x] They can be expensive to train.

 </b>
</div>
</details>



