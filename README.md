**The above files are written to produce:**

- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the current/most recent postcode of a user.
- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the postcode a user was in at the time when that user made a pageview.

**Design of the warehouse:**
![alt text](https://github.com/sashadeezauch/page_view/blob/main/Diagram.png?raw=true)

**Tables:**

*master_db.users_extract:* list of user ids and their current postcode. Updated once a day.

*master_db.pageviews_extract:* list of pages visited, user ids and timestamp. Updated every hour but only contains one hour worth of data.

*analytics_db.pageviews_user_history:* used to record the list of all pageview extract along with their user’s postcode at the time. Its needed because the pageviews_extract table is truncated after each run and is a one hour extract of the pageviews which is required to record the postcode at the time of pageview.

*analytics_db.pageview_postcode:* used to record the total number of pageviews on a given date, hour and postcode. As the users_extract table only contains the latest user data we have to join it with the user history table to extract the most recent postcode - this only really needs to be done once a day as the users_extract gets updated once a day.

*analytics_db.pageview_postcode_history:* used to record the total number of pageviews of pageviews_user_history on a given date, hour and postcode at the time of visit.

**Airflow DAG to automate the script:**
pageview_postcode.py 
