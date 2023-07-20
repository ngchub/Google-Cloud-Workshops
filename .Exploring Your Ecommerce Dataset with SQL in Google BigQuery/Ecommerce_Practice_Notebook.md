# Exploring Your Ecommerce Dataset with SQL in Google BigQuery

Welcome to extract valuable information from ecommerce data by using Google Cloud's powerful storage that is cheap and fast. 

In this workshop, you could able to practice your SQL skills with Big Query while getting insights from one of the public datasets Google Analytics(for access [https://support.google.com/analytics/answer/7586738?hl=en#access-the-dataset&zippy=%2Cin-this-article](https://developers.google.com/analytics/bigquery))

<img src="https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/5fdfe449-5a1e-4f69-bb8a-13f4ca6fd3e5" width="25%" height="25%" align="left" /> <br/>


Providing Google Analytics 4 event data from an ecommerce website, the dataset is useful for exploring the benefits of exporting Google Analytics 4 event data into BigQuery via the integration. The data collection data is between 2020-11-01 to 2021-01-31. For dataset details follow the link [https://support.google.com/analytics/answer/7586738?hl=en#where-the-data-comes-from&zippy=%2Cin-this-article](https://developers.google.com/analytics/bigquery/web-ecommerce-demo-dataset)




In this workshop we want to explore information by using some basic and advance scenarios. Each scenario should be answered by writing a SQL query on Big Query.

For more information about Big Query please follow the link: https://cloud.google.com/bigquery



BigQuery is a serverless and cost-effective enterprise data warehouse that works across clouds and scales with your data. Use built-in ML/AI and BI for insights at scale. 

Let's get started.

## Accessing Big Query

1. Open [https://www.cloud.google.com](https://cloud.google.com/)
After login or sign into with you account:
2. Go to Navigation Menu and select **Big Query**

https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/ddcbec06-67a4-4f12-9167-3fe6472eb2fd"

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

![Screenshot from 2023-07-18 15-49-10](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/83efb7ff-b03e-4686-b012-d608c1fc5077)


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

#### Let's interpreting these results:


Each row represents a specific event that occurred on a particular date. Here's how you can interpret the information:

***Event Date***: This column represents the date on which the event occurred. In this dataset, events occurred on December 1st, 2020 (rows 1-3) and December 2nd, 2020 (rows 4-6).

***Event Name***: This column indicates the type or name of the event that took place. In this dataset, three types of events are mentioned: "page_view" (rows 1 and 4), "session_start" (rows 2 and 5), and "purchase" (rows 3 and 6).

***Event Count***: This column specifies the count or frequency of each event type that occurred on the corresponding date. For example, on December 1st, 2020, there were 21,511 page views (row 1), 4,912 session starts (row 2), and 107 purchases (row 3). On December 2nd, 2020, there were 19,866 page views (row 4), 4,759 session starts (row 5), and 82 purchases (row 6).

This dataset provides a snapshot of the events that took place on your website on specific dates. By analyzing this data, you can gain insights into <ins>user engagement</ins>, <ins>website performance</ins>, and <ins>conversion rates</ins>. Further analysis, such as tracking trends over time or comparing events across different dates, can provide valuable information for optimizing your website's user experience and marketing strategies.


To interpret the results from the provided dataset, you can analyze the event counts and their types to gain insights into user behavior and website performance. Here are some ways to interpret the results:

**Event Trends**: By comparing event counts across different dates, you can identify trends in user engagement. For example, you can observe whether the number of page views, session starts, or purchases is increasing, decreasing, or remaining stable over time. This analysis can help you understand the overall growth or decline of user activity on your website.

**Popular Events**: Look for events with high counts to determine which actions users are frequently performing on your website. For instance, if page views consistently have high counts compared to other events, it suggests that users are exploring different pages of your website extensively. On the other hand, if purchases have a high count, it indicates successful conversions.

**Conversion Rate**: Analyze the ratio between the "purchase" event count and other events, such as "page_view" or "session_start." This will provide insights into the effectiveness of your website in converting user interactions into actual purchases. For example, if the purchase count is relatively low compared to page views, it may indicate potential areas for improving the conversion funnel or optimizing the user experience to encourage more purchases.

**User Engagement**: Compare event counts like "session_start" and "page_view" to evaluate user engagement levels. Higher session starts coupled with a significant number of page views could indicate that users are actively exploring multiple pages during their sessions, suggesting higher engagement. Lower session starts or a lower ratio of page views to session starts might indicate a need to improve user retention or encourage more exploration within sessions.

**Day-to-Day Variations**: Analyze event counts on a daily basis to identify any patterns or variations. Certain events might exhibit recurring patterns based on weekdays, weekends, or specific marketing campaigns. Understanding these variations can help you optimize your website's content, marketing strategies, or promotions accordingly.

Remember, interpreting these results should be done in the context of your specific website and business goals. It's essential to consider additional factors such as <ins>user demographics</ins>, <ins>marketing campaigns</ins>, and changes to the <ins>website or product offerings</ins> to gain a comprehensive understanding of the data and make informed decisions.


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

#### Let's interpreting these results:
![score_card_1](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/d2a54c39-2c5a-41c1-8135-a2ee1c91b3ae)


***Total User Count***: This refers to the cumulative number of users who have visited your website over a given period. It represents the total number of unique individuals who have interacted with your website, including both new and returning users. In this case, you have had a total of 79,421 users in the specified timeframe.

***New User Count***: This refers to the number of users who have visited your website for the first time during the specified period. It represents the number of unique individuals who have discovered your website and engaged with it for the first time. In this case, you have had 71,734 new users during the given timeframe.

By comparing these two figures, you can gather insights about the growth and retention of your website's user base. In your case, since the new user count (71,734) is lower than the total user count (79,421), it suggests that some users who previously visited your website are returning, while others might not be actively engaging or have dropped off.

Analyzing this data further, you could consider metrics such as user engagement, conversion rates, or user retention to gain a more comprehensive understanding of your website's performance and the effectiveness of your strategies for attracting and retaining new users.

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

#### Let's interpreting these results:

The result "1.23" represents the average transaction per purchaser. This metric provides insights into the average number of transactions made by each individual purchaser on your website. Here's how you can interpret this result:

***Average Transaction per Purchaser***: The value "1.23" indicates that, on average, each purchaser on your website makes 1.23 transactions. This means that when someone makes a purchase on your website, they, on average, complete 1.23 transactions during their interaction with your business.

**Purchaser Behavior**: The average transaction per purchaser metric helps you understand how engaged and active your purchasers are. A higher value, such as 1.23, suggests that purchasers tend to make more than one transaction, indicating potential repeat purchases or multiple transactions during a single visit.

**Revenue Generation**: By knowing the average transaction per purchaser, you can estimate the revenue potential of each purchaser. For example, if the average transaction value is $50, then the average revenue generated per purchaser would be approximately $61.50 ($50 x 1.23).

**Customer Retention**: Monitoring the average transaction per purchaser over time can provide insights into customer retention and loyalty. If the average transaction per purchaser increases over time, it suggests that purchasers are becoming more engaged and making multiple transactions. Conversely, a decreasing trend may indicate a need to focus on improving customer retention strategies.

**Marketing and Upselling Opportunities**: Understanding the average transaction per purchaser can help you identify opportunities for upselling or cross-selling. If the current average is relatively low, you can consider implementing strategies to encourage purchasers to make additional transactions or explore higher-value products/services.

It's important to note that interpreting the average transaction per purchaser metric should be done in conjunction with other relevant metrics and factors specific to your business, such as <ins>customer acquisition costs</ins>, <ins>customer lifetime value</ins>, and <ins>overall business objectives</ins>. This will provide a more comprehensive understanding of the metric's implications and guide decision-making processes for optimizing sales, marketing, and customer retention strategies.

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

#### Let's interpreting these results:
![transferring_data](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/be437dee-e1a0-495e-9a7d-be9362e3cc62)

To figure out the values of events within a specific time range, you need to identify the events that fall within the desired range based on their event timestamps. From the provided dataset, here's how you can interpret the results:

***Event Timestamp***: The event timestamps represent the date and time when each event occurred.

***Event Value***: The event values column provides the associated values for each event.

To determine the values of events within a specific time range, follow these steps:

Define the desired time range by specifying the start and end timestamps.

Iterate through the dataset and identify the events that have timestamps falling within the defined time range.

Retrieve the event values associated with the events identified in step 2.

Here's an example of retrieving events within a specific time range:

Let's say you want to find events between timestamps 1606800000000000 and 1606820000000000 (inclusive). In the given dataset, the following rows have event timestamps within this range:

Row 2: event_timestamp = 1606815536636655, event_value = 55.2
Row 7: event_timestamp = 1606829753792895, event_value = 24.0
Based on this, the values of events within the specified time range are 55.2 and 24.0, corresponding to the respective rows.

Remember to adjust the time range and adapt the steps according to your specific requirements and the structure of your dataset.

Keep in mind that if you have a larger dataset or need to perform more complex filtering, you might need to use programming or scripting techniques to efficiently filter and extract events within the desired time range.

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

#### Let's interpreting these results:
![bq_at_scale](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/8de204f7-93fd-4ea1-8607-7803a89216dc)

The provided result, "11455.08," represents the value for a specific event, which in this case is the "purchase" event. Here's how you can interpret this result:

***Event Value***: The event value, "11455.08," indicates the specific value associated with the "purchase" event. The nature of this value depends on the context of your dataset and the specific meaning of the "purchase" event in your domain.

**Financial Insights**: The value of "11455.08" can provide insights into the financial performance of your business or website in terms of the purchases made. It can be used to track and analyze revenue trends, average purchase values, or the impact of different factors on purchase amounts.

**Business Decision-making**: Understanding the value associated with the "purchase" event can help guide business decisions. For example, you can use this information to assess the effectiveness of marketing campaigns, evaluate the profitability of specific products or services, or identify patterns in customer spending behavior.

**Comparison and Analysis**: To gain further insights, you can compare this value with other relevant metrics or perform analysis based on different segments or time periods. For instance, comparing the "purchase" event values across different customer segments or analyzing changes in purchase values over time can provide valuable information for strategic decision-making.

It's important to note that the interpretation may vary depending on the context of your specific dataset and business domain. Understanding the specific context and considering additional factors such as customer behavior, pricing, or product/service offerings will help provide a more comprehensive interpretation of the "purchase" event value.

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

![q6](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/766435d3-c5b5-4e4f-90a6-21ec25f18456)

#### Let's interpreting these results:
![serverless_bq](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/705f4147-8209-4578-a595-3d984e831fb9)

Based on the provided dataset, which includes item IDs, item names, and user counts, you can interpret the results to identify the top 10 items added to the cart by the most number of users. Here's how you can interpret the information:

***Item ID***: Each item in the dataset is assigned a unique item ID. This ID serves as a reference to identify and distinguish different items.

***Item Name***: The item name column represents the name or description of each item.

***User Count***: The user count column indicates the number of users who have added a particular item to their cart. It represents the count or frequency of users who have expressed interest in purchasing a specific item.

Based on the provided dataset, you can identify the top 10 items added to the cart by the most number of users. Here are the interpretations:

Google Land & Sea Cotton Cap (item ID: GGOEGAPH161899): This item has been added to the cart by 3,567 users, making it the item with the highest user count.

Google Navy Speckled Tee (item ID: GGOEGXXX1344): This item has been added to the cart by 3,526 users, ranking second in terms of user count.

Google Zip Hoodie F/C (item ID: GGOEGXXX1109): This item has been added to the cart by 3,519 users, placing it third in terms of user count.

By analyzing this information, you can prioritize the stock of these top 10 items to ensure sufficient availability and meet the demand of the users who are adding them to their carts. This data can guide your decision-making process for inventory management, marketing strategies, and identifying popular items in your stock.


### Average number of pageviews by purchaser type (purchasers vs non-purchasers)

**Scenario 7**: You want to see average number of pageviews by purchaser type.

```console
WITH
  UserInfo AS (
    SELECT
      user_pseudo_id,
      COUNTIF(event_name = 'page_view') AS page_view_count,
      COUNTIF(event_name IN ('in_app_purchase', 'purchase')) AS purchase_event_count
    -- Replace table name.
    FROM `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
    -- Replace date range.
    WHERE _TABLE_SUFFIX BETWEEN '20201201' AND '20201202'
    GROUP BY 1
  )
SELECT
  (purchase_event_count > 0) AS purchaser,
  COUNT(*) AS user_count,
  SUM(page_view_count) AS total_page_views,
  SUM(page_view_count) / COUNT(*) AS avg_page_views,
FROM UserInfo
GROUP BY 1;
```
![q7](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/37c28f03-4fcd-4371-b9c1-8560b751c787)

#### Let's interpreting these results:

Based on the provided dataset, which includes information about purchasers, user counts, total page views, and average page views, you can interpret the results to understand the sequence of page views made by users during unique sessions. Here's how you can interpret the information:

***Purchaser***: The "purchaser" column indicates whether the user is a purchaser or not. A value of "true" suggests that the user is a purchaser, while "false" indicates that the user is not a purchaser.

***User Count***: The "user_count" column represents the number of users who have engaged in unique sessions. It indicates the count or frequency of unique individuals who have visited your website or app and initiated a session.

***Total Page Views***: The "total_page_views" column shows the total number of page views recorded during all the unique sessions. It provides an overall count of the pages that were viewed across the sessions.

***Average Page Views***: The "avg_page_views" column represents the average number of page views per session. It is calculated by dividing the total page views by the user count, providing an average measure of the number of pages viewed during each unique session.

Interpreting the results:

Row 1: For the users who are not purchasers (purchaser: false), there are 7,916 unique sessions recorded. These users generated a total of 34,786 page views across those sessions, resulting in an average of approximately 4.39 page views per session.

Row 2: For the users who are purchasers (purchaser: true), there are 172 unique sessions recorded. These purchasers generated a total of 6,591 page views, resulting in an average of approximately 38.32 page views per session.

These results provide insights into user engagement and behavior during unique sessions:

Users who are purchasers (purchaser: true) tend to have a <ins>higher average number of page views per session compared to users who are not purchasers</ins> (purchaser: false). This suggests that purchasers are more likely to explore multiple pages or engage more deeply with the website or app during their sessions.

The average page views per session can serve as an indicator of user engagement and the level of interaction with your content or offerings. Higher average page views per session may indicate higher levels of interest or a more extensive exploration of your website or app.

Analyzing the sequence of page views during unique sessions can provide insights into user navigation patterns, content preferences, or potential bottlenecks that hinder users from reaching desired pages or completing specific actions.

By understanding these insights, you can optimize your website or app experience, content placement, and navigation to enhance user engagement, increase conversion rates, and improve overall user satisfaction.

### Sequence of pageviews

**Scenario 8**: You want to know the sequence of pageviews made by users during unique sessions.

```console
SELECT
  user_pseudo_id,
  FORMAT_DATE('%d-%m-%Y', PARSE_DATE('%Y%m%d', event_date)) AS date, 
  FORMAT_TIME('%T', TIME(TIMESTAMP_MICROS(event_timestamp))) time,
  (SELECT value.int_value FROM UNNEST(event_params) WHERE key = 'ga_session_id') AS ga_session_id,
  (SELECT value.string_value FROM UNNEST(event_params) WHERE key = 'page_location')
    AS page_location,
  (SELECT value.string_value FROM UNNEST(event_params) WHERE key = 'page_title') AS page_title
FROM
  -- Replace table name.
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
WHERE
  event_name = 'page_view'
  -- Replace date range.
  AND _TABLE_SUFFIX BETWEEN '20201201' AND '20201202'
ORDER BY
  user_pseudo_id,
  ga_session_id,
  date,
  time ASC;
```
![q8](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/19e290db-e0ba-471b-be92-5152d20fbd62)

#### Let's interpreting these results:

To interpret the provided results related to the sequence of pageviews made by users during unique sessions, you can analyze the information available in the dataset. Here's how you can interpret the information:

***User Pseudo ID***: The "user_pseudo_id" column represents a unique identifier for each user. It allows tracking user activity across different sessions.

***Date and Time***: The "date" and "time" columns indicate the date and time when a particular pageview occurred.

***GA Session ID***: The "ga_session_id" column represents the session ID associated with the pageviews. It helps identify unique sessions for each user.

Page Location and Page Title: The "page_location" and "page_title" columns provide information about the specific page visited by the user during a session. The "page_location" contains the URL of the page, and the "page_title" provides the title or description of the page.

Interpreting the results:

**Sequential Pageviews**: By examining the rows in the dataset, you can determine the sequence of pageviews made by users during their unique sessions. Each row represents a pageview event and is associated with a specific user and session.

**User Behavior**: Analyzing the sequence of pageviews can provide insights into user behavior and their navigation patterns on the website. It can reveal the pages users tend to visit consecutively during their sessions.

**Popular Pages**: By examining the "page_title" and "page_location," you can identify which pages users are visiting frequently or in a specific order. This information can help you understand popular pages, user interests, or potential areas for improvement.

**Session Duration**: Analyzing the time intervals between consecutive pageviews within the same session can provide insights into user engagement and session duration. Longer intervals might indicate users spending more time on a particular page, while shorter intervals suggest quick navigation between pages.

**User Experience Optimization**: By understanding the sequence of pageviews, you can identify potential bottlenecks or issues in the user experience. This information can guide you in improving page navigation, content placement, or the overall website flow to enhance user engagement and satisfaction.

It's important to note that the provided dataset represents a sample, and further analysis may require a larger dataset or additional information. Additionally, depending on your specific website or application, you may have additional variables or data points that can provide more insights into user behavior and session sequences.

### Event parameter list

**Scenario 9**: You want to list all available event parameters and count their occurrences.

```console
SELECT
  EP.key AS event_param_key,
  COUNT(*) AS occurrences
FROM
  -- Replace table name.
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`, UNNEST(event_params) AS EP
WHERE
  -- Replace date range.
  _TABLE_SUFFIX BETWEEN '20201201' AND '20201202'
GROUP BY
  event_param_key
ORDER BY
  event_param_key ASC;
```

![q9](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/00c068b6-656a-4675-af7b-b00a052a76c1)

#### Let's interpreting these results:

Based on the provided dataset, which includes event parameter keys and the occurrences of each key, you can interpret the results to understand the available event parameters and their respective frequencies. Here's how you can interpret the information:

***Event Param Key***: The "event_param_key" column represents the parameter keys associated with each event. These keys are used to capture specific information related to the events.

***Occurrences***: The "occurrences" column indicates the number of times each event parameter key occurs in the dataset. It represents the frequency or count of occurrences for each parameter key.

Interpreting the results:

**Available Event Parameters**: The dataset provides a list of available event parameter keys, such as "gclsrc," "currency," "search_term," "transaction_id," and more. These keys represent different types of information that can be captured for events.

**Frequency of Occurrences**: The "occurrences" column shows the number of times each event parameter key appears in the dataset. This indicates how frequently each parameter key is captured or recorded in the events.

**Importance of Event Parameters**: The frequency of occurrences provides insights into the importance or relevance of specific event parameters in the dataset. Parameters with higher occurrences are more commonly captured and may represent key aspects of the events.

**Commonly Captured Information**: The higher occurrence of event parameters like "gclsrc," "currency," "search_term," and "unique_search_term" suggests that these parameters are frequently used to capture information related to the source of the event, currency used, and search terms associated with the event.

**Transaction-related Information**: Event parameters like "transaction_id," "tax," "value," "payment_type," and "shipping_tier" occur with similar frequencies, indicating that these parameters are often captured for events related to transactions, such as purchases. They provide information about transaction identifiers, tax amounts, transaction values, payment types, and shipping tiers.

**Promotion and Link Information**: Parameters like "coupon," "promotion_name," "dclid," "link_url," "outbound," and "link_domain" occur with lower frequencies. These parameters may capture details related to promotions, coupon codes, link URLs, and outbound link tracking.

By interpreting these results, you can gain insights into the available event parameters and their usage within the dataset. This understanding can guide your data analysis, processing, and decision-making processes, allowing you to focus on the event parameters with higher occurrences and explore their significance for your specific analysis objectives or business goals.

### Products purchased by customers who purchased a certain product

**Scenario 10**: You want to investigate customers who purchased a certain product.

```console
-- `Params` is used to hold the value of the selected product and is referenced
-- throughout the query.

WITH
  Params AS (
    -- Replace with selected item_name or item_id.
    SELECT 'Google Navy Speckled Tee' AS selected_product
  ),
  PurchaseEvents AS (
    SELECT
      user_pseudo_id,
      items
    FROM
      -- Replace table name.
      `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
    WHERE
      -- Replace date range.
      _TABLE_SUFFIX BETWEEN '20201101' AND '20210131'
      AND event_name = 'purchase'
  ),
  ProductABuyers AS (
    SELECT DISTINCT
      user_pseudo_id
    FROM
      Params,
      PurchaseEvents,
      UNNEST(items) AS items
    WHERE
      -- item.item_id can be used instead of items.item_name.
      items.item_name = selected_product
  )
SELECT
  items.item_name AS item_name,
  SUM(items.quantity) AS item_quantity
FROM
  Params,
  PurchaseEvents,
  UNNEST(items) AS items
WHERE
  user_pseudo_id IN (SELECT user_pseudo_id FROM ProductABuyers)
  -- item.item_id can be used instead of items.item_name
  AND items.item_name != selected_product
GROUP BY 1
ORDER BY item_quantity DESC;
```
![q10](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/096ecd83-4263-465d-b381-4fe6864813a9)

#### Let's interpreting these results:

Based on the provided dataset, which includes the item names and the quantities purchased for each item, you can interpret the results to investigate customers who purchased a certain product. Here's how you can interpret the information:

***Item Name***: The "item_name" column represents the names or descriptions of the purchased items.

***Item Quantity***: The "item_quantity" column indicates the quantity of each item that was purchased.

Interpreting the results:

**Purchased Items**: The dataset provides a list of items that were purchased. Each item is identified by its name, such as "Google Camp Mug Ivory," "Google Small Standard Journal Navy," and so on.

**Quantity Purchased**: The "item_quantity" column indicates the quantity of each item that was purchased. It shows how many units of each item were bought.

**Popularity of Items**: By analyzing the quantities purchased, you can identify the popularity or demand for each item. Items with higher quantities indicate a higher demand or more frequent purchases.

**Customer Preferences**: The quantities purchased for each item can provide insights into customer preferences or the appeal of specific products. Items with higher quantities purchased may be more popular among customers.

**Inventory Management**: Analyzing the quantities purchased can help with inventory management. It allows you to identify items that are selling well and may require replenishment to meet customer demand.

**Sales Analysis**: By examining the quantities purchased for each item, you can track sales performance and identify trends or patterns. This information can be used to evaluate the success of marketing efforts, assess the popularity of certain products, or make data-driven decisions to improve sales strategies.

By interpreting these results, you can gain insights into the purchases made by customers for specific products. This information can guide your understanding of customer preferences, inventory management, and sales analysis, allowing you to make informed decisions to optimize your product offerings and improve customer satisfaction.

### Average amount of money spent per purchase session by user

**Scenario 11**: You want to investigate how much mony that a customer spent during purcahe session

```console
-- Example: Average amount of money spent per purchase session by user.

SELECT
  user_pseudo_id,
  COUNT(
    DISTINCT(SELECT EP.value.int_value FROM UNNEST(event_params) AS EP WHERE key = 'ga_session_id'))
    AS session_count,
  AVG(
    (
      SELECT COALESCE(EP.value.int_value, EP.value.float_value, EP.value.double_value)
      FROM UNNEST(event_params) AS EP
      WHERE key = 'value'
    )) AS avg_spend_per_session_by_user,
FROM
  -- Replace table name.
  `bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`
WHERE
  event_name = 'purchase'
  -- Replace date range.
  AND _TABLE_SUFFIX BETWEEN '20201101' AND '20210131'
GROUP BY
  1;
```

![q11](https://github.com/ngchub/Google-Cloud-Workshops/assets/28653377/86a43baa-2f12-4954-919c-001e8332018c)

#### Let's interpreting these results:

Based on the provided dataset, which includes user pseudo IDs, session counts, and average spend per session by user, you can interpret the results to understand the amount of money customers spent during their purchase sessions. Here's how you can interpret the information:

***User Pseudo ID***: The "user_pseudo_id" column represents a unique identifier for each user. It allows tracking user activity and purchases across different sessions.

***Session Count***: The "session_count" column indicates the number of purchase sessions recorded for each user. It represents the count or frequency of unique sessions in which purchases were made.

***Average Spend per Session by User***: The "avg_spend_per_session_by_user" column shows the average amount of money spent by each user during their purchase sessions.

Interpreting the results:

**User Purchase Behavior**: By analyzing the average spend per session by user, you can gain insights into the spending patterns and behaviors of customers during their purchase sessions. It provides an understanding of the typical amount of money customers spend when making a purchase.

**Session-Level Spending**: The average spend per session represents the average amount of money spent by users during individual purchase sessions. It can help you gauge the spending range and potential revenue generated from each session.

**User Segmentation**: By considering the session count, you can identify users who have made multiple purchase sessions. Users with a higher session count may represent more frequent or loyal customers who engage in multiple purchase activities.

**Overall Spending**: The average spend per session by user provides a general measure of the amount of money customers spend during their purchase sessions. This can be useful for evaluating revenue generation, analyzing customer lifetime value, or assessing the overall financial performance of your business.

**Customer Satisfaction and Engagement**: Monitoring the average spend per session by user over time can help gauge customer satisfaction and engagement. An increase in the average spend per session may indicate increased customer loyalty or a positive response to marketing efforts.

By interpreting these results, you can gain insights into customer spending behavior during purchase sessions. This information can guide your understanding of customer preferences, revenue generation, customer segmentation, and overall business performance, helping you make data-driven decisions to optimize your sales strategies and improve customer satisfaction.
