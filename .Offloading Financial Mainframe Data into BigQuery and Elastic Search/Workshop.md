This workshop was developed with one of the Google partner, Elastic.
#### $\textcolor{red}{\textsf{This workshop is paid.}}$  
For Google funds and pricing, you can reach us at support@ngc.com.tr and get detailed information.

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

**Note**: You must use your personal email, not your student account, don't attempt to sign up with google, unless you sign out of your lab account first. If you attempt to sign up with your student id, your trial will be rejected or canceled.  <br/>

3. Enter some details about yourself <br/>
   ![Screenshot from 2023-07-18 16-34-01](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/77b5717c-ab06-4874-a00d-9cbfa8453ce1)

4. Create a simple deployment of Elastic Search  <br/>
   ![Screenshot from 2023-07-18 16-34-50](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/59ee54fb-967e-484e-8f46-12816aef43f0)

5. Save your deployment credentials, you may need it later
   ![Screenshot from 2023-07-18 16-35-59](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/29075468-7639-46d2-95b2-f71d382056ec)

6. Click "**continue**" to go to your elastic deployment
   ![Screenshot from 2023-07-18 16-36-43](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/68b18e15-9f13-4cec-92c8-a0b739aaf87b)

7. Click the hamburger menu (1) and then click "Stack Management".
   ![Screenshot from 2023-07-18 16-37-16](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/022ce021-9a4d-4ef4-ac8f-3f3ea9c90627)

8. On the right side of the page, select "**API keys**"
   ![Screenshot from 2023-07-18 16-37-57](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/5d095f7a-4da5-4000-ba6b-b23b789cbe98)

9. Create a new **API Key**  <br/>
    
10. Name your key "**bigquery-import**" and select "**Create API Key**" to generate a new key  <br/>
    
11. Save your new API key for later.  <br/>
    ![Screenshot from 2023-07-18 16-39-09](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/7581c733-8027-4231-b8ac-9b7f1db2a512)
    
12.From the hamburger menu on the left. Click "**Manage this deployment**"
    ![Screenshot from 2023-07-18 16-40-11](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/8147494d-baa3-4f24-81bf-779bf498a7e5)

13.Click the **Gear** icon in the "Manage Deployment" column:
   ![Screenshot from 2023-07-18 16-40-51](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/6731d37d-8bb0-4e09-89f4-9df8b1d21848)

14. Copy the Cloud ID to your clipboard and save it for later:
   ![Screenshot from 2023-07-18 16-41-30](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/c59169ec-412f-4e7c-bbab-98c1f726ddcc)

Note: Hold onto the CloudID and API key, you will need them later when you load data from Bigquery into Elastic.  <br/>

# Task 2. Create a Cloud Storage Bucket

1. Paste the below code into the Cloud Shell to create a new bucket and copy data from an existing bucket
```console
export GOOGLE_CLOUD_PROJECT=<Your Project-Id>
```

Note: Please replace <Your Project-Id> with the project id.

```console
gsutil mb gs://$GOOGLE_CLOUD_PROJECT
gsutil cp -r gs://spls/gsp1153/* gs://$GOOGLE_CLOUD_PROJECT
```

2. Go to the bucket you created and confirm that data was copied over. This should look similar to the image below:
   ![ke8PYTIHiNBZ6V9aPkSnp6+FzDROTfWvB07CCxR5Z2c=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/fcc872d4-734b-4248-8051-d52a5e2d2c2e)

# Task 3. Create a BigQuery dataset and import data from Cloud Storage

1. Create a BigQuery dataset by pasting the below commands into the Cloud Shell:

```console
bq --location=us mk --dataset mainframe_import
```

This command creates a BigQuery dataset in the US called "mainframe_import". You should see a result that looks like this:
![edlQlbR2O1g9dB4G9umbrYWfwWE_O0tibfpzvChEhxA=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/bb0166dc-5b5a-4679-b1ec-edd29cd41fe0)

