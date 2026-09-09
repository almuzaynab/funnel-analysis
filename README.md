# funnel-analysis
Using SQL to explore ecommerce data to determine trends between the phases of online shopping. Determining if there are issues from website/product functionality, observing user behavior, developing marketing campaigns.

---

Technical Skills:

SQL (Using BigQuery for this project)

---

Soft Skills:

Data Wrangling, Data Transformation, Data Cleaning, Data Storytelling, Project Scoping, Developing Insights, and Translating a Business Problem Into Data

---

Methodology: 

Explore and abstract the count values of each event type (or phases).

<img width="847" height="67" alt="image" src="https://github.com/user-attachments/assets/11d05b86-3af7-4e0b-bf0f-7fcdaab4d02c" />

When retention decreases after each step. Using the count values, develop the conversion rates between each step. 

<img width="890" height="55" alt="image" src="https://github.com/user-attachments/assets/010ecacc-58b2-4aba-9573-34143d666f9c" />

Only 17% of views on the item was successfully converted to a payment. 92% was the rate between payment to purchases so it is likely to assume there are limited issues between the payment portal technology. The most noticable gap is between viewing the item and adding said item to checkout. Although is expected since people often just browse items when looking at an online shop. Most likely marketing to promote why someone should buy the item. 

--

Now, let's look at the source of these interactions to help marketing determine focus.

<img width="887" height="186" alt="image" src="https://github.com/user-attachments/assets/a4d7becb-71d5-4d79-ba68-c60017b9f3b9" />

Looking at the date like with raw values alone does not explain what is going on so convert to rates. 

<img width="890" height="156" alt="image" src="https://github.com/user-attachments/assets/4f5b892f-ed45-44c0-af2a-9fd81201d899" />

Overall, cart to purchase rates remain consistent regardless of source. The most noticible metric is when looking at website data driven via social media. Despite social media bringing in high amounts of views, the website views do not transfer well to purchase. The rates of adding an item is the lowest (14%) and even more so when looking at website views to purchasing an item (7%). The most successful avenue of website traffic is via email. This makes sense as customers voluntarily sign up with pre-existing desire to shop from the brand and hope to recieve deals that are communicated to them via email. Marketing should focus more on retaining client base via email. 

--

Now, let's take a look at the time spent on time between events on the website.

<img width="887" height="62" alt="image" src="https://github.com/user-attachments/assets/b63ca1ac-e1a3-429f-8e33-644372eeb4f9" />

The whole shopping from the initial viewing to the purchase averages about 25 minutes. Is there a way to design the UI of a website so that this is more streamlined?

--

Finally, a look at revenue.

<img width="890" height="51" alt="image" src="https://github.com/user-attachments/assets/d5db9b97-dcf3-4349-b86e-4c833310f7db" />

Average orders appear to be $105-$110. The revenue per visitor starkly drops most likely due to the social media traffic. 

--- 
Conclusion and General Notes: 
- There are limited issues when using the payment portal so do not focus on that.
- Most of the views are generated via social media, however, these views have the least conversion to sales. The rate between views to purchase via social media has a large effect on decreasing the total view to sales conversion. 
- The largest view to sale traffic is via email. Remain consistent with newsletters and implement more users on an email list. As email is the most sucessful channel for purchases, shift focus from social media to emails.

