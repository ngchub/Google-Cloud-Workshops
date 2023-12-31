# Vertex AI Search

This introduction is intended for developers that have some coding experience you'll be referencing examples of how to use the api's and sdks to access Vertex AI search.

![chrome-capture-2023-9-26](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/546248b5-60cf-4a73-8eb6-766ea2d7165f)

   - You'll learn about the different generative AI product offerings in Google Cloud
   - You'll explore several use cases where Vertex AI search can provide better search and recommendation experiences and then gain a better understanding of the Vertex AI search product architecture and how to configure the product to be secure accessible and cost effective
   - You'll also learn to index several data sources in the search engine display only information of interest in your search results integrate Vertex AI search into your applications and understand product usage through analytics and metrics
   - 
![chrome-capture-2023-9-26 (1)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/9868829c-0d6f-45b1-8d17-3f2e473351be)

## What is the difference of Gen AI?

Machine learning or predictive AI are the most classical models which are trained on historical data to classify or make predictions on similar data for example you would train a vision model to identify whether the animal is a cat by providing a data set of images labeled as cats or other animals then when you provide a new image the predictive model will be able to tell you whether it is a cat.

![chrome-capture-2023-9-26 (2)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/62dc2230-aea4-4976-bbd0-fbe57ef04cfe)


**Generative AI** is the new paradigm which creates new data based on the patterns it has learned from training data training data is general and not specific to a particular task it can come in several formats of unlabeled data such as images text oraudio in the pre-training stage large General data sets are used later smaller and more specific data sets are used to fine-tune the model once the model is trained it can generate new unique data that it has not seen before.

## Why Google Cloud?

![chrome-capture-2023-9-26 (3)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/798cc1cc-49d7-4e3d-9057-2ac4443fcc62)

**Competitive Advantage**: Google Cloud products Empower Enterprises to embrace the generative AI with the confidence that there's data governance built in this is especially important in highly regulated Industries like financial services and Healthcare. You need a guarantee that no one can see the questions your users are asking or the training data that provides your unique competitive advantage. <br/>
**Match Cost to Value**:Google Cloud doesn't believe that one model fits all in fact bigger is not better especially from a cost of inference perspective large 300 billion parameter models can cost as much as one thousand dollars per user per year to run which adds up to one billion dollars for 1 million users. You shouldn't need to use a public model that has to search through the player rosters in every world cup or the inspiration for every Taylor Swift song in order to answer a question like when can I withdraw from my retirement account instead Google Cloud provides match to cost value that gives you the ability to choose the right model for the right job. <br/>
**Grounded in facility**: In the Enterprise it's important not just to provide an answer but to prove where the answer came from and what information was used to create the answer this process ensures that your results are grounded in factuality. Enterprise customers have built stores of knowledge and data warehouses filled with facts they also integrate many third-party data sources with highly curated facts. <br/>
**Easy to get started**: Google Cloud provides a wide range of easy to use tools including out of the box search in conversation and quick access apis this helps you to get started in days rather than requiring you to learn the Deep mathematics and generative AI or tune a model to every possible question that could be asked.<br/>
**Manageable at scale**: Enterprises will need to manage many models user interfaces data corpora and Integrations with first and third-party data sources Google Cloud provides a manageable at scale platform that integrates into your existing user security data management and entitlements workflow. <br/>

## Google Cloud's approach to Responsible AI

   - Generative AI comes with its own set of unique challenges.
   - Google is integrating AI into its products boldly and with a deep sense of responsibility the highest standards of information.
   - Integrity with it's AI principles this includes education research and tools including online training courses, guidebooks, research papers and our product documentation.
   - There are also product and use case reviews such as customer AI use case reviews product development reviews and fairness testing additionally there are highly relevant responsible AI resources and tooling for new generative AI offerings.
   - These are being rapidly developed and will be coming soon in continuous development are governance and Assurance tooling to support the responsible development and implementation of AI in 2022 the Vertex ai explainable ai offerings were expanded to include new features as part of model evaluation model monitoring and model registry to support data and model governance this is in addition to Google's open source responsible AI toolkit that's available to Google Cloud customers for their projects and anyone with an AI project at no cost

![chrome-capture-2023-9-26 (4)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/4eaab27a-2f5f-4ba0-8e8a-54a401505969)

## Generative AI building blocks

Google Cloud brings generative AI to organizations by uniting Foundation models with Vertex AI search and conversation together they help you build transformative applications powered by your data.

These are the fundamental building blocks of generative AI.

![chrome-capture-2023-9-26 (5)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/b1f33349-39b7-4de4-9c35-886dae946216)

A foundation model is any model that is trained on a broad variety of data at scale and can be adapted to a wide range of Downstream tasks and applications either by fine-tuning or using in context learning these models are the basis of many generative AI products. 

**Vertex AI conversation** is a type of artificial intelligence that can simulate human conversation it's made possible by natural language processing a field of AI that allows computers to understand and process human language with Vertex AI conversation. You can answer complex questions out of the box and easily add transactional capabilities such as multi-turn conversations that build upon context and completing API transactions. 

**Vertex AI search** is an offering from Google Cloud that lets organizations quickly build generative AI powered search engines for customers and employees. Vertex AI search enables you to get quality results out of the box and you can easily customize these results according to your business needs such as responding to single independent queries with a lot of results and fine-grained control over results ranking 

It's important to distinguish between the main Vertex AI Enterprise Products. 

![chrome-capture-2023-9-26 (6)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/2a85b6b2-cd93-490c-9de9-77e6e36ca5ef)

**Vertex AI** is an end-to-end machine learning platform that allows you to serve and tune Foundation models to meet your customers specific needs and **Vertex AI Searching&Conversation** which enables fast application development leveraging the power of search immersive conversational experiences and Foundation models with Enterprise controls. 

There are a variety of opportunities across internal and external use cases addressing the needs of customers staff and machines. You can build generative AI experiences for external users on your websites or internal Enterprise or technical applications.

![chrome-capture-2023-9-26 (7)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/ce866d36-c536-48c9-8d0c-2646304c7fe7)

**External use cases** that are scoped around servicing customers external to the Enterprise for example e-commerce media serving and customer service support. <br/>
**Functional use cases** that are scoped around servicing internal applications and vertical Solutions typically around knowledge workers such as knowledge bases document repositories and intranets.  <br/>
**Technical use cases** that are scoped around servicing machine generated data and systems automation including infrastructure logging and debugging reports with Google Cloud's generative AI platforms powered by large language models. <br/>

Developers are enabled to build immersive experiences with Vertex AI search and conversation built into your applications transform the consumer search experience into an intuitive natural language experience that Delights your customers and drives conversion