2. Download the schemas and create two BigQuery tables in the dataset with data from Cloud Storage running the below code sequentially

```console
gsutil cp gs://$GOOGLE_CLOUD_PROJECT/schema_*.json .
```

```console
bq load --source_format=NEWLINE_DELIMITED_JSON     mainframe_import.accounts gs://$GOOGLE_CLOUD_PROJECT/accounts.json schema_accounts.json
```

```console
bq load --source_format=NEWLINE_DELIMITED_JSON     mainframe_import.transactions  gs://$GOOGLE_CLOUD_PROJECT/transactions.json schema_transactions.json
```

3. Navigate to BigQuery using the Search bar or Navigation Menu on the left hand side.

4. Click the drop down arrow under your project to view your dataset and table.

There should be two tables in your BigQuery dataset: ‘accounts' and ‘transactions'

table 1: Accounts
![rNwYRSsvIrZway0485LyBhMqEEePPkzpXmavMRvVqjs=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/58d8a67d-e898-4b91-b927-dd1677c00b48)

table 2: Transactions
![y5e_9zjRgIHblMpC06hfZ0BAgD_QmhJTav2xlJ6mNcU=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/6dd5f474-3419-4271-ad1c-8e5a7ebaecd7)

Note: this is a small data set of simulated financial data, it doesn't represent real accounts or financial transactions.

5. Join the tables into a BigQuery view by pasting the below code into the Cloud Shell

```console
bq query --use_legacy_sql=false \
"CREATE OR REPLACE VIEW $GOOGLE_CLOUD_PROJECT.mainframe_import.account_transactions AS (
  SELECT t.*, a.* EXCEPT (id)
  FROM $GOOGLE_CLOUD_PROJECT.mainframe_import.accounts AS a,
    $GOOGLE_CLOUD_PROJECT.mainframe_import.transactions AS t
  WHERE a.id = t.account_id
)"
```

You should see a message similar to the one below with current status ‘DONE'
![dX9_u7Y+qaGjYOTonZ2RCl+TFowF9xeTVnKtcuZnVe8=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/c71a4dce-6626-4770-b154-58d9d897ac8b)

In the BigQuery console, you should see two tables and a view:
![1tsE3f47pbkqPZZTLsXvx2gtEZkTS2+BVF7DzHAjFIw=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/b085dc72-ba7d-4a99-a18a-bdb9b4f745b1)

# Task 4. Explore the mainframe data in BigQuery

1. Go to **BigQuery** → **mainframe_import** → **transactions**

2. Explore the newly imported data.

3. If you go to "Schema" you can see the table's schema

4. "Details" provides metadata on the table, including creation time, data location, size (on disk) and number of rows.

5. "Preview" provides a snapshot of the data
<img width="337" alt="0aiqGVydr7mhzycad86faUeaCZ6sE7kSHa1rTo+mbbs=" src="https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/9ad9d755-caad-4eb7-89b3-05ab6b43f0f6">

6. Run the below query to select the first 100 rows of data in the table

```console
SELECT * FROM `mainframe_import.transactions` LIMIT 100
```
7. Explore the data more by seeing how many unique occupations are in the accounts dataset. Copy the code below to count the distinct number of occupations

```console
SELECT DISTINCT(occupation), COUNT(occupation)
FROM `mainframe_import.accounts`
GROUP BY occupation
```

8. Explore the salary range column. Start by querying the highest salary range

```console
SELECT * FROM `mainframe_import.accounts` WHERE salary_range = "110,000+" ORDER BY name
```
One hypothesis a Data Analyst might make is that there is a correlation between salary range and age (although other factors such as Occupation will most likely influence this). <br/>
  - See if you can prove or disprove this. Hint: Only select the columns you need (occupation, salary_range and age_range)


# Task 5. Create a Dataflow job reading from BQ and pushing to Elastic

1. The Dataflow API should already be enabled, if not find it using the search bar

