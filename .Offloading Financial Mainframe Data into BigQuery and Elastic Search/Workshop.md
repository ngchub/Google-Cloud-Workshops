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
