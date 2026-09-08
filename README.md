# funnel-analysis
Using SQL to explore ecommerce data to determine trends between the phases of online shopping. Determining if there are issues from website/product functionality, observing user behavior, developing marketing campaigns.

Executive Summary:

Exploring ecommerce data to determine trends between the phases of online shopping. Determining if there are issues from website/product functionality, observing user behavior, developing marketing campaigns.


Technical Skills:

SQL (Using BigQuery for this project)

 

Soft Skills:

Data Wrangling, Data Transformation, Data Cleaning, Data Storytelling, Project Scoping, Developing Insights, and Translating a Business Problem Into Data


Methodology: 

Explore and abstract the count values of each event type (or phases). 

WITH funnel_stages AS (

  SELECT
    COUNT(DISTINCT CASE WHEN event_type = 'page_view' THEN user_id END) AS stage_1_views,
    COUNT(DISTINCT CASE WHEN event_type = 'add_to_cart' THEN user_id END) AS stage_2_add,
    COUNT(DISTINCT CASE WHEN event_type = 'checkout_start' THEN user_id END) AS stage_3_checkout,
    COUNT(DISTINCT CASE WHEN event_type = 'payment_info' THEN user_id END) AS stage_4_payment,
    COUNT(DISTINCT CASE WHEN event_type = 'purchase' THEN user_id END) AS stage_5_purchase
  FROM `portfolio-projects-814814.project.user_events` 

)

SELECT * 
FROM funnel_stages

Outcome: 



Retention decreases after each step. From these values, develop the conversion rates between each step. 

WITH funnel_stages AS (

  SELECT
    COUNT(DISTINCT CASE WHEN event_type = 'page_view' THEN user_id END) AS stage_1_views,
    COUNT(DISTINCT CASE WHEN event_type = 'add_to_cart' THEN user_id END) AS stage_2_add,
    COUNT(DISTINCT CASE WHEN event_type = 'checkout_start' THEN user_id END) AS stage_3_checkout,
    COUNT(DISTINCT CASE WHEN event_type = 'payment_info' THEN user_id END) AS stage_4_payment,
    COUNT(DISTINCT CASE WHEN event_type = 'purchase' THEN user_id END) AS stage_5_purchase
  FROM `portfolio-projects-814814.project.user_events` 

)

SELECT 

  ROUND(stage_2_add * 100 / stage_1_views) AS view_to_add_rate,
  ROUND(stage_3_checkout * 100 / stage_2_add) AS add_to_checkout_rate,
  ROUND(stage_4_payment * 100 / stage_3_checkout) AS checkout_to_payment_rate,
  ROUND(stage_5_purchase * 100 / stage_4_payment) AS payment_to_purchase_rate,
  ROUND(stage_5_purchase * 100 / stage_1_views) AS view_to_purchase_rate,

FROM funnel_stages

Output: 



Only 17% of views on the item was successfully converted to a payment. 92% was the rate between payment to purchases so it is likely to assume there are limited issues between the payment portal technology. The most noticable gap is between viewing the item and adding said item to checkout. Although is expected since people often just browse items when looking at an online shop. Most likely marketing to promote why someone should buy the item. 

-

Now, let's look at the source of these interactions to help marketing determine focus. 

WITH funnel_sources AS (

  SELECT
  traffic_source, 
    COUNT(DISTINCT CASE WHEN event_type = 'page_view' THEN user_id END) AS views,
    COUNT(DISTINCT CASE WHEN event_type = 'add_to_cart' THEN user_id END) AS add_cart,
    COUNT(DISTINCT CASE WHEN event_type = 'purchase' THEN user_id END) AS purchase,
  FROM `portfolio-projects-814814.project.user_events` 

  GROUP BY traffic_source
)

SELECT *
FROM funnel_sources

Results: 



Looking at the date like this alone does not explain what is going on so convert to rates. 

WITH source_funnel AS (

  SELECT
  traffic_source, 
    COUNT(DISTINCT CASE WHEN event_type = 'page_view' THEN user_id END) AS views,
    COUNT(DISTINCT CASE WHEN event_type = 'add_to_cart' THEN user_id END) AS add_cart,
    COUNT(DISTINCT CASE WHEN event_type = 'purchase' THEN user_id END) AS purchase,
  FROM `portfolio-projects-814814.project.user_events` 

  GROUP BY traffic_source
)

SELECT
  traffic_source,
  views,
  ROUND(add_cart * 100 / views) AS cart_conversion_rate,
  ROUND(purchase * 100 / views) AS views_to_purchase_conversion_rate,
  ROUND(purchase * 100 / add_cart) AS cart_to_purchase_conversion_rate

FROM source_funnel
ORDER BY purchase DESC

Output: 


Overall, cart to purchase rates remain consistent regardless of source. The most noticible metric is when looking at website data driven via social media. Despite social media bringing in high amounts of views, the website views do not transfer well to purchase. The rates of adding an item is the lowest (14%) and even more so when looking at website views to purchasing an item (7%). The most successful avenue of website traffic is via email. This makes sense as customers voluntarily sign up with pre-existing desire to shop from the brand and hope to recieve deals that are communicated to them via email. Marketing should focus more on retaining client base via email. 

-

Now, let's take a look at the time spent on time between events on the website. 

WITH user_time AS (

  SELECT
    user_id, 
    MIN(CASE WHEN event_type = 'page_view' THEN event_date END) AS view_times,
    MIN(CASE WHEN event_type = 'add_to_cart' THEN event_date END) AS cart_times,
    MIN(CASE WHEN event_type = 'purchase' THEN event_date END) AS purchase_times,
  FROM `portfolio-projects-814814.project.user_events` 

  GROUP BY user_id
  HAVING MIN(CASE WHEN event_type = 'purchase' THEN event_date END) IS NOT NULL
)

SELECT
  COUNT(*) AS converted_users,
  ROUND(AVG(TIMESTAMP_DIFF(cart_times, view_times, MINUTE)),2) AS avg_view_to_cart_minutes,
  ROUND(AVG(TIMESTAMP_DIFF(purchase_times, cart_times, MINUTE)),2) AS avg_cart_to_purchase_minutes,
  ROUND(AVG(TIMESTAMP_DIFF(purchase_times, view_times, MINUTE)),2) AS avg_total_minutes

FROM user_time

Output: 



The whole shopping from the initial viewing to the purchase averages about 25 minutes. Is there a way to design the UI of a website so that this is more streamlined?

-

Finally, a look at revenue.

WITH funnel_revenue AS (

  SELECT 
    COUNT(DISTINCT CASE WHEN event_type = 'page_view' THEN user_id END) AS total_visitors,
    COUNT(DISTINCT CASE WHEN event_type = 'purchase' THEN user_id END) AS total_buyers,
    SUM(CASE WHEN event_type = 'purchase' THEN amount END) AS total_revenue,
    COUNT(CASE WHEN event_type = 'purchase' THEN 1 END) AS total_orders,
  FROM `portfolio-projects-814814.project.user_events` 
)

SELECT
  total_visitors,
  total_buyers,
  ROUND(total_revenue) AS total_sales,
  total_orders,
  ROUND(total_revenue / total_orders) AS avg_order_value,
  ROUND(total_revenue / total_buyers) AS revenue_per_buyer,
  ROUND(total_revenue / total_visitors) AS revenue_per_visitor
FROM funnel_revenue

Output: 



Average orders appear to be $105-$110. The revenue per visitor starkly drops most likely due to the social media traffic. 