2. Paste the below code into the Cloud Shell to create a Dataflow job, making edits to the parts in ```<< >>``` for ```CONNECTION_URL``` and ```API_KEY```. This job will read data from your BigQuery dataset and push it to Elastic

```console
# enter these values by hand into the cloud shell (one by one). 
export CONNECTION_URL=<< your cloud ID from step 1.13 >>
export API_KEY=<< your API key from step 1.10 >>
# to create and run a dataflow job, 
# cut and paste the following 7 lines into the cloud shell.
gcloud dataflow flex-template run bqtoelastic-`date +%s` --template-file-gcs-location gs://dataflow-templates-us-central1/latest/flex/BigQuery_to_Elasticsearch --region us-central1 --num-workers 1 --parameters index=transactions,maxNumWorkers=1,query="select * from $GOOGLE_CLOUD_PROJECT.mainframe_import.account_transactions",connectionUrl=$CONNECTION_URL,apiKey=$API_KEY
```

This should generate a message similar to the one below

![VWIQC6xzJzgf412MwvsF9jte70x+zub4dWGxIGrrwIc=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/c106a7d1-c066-4839-b01f-10fd00e8b05c)

3. Go to **Dataflow** → **Jobs** to make sure you job is running
4. 
![+ENDmiSgQjcmTRekOmN9pu1qIPwZSyRXjmDW3kKV7pE=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/0c49c7dc-2308-47e6-b0ad-7e9082ebea33)

# Task 6. Explore the data in Elastic

1. Go back to the Elastic Cloud

2. Go to **Discover**
   ![5BLPCTBiu6ie3zwxKe5j4uaAeLoL85Yo+vlo5DIBTLs=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/fc607e4a-3973-4e04-bf68-8ef54e7a94c9)

3. Click ‘**Create a data view**'
![SdtMHY+oXzoapHVbRbqNa8QqvpHhcY2pJVH32VopuzM=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/0dc9de72-fd3c-4d7b-9da5-81821036d920)

4. Include the Name, Index pattern and select timestamp from the Timestamp field dropdown. Then click "**Save data view to Kibana**"
   <img width="721" alt="i5mvnLfPh3XELKf9bnmPXPraG4HmLoTUFkUUgY9VSeQ=" src="https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/3d13a32c-f53b-44d3-acb3-00b244a1602a">

5. In order to see the sample dataset, set the date range from Jan 3, 2020 to Jan 12, 2020
   ![1WLkcBs5fL0qwk4GrmoHSAgsZR1fmSzpSCiKJS7pAhc=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/73855494-4b24-4606-be17-0064a4a1471c)

6. Expand one of the transactions to see the fields you have to work with
   ![FW1hPgY3BWgPGnTsoZeE+BBIQR6tR+uecVgn2nAioCc=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/49c217a9-f275-4d73-a9c5-d8dccfb6de95)
   ![LlIScvfu4HaYj0k0TDFzIZlPWmFVlVkzISzze0LuGxI=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/48df6680-f215-4ef6-9015-c594a288ac41)

# Task 7. Create a simple dashboard
1. Select the Analytics "**Dashboard**" from the left Menu and then select "**Create a dashboard**"
   <img width="530" alt="TYQW5e71llRm6WnX+HXD36VEnpbmqR+1lQnaKKmkg2U=" src="https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/f0ca4623-ead1-48bd-9b1f-946be1cdfd5c">

2. Click "Create visualization" and then drag and drop the field "Records" onto the visualization canvas
   ![0P41PXMebMPgklS+544r9EtJvIIWLPFuDKmPFPVU5yE=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/7bb54f44-99e6-497f-b15e-33d353bd6922)

3. Click "**Save and Return**" to save the visualization and return to the dashboard. Grab the lower right corner of the visualization and resize it to look something like this
   ![Z17YbH4C2gWHpCMoE0O1QbkNi0h3x1Jk9ReSLXCXDYI=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/b723e46f-d5ae-4164-9aba-ccf0181da024)

