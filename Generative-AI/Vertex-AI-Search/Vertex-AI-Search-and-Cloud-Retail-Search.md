# Vertex AI Search vs. Cloud Retail Search

This ReadMe shows you to whether to use vertex AI search or Cloud Retail Search in your solution.

With access to Google Cloud's no code conversational and search tools powered by Foundation models organizations can get started with a few clicks. They can quickly build high quality experiences that can be integrated into their applications and websites.


There are three key elements to Vertex AI Search and Conversation:

![Screenshot from 2023-10-31 14-03-22](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/f6d83a2b-2bec-483b-89fc-e469630e506d)



**Vertex AI Search** where you can build a Google quality search engine on your own data and embed a search bar in your web page or application.

**Personalized** self-service customer experiences such as building a state-of-the-art ***recommendation engine*** on your own data that can suggest content similar to the content that the user is currently viewing.

***Generative AI agents*** which complements Dialogflow CX with an ***LLM*** based chat bot trained on links or documents so that your end users can have conversations about the content.

Let's explore Vertex AI Search in a little more detail.

There are two key components to Vertex AI Search:

![two_platforms_of _search](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/78b68df4-e99a-4b9b-8cd6-a0104b581e66)


***Vertex AI Search Platform*** and ***Cloud Retail Search*** 

![chrome-capture-2023-9-31](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/7a228257-0d1a-4209-b263-88fec50e8075)

**Vertex AI Search** is a horizontal search platform that is not industry specific. It's used to build an AI enabled search capability and embedded vertical solution.

Developers and data scientists from a wide range of Industries have started to use vertex AI search.

For use cases such as medical records history artifact search customer support and manufacturing inventory search. 

Vertex AI search helps deliver more relevant results than traditional keyword-based search techniques by using natural language processing and machine learning techniques.

This allows Vertex AI Search to infer relationships within the content and the intent of the user's query input. 

Vertex AI Search is something you can build on top of however it's not going to have the retail specific tuning. 


That's where Cloud Retail Search comes into play.

**Cloud Retail Search** can be considered a vertical specific pre-tuned instance of the Vertex AI Search Platform. It's industry specific for e-commerce and external catalog Services optimized for e-commerce transactions.

![cloud_retail_Search](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/f9d8d490-6191-4be6-b5bc-7a4c9f8938f7)

Suppose you're an e-commerce business looking to use a fully managed service to increase the performance of the revenue per visit of your digital properties. In that case Cloud Retail Search is the right choice. Cloud Retail Search is an industry solution for retailers and e-commerce. Providing personalized product search browsing and recommendations. <ins>It's tuned for retail through large language models</ins> which means it's not tuned for clicks or conversion prediction but rather **Revenue** prediction with access to Google shopping data. The time to value for Cloud Retail Search is as fast as 6 to 12 months. Also because they are complementary products, customers that upgrade to Vertex AI search enhance their benefits from Cloud Retail Search. 

Some important details to ask when trying to decide between **Vertex AI Search** and **Cloud Retail Search**:


![selection_criteria](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/e6bbdf69-f670-4d3f-9377-4acdf060265b)


  - Are y0u earning revenue online?
  - Are you selling products?
  - Does each product have its own price?
  - Does your data fit the retail product catalog schema?
  - Are you interested in optimizing for profit and loss?

Another factor that can affect your decision is your team's application development and AI skills.

![personas](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/4c785608-9f26-42c9-b224-9874171d07cd)

Google Cloud's out-of-the-box search products are fast and easy to set up even if your application developers have no machine learning experience. 
To develop a customized or tuned search product your developers should have a firm understanding of machine learning and to create a fully custom-built search product you'll require AI practitioners with Advanced machine learning abilities in model training and tuning. 

It's important to know that tunable search and build your own search are future capabilities of the product still in development and will be available soon.


Let's practice our knowledge for Vertex AI Search&Conversation:

<h3> Question 1.What features are available as part of Vertex AI Search and Conversation? </h3>

- [ ] Vertex AI Search, Personalize, Dialogflow Agents <br/>
- [ ] Vertex AI Search, Coding, Personalize <br/>
- [ ] Vertex AI Search, Image Generation, Conversational AI <br/>

</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
   
- [x] Vertex AI Search, Personalize, Dialogflow Agents <br/>
- [ ] Vertex AI Search, Coding, Personalize <br/>
- [ ] Vertex AI Search, Image Generation, Conversational AI <br/>

 </b>
</div>
</details>


<h3> Question 2. What product should an enterprise use if they don’t have any ML expertise? (Select all that apply) </h3>

- [ ] MakerSuite <br/>
- [ ] Vertex AI <br/>
- [ ] Vertex AI Search and Conversation <br/>
- [ ] Bard <br/>
</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
   
- [ ] MakerSuite <br/>
- [x] Vertex AI <br/>
- [x] Vertex AI Search and Conversation <br/>
- [ ] Bard <br/>

 </b>
</div>
</details>


<h3> Question 3. Why would you choose Google Cloud instead of the competition for Generative AI applications? </h3>

- [ ] You can learn from other customers data
- [ ] You can create enterprise-scale Generative AI applications
- [ ] All of the options are correct
- [ ] You don’t have to worry about where the answer came from

</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
  
- [ ] You can learn from other customers data
- [x] You can create enterprise-scale Generative AI applications
- [ ] All of the options are correct
- [ ] You don’t have to worry about where the answer came from


 </b>
</div>
</details>

<h3> Question 4. What tool should you use to provide search functionality in your financial services product? </h3>

- [ ] Cloud Retail Search
- [ ] Google Cloud Search
- [ ] Vertex AI Search

</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
  
- [ ] Cloud Retail Search
- [ ] Google Cloud Search
- [x] Vertex AI Search
 </b>
</div>
</details>

<h3> Question 5. What product should you use for your enterprise use cases? (Select all that apply) </h3>

- [ ] MakerSuite + Vertex AI Search and Conversation
- [ ] Bard + MakerSuite
- [ ] Bard + Vertex AI
- [ ] Vertex AI + Vertex AI Search and Conversation

</div>

<details>
  <summary><b>Click here for the answer</b></summary>
<br>
<div id="q79" class="collapse">
  
- [ ] MakerSuite + Vertex AI Search and Conversation
- [ ] Bard + MakerSuite
- [ ] Bard + Vertex AI
- [x] Vertex AI + Vertex AI Search and Conversation

 </b>
</div>
</details>









