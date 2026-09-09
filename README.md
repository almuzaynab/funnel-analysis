# funnel-analysis
Using SQL to explore ecommerce data to determine trends between the phases of online shopping. Determining if there are issues from website/product functionality, observing user behavior, developing marketing campaigns.



Technical Skills:

SQL (Using BigQuery for this project)

 

Soft Skills:

Data Wrangling, Data Transformation, Data Cleaning, Data Storytelling, Project Scoping, Developing Insights, and Translating a Business Problem Into Data


Methodology: 

Explore and abstract the count values of each event type (or phases). 
When retention decreases after each step. Using the count values, develop the conversion rates between each step. 

Only 17% of views on the item was successfully converted to a payment. 92% was the rate between payment to purchases so it is likely to assume there are limited issues between the payment portal technology. The most noticable gap is between viewing the item and adding said item to checkout. Although is expected since people often just browse items when looking at an online shop. Most likely marketing to promote why someone should buy the item. 

-

Now, let's look at the source of these interactions to help marketing determine focus.
Looking at the date like with raw values alone does not explain what is going on so convert to rates. 

Overall, cart to purchase rates remain consistent regardless of source. The most noticible metric is when looking at website data driven via social media. Despite social media bringing in high amounts of views, the website views do not transfer well to purchase. The rates of adding an item is the lowest (14%) and even more so when looking at website views to purchasing an item (7%). The most successful avenue of website traffic is via email. This makes sense as customers voluntarily sign up with pre-existing desire to shop from the brand and hope to recieve deals that are communicated to them via email. Marketing should focus more on retaining client base via email. 

-

Now, let's take a look at the time spent on time between events on the website.

The whole shopping from the initial viewing to the purchase averages about 25 minutes. Is there a way to design the UI of a website so that this is more streamlined?

-

Finally, a look at revenue.

Average orders appear to be $105-$110. The revenue per visitor starkly drops most likely due to the social media traffic. 