This bar chart displays the number of transactions that occurred over the time frame. It will also make it easy for the user to zoom in to a specific day or hour that they are interested in. <br/>

4. Click "**Create visualization**" to add another visualization to the dashboard, again drag and drop the field "**Records**" onto the canvas. Change the visualization type to "**Legacy Metric**". Click "**Save and return**" to save the visualization and return to the Dashboard.
<img width="486" alt="STvBbWtTtAF5UX5X2vB2MElaVQOUNPJSN60FNbkK3PE=" src="https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/b1fba5d9-cdb7-428f-9309-8744336df135">

5. Resize and rearrange to visualizations to look something like this:
   ![ISjLxdpeLmIMA46Ig9_9mXqA1fKiZBRBMtkPYSwudDw=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/f7ec3ed2-4c4a-44bf-8075-faf368966397)

6. Click "**Create visualization**" and drag and drop the file "**absolute_amount**" onto the canvas. Change the visualization type to "**Area**" and set the vertical Axis to "**Average**". Click "**Save and return**"
<img width="370" alt="m5oANTEl+djuEGzu7ggt3Tt9Cq70PgcMoFkg7uHUBrM=" src="https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/d26a6ce4-6bc9-4845-a918-b480bd0b7704">

7. Click "**Create visualization**" and select the Donut visualization type. Drag the field "**gender.keyword**" onto the "**Slice by**" field, and drag the "**running_balance.amount**" field onto the metric field. Change the metric function from Median to Average. Click "**Save and return**"
   ![4Q1IOrC9bbS6CgntgjF1dEG5KygcNnEg3zEVlRQsXqk=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/a6851d67-9865-4447-9333-6bc587cf74dd)

8. Resize and rearrange the visualizations to look something like this
   ![pQvWmieQaFNAaotSdk+__1+GYZLP0IhF24KXoks2+GU=](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/17fa439d-0a9c-4453-ba5f-077ddae0325b)

9. Click "**Save**" and enter a title for your Dashboard, check "**Store time with dashboard**" to set the current time range everytime you load the dashboard in the future. Click "**Save**" to finish saving your dashboard.
    <img width="449" alt="Cg6hKNYp_fZxPSI2XclxN8PC0CARkvfu2esBDCS5Ink=" src="https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/eb5b2437-94b8-41b9-99af-ab7cbf5fef44">

Congratulations, you have created your first dashboard.

See if you can create some of these visualizations from the data:

  - Create three of the below visualizations in the dashboard, ‘Transaction Count’, ‘Customer Count’ and ‘Top 10 Spenders pie chart’

![tSk5RWmwj8EnWBo+FMeXwlaD699mUsD5pV3SyFhcc6o= (1)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/8464a977-9681-4cad-b350-940395cfac0f)

Congratulations!
In this workshop, you have:

  - Simulated exporting mainframe financial data (accounts and transactions)

  - Imported mainframe data into BigQuery

  - Explored and normalized the data using SQL in BigQuery

  - Loaded the normalized data into Elastic using DataFlow

  - Created a "time series" dashboard to visualize the financial data

### Next Steps / Learn More
  - [Elastic](https://www.elastic.co/products/) on the Google Cloud Marketplace!
  - [Elastic Cloud](https://console.cloud.google.com/marketplace/browse?q=Elastic&utm_source=Elastic&utm_medium=qwiklabs&utm_campaign=Qwiklabs%20to%20Marketplace) offers a fully managed experience so that you can focus on your data instead of managing the cluster. You can check it out [here](https://www.elastic.co/cloud/) and play with a free trial.
  - Check out the [Elastic Integrations](https://www.elastic.co/integrations/) page and see how easily you can stream in logs, metrics, traces, content, and more from your apps, endpoints, infrastructure, cloud, network, workplace tools, and every other common source in your ecosystem.
  - Leverage the out-of-the-box [solutions](https://www.elastic.co/products/) to give your Elastic project a jump start
