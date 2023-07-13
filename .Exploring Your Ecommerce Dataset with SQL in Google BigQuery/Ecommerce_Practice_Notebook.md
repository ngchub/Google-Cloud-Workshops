# Exploring Your Ecommerce Dataset with SQL in Google BigQuery

Welcome to extract valuable information from ecommerce data by using Google Cloud's powerful storage that is cheap and fast. 

In this workshop, you could able to practice your SQL skills with Big Query while getting insights from one of the public datasets Google Analytics(for access [https://support.google.com/analytics/answer/7586738?hl=en#access-the-dataset&zippy=%2Cin-this-article](https://developers.google.com/analytics/bigquery))

Providing Google Analytics 4 event data from an ecommerce website, the dataset is useful for exploring the benefits of exporting Google Analytics 4 event data into BigQuery via the integration. The data collection data is between 2020-11-01 to 2021-01-31. For dataset details follow the link [https://support.google.com/analytics/answer/7586738?hl=en#where-the-data-comes-from&zippy=%2Cin-this-article](https://developers.google.com/analytics/bigquery/web-ecommerce-demo-dataset)

In this workshop we want to explore information by using some basic and advance scenarios. Each scenario should be answered by writing a SQL query on Big Query.

For more information about Big Query please follow the link: https://cloud.google.com/bigquery
![Screenshot from 2023-07-13 00-19-47](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/5fdfe449-5a1e-4f69-bb8a-13f4ca6fd3e5)

BigQuery is a serverless and cost-effective enterprise data warehouse that works across clouds and scales with your data. Use built-in ML/AI and BI for insights at scale. 

Let's get started.

## Accessing Big Query

1. Open [https://www.cloud.google.com](https://cloud.google.com/)
After login or sign into with you account:
2. Go to Navigation Menu and select **Big Query** ![nUxFb6oRFr435O3t6V7WYJAjeDFcrFb16G9wHWp5BzU= (1)](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/ddcbec06-67a4-4f12-9167-3fe6472eb2fd)

## Adding ga4_obfuscated_sample_ecommerce dataset into Big Query

1. Click on **+Add** button<br/>
![add](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/0a2d7c28-3bb5-4202-84a7-9ffe449505db)<br/>

2.Select **Star a project by name** <br/>
![star](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/7fe0f98a-5982-405b-86ed-9e9ba5659464)<br/>

3.Enter **bigquery-public-data** on Project Name box then click **SAVE**<br/>
![starsave](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/68c6be98-a122-4db0-bc59-476d3bb04124)<br/>
Now, you can see the public datasets
![datapublic](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/d382ef14-f0fd-411a-a24c-123f40745050)<br/>

4.You can find **ga4_obfuscated_sample_ecommerce** in the Google public dataset list<br/>
![Screenshot from 2023-07-13 01-05-39](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/5333a94a-3507-4b80-b57f-b8a181ee43cd)<br/>

For more information about accessing Google public datasets click: https://cloud.google.com/bigquery/public-data

## Getting Insight from GA4 Data


### Query a specific date range for selected events

**Scenario 1**: You want to count unique events by date and by event name for a specifc period of days and
-- selected events(page_view, session_start, and purchase).

```console
SELECT
  event_date,
  event_name,
  COUNT(*) AS event_count
FROM
  -- Replace table name.
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
WHERE
  event_name IN ('page_view', 'session_start', 'purchase')
  -- Replace date range.
  AND _TABLE_SUFFIX BETWEEN '20201201' AND '20201202'
GROUP BY 1, 2;
```

![q1](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/1a6cb855-847a-4b65-87ed-d0ec74e61525)

### User count and new user count

**Scenario 2**:You want to get the total user count, count the number of distinct user_id. However, if your Google Analytics client does not send back a user_id with each hit or if you are unsure, count the number of distinct user_pseudo_id.
**Note**: For new users, you can take the same count approach described above but for the following values of event_name:
  - first_visit
  - first_open

```console

WITH
  UserInfo AS (
    SELECT
      user_pseudo_id,
      MAX(IF(event_name IN ('first_visit', 'first_open'), 1, 0)) AS is_new_user
    -- Replace table name.
    FROM `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
    -- Replace date range.
    WHERE _TABLE_SUFFIX BETWEEN '20201101' AND '20201130'
    GROUP BY 1
  )
SELECT
  COUNT(*) AS user_count,
  SUM(is_new_user) AS new_user_count
FROM UserInfo;
```

![q2](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/440f20e4-f110-4261-85f3-560866c5abdc)

### Average number of transactions per purchaser

**Scenario 3**: You want to examine the average number of transactions per purchaser.

```console
SELECT
  ROUND(COUNT(*) / COUNT(DISTINCT user_pseudo_id), 2) AS avg_transaction_per_purchaser
FROM
  -- Replace table name.
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
WHERE
  event_name IN ('in_app_purchase', 'purchase')
  -- Replace date range.
  AND _TABLE_SUFFIX BETWEEN '20201201' AND '20201231';
```
![q3](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/76dfc18d-7718-4468-806e-5f73c80b0841)

### Values for a specific event name

**Scenario 4**: You want to figure out values of events between a spesific time range.

```console
SELECT
  event_timestamp,
  (
    SELECT COALESCE(value.int_value, value.float_value, value.double_value)
    FROM UNNEST(event_params)
    WHERE key = 'value'
  ) AS event_value
FROM
  -- Replace table name.
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
WHERE
  event_name = 'purchase'
  -- Replace date range.
  AND _TABLE_SUFFIX BETWEEN '20201201' AND '20201202';
```

![q4](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/50ef5453-1aee-4ec0-9c9c-58b1c35f1efe)

**Scenario 5**: You want to figure out what is the value for a spesific event ***purchase*** has.

```console
SELECT
  SUM(
    (
      SELECT COALESCE(value.int_value, value.float_value, value.double_value)
      FROM UNNEST(event_params)
      WHERE key = 'value'
    ))
    AS event_value
FROM
  -- Replace table name.
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
WHERE
  event_name = 'purchase'
  -- Replace date range.
  AND _TABLE_SUFFIX BETWEEN '20201201' AND '20201202';
```

![q5](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/57e2dee9-1609-4456-ad1d-1144f7d6975c)


### Top 10 items added to cart

**Scenario 6**: You will make decisions for stock optimization and want to get the information about top 10 item added to cart by the most number of users.

```console
SELECT
  item_id,
  item_name,
  COUNT(DISTINCT user_pseudo_id) AS user_count
FROM
  -- Replace table name.
   `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`, UNNEST(items)
WHERE
  -- Replace date range.
  _TABLE_SUFFIX BETWEEN '20201101' AND '20210131'
  AND event_name IN ('add_to_cart')
GROUP BY
  1, 2
ORDER BY
  user_count DESC
LIMIT 10;
```
