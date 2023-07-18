This lab was developed with one of the Google partner, Elastic.

# Overview

Financial institutions have vast amounts of data about their customers. However, many of them struggle to leverage data to their advantage. Data may be sitting in silos or trapped on costly mainframes. Customers may only have access to a limited quantity of data, or service providers may need to search through multiple systems of record to handle a simple customer inquiry. This creates a hazard for providers and a headache for customers.

Elastic and Google Cloud enable institutions to manage this information. Powerful search tools allow data to be surfaced faster than ever - Whether it's card payments, ACH (Automated Clearing House), wires, bank transfers, real-time payments, or another payment method. This information can be correlated to customer profiles, cash balances, merchant info, purchase history, and other relevant information to enable the customer or business objective.

In this hands-on lab, you'll import synthetic data representing financial records offloaded from a bank's mainframe into BigQuery. You'll then explore it using SQL, then create a Dataflow job to process and ingest a subset of that data into Elastic Search. Finally, you'll create a dashboard in Elastic's Kibana tool to gain a 360 degree view of a customer's financial history.

# Objectives
  - Importing mainframe data into BigQuery and exploring it using SQL
  - Get an Elastic Trial and deploy an Elastic Cluster on Google Cloud
  - Creating a Dataflow job from an Elastic template
  - Running and monitoring a Dataflow job's progress
  - Inspecting datasets in Elastic with Kibana
  - Building a dashboard to visualize the mainframe data


# Requirements

## Activate Cloud Shell

![Screenshot from 2023-07-18 16-04-58](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/0178e924-d639-4af0-a70d-82404a19f924)

```console
gcloud auth list
```

![Screenshot from 2023-07-18 16-05-48](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/043e1cb9-ab8d-4933-9c43-4c1b0f07a58e)

```console
gcloud config list project
```

![Screenshot from 2023-07-18 16-06-59](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/59e99715-a906-4dbc-a424-fac78cb1ae19)

**Note:** Note: For full documentation of gcloud, in Google Cloud, refer to the [gcloud CLI](https://cloud.google.com/sdk/gcloud) overview guide.


# Task 1. Elastic - Set up trial account

1. Sign up for a [free trial](https://www.elastic.co/cloud/elasticsearch-service/signup?utm_source=referral&utm_medium=qwiklabs&utm_campaign=cloud-trial-subscription-pm&utm_id=701610000005lJVAAY)
    - Click Start free trial.

    ![IeW2Zl90CIA6Qzzulrw71VTTVbQBLBY3NMEnUV2mea4=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/fa612e1b-0dc7-40fb-9452-1b790bdfbadd)

2. Sign up using your personal email and a unique password. Do NOT click the "sign up with Google" button:
   ![oWpnHe1VmNca198Osvo+QzCKrRRSitdAmCTo3wQXEK8=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/c2915c58-8407-441c-98d6-c9940e749525)

**Note**: You must use your personal email, not your student account, don't attempt to sign up with google, unless you sign out of your lab account first. If you attempt to sign up with your student id, your trial will be rejected or canceled.

3. Enter some details about yourself
   ![Screenshot from 2023-07-18 16-34-01](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/77b5717c-ab06-4874-a00d-9cbfa8453ce1)

4. Create a simple deployment of Elastic Search
   ![Screenshot from 2023-07-18 16-34-50](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/59ee54fb-967e-484e-8f46-12816aef43f0)

5. Save your deployment credentials, you may need it later
   ![Screenshot from 2023-07-18 16-35-59](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/29075468-7639-46d2-95b2-f71d382056ec)

6. Click "**continue**" to go to your elastic deployment
   ![Screenshot from 2023-07-18 16-36-43](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/68b18e15-9f13-4cec-92c8-a0b739aaf87b)

7. Click the hamburger menu (1) and then click "Stack Management".
   ![Screenshot from 2023-07-18 16-37-16](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/022ce021-9a4d-4ef4-ac8f-3f3ea9c90627)

8. On the right side of the page, select "**API keys**"
   ![Screenshot from 2023-07-18 16-37-57](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/5d095f7a-4da5-4000-ba6b-b23b789cbe98)

9. Create a new **API Key**
    
11. Name your key "**bigquery-import**" and select "**Create API Key**" to generate a new key
    
13. Save your new API key for later.
    ![Screenshot from 2023-07-18 16-39-09](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/7581c733-8027-4231-b8ac-9b7f1db2a512)
    
12.From the hamburger menu on the left. Click "**Manage this deployment**"
    ![Screenshot from 2023-07-18 16-40-11](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/8147494d-baa3-4f24-81bf-779bf498a7e5)

13.Click the **Gear** icon in the "Manage Deployment" column:
   ![Screenshot from 2023-07-18 16-40-51](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/6731d37d-8bb0-4e09-89f4-9df8b1d21848)

14. Copy the Cloud ID to your clipboard and save it for later:
   ![Screenshot from 2023-07-18 16-41-30](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/c59169ec-412f-4e7c-bbab-98c1f726ddcc)

Note: Hold onto the CloudID and API key, you will need them later when you load data from Bigquery into Elastic.

# Task 2. Create a Cloud Storage Bucket


